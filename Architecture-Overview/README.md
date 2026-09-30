# Avayler Architecture Overview

This folder describes the architecture for Avayler, a vehicle workshop management platform deployed to AWS. Multi-tenant operation is an aspiration, not the current deployment model.

The platform supports point-of-sale, point-of-service, administration, workshop operations, scheduling, customer and vehicle management, commerce, and external business integrations.

### Start here

1. [Platform Architecture](Architecture-Overview/Architecture/Platform%20Architecture.md) - system context, runtime topology, and service boundaries.
2. [Domain Architecture](Architecture-Overview/Architecture/Domain%20Architecture.md) - bounded contexts, ownership, and the Order snapshot pattern.
3. [Integration Architecture](Architecture-Overview/Architecture/Integration%20Architecture.md) - API, events, partner integrations, and failure handling.
4. [Data Architecture](Architecture-Overview/Architecture/Data%20Architecture.md) - master data, transactional data, storage, and data movement.
5. [Security and Operations](Architecture-Overview/Architecture/Security%20and%20Operations.md) - identity, tenancy, observability, resilience, and delivery.
6. [Architecture Decisions](Architecture-Overview/Architecture/Architecture%20Decisions.md) - decisions and open questions that require governance.
7. [Operational Processes](Architecture-Overview/Processes/Operational%20Processes.md) - the workshop lifecycle from booking to completion.

### Documentation conventions

- **Target** describes the intended architecture.
- **Current** describes an observed implementation or existing integration.
- **Decision required** identifies an unresolved governance item.
- Service names describe business capabilities, not AWS resources.
- Diagrams show logical ownership. Deployment details belong in infrastructure repositories and runbooks.

### Scope and assumptions

This overview assumes .NET microservices deployed primarily as AWS Lambda functions behind API Gateway, with S3 and relational databases used according to workload needs. The web application is a React frontend with a Node.js backend-for-frontend or edge layer. The current operating model provisions a separate AWS account for each customer and environment required, such as development, test, staging, and production. Exact region, engine, and capacity choices are environment-specific and must be confirmed through infrastructure-as-code.
