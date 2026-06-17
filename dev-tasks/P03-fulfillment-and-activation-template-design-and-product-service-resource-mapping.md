# Service And Resource Design Studio P03 - Fulfillment And Activation Template Design And Product-Service-Resource Mapping And Resource Catalog Development Tasks

Suite: OSS Engineering, Inventory, And Fulfillment

App: Service And Resource Design Studio

App slug: `service-and-resource-design-studio`

Implementation repository: `ts-oss-eng-service-and-resource-design-studio`

Phase: P03 - Fulfillment And Activation Template Design And Product-Service-Resource Mapping And Resource Catalog

Phase file: `P03-fulfillment-and-activation-template-design-and-product-service-resource-mapping.md`

Phase rationale: Build the Fulfillment And Activation Template Design, Product-Service-Resource Mapping, Resource Catalog capability cluster for Service And Resource Design Studio, carrying source workflows, APIs, events, tables, controls, and tests from the feature files into implementable work.

Phase exit gate: Service And Resource Design Studio can execute the Fulfillment And Activation Template Design, Product-Service-Resource Mapping, Resource Catalog workflows through UI, API, `service_resource_design` persistence, outbox events, audit evidence, and release tests.

Out of scope for this phase: Runtime bootstrap is in P01; unrelated feature clusters and post-launch operations remain in their own phases.

Source tracker: [development-task-tracker.md](development-task-tracker.md)

Repository strategy: [TelcoSuite Repository Strategy](../../../../repository-strategy.md)

## Phase Coverage

- [Fulfillment And Activation Template Design](../features/fulfillment-and-activation-template-design.md)
- [Product-Service-Resource Mapping](../features/product-service-resource-mapping.md)
- [Resource Catalog](../features/resource-catalog.md)

## Phase Tasks

### DT-03-service-and-resource-design-studio-P03-T001: Build Fulfillment And Activation Template Design API, data model, workflow, and event spine

| Field | Value |
| --- | --- |
| Phase | P03 - Fulfillment And Activation Template Design And Product-Service-Resource Mapping And Resource Catalog |
| Priority | P0 |
| Source evidence | [Fulfillment And Activation Template Design](../features/fulfillment-and-activation-template-design.md), [Implementation usage](../implementation-file-usage.md), [App README](../README.md), [App overview](../../service-and-resource-design-studio.md), [Modules and features](../modules-and-features.md), [Personas and journeys](../personas-and-user-journeys.md), [Suite tech/UI guidance](../../tech-and-ui-guidance.md), [Suite data model](../../data-model.md), [Suite implementation guide](../../implementation-file-usage-guide.md), [Repository strategy](../../../../repository-strategy.md) |
| Feature or module | Fulfillment And Activation Template Design |
| Build area | API/Data/Event/Workflow/Security/Test |
| Target artifact | `backend/src/main/java/com/telcosuite/ossengineeringinventoryfulfillment/serviceandresourcedesignstudio/FulfillmentAndActivationTemplateDesignController.java`, `service_resource_design.fulfillment_and_activation_template_design`, `contracts/events/FulfillmentAndActivationTemplateDesignStateChangedEvent.json`, and `/api/03-oss-engineering-inventory-fulfillment/service-and-resource-design-studio/v1/fulfillment-and-activation-template-design` |
| Dependencies | DT-03-service-and-resource-design-studio-P01-T013 |
| Outputs | `FulfillmentAndActivationTemplateDesignController`, `FulfillmentAndActivationTemplateDesignService`, `service_resource_design.fulfillment_and_activation_template_design` migration, `FulfillmentAndActivationTemplateDesignStateChangedEvent` outbox schema, OpenAPI operations, unit/contract/migration/event replay tests |
| Missing evidence | No |

#### Implementation Notes

- Implement command and query APIs for `/api/03-oss-engineering-inventory-fulfillment/service-and-resource-design-studio/v1/fulfillment-and-activation-template-design` using TMF633, TMF634, TMF640, TMF641, TMF652, TMF664, TMF760, with create, update, search, detail, lifecycle transition, timeline, evidence, and exception endpoints where the feature lifecycle requires them.
- Persist `Fulfillment And Activation Template Design` state in `service_resource_design.fulfillment_and_activation_template_design` with tenant, brand/market, lifecycle state, source authority, idempotency key, correlation ID, actor, reason code, audit fields, and `tmf_payload` JSONB.
- Publish `FulfillmentAndActivationTemplateDesignStateChangedEvent` through the transactional outbox with changed fields, replay metadata, consumer acknowledgement state, and reconciliation status for workflows: Trigger, Validation, Orchestration, Exception.
- Carry source details into code and tests for personas Service designer, Resource designer, Network engineer and objects Master entity, Referenced entities, Primary decisions, ODA boundary; keep cross-app references read-only unless they arrive through governed APIs/events/projections.

#### Acceptance Criteria

