# Service And Resource Design Studio P02 - Advanced Network Cloud And Device Resource Models And Catalog Version Certification And Retirement Mapping And Entity Catalog Development Tasks

Suite: OSS Engineering, Inventory, And Fulfillment

App: Service And Resource Design Studio

App slug: `service-and-resource-design-studio`

Implementation repository: `ts-oss-eng-service-and-resource-design-studio`

Phase: P02 - Advanced Network Cloud And Device Resource Models And Catalog Version Certification And Retirement Mapping And Entity Catalog

Phase file: `P02-advanced-network-cloud-and-device-resource-models-and-catalog-version.md`

Phase rationale: Build the Advanced Network Cloud And Device Resource Models, Catalog Version Certification And Retirement Mapping, Entity Catalog capability cluster for Service And Resource Design Studio, carrying source workflows, APIs, events, tables, controls, and tests from the feature files into implementable work.

Phase exit gate: Service And Resource Design Studio can execute the Advanced Network Cloud And Device Resource Models, Catalog Version Certification And Retirement Mapping, Entity Catalog workflows through UI, API, `service_resource_design` persistence, outbox events, audit evidence, and release tests.

Out of scope for this phase: Runtime bootstrap is in P01; unrelated feature clusters and post-launch operations remain in their own phases.

Source tracker: [development-task-tracker.md](development-task-tracker.md)

Repository strategy: [TelcoSuite Repository Strategy](../../../../repository-strategy.md)

## Phase Coverage

- [Advanced Network Cloud And Device Resource Models](../features/advanced-network-cloud-and-device-resource-models.md)
- [Catalog Version Certification And Retirement Mapping](../features/catalog-version-certification-and-retirement-mapping.md)
- [Entity Catalog](../features/entity-catalog.md)

## Phase Tasks

### DT-03-service-and-resource-design-studio-P02-T001: Build Advanced Network Cloud And Device Resource Models API, data model, workflow, and event spine

| Field | Value |
| --- | --- |
| Phase | P02 - Advanced Network Cloud And Device Resource Models And Catalog Version Certification And Retirement Mapping And Entity Catalog |
| Priority | P0 |
| Source evidence | [Advanced Network Cloud And Device Resource Models](../features/advanced-network-cloud-and-device-resource-models.md), [Implementation usage](../implementation-file-usage.md), [App README](../README.md), [App overview](../../service-and-resource-design-studio.md), [Modules and features](../modules-and-features.md), [Personas and journeys](../personas-and-user-journeys.md), [Suite tech/UI guidance](../../tech-and-ui-guidance.md), [Suite data model](../../data-model.md), [Suite implementation guide](../../implementation-file-usage-guide.md), [Repository strategy](../../../../repository-strategy.md) |
| Feature or module | Advanced Network Cloud And Device Resource Models |
| Build area | API/Data/Event/Workflow/Security/Test |
| Target artifact | `backend/src/main/java/com/telcosuite/ossengineeringinventoryfulfillment/serviceandresourcedesignstudio/AdvancedNetworkCloudAndDeviceResourceModelsController.java`, `service_resource_design.advanced_network_cloud_and_device_resource_models`, `contracts/events/AdvancedNetworkCloudAndDeviceResourceModelsStateChangedEvent.json`, and `/api/03-oss-engineering-inventory-fulfillment/service-and-resource-design-studio/v1/advanced-network-cloud-and-device-resource-models` |
| Dependencies | DT-03-service-and-resource-design-studio-P01-T013 |
| Outputs | `AdvancedNetworkCloudAndDeviceResourceModelsController`, `AdvancedNetworkCloudAndDeviceResourceModelsService`, `service_resource_design.advanced_network_cloud_and_device_resource_models` migration, `AdvancedNetworkCloudAndDeviceResourceModelsStateChangedEvent` outbox schema, OpenAPI operations, unit/contract/migration/event replay tests |
| Missing evidence | No |

#### Implementation Notes

- Implement command and query APIs for `/api/03-oss-engineering-inventory-fulfillment/service-and-resource-design-studio/v1/advanced-network-cloud-and-device-resource-models` using TMF634, TMF639, TMF640, TMF664, TMF730, with create, update, search, detail, lifecycle transition, timeline, evidence, and exception endpoints where the feature lifecycle requires them.
- Persist `Advanced Network Cloud And Device Resource Models` state in `service_resource_design.advanced_network_cloud_and_device_resource_models` with tenant, brand/market, lifecycle state, source authority, idempotency key, correlation ID, actor, reason code, audit fields, and `tmf_payload` JSONB.
- Publish `AdvancedNetworkCloudAndDeviceResourceModelsStateChangedEvent` through the transactional outbox with changed fields, replay metadata, consumer acknowledgement state, and reconciliation status for workflows: Trigger, Validation, Orchestration, Exception.
- Carry source details into code and tests for personas Service designer, Resource designer, Network engineer and objects Master entity, Referenced entities, Primary decisions, ODA boundary; keep cross-app references read-only unless they arrive through governed APIs/events/projections.

