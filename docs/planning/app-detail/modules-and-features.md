# Service And Resource Design Studio App Modules And Features

Reviewed: 2026-06-06

This document expands each app module into feature-level planning guidance. It should be used to create epics, stories, API contracts, event contracts, screens, permissions, and test cases.

Source overview: [service-and-resource-design-studio.md](../service-and-resource-design-studio.md)

## App-Level Feature Principles

- Every feature must have an owning module and an owning app API.
- UI actions must call app APIs rather than writing directly to shared data stores.
- Cross-app reads should use APIs, subscribed events, governed projections, or data products.
- Each module should expose enough lifecycle state for operations, audit, automation, and customer/partner visibility.
- Feature design must include happy path, exception path, audit path, and reporting path.

## App Data Ownership Context

Owns service specifications, resource specifications, realization rules, technical compatibility rules, design templates, and entity templates. It does not own active inventory or customer product instances.

## First Release Context

Deliver service catalog, resource catalog, product-service-resource mapping, and basic compatibility validation for the first supported products. Add advanced model extension and technology-specific design automation over time.

## Module 1: Service Catalog

Anchor: `service-catalog`

### Capability Intent

Manage customer-facing and resource-facing service specs, characteristics, relationships, dependencies, lifecycle, versioning, product mapping, release, retirement, and compatibility.

### Primary Personas Supported

- Service designer: models customer-facing and resource-facing service specifications.
- Resource designer: models reusable physical, logical, cloud, software, and network resources.
- Network engineer: validates technology-specific design and compatibility.
- Product/catalog governance user: confirms product-service-resource mapping before offer launch.
- Fulfillment architect: defines decomposition and activation patterns.

### Feature Backlog Candidates

- Manage customer-facing and resource-facing service specs.
- Characteristics.
- Relationships.
- Dependencies.
- Product mapping.
- And compatibility.

### Feature Groups

| Feature group | Feature detail |
| --- | --- |
| Record and lifecycle management | Create, search, view, update, retire, reinstate, and track lifecycle state for service catalog records. Maintain ownership, status reason, timestamps, and relationships to upstream and downstream entities. |
| Validation, policy, and eligibility | Validate service catalog changes against catalog rules, customer/account context, serviceability, inventory state, compliance policy, role permissions, and data-quality constraints relevant to this app. |
| Work queues and approvals | Provide queues for draft, pending approval, blocked, exception, fallout, rejected, completed, and archived work. Support assignment, SLA/OLA tracking, escalation, comments, and handoff. |
| Search, timeline, and operational views | Offer filtered search, saved views, dependency views, lifecycle timeline, related orders/tickets/events, and persona-specific dashboards for service catalog work. |
| API and event behavior | Expose command, query, and event contracts for service catalog so UIs, workflows, partner channels, analytics, and downstream apps do not bypass the owning app. |
| Audit, evidence, and reporting | Capture actor, reason, before/after state, source channel, approval evidence, policy decisions, and reporting measures needed for operations, compliance, and continuous improvement. |

### User Journey Coverage

| Journey | Trigger | App behavior | Successful outcome |
| --- | --- | --- | --- |
| Maintain Service Catalog | User creates or updates domain information | Validate context, capture change, publish event, update projections | Accurate service catalog state available through APIs |
| Handle Service Catalog exception | Conflict, validation failure, policy exception, fallout, or missing dependency | Route to owner, capture evidence, resolve or escalate, notify dependent work | Exception closed with auditable reason and downstream handoff |
| Review Service Catalog performance | Supervisor, planner, compliance, or operations user needs visibility | Filter records, inspect trend, export/report, create follow-up task | Actionable operational insight and accountable next step |

### API And Integration Alignment

Related APIs and API areas: [TMF633](../../../../references/tmforum-open-apis/openapi-specs/TMF633_ServiceCatalog), [TMF620](../../../../references/tmforum-open-apis/openapi-specs/TMF620_ProductCatalog)

Implementation guidance:

