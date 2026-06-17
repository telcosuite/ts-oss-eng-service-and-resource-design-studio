# Service And Resource Design Studio Phase Discovery

## App Identity

| Field | Value |
| --- | --- |
| Suite | OSS Engineering, Inventory, And Fulfillment |
| App | Service And Resource Design Studio |
| App slug | `service-and-resource-design-studio` |
| Implementation repo | `ts-oss-eng-service-and-resource-design-studio` |
| Database | `ts_oss_engineering_fulfillment` |
| Schema | `service_resource_design` |
| APIs | TMF633, TMF620, TMF634, TMF730, TMF701, TMF645, TMF679, TMF662 |
| Generated date | 2026-06-17 |
| Phase/task signature | 4 phases / P01=14, P02=7, P03=7, P04=5 |

Phase count decision: 4 phases are evidence-derived from the current app-repo state, P01 runtime bootstrap requirements, and 8 build-ready feature files grouped by lifecycle, UI/API/data/event ownership, integration risk, and release gates.

Repeated skeleton audit: Evidence-derived and accepted for this app. Even when another app shares a phase/task-count signature, this discovery file cites this app's feature files, phase files, current repo state, and split/merge decisions; regenerate and split or merge phases if those inputs change.

## Input Evidence Inventory

| Evidence | Link | Status |
| --- | --- | --- |
| App implementation usage | [../implementation-file-usage.md](../implementation-file-usage.md) | Present |
| App README | [../README.md](../README.md) | Present |
| Modules and features | [../modules-and-features.md](../modules-and-features.md) | Present |
| Personas and journeys | [../personas-and-user-journeys.md](../personas-and-user-journeys.md) | Present |
| Suite data model | [../../data-model.md](../../data-model.md) | Present |
| Suite tech/UI guidance | [../../tech-and-ui-guidance.md](../../tech-and-ui-guidance.md) | Present |
| Suite implementation guide | [../../implementation-file-usage-guide.md](../../implementation-file-usage-guide.md) | Present |
| Repository strategy | [../../../../repository-strategy.md](../../../../repository-strategy.md) | Present |
| Feature: Advanced Network Cloud And Device Resource Models | [../features/advanced-network-cloud-and-device-resource-models.md](../features/advanced-network-cloud-and-device-resource-models.md) | Present |
| Feature: Catalog Version Certification And Retirement Mapping | [../features/catalog-version-certification-and-retirement-mapping.md](../features/catalog-version-certification-and-retirement-mapping.md) | Present |
| Feature: Entity Catalog | [../features/entity-catalog.md](../features/entity-catalog.md) | Present |
| Feature: Fulfillment And Activation Template Design | [../features/fulfillment-and-activation-template-design.md](../features/fulfillment-and-activation-template-design.md) | Present |
| Feature: Product-Service-Resource Mapping | [../features/product-service-resource-mapping.md](../features/product-service-resource-mapping.md) | Present |
| Feature: Resource Catalog | [../features/resource-catalog.md](../features/resource-catalog.md) | Present |
| Feature: Service Catalog | [../features/service-catalog.md](../features/service-catalog.md) | Present |
| Feature: Technical Compatibility And Design Rule | [../features/technical-compatibility-and-design-rule.md](../features/technical-compatibility-and-design-rule.md) | Present |

## App Repository Current State Inventory

| Marker | Value |
| --- | --- |
| Repo exists | Yes |
| Runnable frontend: | No |
| Runnable backend: | No |
| App-specific migrations: | Yes |
| OpenAPI contract | Yes |
| Event contracts | Yes |
| Deployment skeleton | Yes |
| CI workflow | No |
| Current implementation conclusion: | Keep the zero-to-one foundation explicit until runnable frontend, backend, migrations, contracts, CI, deployment, and proof-slice evidence are all present in `ts-oss-eng-service-and-resource-design-studio`. |

## Feature/Module Cluster Analysis