#### Acceptance Criteria

1. Given an authorized persona submits `POST /api/03-oss-engineering-inventory-fulfillment/service-and-resource-design-studio/v1/advanced-network-cloud-and-device-resource-models`, when required fields and policy checks pass, then the API returns `201` with `$.state`, persists `service_resource_design.advanced_network_cloud_and_device_resource_models.id`, and appends `AdvancedNetworkCloudAndDeviceResourceModelsStateChangedEvent` to `service_resource_design.event_outbox`.
2. Given a stale, duplicate, or out-of-order request hits `PATCH /api/03-oss-engineering-inventory-fulfillment/service-and-resource-design-studio/v1/advanced-network-cloud-and-device-resource-models/{id}`, when optimistic locking or idempotency validation fails, then the API returns `409` with `$.error.code='stale-or-duplicate-command'` and no second event is emitted.
3. Given another app needs `Advanced Network Cloud And Device Resource Models` state, when it requests data, then it receives TMF-aligned API/event/projection output and no direct database access to `service_resource_design.advanced_network_cloud_and_device_resource_models` is required.

#### Definition Of Done

- `AdvancedNetworkCloudAndDeviceResourceModelsController`, service, repository, DTOs, validation, error model, and migration for `service_resource_design.advanced_network_cloud_and_device_resource_models` are committed under `ts-oss-eng-service-and-resource-design-studio`.
- OpenAPI contract tests, unit tests, Flyway migration tests, event schema tests, and event replay tests cover `/api/03-oss-engineering-inventory-fulfillment/service-and-resource-design-studio/v1/advanced-network-cloud-and-device-resource-models`, `service_resource_design.advanced_network_cloud_and_device_resource_models`, and `AdvancedNetworkCloudAndDeviceResourceModelsStateChangedEvent`.
- `development-task-tracker.md` records command output, source feature link, PR/evidence links, and any blocked downstream consumer.

#### Negative Scenarios

- Unauthorized, cross-tenant, or wrong-purpose requests to `/api/03-oss-engineering-inventory-fulfillment/service-and-resource-design-studio/v1/advanced-network-cloud-and-device-resource-models` return `403` and write a denial audit row instead of exposing `Advanced Network Cloud And Device Resource Models` data.
- Missing source authority, stale dependency state, invalid lifecycle transition, or failed policy decision keeps `service_resource_design.advanced_network_cloud_and_device_resource_models` in blocked/exception state with owner and due date.
- Downstream outage or consumer rejection queues retry/replay for `AdvancedNetworkCloudAndDeviceResourceModelsStateChangedEvent` and prevents silent completion.

#### Edge Cases

- Bulk or project-scale updates to `Advanced Network Cloud And Device Resource Models` use preview, partial-failure reporting, idempotency keys, rollback/repair notes, and async export where needed.
- Historical correction preserves previous `service_resource_design.advanced_network_cloud_and_device_resource_models` values, audit reason, source timestamp, actor, and downstream recalculation/replay instructions.
- Multi-tenant, market, residency, localization, and high-volume queue cases include pagination, back-pressure, circuit breaker, and replay controls.

#### Test Expectations

- `mvn test` covers `AdvancedNetworkCloudAndDeviceResourceModelsService`, validation, authorization, idempotency, and lifecycle transition rules.
- OpenAPI contract tests call `POST/GET/PATCH /api/03-oss-engineering-inventory-fulfillment/service-and-resource-design-studio/v1/advanced-network-cloud-and-device-resource-models` and verify `$.state`, `$.id`, error payloads, and pagination/filter behavior.
- Flyway migration tests verify `service_resource_design.advanced_network_cloud_and_device_resource_models` columns and indexes; event replay tests validate `contracts/events/AdvancedNetworkCloudAndDeviceResourceModelsStateChangedEvent.json` and `service_resource_design.event_outbox` ordering.

### DT-03-service-and-resource-design-studio-P02-T002: Build Advanced Network Cloud And Device Resource Models workbench, controls, observability, and release tests

| Field | Value |
| --- | --- |
| Phase | P02 - Advanced Network Cloud And Device Resource Models And Catalog Version Certification And Retirement Mapping And Entity Catalog |
| Priority | P1 |
| Source evidence | [Advanced Network Cloud And Device Resource Models](../features/advanced-network-cloud-and-device-resource-models.md), [Implementation usage](../implementation-file-usage.md), [App README](../README.md), [App overview](../../service-and-resource-design-studio.md), [Modules and features](../modules-and-features.md), [Personas and journeys](../personas-and-user-journeys.md), [Suite tech/UI guidance](../../tech-and-ui-guidance.md), [Suite data model](../../data-model.md), [Suite implementation guide](../../implementation-file-usage-guide.md), [Repository strategy](../../../../repository-strategy.md) |
| Feature or module | Advanced Network Cloud And Device Resource Models |
| Build area | UI/Security/Ops/Test |
| Target artifact | `frontend/src/app/pages/advanced-network-cloud-and-device-resource-models/`, `tests/e2e/advanced-network-cloud-and-device-resource-models.spec.ts`, Grafana panel `advanced-network-cloud-and-device-resource-models`, and `docs/operations-runbook.md#advanced-network-cloud-and-device-resource-models` |
| Dependencies | DT-03-service-and-resource-design-studio-P02-T001 |
| Outputs | Angular workbench, queue/detail/timeline/evidence panels, role-aware guards, accessibility states, E2E tests, dashboard JSON, alert rules, runbook section |
| Missing evidence | No |

