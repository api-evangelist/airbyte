# Airbyte GraphQL

Airbyte exposes a GraphQL endpoint at `https://api.airbyte.com/graphql`. The endpoint requires authentication and returns a 401 for unauthenticated requests, confirming a live GraphQL surface. The schema is derived from Airbyte's public OpenAPI specification published in the [airbyte-platform](https://github.com/airbytehq/airbyte-platform/tree/main/airbyte-api/server-api/src/main/openapi) repository.

## Endpoint

```
POST https://api.airbyte.com/graphql
```

### Authentication

Airbyte uses OAuth 2.0 client credentials. Obtain a bearer token by posting to `/applications/token` with your `client_id` and `client_secret`, then pass it as a Bearer token:

```
Authorization: Bearer <access_token>
```

## Schema Overview

The schema covers six primary resource domains: Workspaces, Sources, Destinations, Connections, Jobs, and Users/Permissions. A full GraphQL SDL is provided in [airbyte-schema.graphql](airbyte-schema.graphql).

## Core Types

### Workspace

The top-level organizational unit. Each workspace contains sources, destinations, and connections.

| Field | Type | Description |
|-------|------|-------------|
| workspaceId | UUID! | Unique identifier |
| name | String! | Workspace display name |
| dataResidency | String | Data residency region |
| notifications | NotificationsConfig | Email and webhook notification settings |
| organizationId | UUID | Parent organization |
| createdAt | DateTime | Creation timestamp |
| updatedAt | DateTime | Last updated timestamp |

### Source

A connector that pulls data from an external system (database, SaaS API, file storage, etc.).

| Field | Type | Description |
|-------|------|-------------|
| sourceId | UUID! | Unique identifier |
| name | String! | Display name |
| sourceType | String! | Connector slug (e.g., "stripe", "postgres") |
| definitionId | UUID! | Source definition identifier |
| workspaceId | UUID! | Owning workspace |
| configuration | JSON | Connector-specific config |
| createdAt | DateTime | Creation timestamp |
| resourceAllocation | ScopedResourceRequirements | CPU/memory limits |

### Destination

A connector that writes data to a target system (data warehouse, data lake, vector store, etc.).

| Field | Type | Description |
|-------|------|-------------|
| destinationId | UUID! | Unique identifier |
| name | String! | Display name |
| destinationType | String! | Connector slug (e.g., "snowflake", "bigquery") |
| workspaceId | UUID! | Owning workspace |
| configuration | JSON | Connector-specific config |
| createdAt | DateTime | Creation timestamp |
| resourceAllocation | ScopedResourceRequirements | CPU/memory limits |

### Connection

Links a source to a destination with sync scheduling and stream configuration.

| Field | Type | Description |
|-------|------|-------------|
| connectionId | UUID! | Unique identifier |
| name | String! | Display name |
| sourceId | UUID! | Source connector |
| destinationId | UUID! | Destination connector |
| workspaceId | UUID! | Owning workspace |
| status | ConnectionStatus! | active, inactive, deprecated, locked |
| schedule | ConnectionSchedule | Sync schedule (cron, basic, or manual) |
| configurations | StreamConfigurations | Per-stream sync modes and settings |
| nonBreakingSchemaUpdatesBehavior | NonBreakingSchemaUpdatesBehavior | Schema change handling |
| namespaceDefinition | NamespaceDefinition | Namespace routing strategy |
| tags | [Tag!] | Organizational tags |
| createdAt | DateTime | Creation timestamp |

### Job

Represents a single sync, reset, refresh, or clear operation execution.

| Field | Type | Description |
|-------|------|-------------|
| id | UUID! | Unique identifier |
| status | JobStatus! | pending, running, succeeded, failed, cancelled |
| jobType | JobType! | sync, reset_connection, refresh, clear |
| connectionId | UUID! | Connection being operated on |
| startedAt | DateTime | Execution start time |
| bytesSynced | Float | Bytes transferred |
| rowsSynced | Float | Records transferred |

### StreamConfiguration

Per-stream settings within a Connection defining how each data stream is synced.