- Provide create, read, update, lifecycle transition, search, event notification, and audit retrieval behavior where the domain lifecycle requires it.
- Publish domain events for state changes that other apps need for projections, workflow triggers, analytics, or customer/partner communication.
- Keep integration retries, idempotency keys, correlation IDs, and external reference IDs visible to operators.

### Data, Control, And Reporting Needs

- Store app-owned operational records in the app's logical database defined in the database setup document.
- Store external IDs, source channel, owner, status reason, timestamps, and relationship references needed for traceability.
- Provide operational metrics for volume, aging, fallout, SLA/OLA status, exception rate, policy overrides, and automation success.
- Support role-based access, tenant/region boundaries, sensitive-data masking, and export controls where applicable.

### First Release Interpretation

For the first release, implement the minimum lifecycle, search, validation, API, event, audit, and operational queue behavior needed for this module to participate in the app's core workflow. Advanced automation, AI assistance, bulk optimization, simulation, and deep analytics can follow after the app proves the core operating loop.

## Module 2: Resource Catalog

Anchor: `resource-catalog`

### Capability Intent

Manage physical, logical, compute, software, and network resource specs. Define resource characteristics, compatibility, capacity units, lifecycle, reusable templates, activation links, and inventory model links.

### Primary Personas Supported

- Service designer: models customer-facing and resource-facing service specifications.
- Resource designer: models reusable physical, logical, cloud, software, and network resources.
- Network engineer: validates technology-specific design and compatibility.
- Product/catalog governance user: confirms product-service-resource mapping before offer launch.
- Fulfillment architect: defines decomposition and activation patterns.

### Feature Backlog Candidates

- Manage physical.
- And network resource specs.
- Define resource characteristics.
- Compatibility.
- Capacity units.
- Reusable templates.
- Activation links.
- And inventory model links.

### Feature Groups

| Feature group | Feature detail |
| --- | --- |
| Record and lifecycle management | Create, search, view, update, retire, reinstate, and track lifecycle state for resource catalog records. Maintain ownership, status reason, timestamps, and relationships to upstream and downstream entities. |
| Validation, policy, and eligibility | Validate resource catalog changes against catalog rules, customer/account context, serviceability, inventory state, compliance policy, role permissions, and data-quality constraints relevant to this app. |
| Work queues and approvals | Provide queues for draft, pending approval, blocked, exception, fallout, rejected, completed, and archived work. Support assignment, SLA/OLA tracking, escalation, comments, and handoff. |
| Search, timeline, and operational views | Offer filtered search, saved views, dependency views, lifecycle timeline, related orders/tickets/events, and persona-specific dashboards for resource catalog work. |
| API and event behavior | Expose command, query, and event contracts for resource catalog so UIs, workflows, partner channels, analytics, and downstream apps do not bypass the owning app. |
| Audit, evidence, and reporting | Capture actor, reason, before/after state, source channel, approval evidence, policy decisions, and reporting measures needed for operations, compliance, and continuous improvement. |

### User Journey Coverage

| Journey | Trigger | App behavior | Successful outcome |
| --- | --- | --- | --- |
| Maintain Resource Catalog | User creates or updates domain information | Validate context, capture change, publish event, update projections | Accurate resource catalog state available through APIs |
| Handle Resource Catalog exception | Conflict, validation failure, policy exception, fallout, or missing dependency | Route to owner, capture evidence, resolve or escalate, notify dependent work | Exception closed with auditable reason and downstream handoff |
| Review Resource Catalog performance | Supervisor, planner, compliance, or operations user needs visibility | Filter records, inspect trend, export/report, create follow-up task | Actionable operational insight and accountable next step |

### API And Integration Alignment

Related APIs and API areas: [TMF634](../../../../references/tmforum-open-apis/openapi-specs/TMF634_ResourceCatalog), [TMF730](../../../../references/tmforum-open-apis/openapi-specs/TMF730_SoftwareAndComputeManagement)

Implementation guidance:

- Provide create, read, update, lifecycle transition, search, event notification, and audit retrieval behavior where the domain lifecycle requires it.
- Publish domain events for state changes that other apps need for projections, workflow triggers, analytics, or customer/partner communication.
- Keep integration retries, idempotency keys, correlation IDs, and external reference IDs visible to operators.