#### Implementation Notes

- Create `frontend/src/app/pages/advanced-network-cloud-and-device-resource-models/` with search/intake, detail, lifecycle timeline, exception queue, evidence drawer, dependency freshness panel, and allowed-next-action controls for personas Service designer, Resource designer, Network engineer.
- Wire route guards, tenant/brand/market context, masking, no-permission states, keyboard navigation, PrimeNG table/form patterns, and saved filters using `ts-shared-ui-design-system`.
- Add dashboard metrics and runbook steps for workflows Trigger, Validation, Orchestration, Exception, event replay backlog, queue aging, policy denials, consumer lag, and completion quality.

#### Acceptance Criteria

1. Given an authorized persona opens `/app/service-and-resource-design-studio/advanced-network-cloud-and-device-resource-models`, when records exist, then the workbench returns `$.uiState='ready'` and renders `Advanced Network Cloud And Device Resource Models` rows with lifecycle state, owner, freshness, SLA/OLA timer, and action menu.
2. Given the persona lacks permission, when the same route loads, then the UI shows a no-permission state and the backend returns `403` with `$.error.code='access-denied'`.
3. Given replay backlog or queue aging exceeds threshold, when Grafana dashboard `advanced-network-cloud-and-device-resource-models` refreshes, then it shows the metric and links to `docs/operations-runbook.md#advanced-network-cloud-and-device-resource-models`.

#### Definition Of Done

- `frontend/src/app/pages/advanced-network-cloud-and-device-resource-models/` includes route, component, service, state, fixtures, empty/loading/error/no-permission states, and accessibility labels.
- `tests/e2e/advanced-network-cloud-and-device-resource-models.spec.ts`, accessibility checks, security tests, dashboard checks, and runbook review pass and are linked from the tracker.
- `development-task-tracker.md` captures screenshots, command output, PR links, dashboard/runbook links, and unresolved blockers.

#### Negative Scenarios

- Do not render `Advanced Network Cloud And Device Resource Models` details across tenant/residency boundaries; masked values stay masked in table, detail, export, timeline, and dashboard paths.
- Do not close UI actions when backend validation, event publication, reconciliation, or required evidence is incomplete.
- Do not hide downstream outage, stale source data, policy denial, or manual override behind a generic success toast.

#### Edge Cases

- Mobile or constrained layouts for `Advanced Network Cloud And Device Resource Models` collapse tables into accessible cards without losing lifecycle, owner, SLA/OLA, or evidence fields.
- Bulk/replay actions require preview, explicit confirmation, partial-failure details, rollback/repair notes, and operator evidence.
- High-volume dashboard and queue views use pagination, saved filters, async export, trace IDs, and back-pressure indicators.

#### Test Expectations

- `npm run lint`, `npm test`, and `tests/e2e/advanced-network-cloud-and-device-resource-models.spec.ts` validate route, forms, guards, workbench states, and API integration.
- Accessibility tests cover keyboard navigation, focus order, screen-reader labels, color contrast, density, and responsive layout.
- Operational-readiness tests validate Grafana dashboard JSON, alert rules, event replay panel, runbook links, and release evidence.

### DT-03-service-and-resource-design-studio-P02-T003: Build Catalog Version Certification And Retirement Mapping API, data model, workflow, and event spine

| Field | Value |
| --- | --- |
| Phase | P02 - Advanced Network Cloud And Device Resource Models And Catalog Version Certification And Retirement Mapping And Entity Catalog |
| Priority | P0 |
| Source evidence | [Catalog Version Certification And Retirement Mapping](../features/catalog-version-certification-and-retirement-mapping.md), [Implementation usage](../implementation-file-usage.md), [App README](../README.md), [App overview](../../service-and-resource-design-studio.md), [Modules and features](../modules-and-features.md), [Personas and journeys](../personas-and-user-journeys.md), [Suite tech/UI guidance](../../tech-and-ui-guidance.md), [Suite data model](../../data-model.md), [Suite implementation guide](../../implementation-file-usage-guide.md), [Repository strategy](../../../../repository-strategy.md) |
| Feature or module | Catalog Version Certification And Retirement Mapping |
| Build area | API/Data/Event/Workflow/Security/Test |
| Target artifact | `backend/src/main/java/com/telcosuite/ossengineeringinventoryfulfillment/serviceandresourcedesignstudio/CatalogVersionCertificationAndRetirementMappingController.java`, `service_resource_design.catalog_version_certification_and_retirement_mapping`, `contracts/events/CatalogVersionRejected.json`, and `/api/03-oss-engineering-inventory-fulfillment/service-and-resource-design-studio/v1/catalog-version-certification-and-retirement-mapping` |
| Dependencies | DT-03-service-and-resource-design-studio-P02-T001 |
| Outputs | `CatalogVersionCertificationAndRetirementMappingController`, `CatalogVersionCertificationAndRetirementMappingService`, `service_resource_design.catalog_version_certification_and_retirement_mapping` migration, `CatalogVersionRejected` outbox schema, OpenAPI operations, unit/contract/migration/event replay tests |
| Missing evidence | No |