1. Given an authorized persona submits `POST /api/03-oss-engineering-inventory-fulfillment/service-and-resource-design-studio/v1/fulfillment-and-activation-template-design`, when required fields and policy checks pass, then the API returns `201` with `$.state`, persists `service_resource_design.fulfillment_and_activation_template_design.id`, and appends `FulfillmentAndActivationTemplateDesignStateChangedEvent` to `service_resource_design.event_outbox`.
2. Given a stale, duplicate, or out-of-order request hits `PATCH /api/03-oss-engineering-inventory-fulfillment/service-and-resource-design-studio/v1/fulfillment-and-activation-template-design/{id}`, when optimistic locking or idempotency validation fails, then the API returns `409` with `$.error.code='stale-or-duplicate-command'` and no second event is emitted.
3. Given another app needs `Fulfillment And Activation Template Design` state, when it requests data, then it receives TMF-aligned API/event/projection output and no direct database access to `service_resource_design.fulfillment_and_activation_template_design` is required.

#### Definition Of Done

- `FulfillmentAndActivationTemplateDesignController`, service, repository, DTOs, validation, error model, and migration for `service_resource_design.fulfillment_and_activation_template_design` are committed under `ts-oss-eng-service-and-resource-design-studio`.
- OpenAPI contract tests, unit tests, Flyway migration tests, event schema tests, and event replay tests cover `/api/03-oss-engineering-inventory-fulfillment/service-and-resource-design-studio/v1/fulfillment-and-activation-template-design`, `service_resource_design.fulfillment_and_activation_template_design`, and `FulfillmentAndActivationTemplateDesignStateChangedEvent`.
- `development-task-tracker.md` records command output, source feature link, PR/evidence links, and any blocked downstream consumer.

#### Negative Scenarios

- Unauthorized, cross-tenant, or wrong-purpose requests to `/api/03-oss-engineering-inventory-fulfillment/service-and-resource-design-studio/v1/fulfillment-and-activation-template-design` return `403` and write a denial audit row instead of exposing `Fulfillment And Activation Template Design` data.
- Missing source authority, stale dependency state, invalid lifecycle transition, or failed policy decision keeps `service_resource_design.fulfillment_and_activation_template_design` in blocked/exception state with owner and due date.
- Downstream outage or consumer rejection queues retry/replay for `FulfillmentAndActivationTemplateDesignStateChangedEvent` and prevents silent completion.

#### Edge Cases

- Bulk or project-scale updates to `Fulfillment And Activation Template Design` use preview, partial-failure reporting, idempotency keys, rollback/repair notes, and async export where needed.
- Historical correction preserves previous `service_resource_design.fulfillment_and_activation_template_design` values, audit reason, source timestamp, actor, and downstream recalculation/replay instructions.
- Multi-tenant, market, residency, localization, and high-volume queue cases include pagination, back-pressure, circuit breaker, and replay controls.

#### Test Expectations

- `mvn test` covers `FulfillmentAndActivationTemplateDesignService`, validation, authorization, idempotency, and lifecycle transition rules.
- OpenAPI contract tests call `POST/GET/PATCH /api/03-oss-engineering-inventory-fulfillment/service-and-resource-design-studio/v1/fulfillment-and-activation-template-design` and verify `$.state`, `$.id`, error payloads, and pagination/filter behavior.
- Flyway migration tests verify `service_resource_design.fulfillment_and_activation_template_design` columns and indexes; event replay tests validate `contracts/events/FulfillmentAndActivationTemplateDesignStateChangedEvent.json` and `service_resource_design.event_outbox` ordering.

### DT-03-service-and-resource-design-studio-P03-T002: Build Fulfillment And Activation Template Design workbench, controls, observability, and release tests

| Field | Value |
| --- | --- |
| Phase | P03 - Fulfillment And Activation Template Design And Product-Service-Resource Mapping And Resource Catalog |
| Priority | P1 |
| Source evidence | [Fulfillment And Activation Template Design](../features/fulfillment-and-activation-template-design.md), [Implementation usage](../implementation-file-usage.md), [App README](../README.md), [App overview](../../service-and-resource-design-studio.md), [Modules and features](../modules-and-features.md), [Personas and journeys](../personas-and-user-journeys.md), [Suite tech/UI guidance](../../tech-and-ui-guidance.md), [Suite data model](../../data-model.md), [Suite implementation guide](../../implementation-file-usage-guide.md), [Repository strategy](../../../../repository-strategy.md) |
| Feature or module | Fulfillment And Activation Template Design |
| Build area | UI/Security/Ops/Test |
| Target artifact | `frontend/src/app/pages/fulfillment-and-activation-template-design/`, `tests/e2e/fulfillment-and-activation-template-design.spec.ts`, Grafana panel `fulfillment-and-activation-template-design`, and `docs/operations-runbook.md#fulfillment-and-activation-template-design` |
| Dependencies | DT-03-service-and-resource-design-studio-P03-T001 |
| Outputs | Angular workbench, queue/detail/timeline/evidence panels, role-aware guards, accessibility states, E2E tests, dashboard JSON, alert rules, runbook section |
| Missing evidence | No |