### Data, Control, And Reporting Needs

- Store app-owned operational records in the app's logical database defined in the database setup document.
- Store external IDs, source channel, owner, status reason, timestamps, and relationship references needed for traceability.
- Provide operational metrics for volume, aging, fallout, SLA/OLA status, exception rate, policy overrides, and automation success.
- Support role-based access, tenant/region boundaries, sensitive-data masking, and export controls where applicable.

### First Release Interpretation

For the first release, implement the minimum lifecycle, search, validation, API, event, audit, and operational queue behavior needed for this module to participate in the app's core workflow. Advanced automation, AI assistance, bulk optimization, simulation, and deep analytics can follow after the app proves the core operating loop.

## Module 3: Product-Service-Resource Mapping

Anchor: `product-service-resource-mapping`

### Capability Intent

Define how products decompose into services and resources across fiber, mobile, fixed wireless, enterprise VPN, IoT, NaaS, cloud connectivity, and partner products. Provide rules to order orchestration.

### Primary Personas Supported

- Service designer: models customer-facing and resource-facing service specifications.
- Resource designer: models reusable physical, logical, cloud, software, and network resources.
- Network engineer: validates technology-specific design and compatibility.
- Product/catalog governance user: confirms product-service-resource mapping before offer launch.
- Fulfillment architect: defines decomposition and activation patterns.

### Feature Backlog Candidates

- Define how products decompose into services and resources across fiber.
- Fixed wireless.
- Enterprise VPN.
- Cloud connectivity.
- And partner products.
- Provide rules to order orchestration.

### Feature Groups

| Feature group | Feature detail |
| --- | --- |
| Record and lifecycle management | Create, search, view, update, retire, reinstate, and track lifecycle state for product-service-resource mapping records. Maintain ownership, status reason, timestamps, and relationships to upstream and downstream entities. |
| Validation, policy, and eligibility | Validate product-service-resource mapping changes against catalog rules, customer/account context, serviceability, inventory state, compliance policy, role permissions, and data-quality constraints relevant to this app. |
| Work queues and approvals | Provide queues for draft, pending approval, blocked, exception, fallout, rejected, completed, and archived work. Support assignment, SLA/OLA tracking, escalation, comments, and handoff. |
| Search, timeline, and operational views | Offer filtered search, saved views, dependency views, lifecycle timeline, related orders/tickets/events, and persona-specific dashboards for product-service-resource mapping work. |
| API and event behavior | Expose command, query, and event contracts for product-service-resource mapping so UIs, workflows, partner channels, analytics, and downstream apps do not bypass the owning app. |
| Audit, evidence, and reporting | Capture actor, reason, before/after state, source channel, approval evidence, policy decisions, and reporting measures needed for operations, compliance, and continuous improvement. |

### User Journey Coverage

| Journey | Trigger | App behavior | Successful outcome |
| --- | --- | --- | --- |
| Maintain Product-Service-Resource Mapping | User creates or updates domain information | Validate context, capture change, publish event, update projections | Accurate product-service-resource mapping state available through APIs |
| Handle Product-Service-Resource Mapping exception | Conflict, validation failure, policy exception, fallout, or missing dependency | Route to owner, capture evidence, resolve or escalate, notify dependent work | Exception closed with auditable reason and downstream handoff |
| Review Product-Service-Resource Mapping performance | Supervisor, planner, compliance, or operations user needs visibility | Filter records, inspect trend, export/report, create follow-up task | Actionable operational insight and accountable next step |

### API And Integration Alignment

Related APIs and API areas: [TMF620](../../../../references/tmforum-open-apis/openapi-specs/TMF620_ProductCatalog), [TMF633](../../../../references/tmforum-open-apis/openapi-specs/TMF633_ServiceCatalog), [TMF634](../../../../references/tmforum-open-apis/openapi-specs/TMF634_ResourceCatalog), [TMF701](../../../../references/tmforum-open-apis/openapi-specs/TMF701_ProcessFlow)

Implementation guidance:

