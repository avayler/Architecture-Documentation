# Architecture Decisions

This is the decision register for the target architecture. A decision is complete only when its owner, date, options, consequences, and implementation impact are recorded.

## Confirmed direction

| Decision | Rationale |
| --- | --- |
| Use .NET microservices on AWS Lambda behind API Gateway | Independent business capability deployment with managed scaling and a common platform runtime |
| Use React with a Node.js BFF/edge layer for POS and administration | A responsive web experience with server-side aggregation and policy where needed |
| Keep service-owned persistence | Prevents coupling and preserves bounded-context ownership |
| Use RDS for transactional relational data and S3 for documents/bulk objects | Matches relational workflows and durable object storage needs |
| Treat the Order snapshot as the active transaction view | Preserves contractual history and prevents live master-data drift |
| Prefer asynchronous events for propagation and integration | Improves resilience and reduces synchronous dependency chains |
| Deploy a separate AWS account for each customer and environment | Reduces breach and failure blast radius and provides independent access, change, and recovery boundaries |

## Decisions required

| Topic | Question |
| --- | --- |
| Event backbone | Which AWS event bus, queue, schema registry, and event retention policy are standard? |
| Identity | Which managed identity provider and customer-instance model are authoritative? |
| RDS topology | Which engine, account/region topology, proxy, backup, and failover tier are required within the account-isolated model? |
| API governance | Which versioning, deprecation, partner onboarding, and contract-testing process is mandatory? |
| Integration ownership | Which team owns each partner adapter and its production SLA? |
| Data retention | What are the retention, deletion, anonymisation, and residency rules by data class? |
| Scheduling | Is scheduling a platform capability, a dedicated service, or an external engine integration? |
| Frontend runtime | Which hosting and deployment pattern is standard for React assets and the Node.js BFF? |
| Shared multi-tenancy | If and when should Avayler move from account-per-customer-and-environment to shared multi-tenant hosting, and what isolation evidence is required? |