| Feature | Feature ID | Source detail carried into tasks | Implementing task IDs | Phase |
| --- | --- | --- | --- | --- |
| [Advanced Network Cloud And Device Resource Models](../features/advanced-network-cloud-and-device-resource-models.md) | F-advanced-network-cloud-and-device-resource-models-01 |  | DT-03-service-and-resource-design-studio-P02-T001, DT-03-service-and-resource-design-studio-P02-T002, DT-03-service-and-resource-design-studio-P02-T007 | P02 - Advanced Network Cloud And Device Resource Models And Catalog Version Certification And Retirement Mapping And Entity Catalog |
| [Catalog Version Certification And Retirement Mapping](../features/catalog-version-certification-and-retirement-mapping.md) | F-catalog-version-certification-and-retirement-mapping-01 |  | DT-03-service-and-resource-design-studio-P02-T003, DT-03-service-and-resource-design-studio-P02-T004, DT-03-service-and-resource-design-studio-P02-T007 | P02 - Advanced Network Cloud And Device Resource Models And Catalog Version Certification And Retirement Mapping And Entity Catalog |
| [Entity Catalog](../features/entity-catalog.md) | F-entity-catalog-01 |  | DT-03-service-and-resource-design-studio-P02-T005, DT-03-service-and-resource-design-studio-P02-T006, DT-03-service-and-resource-design-studio-P02-T007 | P02 - Advanced Network Cloud And Device Resource Models And Catalog Version Certification And Retirement Mapping And Entity Catalog |
| [Fulfillment And Activation Template Design](../features/fulfillment-and-activation-template-design.md) | F-fulfillment-and-activation-template-design-01 |  | DT-03-service-and-resource-design-studio-P03-T001, DT-03-service-and-resource-design-studio-P03-T002, DT-03-service-and-resource-design-studio-P03-T007 | P03 - Fulfillment And Activation Template Design And Product-Service-Resource Mapping And Resource Catalog |
| [Product-Service-Resource Mapping](../features/product-service-resource-mapping.md) | F-product-service-resource-mapping-01 |  | DT-03-service-and-resource-design-studio-P03-T003, DT-03-service-and-resource-design-studio-P03-T004, DT-03-service-and-resource-design-studio-P03-T007 | P03 - Fulfillment And Activation Template Design And Product-Service-Resource Mapping And Resource Catalog |
| [Resource Catalog](../features/resource-catalog.md) | F-resource-catalog-01 |  | DT-03-service-and-resource-design-studio-P03-T005, DT-03-service-and-resource-design-studio-P03-T006, DT-03-service-and-resource-design-studio-P03-T007 | P03 - Fulfillment And Activation Template Design And Product-Service-Resource Mapping And Resource Catalog |
| [Service Catalog](../features/service-catalog.md) | F-service-catalog-01 |  | DT-03-service-and-resource-design-studio-P04-T001, DT-03-service-and-resource-design-studio-P04-T002, DT-03-service-and-resource-design-studio-P04-T005 | P04 - Service Catalog And Technical Compatibility And Design Rule |
| [Technical Compatibility And Design Rule](../features/technical-compatibility-and-design-rule.md) | F-technical-compatibility-and-design-rule-01 |  | DT-03-service-and-resource-design-studio-P04-T003, DT-03-service-and-resource-design-studio-P04-T004, DT-03-service-and-resource-design-studio-P04-T005 | P04 - Service Catalog And Technical Compatibility And Design Rule |

## Phase Decision Matrix

| Phase file | Task count | Evidence basis | Exit gate |
| --- | --- | --- | --- |
| [P01-from-scratch-app-foundation-and-delivery-runtime.md](P01-from-scratch-app-foundation-and-delivery-runtime.md) | 14 | The planning pack and local repo inspection do not prove a complete runnable implementation for `ts-oss-eng-service-and-resource-design-studio`; this from-scratch foundation phase creates the app-root runtime, governance, contracts, data, CI, deployment, observability, and proof slice before feature delivery. | A clean checkout of `ts-oss-eng-service-and-resource-design-studio` can run Angular and Spring Boot, apply `service_resource_design` migrations, validate contracts/events, run Docker Compose and Helm checks, and prove one UI/API/data/event slice. |
| [P02-advanced-network-cloud-and-device-resource-models-and-catalog-version.md](P02-advanced-network-cloud-and-device-resource-models-and-catalog-version.md) | 7 | Build the Advanced Network Cloud And Device Resource Models, Catalog Version Certification And Retirement Mapping, Entity Catalog capability cluster for Service And Resource Design Studio, carrying source workflows, APIs, events, tables, controls, and tests from the feature files into implementable work. | Service And Resource Design Studio can execute the Advanced Network Cloud And Device Resource Models, Catalog Version Certification And Retirement Mapping, Entity Catalog workflows through UI, API, `service_resource_design` persistence, outbox events, audit evidence, and release tests. |
| [P03-fulfillment-and-activation-template-design-and-product-service-resource-mapping.md](P03-fulfillment-and-activation-template-design-and-product-service-resource-mapping.md) | 7 | Build the Fulfillment And Activation Template Design, Product-Service-Resource Mapping, Resource Catalog capability cluster for Service And Resource Design Studio, carrying source workflows, APIs, events, tables, controls, and tests from the feature files into implementable work. | Service And Resource Design Studio can execute the Fulfillment And Activation Template Design, Product-Service-Resource Mapping, Resource Catalog workflows through UI, API, `service_resource_design` persistence, outbox events, audit evidence, and release tests. |
| [P04-service-catalog-and-technical-compatibility-and-design-rule.md](P04-service-catalog-and-technical-compatibility-and-design-rule.md) | 5 | Build the Service Catalog, Technical Compatibility And Design Rule capability cluster for Service And Resource Design Studio, carrying source workflows, APIs, events, tables, controls, and tests from the feature files into implementable work. | Service And Resource Design Studio can execute the Service Catalog, Technical Compatibility And Design Rule workflows through UI, API, `service_resource_design` persistence, outbox events, audit evidence, and release tests. |

## Split/Merge Decisions

- P01 remains the app-runtime foundation because the local repo inspection does not prove a complete runnable implementation for `ts-oss-eng-service-and-resource-design-studio`.
- Feature phases are grouped from source `features/*.md` files by lifecycle ownership, UI workbench/API/data/event coupling, security/privacy controls, observability, and release-test needs.
- Every feature file appears in task `Source evidence`, the tracker coverage matrix, and this discovery artifact; tracker-only feature references are not accepted as coverage.
- Generic phase names from older task packs are retired by this refresh and replaced with feature-derived phase names.

## Validator and Regeneration Notes

- Run `python3 telcosuite-skills/skills/tmf-dev-task-planner/scripts/validate_dev_tasks.py --root ts-planning/planning/suite-details/03-oss-engineering-inventory-fulfillment/service-and-resource-design-studio --strict` after refresh.
- Re-run the mirror driver after validation so `ts-oss-eng-service-and-resource-design-studio/dev-tasks/` remains byte-identical to the planning source.
- If a source feature changes, refresh this app pack and verify phase count, feature coverage, task detail quality, and mirror parity again.