#### Implementation Notes

- Create `frontend/src/app/pages/fulfillment-and-activation-template-design/` with search/intake, detail, lifecycle timeline, exception queue, evidence drawer, dependency freshness panel, and allowed-next-action controls for personas Service designer, Resource designer, Network engineer.
- Wire route guards, tenant/brand/market context, masking, no-permission states, keyboard navigation, PrimeNG table/form patterns, and saved filters using `ts-shared-ui-design-system`.
- Add dashboard metrics and runbook steps for workflows Trigger, Validation, Orchestration, Exception, event replay backlog, queue aging, policy denials, consumer lag, and completion quality.

#### Acceptance Criteria

1. Given an authorized persona opens `/app/service-and-resource-design-studio/fulfillment-and-activation-template-design`, when records exist, then the workbench returns `$.uiState='ready'` and renders `Fulfillment And Activation Template Design` rows with lifecycle state, owner, freshness, SLA/OLA timer, and action menu.
2. Given the persona lacks permission, when the same route loads, then the UI shows a no-permission state and the backend returns `403` with `$.error.code='access-denied'`.
3. Given replay backlog or queue aging exceeds threshold, when Grafana dashboard `fulfillment-and-activation-template-design` refreshes, then it shows the metric and links to `docs/operations-runbook.md#fulfillment-and-activation-template-design`.

#### Definition Of Done

- `frontend/src/app/pages/fulfillment-and-activation-template-design/` includes route, component, service, state, fixtures, empty/loading/error/no-permission states, and accessibility labels.
- `tests/e2e/fulfillment-and-activation-template-design.spec.ts`, accessibility checks, security tests, dashboard checks, and runbook review pass and are linked from the tracker.
- `development-task-tracker.md` captures screenshots, command output, PR links, dashboard/runbook links, and unresolved blockers.

#### Negative Scenarios

- Do not render `Fulfillment And Activation Template Design` details across tenant/residency boundaries; masked values stay masked in table, detail, export, timeline, and dashboard paths.
- Do not close UI actions when backend validation, event publication, reconciliation, or required evidence is incomplete.
- Do not hide downstream outage, stale source data, policy denial, or manual override behind a generic success toast.

#### Edge Cases

- Mobile or constrained layouts for `Fulfillment And Activation Template Design` collapse tables into accessible cards without losing lifecycle, owner, SLA/OLA, or evidence fields.
- Bulk/replay actions require preview, explicit confirmation, partial-failure details, rollback/repair notes, and operator evidence.
- High-volume dashboard and queue views use pagination, saved filters, async export, trace IDs, and back-pressure indicators.

#### Test Expectations

- `npm run lint`, `npm test`, and `tests/e2e/fulfillment-and-activation-template-design.spec.ts` validate route, forms, guards, workbench states, and API integration.
- Accessibility tests cover keyboard navigation, focus order, screen-reader labels, color contrast, density, and responsive layout.
- Operational-readiness tests validate Grafana dashboard JSON, alert rules, event replay panel, runbook links, and release evidence.

### DT-03-service-and-resource-design-studio-P03-T003: Build Product-Service-Resource Mapping API, data model, workflow, and event spine

| Field | Value |
| --- | --- |
| Phase | P03 - Fulfillment And Activation Template Design And Product-Service-Resource Mapping And Resource Catalog |
| Priority | P0 |
| Source evidence | [Product-Service-Resource Mapping](../features/product-service-resource-mapping.md), [Implementation usage](../implementation-file-usage.md), [App README](../README.md), [App overview](../../service-and-resource-design-studio.md), [Modules and features](../modules-and-features.md), [Personas and journeys](../personas-and-user-journeys.md), [Suite tech/UI guidance](../../tech-and-ui-guidance.md), [Suite data model](../../data-model.md), [Suite implementation guide](../../implementation-file-usage-guide.md), [Repository strategy](../../../../repository-strategy.md) |
| Feature or module | Product-Service-Resource Mapping |
| Build area | API/Data/Event/Workflow/Security/Test |
| Target artifact | `backend/src/main/java/com/telcosuite/ossengineeringinventoryfulfillment/serviceandresourcedesignstudio/ProductServiceResourceMappingController.java`, `service_resource_design.product_service_resource_mapping`, `contracts/events/ProductServiceResourceMappingStateChangedEvent.json`, and `/api/03-oss-engineering-inventory-fulfillment/service-and-resource-design-studio/v1/product-service-resource-mapping` |
| Dependencies | DT-03-service-and-resource-design-studio-P03-T001 |
| Outputs | `ProductServiceResourceMappingController`, `ProductServiceResourceMappingService`, `service_resource_design.product_service_resource_mapping` migration, `ProductServiceResourceMappingStateChangedEvent` outbox schema, OpenAPI operations, unit/contract/migration/event replay tests |
| Missing evidence | No |