#### Implementation Notes

- Implement command and query APIs for `/api/03-oss-engineering-inventory-fulfillment/service-and-resource-design-studio/v1/catalog-version-certification-and-retirement-mapping` using TMF633, TMF634, TMF701, TMF704, TMF707, TMF760, with create, update, search, detail, lifecycle transition, timeline, evidence, and exception endpoints where the feature lifecycle requires them.
- Persist `Catalog Version Certification And Retirement Mapping` state in `service_resource_design.catalog_version_certification_and_retirement_mapping` with tenant, brand/market, lifecycle state, source authority, idempotency key, correlation ID, actor, reason code, audit fields, and `tmf_payload` JSONB.
- Publish `CatalogVersionRejected` through the transactional outbox with changed fields, replay metadata, consumer acknowledgement state, and reconciliation status for workflows: Trigger, Validation, Orchestration, Exception.
- Carry source details into code and tests for personas Service designer, Resource designer, Network engineer and objects Master entity, Referenced entities, Primary decisions, ODA boundary; keep cross-app references read-only unless they arrive through governed APIs/events/projections.

#### Acceptance Criteria

1. Given an authorized persona submits `POST /api/03-oss-engineering-inventory-fulfillment/service-and-resource-design-studio/v1/catalog-version-certification-and-retirement-mapping`, when required fields and policy checks pass, then the API returns `201` with `$.state`, persists `service_resource_design.catalog_version_certification_and_retirement_mapping.id`, and appends `CatalogVersionRejected` to `service_resource_design.event_outbox`.
2. Given a stale, duplicate, or out-of-order request hits `PATCH /api/03-oss-engineering-inventory-fulfillment/service-and-resource-design-studio/v1/catalog-version-certification-and-retirement-mapping/{id}`, when optimistic locking or idempotency validation fails, then the API returns `409` with `$.error.code='stale-or-duplicate-command'` and no second event is emitted.
3. Given another app needs `Catalog Version Certification And Retirement Mapping` state, when it requests data, then it receives TMF-aligned API/event/projection output and no direct database access to `service_resource_design.catalog_version_certification_and_retirement_mapping` is required.

#### Definition Of Done

- `CatalogVersionCertificationAndRetirementMappingController`, service, repository, DTOs, validation, error model, and migration for `service_resource_design.catalog_version_certification_and_retirement_mapping` are committed under `ts-oss-eng-service-and-resource-design-studio`.
- OpenAPI contract tests, unit tests, Flyway migration tests, event schema tests, and event replay tests cover `/api/03-oss-engineering-inventory-fulfillment/service-and-resource-design-studio/v1/catalog-version-certification-and-retirement-mapping`, `service_resource_design.catalog_version_certification_and_retirement_mapping`, and `CatalogVersionRejected`.
- `development-task-tracker.md` records command output, source feature link, PR/evidence links, and any blocked downstream consumer.

#### Negative Scenarios

- Unauthorized, cross-tenant, or wrong-purpose requests to `/api/03-oss-engineering-inventory-fulfillment/service-and-resource-design-studio/v1/catalog-version-certification-and-retirement-mapping` return `403` and write a denial audit row instead of exposing `Catalog Version Certification And Retirement Mapping` data.
- Missing source authority, stale dependency state, invalid lifecycle transition, or failed policy decision keeps `service_resource_design.catalog_version_certification_and_retirement_mapping` in blocked/exception state with owner and due date.
- Downstream outage or consumer rejection queues retry/replay for `CatalogVersionRejected` and prevents silent completion.

#### Edge Cases

- Bulk or project-scale updates to `Catalog Version Certification And Retirement Mapping` use preview, partial-failure reporting, idempotency keys, rollback/repair notes, and async export where needed.
- Historical correction preserves previous `service_resource_design.catalog_version_certification_and_retirement_mapping` values, audit reason, source timestamp, actor, and downstream recalculation/replay instructions.
- Multi-tenant, market, residency, localization, and high-volume queue cases include pagination, back-pressure, circuit breaker, and replay controls.

#### Test Expectations

- `mvn test` covers `CatalogVersionCertificationAndRetirementMappingService`, validation, authorization, idempotency, and lifecycle transition rules.
- OpenAPI contract tests call `POST/GET/PATCH /api/03-oss-engineering-inventory-fulfillment/service-and-resource-design-studio/v1/catalog-version-certification-and-retirement-mapping` and verify `$.state`, `$.id`, error payloads, and pagination/filter behavior.
- Flyway migration tests verify `service_resource_design.catalog_version_certification_and_retirement_mapping` columns and indexes; event replay tests validate `contracts/events/CatalogVersionRejected.json` and `service_resource_design.event_outbox` ordering.