- Provide create, read, update, lifecycle transition, search, event notification, and audit retrieval behavior where the domain lifecycle requires it.
- Publish domain events for state changes that other apps need for projections, workflow triggers, analytics, or customer/partner communication.
- Keep integration retries, idempotency keys, correlation IDs, and external reference IDs visible to operators.

### Data, Control, And Reporting Needs

- Store app-owned operational records in the app's logical database defined in the database setup document.
- Store external IDs, source channel, owner, status reason, timestamps, and relationship references needed for traceability.
- Provide operational metrics for volume, aging, fallout, SLA/OLA status, exception rate, policy overrides, and automation success.
- Support role-based access, tenant/region boundaries, sensitive-data masking, and export controls where applicable.

### First Release Interpretation

For the first release, implement the minimum lifecycle, search, validation, API, event, audit, and operational queue behavior needed for this module to participate in the app's core workflow. Advanced automation, AI assistance, bulk optimization, simulation, and deep analytics can follow after the app proves the core operating loop.

## Module 4: Technical Compatibility And Design Rule

Anchor: `technical-compatibility-and-design-rule`

### Capability Intent

Define compatibility rules across products, services, resources, technologies, locations, customer types, topology, serviceability, and capacity pools. Support exception approvals and feasibility checks.

### Primary Personas Supported

- Service designer: models customer-facing and resource-facing service specifications.
- Resource designer: models reusable physical, logical, cloud, software, and network resources.
- Network engineer: validates technology-specific design and compatibility.
- Product/catalog governance user: confirms product-service-resource mapping before offer launch.
- Fulfillment architect: defines decomposition and activation patterns.

### Feature Backlog Candidates

- Define compatibility rules across products.
- Technologies.
- Customer types.
- Serviceability.
- And capacity pools.
- Support exception approvals and feasibility checks.

### Feature Groups

| Feature group | Feature detail |
| --- | --- |
| Record and lifecycle management | Create, search, view, update, retire, reinstate, and track lifecycle state for technical compatibility and design rule records. Maintain ownership, status reason, timestamps, and relationships to upstream and downstream entities. |
| Validation, policy, and eligibility | Validate technical compatibility and design rule changes against catalog rules, customer/account context, serviceability, inventory state, compliance policy, role permissions, and data-quality constraints relevant to this app. |
| Work queues and approvals | Provide queues for draft, pending approval, blocked, exception, fallout, rejected, completed, and archived work. Support assignment, SLA/OLA tracking, escalation, comments, and handoff. |
| Search, timeline, and operational views | Offer filtered search, saved views, dependency views, lifecycle timeline, related orders/tickets/events, and persona-specific dashboards for technical compatibility and design rule work. |
| API and event behavior | Expose command, query, and event contracts for technical compatibility and design rule so UIs, workflows, partner channels, analytics, and downstream apps do not bypass the owning app. |
| Audit, evidence, and reporting | Capture actor, reason, before/after state, source channel, approval evidence, policy decisions, and reporting measures needed for operations, compliance, and continuous improvement. |

### User Journey Coverage

| Journey | Trigger | App behavior | Successful outcome |
| --- | --- | --- | --- |
| Maintain Technical Compatibility And Design Rule | User creates or updates domain information | Validate context, capture change, publish event, update projections | Accurate technical compatibility and design rule state available through APIs |
| Handle Technical Compatibility And Design Rule exception | Conflict, validation failure, policy exception, fallout, or missing dependency | Route to owner, capture evidence, resolve or escalate, notify dependent work | Exception closed with auditable reason and downstream handoff |
| Review Technical Compatibility And Design Rule performance | Supervisor, planner, compliance, or operations user needs visibility | Filter records, inspect trend, export/report, create follow-up task | Actionable operational insight and accountable next step |

### API And Integration Alignment

Related APIs and API areas: [TMF645](../../../../references/tmforum-open-apis/openapi-specs/TMF645_ServiceQualification), [TMF679](../../../../references/tmforum-open-apis/openapi-specs/TMF679_ProductOfferingQualification)

Implementation guidance:

