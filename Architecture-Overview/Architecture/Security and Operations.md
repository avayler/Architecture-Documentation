# Security and Operations

## Identity and access

- Use a managed identity provider with customer-instance-aware claims and role-based access control.
- Authenticate browser and partner traffic at API Gateway; authorise the requested business action in the owning service.
- Give each Lambda and integration adapter a least-privilege IAM role.
- Keep secrets in AWS Secrets Manager or an equivalent managed store; never commit credentials or place them in logs.
- Separate production from non-production accounts and access paths.

## Current account isolation

The current isolation boundary is the AWS account: each customer and environment is deployed to a separate account. This reduces the blast radius of a breach or service failure and allows customer and environment access, deployment, monitoring, quotas, and recovery to be governed independently.

Within an account, every request, event, and persisted aggregate must carry the customer-instance context where applicable. Services must enforce that context server-side and must not rely on a client-supplied customer or account identifier. Cross-customer access is not part of the normal runtime model and requires an explicit operational access path and audit record.

## Future multi-tenant aspiration

Shared multi-tenant hosting may be evaluated in the future to improve deployment efficiency or reduce operational duplication. It is not the current architecture. Any move to shared tenancy requires a documented decision covering isolation, data partitioning, identity, noisy-neighbour controls, breach containment, migration, and customer/regulatory acceptance.

## Network and data protection

Use private networking for RDS and internal dependencies, controlled egress for partner calls, TLS for all service communication, encrypted RDS and S3 storage, and KMS key policies aligned to data ownership. Apply S3 public-access blocks and verify them continuously.

## Observability

Every request and event carries a correlation ID. Capture structured logs, latency, error rates, throttles, Lambda duration, queue age, dead-letter counts, database health, and partner response outcomes. Dashboards and alarms should reflect customer journeys such as order completion, booking, payment, and invoice issuance.

## Resilience

Define timeouts, retry limits, idempotency keys, concurrency limits, and failure responses per integration. Protect RDS from Lambda connection bursts with appropriate pooling or proxying. Use queues for load smoothing and dead-letter queues for operator intervention. Test restore, replay, and partner outage procedures.

## Delivery

Build, test, scan, and deploy each service independently through infrastructure-as-code and an approved CI/CD pipeline. Use immutable artifacts, environment promotion, automated rollback signals, contract tests, and database migration controls. Record environment-specific details in [AWS Environments](../AWS%20Environments.md), replacing the current cost-only table with account, region, ownership, and lifecycle information.