#### Implementation Notes

- Implement command and query APIs for `/api/03-oss-engineering-inventory-fulfillment/service-and-resource-design-studio/v1/product-service-resource-mapping` using TMF620, TMF633, TMF634, TMF641, TMF652, TMF701, with create, update, search, detail, lifecycle transition, timeline, evidence, and exception endpoints where the feature lifecycle requires them.
- Persist `Product-Service-Resource Mapping` state in `service_resource_design.product_service_resource_mapping` with tenant, brand/market, lifecycle state, source authority, idempotency key, correlation ID, actor, reason code, audit fields, and `tmf_payload` JSONB.
- Publish `ProductServiceResourceMappingStateChangedEvent` through the transactional outbox with changed fields, replay metadata, consumer acknowledgement state, and reconciliation status for workflows: Trigger, Validation, Orchestration, Exception.
- Carry source details into code and tests for personas Service designer, Resource designer, Network engineer and objects Master entity, Referenced entities, Primary decisions, ODA boundary; keep cross-app references read-only unless they arrive through governed APIs/events/projections.

#### Acceptance Criteria

1. Given an authorized persona submits `POST /api/03-oss-engineering-inventory-fulfillment/service-and-resource-design-studio/v1/product-service-resource-mapping`, when required fields and policy checks pass, then the API returns `201` with `$.state`, persists `service_resource_design.product_service_resource_mapping.id`, and appends `ProductServiceResourceMappingStateChangedEvent` to `service_resource_design.event_outbox`.
2. Given a stale, duplicate, or out-of-order request hits `PATCH /api/03-oss-engineering-inventory-fulfillment/service-and-resource-design-studio/v1/product-service-resource-mapping/{id}`, when optimistic locking or idempotency validation fails, then the API returns `409` with `$.error.code='stale-or-duplicate-command'` and no second event is emitted.
3. Given another app needs `Product-Service-Resource Mapping` state, when it requests data, then it receives TMF-aligned API/event/projection output and no direct database access to `service_resource_design.product_service_resource_mapping` is required.

#### Definition Of Done

- `ProductServiceResourceMappingController`, service, repository, DTOs, validation, error model, and migration for `service_resource_design.product_service_resource_mapping` are committed under `ts-oss-eng-service-and-resource-design-studio`.
- OpenAPI contract tests, unit tests, Flyway migration tests, event schema tests, and event replay tests cover `/api/03-oss-engineering-inventory-fulfillment/service-and-resource-design-studio/v1/product-service-resource-mapping`, `service_resource_design.product_service_resource_mapping`, and `ProductServiceResourceMappingStateChangedEvent`.
- `development-task-tracker.md` records command output, source feature link, PR/evidence links, and any blocked downstream consumer.

#### Negative Scenarios

- Unauthorized, cross-tenant, or wrong-purpose requests to `/api/03-oss-engineering-inventory-fulfillment/service-and-resource-design-studio/v1/product-service-resource-mapping` return `403` and write a denial audit row instead of exposing `Product-Service-Resource Mapping` data.
- Missing source authority, stale dependency state, invalid lifecycle transition, or failed policy decision keeps `service_resource_design.product_service_resource_mapping` in blocked/exception state with owner and due date.
- Downstream outage or consumer rejection queues retry/replay for `ProductServiceResourceMappingStateChangedEvent` and prevents silent completion.

#### Edge Cases

- Bulk or project-scale updates to `Product-Service-Resource Mapping` use preview, partial-failure reporting, idempotency keys, rollback/repair notes, and async export where needed.
- Historical correction preserves previous `service_resource_design.product_service_resource_mapping` values, audit reason, source timestamp, actor, and downstream recalculation/replay instructions.
- Multi-tenant, market, residency, localization, and high-volume queue cases include pagination, back-pressure, circuit breaker, and replay controls.

#### Test Expectations

- `mvn test` covers `ProductServiceResourceMappingService`, validation, authorization, idempotency, and lifecycle transition rules.
- OpenAPI contract tests call `POST/GET/PATCH /api/03-oss-engineering-inventory-fulfillment/service-and-resource-design-studio/v1/product-service-resource-mapping` and verify `$.state`, `$.id`, error payloads, and pagination/filter behavior.
- Flyway migration tests verify `service_resource_design.product_service_resource_mapping` columns and indexes; event replay tests validate `contracts/events/ProductServiceResourceMappingStateChangedEvent.json` and `service_resource_design.event_outbox` ordering.

### DT-03-service-and-resource-design-studio-P03-T004: Build Product-Service-Resource Mapping workbench, controls, observability, and release tests