### DT-03-service-and-resource-design-studio-P02-T004: Build Catalog Version Certification And Retirement Mapping workbench, controls, observability, and release tests

| Field | Value |
| --- | --- |
| Phase | P02 - Advanced Network Cloud And Device Resource Models And Catalog Version Certification And Retirement Mapping And Entity Catalog |
| Priority | P1 |
| Source evidence | [Catalog Version Certification And Retirement Mapping](../features/catalog-version-certification-and-retirement-mapping.md), [Implementation usage](../implementation-file-usage.md), [App README](../README.md), [App overview](../../service-and-resource-design-studio.md), [Modules and features](../modules-and-features.md), [Personas and journeys](../personas-and-user-journeys.md), [Suite tech/UI guidance](../../tech-and-ui-guidance.md), [Suite data model](../../data-model.md), [Suite implementation guide](../../implementation-file-usage-guide.md), [Repository strategy](../../../../repository-strategy.md) |
| Feature or module | Catalog Version Certification And Retirement Mapping |
| Build area | UI/Security/Ops/Test |
| Target artifact | `frontend/src/app/pages/catalog-version-certification-and-retirement-mapping/`, `tests/e2e/catalog-version-certification-and-retirement-mapping.spec.ts`, Grafana panel `catalog-version-certification-and-retirement-mapping`, and `docs/operations-runbook.md#catalog-version-certification-and-retirement-mapping` |
| Dependencies | DT-03-service-and-resource-design-studio-P02-T003 |
| Outputs | Angular workbench, queue/detail/timeline/evidence panels, role-aware guards, accessibility states, E2E tests, dashboard JSON, alert rules, runbook section |
| Missing evidence | No |

#### Implementation Notes

- Create `frontend/src/app/pages/catalog-version-certification-and-retirement-mapping/` with search/intake, detail, lifecycle timeline, exception queue, evidence drawer, dependency freshness panel, and allowed-next-action controls for personas Service designer, Resource designer, Network engineer.
- Wire route guards, tenant/brand/market context, masking, no-permission states, keyboard navigation, PrimeNG table/form patterns, and saved filters using `ts-shared-ui-design-system`.
- Add dashboard metrics and runbook steps for workflows Trigger, Validation, Orchestration, Exception, event replay backlog, queue aging, policy denials, consumer lag, and completion quality.

#### Acceptance Criteria

1. Given an authorized persona opens `/app/service-and-resource-design-studio/catalog-version-certification-and-retirement-mapping`, when records exist, then the workbench returns `$.uiState='ready'` and renders `Catalog Version Certification And Retirement Mapping` rows with lifecycle state, owner, freshness, SLA/OLA timer, and action menu.
2. Given the persona lacks permission, when the same route loads, then the UI shows a no-permission state and the backend returns `403` with `$.error.code='access-denied'`.
3. Given replay backlog or queue aging exceeds threshold, when Grafana dashboard `catalog-version-certification-and-retirement-mapping` refreshes, then it shows the metric and links to `docs/operations-runbook.md#catalog-version-certification-and-retirement-mapping`.

#### Definition Of Done

- `frontend/src/app/pages/catalog-version-certification-and-retirement-mapping/` includes route, component, service, state, fixtures, empty/loading/error/no-permission states, and accessibility labels.
- `tests/e2e/catalog-version-certification-and-retirement-mapping.spec.ts`, accessibility checks, security tests, dashboard checks, and runbook review pass and are linked from the tracker.
- `development-task-tracker.md` captures screenshots, command output, PR links, dashboard/runbook links, and unresolved blockers.

#### Negative Scenarios

- Do not render `Catalog Version Certification And Retirement Mapping` details across tenant/residency boundaries; masked values stay masked in table, detail, export, timeline, and dashboard paths.
- Do not close UI actions when backend validation, event publication, reconciliation, or required evidence is incomplete.
- Do not hide downstream outage, stale source data, policy denial, or manual override behind a generic success toast.

#### Edge Cases

- Mobile or constrained layouts for `Catalog Version Certification And Retirement Mapping` collapse tables into accessible cards without losing lifecycle, owner, SLA/OLA, or evidence fields.
- Bulk/replay actions require preview, explicit confirmation, partial-failure details, rollback/repair notes, and operator evidence.
- High-volume dashboard and queue views use pagination, saved filters, async export, trace IDs, and back-pressure indicators.

#### Test Expectations

- `npm run lint`, `npm test`, and `tests/e2e/catalog-version-certification-and-retirement-mapping.spec.ts` validate route, forms, guards, workbench states, and API integration.
- Accessibility tests cover keyboard navigation, focus order, screen-reader labels, color contrast, density, and responsive layout.
- Operational-readiness tests validate Grafana dashboard JSON, alert rules, event replay panel, runbook links, and release evidence.

### DT-03-service-and-resource-design-studio-P02-T005: Build Entity Catalog API, data model, workflow, and event spine