- Provide create, read, update, lifecycle transition, search, event notification, and audit retrieval behavior where the domain lifecycle requires it.
- Publish domain events for state changes that other apps need for projections, workflow triggers, analytics, or customer/partner communication.
- Keep integration retries, idempotency keys, correlation IDs, and external reference IDs visible to operators.

### Data, Control, And Reporting Needs

- Store app-owned operational records in the app's logical database defined in the database setup document.
- Store external IDs, source channel, owner, status reason, timestamps, and relationship references needed for traceability.
- Provide operational metrics for volume, aging, fallout, SLA/OLA status, exception rate, policy overrides, and automation success.
- Support role-based access, tenant/region boundaries, sensitive-data masking, and export controls where applicable.

### First Release Interpretation

For the first release, implement the minimum lifecycle, search, validation, API, event, audit, and operational queue behavior needed for this module to participate in the app's core workflow. Advanced automation, AI assistance, bulk optimization, simulation, and deep analytics can follow after the app proves the core operating loop.

## Module 5: Entity Catalog

Anchor: `entity-catalog`

### Capability Intent

Define reusable entity types, metadata, templates, relationships, extension points, and versioning shared across service, resource, inventory, and assurance models.

### Primary Personas Supported

- Service designer: models customer-facing and resource-facing service specifications.
- Resource designer: models reusable physical, logical, cloud, software, and network resources.
- Network engineer: validates technology-specific design and compatibility.
- Product/catalog governance user: confirms product-service-resource mapping before offer launch.
- Fulfillment architect: defines decomposition and activation patterns.

### Feature Backlog Candidates

- Define reusable entity types.
- Relationships.
- Extension points.
- And versioning shared across service.
- And assurance models.

### Feature Groups

| Feature group | Feature detail |
| --- | --- |
| Record and lifecycle management | Create, search, view, update, retire, reinstate, and track lifecycle state for entity catalog records. Maintain ownership, status reason, timestamps, and relationships to upstream and downstream entities. |
| Validation, policy, and eligibility | Validate entity catalog changes against catalog rules, customer/account context, serviceability, inventory state, compliance policy, role permissions, and data-quality constraints relevant to this app. |
| Work queues and approvals | Provide queues for draft, pending approval, blocked, exception, fallout, rejected, completed, and archived work. Support assignment, SLA/OLA tracking, escalation, comments, and handoff. |
| Search, timeline, and operational views | Offer filtered search, saved views, dependency views, lifecycle timeline, related orders/tickets/events, and persona-specific dashboards for entity catalog work. |
| API and event behavior | Expose command, query, and event contracts for entity catalog so UIs, workflows, partner channels, analytics, and downstream apps do not bypass the owning app. |
| Audit, evidence, and reporting | Capture actor, reason, before/after state, source channel, approval evidence, policy decisions, and reporting measures needed for operations, compliance, and continuous improvement. |

### User Journey Coverage

| Journey | Trigger | App behavior | Successful outcome |
| --- | --- | --- | --- |
| Maintain Entity Catalog | User creates or updates domain information | Validate context, capture change, publish event, update projections | Accurate entity catalog state available through APIs |
| Handle Entity Catalog exception | Conflict, validation failure, policy exception, fallout, or missing dependency | Route to owner, capture evidence, resolve or escalate, notify dependent work | Exception closed with auditable reason and downstream handoff |
| Review Entity Catalog performance | Supervisor, planner, compliance, or operations user needs visibility | Filter records, inspect trend, export/report, create follow-up task | Actionable operational insight and accountable next step |

### API And Integration Alignment

Related APIs and API areas: [TMF662](../../../../references/tmforum-open-apis/openapi-specs/TMF662_EntityCatalog)

Implementation guidance:

- Provide create, read, update, lifecycle transition, search, event notification, and audit retrieval behavior where the domain lifecycle requires it.
- Publish domain events for state changes that other apps need for projections, workflow triggers, analytics, or customer/partner communication.
- Keep integration retries, idempotency keys, correlation IDs, and external reference IDs visible to operators.

### Data, Control, And Reporting Needs