| Field | Value |
| --- | --- |
| Phase | P03 - Fulfillment And Activation Template Design And Product-Service-Resource Mapping And Resource Catalog |
| Priority | P1 |
| Source evidence | [Product-Service-Resource Mapping](../features/product-service-resource-mapping.md), [Implementation usage](../implementation-file-usage.md), [App README](../README.md), [App overview](../../service-and-resource-design-studio.md), [Modules and features](../modules-and-features.md), [Personas and journeys](../personas-and-user-journeys.md), [Suite tech/UI guidance](../../tech-and-ui-guidance.md), [Suite data model](../../data-model.md), [Suite implementation guide](../../implementation-file-usage-guide.md), [Repository strategy](../../../../repository-strategy.md) |
| Feature or module | Product-Service-Resource Mapping |
| Build area | UI/Security/Ops/Test |
| Target artifact | `frontend/src/app/pages/product-service-resource-mapping/`, `tests/e2e/product-service-resource-mapping.spec.ts`, Grafana panel `product-service-resource-mapping`, and `docs/operations-runbook.md#product-service-resource-mapping` |
| Dependencies | DT-03-service-and-resource-design-studio-P03-T003 |
| Outputs | Angular workbench, queue/detail/timeline/evidence panels, role-aware guards, accessibility states, E2E tests, dashboard JSON, alert rules, runbook section |
| Missing evidence | No |

#### Implementation Notes

- Create `frontend/src/app/pages/product-service-resource-mapping/` with search/intake, detail, lifecycle timeline, exception queue, evidence drawer, dependency freshness panel, and allowed-next-action controls for personas Service designer, Resource designer, Network engineer.
- Wire route guards, tenant/brand/market context, masking, no-permission states, keyboard navigation, PrimeNG table/form patterns, and saved filters using `ts-shared-ui-design-system`.
- Add dashboard metrics and runbook steps for workflows Trigger, Validation, Orchestration, Exception, event replay backlog, queue aging, policy denials, consumer lag, and completion quality.

#### Acceptance Criteria

1. Given an authorized persona opens `/app/service-and-resource-design-studio/product-service-resource-mapping`, when records exist, then the workbench returns `$.uiState='ready'` and renders `Product-Service-Resource Mapping` rows with lifecycle state, owner, freshness, SLA/OLA timer, and action menu.
2. Given the persona lacks permission, when the same route loads, then the UI shows a no-permission state and the backend returns `403` with `$.error.code='access-denied'`.
3. Given replay backlog or queue aging exceeds threshold, when Grafana dashboard `product-service-resource-mapping` refreshes, then it shows the metric and links to `docs/operations-runbook.md#product-service-resource-mapping`.

#### Definition Of Done

- `frontend/src/app/pages/product-service-resource-mapping/` includes route, component, service, state, fixtures, empty/loading/error/no-permission states, and accessibility labels.
- `tests/e2e/product-service-resource-mapping.spec.ts`, accessibility checks, security tests, dashboard checks, and runbook review pass and are linked from the tracker.
- `development-task-tracker.md` captures screenshots, command output, PR links, dashboard/runbook links, and unresolved blockers.

#### Negative Scenarios

- Do not render `Product-Service-Resource Mapping` details across tenant/residency boundaries; masked values stay masked in table, detail, export, timeline, and dashboard paths.
- Do not close UI actions when backend validation, event publication, reconciliation, or required evidence is incomplete.
- Do not hide downstream outage, stale source data, policy denial, or manual override behind a generic success toast.

#### Edge Cases

- Mobile or constrained layouts for `Product-Service-Resource Mapping` collapse tables into accessible cards without losing lifecycle, owner, SLA/OLA, or evidence fields.
- Bulk/replay actions require preview, explicit confirmation, partial-failure details, rollback/repair notes, and operator evidence.
- High-volume dashboard and queue views use pagination, saved filters, async export, trace IDs, and back-pressure indicators.

#### Test Expectations

- `npm run lint`, `npm test`, and `tests/e2e/product-service-resource-mapping.spec.ts` validate route, forms, guards, workbench states, and API integration.
- Accessibility tests cover keyboard navigation, focus order, screen-reader labels, color contrast, density, and responsive layout.
- Operational-readiness tests validate Grafana dashboard JSON, alert rules, event replay panel, runbook links, and release evidence.

### DT-03-service-and-resource-design-studio-P03-T005: Build Resource Catalog API, data model, workflow, and event spine