| Field | Value |
| --- | --- |
| Phase | P02 - Advanced Network Cloud And Device Resource Models And Catalog Version Certification And Retirement Mapping And Entity Catalog |
| Priority | P0 |
| Source evidence | [Entity Catalog](../features/entity-catalog.md), [Implementation usage](../implementation-file-usage.md), [App README](../README.md), [App overview](../../service-and-resource-design-studio.md), [Modules and features](../modules-and-features.md), [Personas and journeys](../personas-and-user-journeys.md), [Suite tech/UI guidance](../../tech-and-ui-guidance.md), [Suite data model](../../data-model.md), [Suite implementation guide](../../implementation-file-usage-guide.md), [Repository strategy](../../../../repository-strategy.md) |
| Feature or module | Entity Catalog |
| Build area | API/Data/Event/Workflow/Security/Test |
| Target artifact | `backend/src/main/java/com/telcosuite/ossengineeringinventoryfulfillment/serviceandresourcedesignstudio/EntityCatalogController.java`, `service_resource_design.entity_catalog`, `contracts/events/EntityCatalogStateChangedEvent.json`, and `/api/03-oss-engineering-inventory-fulfillment/service-and-resource-design-studio/v1/entity-catalog` |
| Dependencies | DT-03-service-and-resource-design-studio-P02-T003 |
| Outputs | `EntityCatalogController`, `EntityCatalogService`, `service_resource_design.entity_catalog` migration, `EntityCatalogStateChangedEvent` outbox schema, OpenAPI operations, unit/contract/migration/event replay tests |
| Missing evidence | No |

#### Implementation Notes

- Implement command and query APIs for `/api/03-oss-engineering-inventory-fulfillment/service-and-resource-design-studio/v1/entity-catalog` using TMF633, TMF634, TMF662, TMF703, with create, update, search, detail, lifecycle transition, timeline, evidence, and exception endpoints where the feature lifecycle requires them.
- Persist `Entity Catalog` state in `service_resource_design.entity_catalog` with tenant, brand/market, lifecycle state, source authority, idempotency key, correlation ID, actor, reason code, audit fields, and `tmf_payload` JSONB.
- Publish `EntityCatalogStateChangedEvent` through the transactional outbox with changed fields, replay metadata, consumer acknowledgement state, and reconciliation status for workflows: Trigger, Validation, Orchestration, Exception.
- Carry source details into code and tests for personas Service designer, Resource designer, Network engineer and objects Master entity, Referenced entities, Primary decisions, ODA boundary; keep cross-app references read-only unless they arrive through governed APIs/events/projections.

#### Acceptance Criteria

1. Given an authorized persona submits `POST /api/03-oss-engineering-inventory-fulfillment/service-and-resource-design-studio/v1/entity-catalog`, when required fields and policy checks pass, then the API returns `201` with `$.state`, persists `service_resource_design.entity_catalog.id`, and appends `EntityCatalogStateChangedEvent` to `service_resource_design.event_outbox`.
2. Given a stale, duplicate, or out-of-order request hits `PATCH /api/03-oss-engineering-inventory-fulfillment/service-and-resource-design-studio/v1/entity-catalog/{id}`, when optimistic locking or idempotency validation fails, then the API returns `409` with `$.error.code='stale-or-duplicate-command'` and no second event is emitted.
3. Given another app needs `Entity Catalog` state, when it requests data, then it receives TMF-aligned API/event/projection output and no direct database access to `service_resource_design.entity_catalog` is required.

#### Definition Of Done

- `EntityCatalogController`, service, repository, DTOs, validation, error model, and migration for `service_resource_design.entity_catalog` are committed under `ts-oss-eng-service-and-resource-design-studio`.
- OpenAPI contract tests, unit tests, Flyway migration tests, event schema tests, and event replay tests cover `/api/03-oss-engineering-inventory-fulfillment/service-and-resource-design-studio/v1/entity-catalog`, `service_resource_design.entity_catalog`, and `EntityCatalogStateChangedEvent`.
- `development-task-tracker.md` records command output, source feature link, PR/evidence links, and any blocked downstream consumer.

#### Negative Scenarios

- Unauthorized, cross-tenant, or wrong-purpose requests to `/api/03-oss-engineering-inventory-fulfillment/service-and-resource-design-studio/v1/entity-catalog` return `403` and write a denial audit row instead of exposing `Entity Catalog` data.
- Missing source authority, stale dependency state, invalid lifecycle transition, or failed policy decision keeps `service_resource_design.entity_catalog` in blocked/exception state with owner and due date.
- Downstream outage or consumer rejection queues retry/replay for `EntityCatalogStateChangedEvent` and prevents silent completion.

#### Edge Cases

- Bulk or project-scale updates to `Entity Catalog` use preview, partial-failure reporting, idempotency keys, rollback/repair notes, and async export where needed.
- Historical correction preserves previous `service_resource_design.entity_catalog` values, audit reason, source timestamp, actor, and downstream recalculation/replay instructions.
- Multi-tenant, market, residency, localization, and high-volume queue cases include pagination, back-pressure, circuit breaker, and replay controls.