| Field | Type | Description |
|-------|------|-------------|
| name | String! | Stream name |
| namespace | String | Source namespace |
| syncMode | ConnectionSyncMode! | Sync strategy |
| cursorField | [String!] | Incremental cursor path |
| primaryKey | [[String!]!] | Deduplication key paths |
| selectedFields | [SelectedFieldInfo!] | Column projection |
| mappers | [ConfiguredStreamMapper!] | Data transformation mappers |

### User

A user with access to one or more workspaces or organizations.

| Field | Type | Description |
|-------|------|-------------|
| id | UUID! | Unique identifier |
| name | String! | Full name |
| email | String! | Email address |
| status | UserStatus! | invited, registered, disabled |
| authProvider | AuthProvider | airbyte, google_identity_platform, keycloak |

### Permission

Grants a user a role within a workspace or organization.

| Field | Type | Description |
|-------|------|-------------|
| permissionId | UUID! | Unique identifier |
| permissionType | PermissionType! | Role (admin, editor, reader, member) |
| scope | PermissionScope! | workspace, organization, or instance |
| userId | UUID! | Subject user |
| workspaceId | UUID | Scoped workspace |
| organizationId | UUID | Scoped organization |

## Key Enums

### ConnectionSyncMode

| Value | Description |
|-------|-------------|
| full_refresh_overwrite | Replace all destination data each sync |
| full_refresh_append | Append all source data each sync |
| incremental_append | Append only new/changed records |
| incremental_deduped_history | Append with deduplication |
| incremental_update | Upsert changed records |
| incremental_soft_delete | Mark deleted records |

### JobStatus

| Value | Description |
|-------|-------------|
| pending | Queued for execution |
| running | Currently executing |
| succeeded | Completed successfully |
| failed | Terminated with error |
| cancelled | Manually cancelled |
| incomplete | Partially completed |

### JobType

| Value | Description |
|-------|-------------|
| sync | Regular data sync |
| reset_connection | Clear destination and re-sync |
| refresh | Re-fetch selected streams |
| clear | Delete destination data without re-syncing |

### StreamMapperType

| Value | Description |
|-------|-------------|
| hashing | Hash field values for PII masking |
| field_renaming | Rename destination fields |
| row_filtering | Filter rows by condition |
| encryption | Encrypt field values (AES or RSA) |
| field_filtering | Include or exclude specific fields |

## Sample Queries

### List connections in a workspace

```graphql
query ListConnections($workspaceId: UUID!) {
  connections(workspaceId: $workspaceId, limit: 20) {
    data {
      connectionId
      name
      status
      schedule {
        scheduleType
        cronExpression
      }
      source {
        sourceId
        name
        sourceType
      }
      destination {
        destinationId
        name
        destinationType
      }
    }
    next
  }
}
```

### Trigger a sync job

```graphql
mutation TriggerSync($connectionId: UUID!) {
  createJob(input: {
    connectionId: $connectionId
    jobType: sync
  }) {
    id
    status
    jobType
    startedAt
  }
}
```

### Create a source

```graphql
mutation CreateSource($workspaceId: UUID!, $definitionId: UUID!) {
  createSource(input: {
    name: "Production Postgres"
    workspaceId: $workspaceId
    definitionId: $definitionId
    configuration: {
      host: "db.example.com"
      port: 5432
      database: "prod"
      username: "airbyte"
      password: "secret"
    }
  }) {
    sourceId
    name
    sourceType
    createdAt
  }
}
```

### Poll job status

```graphql
query GetJobStatus($jobId: UUID!) {
  job(jobId: $jobId) {
    id
    status
    jobType
    startedAt
    bytesSynced
    rowsSynced
    connection {
      connectionId
      name
    }
  }
}
```

## Data Transformation Mappers

Mappers are applied per-stream within a connection to transform data in transit:

- **Hashing** — mask PII by hashing field values (SHA-256, MD5, etc.)
- **Field Renaming** — rename source fields at the destination
- **Field Filtering** — include or exclude specific columns
- **Row Filtering** — drop rows matching filter conditions
- **Encryption** — encrypt field values using AES-CBC or RSA

## Related Resources

- [Airbyte API Reference](https://reference.airbyte.com/reference/start)
- [Airbyte Documentation](https://docs.airbyte.com)
- [airbyte-platform OpenAPI Specs](https://github.com/airbytehq/airbyte-platform/tree/main/airbyte-api/server-api/src/main/openapi)
- [GraphQL Schema](airbyte-schema.graphql)