| Field | Value |
| --- | --- |
| Phase | P03 - Fulfillment And Activation Template Design And Product-Service-Resource Mapping And Resource Catalog |
| Priority | P0 |
| Source evidence | [Resource Catalog](../features/resource-catalog.md), [Implementation usage](../implementation-file-usage.md), [App README](../README.md), [App overview](../../service-and-resource-design-studio.md), [Modules and features](../modules-and-features.md), [Personas and journeys](../personas-and-user-journeys.md), [Suite tech/UI guidance](../../tech-and-ui-guidance.md), [Suite data model](../../data-model.md), [Suite implementation guide](../../implementation-file-usage-guide.md), [Repository strategy](../../../../repository-strategy.md) |
| Feature or module | Resource Catalog |
| Build area | API/Data/Event/Workflow/Security/Test |
| Target artifact | `backend/src/main/java/com/telcosuite/ossengineeringinventoryfulfillment/serviceandresourcedesignstudio/ResourceCatalogController.java`, `service_resource_design.resource_catalog`, `contracts/events/ResourceCatalogStateChangedEvent.json`, and `/api/03-oss-engineering-inventory-fulfillment/service-and-resource-design-studio/v1/resource-catalog` |
| Dependencies | DT-03-service-and-resource-design-studio-P03-T003 |
| Outputs | `ResourceCatalogController`, `ResourceCatalogService`, `service_resource_design.resource_catalog` migration, `ResourceCatalogStateChangedEvent` outbox schema, OpenAPI operations, unit/contract/migration/event replay tests |
| Missing evidence | No |

#### Implementation Notes

- Implement command and query APIs for `/api/03-oss-engineering-inventory-fulfillment/service-and-resource-design-studio/v1/resource-catalog` using TMF634, TMF639, TMF685, TMF730, with create, update, search, detail, lifecycle transition, timeline, evidence, and exception endpoints where the feature lifecycle requires them.
- Persist `Resource Catalog` state in `service_resource_design.resource_catalog` with tenant, brand/market, lifecycle state, source authority, idempotency key, correlation ID, actor, reason code, audit fields, and `tmf_payload` JSONB.
- Publish `ResourceCatalogStateChangedEvent` through the transactional outbox with changed fields, replay metadata, consumer acknowledgement state, and reconciliation status for workflows: Trigger, Validation, Orchestration, Exception.
- Carry source details into code and tests for personas Service designer, Resource designer, Network engineer and objects Master entity, Referenced entities, Primary decisions, ODA boundary; keep cross-app references read-only unless they arrive through governed APIs/events/projections.

#### Acceptance Criteria

1. Given an authorized persona submits `POST /api/03-oss-engineering-inventory-fulfillment/service-and-resource-design-studio/v1/resource-catalog`, when required fields and policy checks pass, then the API returns `201` with `$.state`, persists `service_resource_design.resource_catalog.id`, and appends `ResourceCatalogStateChangedEvent` to `service_resource_design.event_outbox`.
2. Given a stale, duplicate, or out-of-order request hits `PATCH /api/03-oss-engineering-inventory-fulfillment/service-and-resource-design-studio/v1/resource-catalog/{id}`, when optimistic locking or idempotency validation fails, then the API returns `409` with `$.error.code='stale-or-duplicate-command'` and no second event is emitted.
3. Given another app needs `Resource Catalog` state, when it requests data, then it receives TMF-aligned API/event/projection output and no direct database access to `service_resource_design.resource_catalog` is required.

#### Definition Of Done

- `ResourceCatalogController`, service, repository, DTOs, validation, error model, and migration for `service_resource_design.resource_catalog` are committed under `ts-oss-eng-service-and-resource-design-studio`.
- OpenAPI contract tests, unit tests, Flyway migration tests, event schema tests, and event replay tests cover `/api/03-oss-engineering-inventory-fulfillment/service-and-resource-design-studio/v1/resource-catalog`, `service_resource_design.resource_catalog`, and `ResourceCatalogStateChangedEvent`.
- `development-task-tracker.md` records command output, source feature link, PR/evidence links, and any blocked downstream consumer.

#### Negative Scenarios

- Unauthorized, cross-tenant, or wrong-purpose requests to `/api/03-oss-engineering-inventory-fulfillment/service-and-resource-design-studio/v1/resource-catalog` return `403` and write a denial audit row instead of exposing `Resource Catalog` data.
- Missing source authority, stale dependency state, invalid lifecycle transition, or failed policy decision keeps `service_resource_design.resource_catalog` in blocked/exception state with owner and due date.
- Downstream outage or consumer rejection queues retry/replay for `ResourceCatalogStateChangedEvent` and prevents silent completion.

#### Edge Cases

- Bulk or project-scale updates to `Resource Catalog` use preview, partial-failure reporting, idempotency keys, rollback/repair notes, and async export where needed.
- Historical correction preserves previous `service_resource_design.resource_catalog` values, audit reason, source timestamp, actor, and downstream recalculation/replay instructions.
- Multi-tenant, market, residency, localization, and high-volume queue cases include pagination, back-pressure, circuit breaker, and replay controls.

#### Test Expectations