- Store app-owned operational records in the app's logical database defined in the database setup document.
- Store external IDs, source channel, owner, status reason, timestamps, and relationship references needed for traceability.
- Provide operational metrics for volume, aging, fallout, SLA/OLA status, exception rate, policy overrides, and automation success.
- Support role-based access, tenant/region boundaries, sensitive-data masking, and export controls where applicable.

### First Release Interpretation

For the first release, implement the minimum lifecycle, search, validation, API, event, audit, and operational queue behavior needed for this module to participate in the app's core workflow. Advanced automation, AI assistance, bulk optimization, simulation, and deep analytics can follow after the app proves the core operating loop.

## Critical Feature Review Enhancements (2026-06-14)

### Critical Assessment

The baseline modules are correct, but the app needs stronger design-governance behavior before implementation. This app must be the source for versioned service/resource definitions, realization rules, compatibility checks, decomposition hints, activation templates, and publication readiness so CPQ, order, fulfillment, inventory, and assurance do not create local technical rule copies.

### Enhancements To Add

| Enhancement | Modules | Implementation need |
| --- | --- | --- |
| Service/resource specification versioning | Service Catalog; Resource Catalog | Manage draft, reviewed, approved, active, superseded, retired, and rollback versions with effective dates, technology domain, market, and compatibility impact. |
| Product-service-resource mapping matrix | Product-Service-Resource Mapping | Map product offering/specification versions to service specs, resource specs, decomposition templates, inventory expectations, and activation patterns. |
| Technical compatibility validation | Technical Compatibility And Design Rule | Validate product, service, resource, location, topology, capacity, customer premises, device, software, and cloud constraints before publication. |
| Activation and decomposition template library | Product-Service-Resource Mapping; Entity Catalog | Define service/resource order hints, workflow pattern, controller adapter target, activation payload template, rollback behavior, and expected inventory handover. |
| Certification readiness gate | Service Catalog; Resource Catalog; Technical Compatibility And Design Rule | Require design review, test evidence, catalog mapping, fulfillment readiness, activation readiness, inventory mapping, and assurance impact before active use. |
| Consumer impact analysis | Entity Catalog; Product-Service-Resource Mapping | Show affected offers, quotes, product orders, service/resource orders, inventory entities, activation workflows, and assurance consumers for any definition change. |

### Required Screens

| Screen | Required behavior |
| --- | --- |
| Design release board | Version status, approval aging, blocked dependencies, certification evidence, consumers, and rollback plan. |
| Mapping matrix | Product-to-service-to-resource mapping with version, applicability, fulfillment pattern, activation template, and inventory expectation. |
| Compatibility workbench | Rule inputs, validation result, failed constraint, affected product/service/resource/location/topology, and exception approval. |
| Publication checklist | Catalog, inventory, fulfillment, activation, assurance, test, and event readiness before a design version becomes active. |

### Open-Source Decision Points

| Need | Candidate options | Decision prompt |
| --- | --- | --- |
| Rule validation | Spring/PostgreSQL rule tables; Drools/Kogito; lightweight JSON rule model | Ask before adding a rules engine; use one only if rule complexity and business-owned authoring justify it. |
| Visual modeling | PrimeNG tables/tree; Angular CDK canvas; Cytoscape.js for dependency views | Add canvas/graph libraries only if table/tree workflows cannot support design analysis. |
| Design evidence storage | PostgreSQL metadata plus object adapter; MinIO | Ask before storing large test packs, templates, or certification evidence outside PostgreSQL. |

### API/Event/Data Additions

| Area | Additions |
| --- | --- |
| APIs | Spec version clone/approve/activate/retire, mapping validate, compatibility check, activation template publish, certification gate approve, impact analysis. |
| Events | `ServiceSpecificationApproved`, `ResourceSpecificationApproved`, `RealizationRuleChanged`, `CompatibilityRuleChanged`, `DesignVersionPublished`, `ActivationTemplatePublished`. |
| Data | Service/resource definitions and realization rules are mastered here; inventory, fulfillment, and activation consume versioned definitions and snapshots. |

### First Release Scope

Include versioned service/resource specs, product-service-resource mapping, compatibility validation, activation/decomposition template metadata, publication checklist, and change impact analysis. Defer advanced visual modeling and automated design generation.
