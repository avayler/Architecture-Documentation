# Domain Architecture

## Bounded contexts

Avayler is organised around business capabilities. A bounded context owns its terminology, rules, API contract, and persistence. Similar words such as *customer*, *vehicle*, and *status* must not be assumed to have identical meaning in every context.

| Context | Core responsibility | Source of truth |
| --- | --- | --- |
| Customer and Vehicle | Canonical party and vehicle records | Customer and Vehicle services |
| Workshop Operations | Work orders, inspections, tasks, and technician progress | Job and Workshop service |
| Commerce | Cart, order lines, pricing, discounts, tax, and invoice lifecycle | Order, Catalog/Pricing, and Invoice services |
| Scheduling | Appointment, resource, capacity, and allocation decisions | Scheduling service |
| Payments | Payment lifecycle and provider reconciliation | Payment service |
| Procurement | Supplier, purchase order, and receiving workflows | Procurement service |
| Identity and Access | User access, customer-instance membership, and policy | User and Access service |
| Integration | External contracts, translations, delivery, and replay | Integration service plus owning domain service |

## Order snapshot pattern

An Order is a transactional record, not a live view of master data.

1. When an order is created, the Order service obtains the relevant Customer and Vehicle records.
2. It stores the required displayable and processable values as an order snapshot, alongside the canonical identifiers.
3. During the active order, clients read customer and vehicle details from the snapshot. They do not repeatedly query master services.
4. Corrections made during the order update the snapshot first. The Order service then propagates approved corrections to the owning master service.
5. At invoicing and audit boundaries, the snapshot remains immutable except through an explicit correction or adjustment workflow.

This protects the commercial record from later master-data changes and avoids circular read dependencies.

## Ownership rules

- Customer and Vehicle services own canonical records and identifiers.
- Order owns the transaction-time representation and commercial state.
- Job owns workshop execution state; it references the Order and does not own pricing or payment truth.
- Scheduling owns appointments and capacity decisions; it does not own work-order completion.
- Invoice owns issued financial documents; it is not a recalculation engine for historical orders.
- Integration adapters translate external models at the boundary. External schemas must not leak into domain aggregates.

## Consistency model

- Intra-service invariants are enforced transactionally.
- Cross-service propagation is eventually consistent and event-driven where possible.
- Every command and event has a stable identifier and correlation identifier.
- Consumers must be idempotent; repeated delivery must not create duplicate orders, payments, invoices, or updates.
- Conflicts are surfaced as business outcomes, not hidden by last-write-wins updates.

## Domain language

The [Master Data Matrix](../Master%20Data%20Matrix.md) and individual pages under [Master Data Matrix](../Master%20Data%20Matrix/) contain the detailed field proposals. They should be treated as reference material until ownership, lifecycle, and validation rules are confirmed by the domain owners.