#### Test Expectations

- `mvn test` covers `EntityCatalogService`, validation, authorization, idempotency, and lifecycle transition rules.
- OpenAPI contract tests call `POST/GET/PATCH /api/03-oss-engineering-inventory-fulfillment/service-and-resource-design-studio/v1/entity-catalog` and verify `$.state`, `$.id`, error payloads, and pagination/filter behavior.
- Flyway migration tests verify `service_resource_design.entity_catalog` columns and indexes; event replay tests validate `contracts/events/EntityCatalogStateChangedEvent.json` and `service_resource_design.event_outbox` ordering.

### DT-03-service-and-resource-design-studio-P02-T006: Build Entity Catalog workbench, controls, observability, and release tests

| Field | Value |
| --- | --- |
| Phase | P02 - Advanced Network Cloud And Device Resource Models And Catalog Version Certification And Retirement Mapping And Entity Catalog |
| Priority | P1 |
| Source evidence | [Entity Catalog](../features/entity-catalog.md), [Implementation usage](../implementation-file-usage.md), [App README](../README.md), [App overview](../../service-and-resource-design-studio.md), [Modules and features](../modules-and-features.md), [Personas and journeys](../personas-and-user-journeys.md), [Suite tech/UI guidance](../../tech-and-ui-guidance.md), [Suite data model](../../data-model.md), [Suite implementation guide](../../implementation-file-usage-guide.md), [Repository strategy](../../../../repository-strategy.md) |
| Feature or module | Entity Catalog |
| Build area | UI/Security/Ops/Test |
| Target artifact | `frontend/src/app/pages/entity-catalog/`, `tests/e2e/entity-catalog.spec.ts`, Grafana panel `entity-catalog`, and `docs/operations-runbook.md#entity-catalog` |
| Dependencies | DT-03-service-and-resource-design-studio-P02-T005 |
| Outputs | Angular workbench, queue/detail/timeline/evidence panels, role-aware guards, accessibility states, E2E tests, dashboard JSON, alert rules, runbook section |
| Missing evidence | No |

#### Implementation Notes

- Create `frontend/src/app/pages/entity-catalog/` with search/intake, detail, lifecycle timeline, exception queue, evidence drawer, dependency freshness panel, and allowed-next-action controls for personas Service designer, Resource designer, Network engineer.
- Wire route guards, tenant/brand/market context, masking, no-permission states, keyboard navigation, PrimeNG table/form patterns, and saved filters using `ts-shared-ui-design-system`.
- Add dashboard metrics and runbook steps for workflows Trigger, Validation, Orchestration, Exception, event replay backlog, queue aging, policy denials, consumer lag, and completion quality.

#### Acceptance Criteria

1. Given an authorized persona opens `/app/service-and-resource-design-studio/entity-catalog`, when records exist, then the workbench returns `$.uiState='ready'` and renders `Entity Catalog` rows with lifecycle state, owner, freshness, SLA/OLA timer, and action menu.
2. Given the persona lacks permission, when the same route loads, then the UI shows a no-permission state and the backend returns `403` with `$.error.code='access-denied'`.
3. Given replay backlog or queue aging exceeds threshold, when Grafana dashboard `entity-catalog` refreshes, then it shows the metric and links to `docs/operations-runbook.md#entity-catalog`.

#### Definition Of Done

- `frontend/src/app/pages/entity-catalog/` includes route, component, service, state, fixtures, empty/loading/error/no-permission states, and accessibility labels.
- `tests/e2e/entity-catalog.spec.ts`, accessibility checks, security tests, dashboard checks, and runbook review pass and are linked from the tracker.
- `development-task-tracker.md` captures screenshots, command output, PR links, dashboard/runbook links, and unresolved blockers.

#### Negative Scenarios

- Do not render `Entity Catalog` details across tenant/residency boundaries; masked values stay masked in table, detail, export, timeline, and dashboard paths.
- Do not close UI actions when backend validation, event publication, reconciliation, or required evidence is incomplete.
- Do not hide downstream outage, stale source data, policy denial, or manual override behind a generic success toast.

#### Edge Cases

- Mobile or constrained layouts for `Entity Catalog` collapse tables into accessible cards without losing lifecycle, owner, SLA/OLA, or evidence fields.
- Bulk/replay actions require preview, explicit confirmation, partial-failure details, rollback/repair notes, and operator evidence.
- High-volume dashboard and queue views use pagination, saved filters, async export, trace IDs, and back-pressure indicators.

#### Test Expectations

- `npm run lint`, `npm test`, and `tests/e2e/entity-catalog.spec.ts` validate route, forms, guards, workbench states, and API integration.
- Accessibility tests cover keyboard navigation, focus order, screen-reader labels, color contrast, density, and responsive layout.
- Operational-readiness tests validate Grafana dashboard JSON, alert rules, event replay panel, runbook links, and release evidence.

### DT-03-service-and-resource-design-studio-P02-T007: Prove Advanced Network Cloud And Device Resource Models And Catalog Version Certification And Retirement Mapping And Entity Catalog release gate, replay, and handoff evidence

