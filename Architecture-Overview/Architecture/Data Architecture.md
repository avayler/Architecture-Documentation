# Data Architecture

## Data ownership

Each microservice owns its persistence boundary. Other services consume published APIs or events. Shared reporting is built from governed projections or an analytics store, never from cross-service joins against operational tables.

| Data class | Owner | Recommended storage |
| --- | --- | --- |
| Customer, contact, consent | Customer | RDS for transactional records; controlled exports for integration |
| Vehicle identity and attributes | Vehicle | RDS; S3 only for supporting documents |
| Orders and order snapshots | Order | RDS with transactional consistency and audit history |
| Jobs, inspections, tasks | Job and Workshop | RDS; S3 for images and attachments |
| Appointments and capacity | Scheduling | RDS or a purpose-built scheduling store |
| Catalog, parts, suppliers, pricing | Catalog/Pricing and Procurement | RDS; S3 for bulk reference imports |
| Payments and invoices | Payment and Invoice | RDS with immutable audit records |
| Documents and media | Owning service | S3 with encryption, retention, and metadata |
| Events and integration delivery state | Integration / owning service | Durable queues plus RDS or event archive |

## Storage rules

- RDS is the default for relational aggregates, constraints, and transactional workflows.
- S3 is the default for large objects, documents, media, exports, and immutable raw inbound files.
- Store object metadata and business ownership in RDS; store the object body in S3.
- Use encryption at rest and in transit, private buckets, restrictive IAM policies, and lifecycle rules.
- Backups, point-in-time recovery, retention, and restore testing are part of the service's operational contract.

## Master and transactional data

Master data is canonical and reusable across transactions. Transactional data records what happened in a particular business process. An Order stores a snapshot of relevant Customer and Vehicle values so that later master-data changes cannot rewrite a historical commercial record. The [Domain Architecture](Domain%20Architecture.md) defines the update and propagation rules.

## Data quality

Required fields, identifiers, country-specific address rules, and reference-data lifecycle must be owned by the relevant service. Validate at ingestion and at command boundaries. Preserve source-system identifiers for reconciliation, but do not use them as internal domain identifiers without an explicit decision.

## Reporting and retention

Operational queries stay within the owning service or a maintained read model. Reporting extracts are versioned, access-controlled, and classified. Personal and payment data must have an approved retention period, deletion or anonymisation process, and audit trail before production rollout.