- `mvn test` covers `ResourceCatalogService`, validation, authorization, idempotency, and lifecycle transition rules.
- OpenAPI contract tests call `POST/GET/PATCH /api/03-oss-engineering-inventory-fulfillment/service-and-resource-design-studio/v1/resource-catalog` and verify `$.state`, `$.id`, error payloads, and pagination/filter behavior.
- Flyway migration tests verify `service_resource_design.resource_catalog` columns and indexes; event replay tests validate `contracts/events/ResourceCatalogStateChangedEvent.json` and `service_resource_design.event_outbox` ordering.

### DT-03-service-and-resource-design-studio-P03-T006: Build Resource Catalog workbench, controls, observability, and release tests

| Field | Value |
| --- | --- |
| Phase | P03 - Fulfillment And Activation Template Design And Product-Service-Resource Mapping And Resource Catalog |
| Priority | P1 |
| Source evidence | [Resource Catalog](../features/resource-catalog.md), [Implementation usage](../implementation-file-usage.md), [App README](../README.md), [App overview](../../service-and-resource-design-studio.md), [Modules and features](../modules-and-features.md), [Personas and journeys](../personas-and-user-journeys.md), [Suite tech/UI guidance](../../tech-and-ui-guidance.md), [Suite data model](../../data-model.md), [Suite implementation guide](../../implementation-file-usage-guide.md), [Repository strategy](../../../../repository-strategy.md) |
| Feature or module | Resource Catalog |
| Build area | UI/Security/Ops/Test |
| Target artifact | `frontend/src/app/pages/resource-catalog/`, `tests/e2e/resource-catalog.spec.ts`, Grafana panel `resource-catalog`, and `docs/operations-runbook.md#resource-catalog` |
| Dependencies | DT-03-service-and-resource-design-studio-P03-T005 |
| Outputs | Angular workbench, queue/detail/timeline/evidence panels, role-aware guards, accessibility states, E2E tests, dashboard JSON, alert rules, runbook section |
| Missing evidence | No |

#### Implementation Notes

- Create `frontend/src/app/pages/resource-catalog/` with search/intake, detail, lifecycle timeline, exception queue, evidence drawer, dependency freshness panel, and allowed-next-action controls for personas Service designer, Resource designer, Network engineer.
- Wire route guards, tenant/brand/market context, masking, no-permission states, keyboard navigation, PrimeNG table/form patterns, and saved filters using `ts-shared-ui-design-system`.
- Add dashboard metrics and runbook steps for workflows Trigger, Validation, Orchestration, Exception, event replay backlog, queue aging, policy denials, consumer lag, and completion quality.

#### Acceptance Criteria

1. Given an authorized persona opens `/app/service-and-resource-design-studio/resource-catalog`, when records exist, then the workbench returns `$.uiState='ready'` and renders `Resource Catalog` rows with lifecycle state, owner, freshness, SLA/OLA timer, and action menu.
2. Given the persona lacks permission, when the same route loads, then the UI shows a no-permission state and the backend returns `403` with `$.error.code='access-denied'`.
3. Given replay backlog or queue aging exceeds threshold, when Grafana dashboard `resource-catalog` refreshes, then it shows the metric and links to `docs/operations-runbook.md#resource-catalog`.

#### Definition Of Done

- `frontend/src/app/pages/resource-catalog/` includes route, component, service, state, fixtures, empty/loading/error/no-permission states, and accessibility labels.
- `tests/e2e/resource-catalog.spec.ts`, accessibility checks, security tests, dashboard checks, and runbook review pass and are linked from the tracker.
- `development-task-tracker.md` captures screenshots, command output, PR links, dashboard/runbook links, and unresolved blockers.

#### Negative Scenarios

- Do not render `Resource Catalog` details across tenant/residency boundaries; masked values stay masked in table, detail, export, timeline, and dashboard paths.
- Do not close UI actions when backend validation, event publication, reconciliation, or required evidence is incomplete.
- Do not hide downstream outage, stale source data, policy denial, or manual override behind a generic success toast.

#### Edge Cases

- Mobile or constrained layouts for `Resource Catalog` collapse tables into accessible cards without losing lifecycle, owner, SLA/OLA, or evidence fields.
- Bulk/replay actions require preview, explicit confirmation, partial-failure details, rollback/repair notes, and operator evidence.
- High-volume dashboard and queue views use pagination, saved filters, async export, trace IDs, and back-pressure indicators.

#### Test Expectations

- `npm run lint`, `npm test`, and `tests/e2e/resource-catalog.spec.ts` validate route, forms, guards, workbench states, and API integration.
- Accessibility tests cover keyboard navigation, focus order, screen-reader labels, color contrast, density, and responsive layout.
- Operational-readiness tests validate Grafana dashboard JSON, alert rules, event replay panel, runbook links, and release evidence.

### DT-03-service-and-resource-design-studio-P03-T007: Prove Fulfillment And Activation Template Design And Product-Service-Resource Mapping And Resource Catalog release gate, replay, and handoff evidence