| Field | Value |
| --- | --- |
| Phase | P02 - Advanced Network Cloud And Device Resource Models And Catalog Version Certification And Retirement Mapping And Entity Catalog |
| Priority | P1 |
| Source evidence | [Advanced Network Cloud And Device Resource Models](../features/advanced-network-cloud-and-device-resource-models.md), [Catalog Version Certification And Retirement Mapping](../features/catalog-version-certification-and-retirement-mapping.md), [Entity Catalog](../features/entity-catalog.md), [Implementation usage](../implementation-file-usage.md), [App README](../README.md), [App overview](../../service-and-resource-design-studio.md), [Modules and features](../modules-and-features.md), [Personas and journeys](../personas-and-user-journeys.md), [Suite tech/UI guidance](../../tech-and-ui-guidance.md), [Suite data model](../../data-model.md), [Suite implementation guide](../../implementation-file-usage-guide.md), [Repository strategy](../../../../repository-strategy.md) |
| Feature or module | Advanced Network Cloud And Device Resource Models And Catalog Version Certification And Retirement Mapping And Entity Catalog |
| Build area | Test/Ops/Release/Event |
| Target artifact | `tests/release/advanced-network-cloud-and-device-resource-models-and-catalog-version.spec.ts`, `docs/release-notes/advanced-network-cloud-and-device-resource-models-and-catalog-version.md`, Grafana dashboard `advanced-network-cloud-and-device-resource-models-and-catalog-version`, and replay fixtures |
| Dependencies | DT-03-service-and-resource-design-studio-P02-T002, DT-03-service-and-resource-design-studio-P02-T004, DT-03-service-and-resource-design-studio-P02-T006 |
| Outputs | Release-gate test, replay/reconciliation evidence, accessibility/security/performance reports, dashboard/runbook links, support handoff notes |
| Missing evidence | No |

#### Implementation Notes

- Create a release-gate checklist for `advanced-network-cloud-and-device-resource-models-and-catalog-version` covering Advanced Network Cloud And Device Resource Models, Catalog Version Certification And Retirement Mapping, Entity Catalog, with happy path, assisted path, negative path, edge cases, event replay, data reconciliation, security, accessibility, performance, and support evidence.
- Record producer and consumer acknowledgements for phase events, reconcile `service_resource_design.event_outbox`, and link replay fixtures and correlation IDs.
- Update `docs/operations-runbook.md`, `docs/release-notes/advanced-network-cloud-and-device-resource-models-and-catalog-version.md`, and `development-task-tracker.md` with release evidence and unresolved blockers.

#### Acceptance Criteria

1. Given all tasks in `P02-advanced-network-cloud-and-device-resource-models-and-catalog-version.md` are complete, when `tests/release/advanced-network-cloud-and-device-resource-models-and-catalog-version.spec.ts` runs, then it returns exit code `0` and links evidence for UI, API, data, event, security, ops, and test gates.
2. Given a consumer rejects an event from `advanced-network-cloud-and-device-resource-models-and-catalog-version`, when replay is triggered, then the replay fixture preserves `$.correlationId`, `$.eventId`, and consumer acknowledgement state.
3. Given release notes are generated, when support reviews `docs/release-notes/advanced-network-cloud-and-device-resource-models-and-catalog-version.md`, then open blockers, rollback steps, runbook links, and ownership contacts are present.

#### Definition Of Done

- `tests/release/advanced-network-cloud-and-device-resource-models-and-catalog-version.spec.ts`, replay fixtures, dashboard/runbook links, and release notes are committed.
- Accessibility, security, contract, migration, event replay, performance, and operational-readiness evidence is linked from the tracker.
- Open blockers have owner, due date, target increment, and rollback or removal criteria.

#### Negative Scenarios

- Do not mark the phase Done if event replay, reconciliation, accessibility, security, or downstream acknowledgement evidence is missing.
- Do not release `advanced-network-cloud-and-device-resource-models-and-catalog-version` with unresolved cross-app writes, direct schema coupling, or stale source authority assumptions.
- Do not suppress failed release gates; record failures with owner, due date, and target increment.

#### Edge Cases

- Coordinated release gates may require downstream app windows; record scheduling, owner, and fallback route in release notes.
- Historical backfill, replay, bulk update, or migration repair runs must include preview, partial failure report, and rollback evidence.
- High-volume launch periods require dashboard thresholds, alert owners, queue back-pressure, and support escalation paths.

#### Test Expectations

- `tests/release/advanced-network-cloud-and-device-resource-models-and-catalog-version.spec.ts`, `mvn test`, OpenAPI/event replay tests, Flyway checks, Playwright/Cypress E2E, accessibility, security, and k6/performance gates pass.
- `docker compose config`, clean-checkout smoke, `helm lint`, Kubernetes dry-run, dashboard JSON validation, and runbook link checks pass.
- Tracker evidence links command output, PRs, screenshots, replay payloads, dashboards, release notes, and support handoff notes.
