# Airbyte (airbyte)
Airbyte is an open-source data integration platform that enables businesses to easily and efficiently move and consolidate their data from various sources into one centralized location. With Airbyte, organizations can seamlessly connect and synchronize data from sources such as databases, APIs, and other third-party applications, allowing for real-time insights and analysis. Airbyte offers both self-hosted and cloud-hosted options, with a catalog of hundreds of pre-built connectors.

**URL:** [Visit APIs.json URL](https://raw.githubusercontent.com/api-evangelist/airbyte/refs/heads/main/apis.yml)

**Run:** [Capabilities Using Naftiko](https://github.com/naftiko/fleet?utm_source=api-evangelist&utm_medium=readme&utm_campaign=company-api-evangelist&utm_content=repo)

## Tags:

 - Data Integration, ETL, ELT, Open Source, Data Pipeline, Connectors, Data

## Timestamps

- **Created:** 2025-01-08
- **Modified:** 2026-04-19

## APIs

### Airbyte
Airbyte is an open-source data integration platform that enables businesses to move and consolidate data from various sources into centralized destinations. The Airbyte API provides programmatic control over sources, destinations, connections, jobs, workspaces, and organizations for both Airbyte Cloud and self-managed deployments.

**Human URL:** [https://airbyte.com](https://airbyte.com)

#### Tags:

 - Data Integration, ETL, ELT, Open Source, Data Pipeline, Connectors

#### Properties

- [Documentation](https://docs.airbyte.com)
- [APIReference](https://reference.airbyte.com/reference/getting-started)
- [OpenAPI](https://raw.githubusercontent.com/api-evangelist/airbyte/refs/heads/main/openapi/airbyte-openapi.yml)
- [Authentication](https://docs.airbyte.com/api-documentation)
- [Python SDK](https://github.com/airbytehq/airbyte-api-python-sdk)
- [Java SDK](https://github.com/airbytehq/airbyte-api-java-sdk)
- [Python SDK PyPI](https://pypi.org/project/airbyte-api/)
- [Terraform Provider](https://github.com/airbytehq/terraform-provider-airbyte)

## Common Properties

- [Portal](https://airbyte.com)
- [Console](https://cloud.airbyte.io)
- [SignUp](https://cloud.airbyte.io)
- [Pricing](https://airbyte.com/pricing)
- [GitHubOrganization](https://github.com/airbytehq)
- [GitHubRepository](https://github.com/airbytehq/airbyte)
- [GettingStarted](https://docs.airbyte.com)
- [StatusPage](https://status.airbyte.com)
- [Blog](https://airbyte.com/blog)
- [Tutorials](https://airbyte.com/tutorials)
- [Support](https://support.airbyte.com/hc/en-us)
- [PrivacyPolicy](https://airbyte.com/company/privacy-policy)
- [TermsOfService](https://airbyte.com/company/terms)
- [Newsletter](https://airbyte.com/community/newsletter)
- [ChangeLog](https://docs.airbyte.com/category/release-notes/)
- [RoadMap](https://github.com/orgs/airbytehq/projects/37/views/1)
- [Integrations](https://airbyte.com/connectors)
- [PyAirbyte](https://github.com/airbytehq/PyAirbyte)
- [CLI - Airbyte CLI (abctl)](https://github.com/airbytehq/abctl)
- [Python Connector CDK](https://github.com/airbytehq/airbyte-python-cdk)
- [Agent SDK](https://github.com/airbytehq/airbyte-agent-sdk)
- [Helm Chart](https://artifacthub.io/packages/helm/airbyte/airbyte)
- [SpectralRules](https://raw.githubusercontent.com/api-evangelist/airbyte/refs/heads/main/rules/airbyte-spectral-rules.yml)
- [NaftikoCapability - Data Pipeline Management](https://raw.githubusercontent.com/api-evangelist/airbyte/refs/heads/main/capabilities/data-pipeline-management.yaml)
- [Vocabulary](https://raw.githubusercontent.com/api-evangelist/airbyte/refs/heads/main/vocabulary/airbyte-vocabulary.yaml)

## Features

| Name | Description |
|------|-------------|
| Data Integration | Connect and sync data from hundreds of sources to destinations. |
| Open Source | Self-host Airbyte on your own infrastructure with full access to source code. |
| Cloud Hosted | Managed cloud offering with 30-day free trial at cloud.airbyte.io. |
| Connector Catalog | Pre-built connectors for databases, APIs, SaaS tools, and data warehouses. |
| Custom Connectors | Build custom connectors using the Python CDK or low-code/no-code builder. |
| AI Agent Integration | Airbyte Agent SDK provides AI agents with reliable, permission-aware access to data sources. |
| Terraform Support | Manage Airbyte infrastructure and connections as code with Terraform. |
| MCP Servers | Model Context Protocol support for integration with AI tools. |
| Embedded Widget | Embed Airbyte connector UI into your own product for white-label data integration. |
| PyAirbyte | Python library for using Airbyte connectors programmatically in Python environments. |

## Use Cases

| Name | Description |
|------|-------------|
| Data Warehouse Loading | Sync operational data to Snowflake, BigQuery, Redshift, or other warehouses. |
| Data Lake Ingestion | Land raw data into S3, GCS, or Azure data lakes. |
| Analytics Pipelines | Build ELT pipelines for business intelligence and analytics. |
| AI/ML Data Preparation | Aggregate training data from multiple sources for machine learning. |
| API Data Sync | Pull data from SaaS APIs (Salesforce, HubSpot, Stripe) into your data stack. |
| Database Replication | Replicate relational databases with CDC change data capture. |
| Vector Database Population | Load and embed data into vector stores for AI search and retrieval. |

## Integrations

| Name | Description |
|------|-------------|
| Apache Airflow | Orchestrate Airbyte syncs from Airflow DAGs. |
| dbt | Transform data after Airbyte syncs with dbt models. |
| Snowflake | Load data into Snowflake data warehouse. |
| BigQuery | Sync data to Google BigQuery. |
| Redshift | Load data into Amazon Redshift. |
| Databricks | Ingest data into Databricks lakehouse. |
| Terraform | Infrastructure-as-code support for Airbyte resources. |
| Kubernetes / Helm | Deploy Airbyte on Kubernetes using official Helm charts. |

## Artifacts

Machine-readable API specifications organized by format.

### OpenAPI

- [Airbyte OpenAPI](openapi/airbyte-openapi.yml)

### JSON Schema

142 schema files covering all Airbyte API resources and data models, including SourceResponse, DestinationResponse, ConnectionResponse, JobResponse, WorkspaceResponse, and more.

### JSON Structure

139 JSON Structure (json-structure.org) files converted from JSON Schema.

### JSON-LD

- [Airbyte Context](json-ld/airbyte-context.jsonld)

### Examples

142 example JSON files generated from JSON Schema definitions.

## Capabilities

Naftiko capabilities organized as shared per-API definitions composed into customer-facing workflows.

### Shared Per-API Definitions

- [Airbyte API](capabilities/shared/airbyte-api.yaml) — 10 operations for data integration management

### Workflow Capabilities

| Workflow | APIs Combined | Tools | Persona |
|----------|--------------|-------|---------|
| [Data Pipeline Management](capabilities/data-pipeline-management.yaml) | Airbyte API | 11 | Data Engineer, Platform Admin |

## Vocabulary

- [Airbyte Vocabulary](vocabulary/airbyte-vocabulary.yaml) — Unified taxonomy mapping 11 resources, 7 actions, 1 workflow, and 2 personas across operational (OpenAPI) and capability (Naftiko) dimensions

## Rules

- [Airbyte Spectral Rules](rules/airbyte-spectral-rules.yml) — 30 rules across 13 categories enforcing Airbyte API conventions

## Maintainers

**FN:** Kin Lane

**Email:** kin@apievangelist.com