| Field | Value |
| --- | --- |
| Phase | P03 - Fulfillment And Activation Template Design And Product-Service-Resource Mapping And Resource Catalog |
| Priority | P1 |
| Source evidence | [Fulfillment And Activation Template Design](../features/fulfillment-and-activation-template-design.md), [Product-Service-Resource Mapping](../features/product-service-resource-mapping.md), [Resource Catalog](../features/resource-catalog.md), [Implementation usage](../implementation-file-usage.md), [App README](../README.md), [App overview](../../service-and-resource-design-studio.md), [Modules and features](../modules-and-features.md), [Personas and journeys](../personas-and-user-journeys.md), [Suite tech/UI guidance](../../tech-and-ui-guidance.md), [Suite data model](../../data-model.md), [Suite implementation guide](../../implementation-file-usage-guide.md), [Repository strategy](../../../../repository-strategy.md) |
| Feature or module | Fulfillment And Activation Template Design And Product-Service-Resource Mapping And Resource Catalog |
| Build area | Test/Ops/Release/Event |
| Target artifact | `tests/release/fulfillment-and-activation-template-design-and-product-service-resource-mapping.spec.ts`, `docs/release-notes/fulfillment-and-activation-template-design-and-product-service-resource-mapping.md`, Grafana dashboard `fulfillment-and-activation-template-design-and-product-service-resource-mapping`, and replay fixtures |
| Dependencies | DT-03-service-and-resource-design-studio-P03-T002, DT-03-service-and-resource-design-studio-P03-T004, DT-03-service-and-resource-design-studio-P03-T006 |
| Outputs | Release-gate test, replay/reconciliation evidence, accessibility/security/performance reports, dashboard/runbook links, support handoff notes |
| Missing evidence | No |

#### Implementation Notes

- Create a release-gate checklist for `fulfillment-and-activation-template-design-and-product-service-resource-mapping` covering Fulfillment And Activation Template Design, Product-Service-Resource Mapping, Resource Catalog, with happy path, assisted path, negative path, edge cases, event replay, data reconciliation, security, accessibility, performance, and support evidence.
- Record producer and consumer acknowledgements for phase events, reconcile `service_resource_design.event_outbox`, and link replay fixtures and correlation IDs.
- Update `docs/operations-runbook.md`, `docs/release-notes/fulfillment-and-activation-template-design-and-product-service-resource-mapping.md`, and `development-task-tracker.md` with release evidence and unresolved blockers.

#### Acceptance Criteria

1. Given all tasks in `P03-fulfillment-and-activation-template-design-and-product-service-resource-mapping.md` are complete, when `tests/release/fulfillment-and-activation-template-design-and-product-service-resource-mapping.spec.ts` runs, then it returns exit code `0` and links evidence for UI, API, data, event, security, ops, and test gates.
2. Given a consumer rejects an event from `fulfillment-and-activation-template-design-and-product-service-resource-mapping`, when replay is triggered, then the replay fixture preserves `$.correlationId`, `$.eventId`, and consumer acknowledgement state.
3. Given release notes are generated, when support reviews `docs/release-notes/fulfillment-and-activation-template-design-and-product-service-resource-mapping.md`, then open blockers, rollback steps, runbook links, and ownership contacts are present.

#### Definition Of Done

- `tests/release/fulfillment-and-activation-template-design-and-product-service-resource-mapping.spec.ts`, replay fixtures, dashboard/runbook links, and release notes are committed.
- Accessibility, security, contract, migration, event replay, performance, and operational-readiness evidence is linked from the tracker.
- Open blockers have owner, due date, target increment, and rollback or removal criteria.

#### Negative Scenarios

- Do not mark the phase Done if event replay, reconciliation, accessibility, security, or downstream acknowledgement evidence is missing.
- Do not release `fulfillment-and-activation-template-design-and-product-service-resource-mapping` with unresolved cross-app writes, direct schema coupling, or stale source authority assumptions.
- Do not suppress failed release gates; record failures with owner, due date, and target increment.

#### Edge Cases

- Coordinated release gates may require downstream app windows; record scheduling, owner, and fallback route in release notes.
- Historical backfill, replay, bulk update, or migration repair runs must include preview, partial failure report, and rollback evidence.
- High-volume launch periods require dashboard thresholds, alert owners, queue back-pressure, and support escalation paths.

#### Test Expectations

- `tests/release/fulfillment-and-activation-template-design-and-product-service-resource-mapping.spec.ts`, `mvn test`, OpenAPI/event replay tests, Flyway checks, Playwright/Cypress E2E, accessibility, security, and k6/performance gates pass.
- `docker compose config`, clean-checkout smoke, `helm lint`, Kubernetes dry-run, dashboard JSON validation, and runbook link checks pass.
- Tracker evidence links command output, PRs, screenshots, replay payloads, dashboards, release notes, and support handoff notes.
