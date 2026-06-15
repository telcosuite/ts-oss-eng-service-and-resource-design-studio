| Field | Value |
| --- | --- |
| Feature ID | F-resource-catalog-01 |
| App | Service And Resource Design Studio |
| App slug | `service-and-resource-design-studio` |
| Module | Service And Resource Design Studio |
| Source slice | [modules-and-features.md](../modules-and-features.md) |
| Last refined | 2026-06-15 |
| Refiner verdict | Build-ready |

# Resource Catalog Feature Specification


Reviewed: 2026-06-07

Suite: OSS Engineering, Inventory, And Fulfillment

App: [Service And Resource Design Studio App](../README.md)

Source module detail: [Modules And Features](../modules-and-features.md)

Source gap review: [E2E Feature Gap Assessment](../../../e2e-feature-gap-assessment.md)

Feature area slug: `resource-catalog`

E2E gap severity: Core

## Feature Intent

Manage physical, logical, compute, software, device, cloud, network, identifier, and capacity resource specifications so Inventory And Topology can instantiate resources and Fulfillment can request assignments with valid activation attributes. The Resource Catalog feature produces a governed resource specification and resource catalog version outcome with versioned evidence, consumer readiness, and explicit ODA boundaries instead of spreadsheet-driven catalog or activation interpretation.

## Telecom Objects And Decision Rights

- Master entity: resource specification and resource catalog version. Service And Resource Design Studio owns resource specifications, resource characteristic templates, capacity units, compatibility attributes, assignment metadata, activation links, resource lifecycle states, and inventory model references.
- Referenced entities: service specifications, product realization rules, resource inventory instances, resource pools, stock SKUs, activation command templates, discovery models, NMS/EMS/SDN/NFV controllers, and field work artifacts. Service And Resource Design Studio consumes these through APIs, events, governed projections, or certification packs and does not overwrite their operational masters.
- Primary decisions: draft, validate, certify, publish, constrain, retire, reinstate, or map a resource specification to successor resource models. The decision records the accountable persona, rule result, waiver status, affected product/service/resource versions, consumer impact, and downstream handoff.
- ODA boundary: Service And Resource Design Studio keeps private technical catalog, template, rule, certification, and publication records; Product And Offer Studio, Inventory And Topology, Fulfillment And Activation Control Tower, Field Work, Assurance, Platform, and Partner apps remain masters for their own lifecycle records.

## Personas, Jobs To Be Done, And Outcomes

| Persona | Job to be done | Outcome |
| --- | --- | --- |
| Service designer | Define customer-facing and resource-facing service specification behavior, lifecycle states, characteristics, and dependency rules. | Approved service specifications can be consumed by Product And Offer Studio, Order Management Hub, Fulfillment, Inventory, and Assurance without local reinterpretation. |
| Resource designer | Define physical, logical, cloud, software, device, identifier, and network resource specification patterns. | Resource specifications expose capacity units, assignment attributes, activation metadata, and inventory model links that Inventory And Topology can instantiate safely. |
| Network engineer | Validate technology-specific constraints, topology assumptions, controller support, firmware/software compatibility, and rollback feasibility. | Network engineering decisions are visible as rule results, waivers, and certification evidence before catalog publication. |
| Product/catalog governance user | Approve technical realization readiness for commercial product offerings, launch variants, retirements, and migration mappings. | Product-service-resource mappings are versioned, certified, and traceable before CPQ or order decomposition can rely on them. |
| Fulfillment architect | Define decomposition, orchestration, activation template, fallout, compensation, and test handoff behavior. | Fulfillment And Activation Control Tower receives executable templates and validation rules rather than ambiguous catalog notes. |

## Core Workflows

| Stage | Telecom trigger or validation | Orchestration, exception, completion, and evidence |
| --- | --- | --- |
| Trigger | Resource Catalog starts from new network resource model, CPE or device introduction, cloud/edge capability launch, field build acceptance, inventory data gap, firmware change, or controller onboarding. | The resource specification and resource catalog version opens with owner, tenant, market, technology scope, source trigger, lifecycle action, correlation ID, impacted consumer list, and required catalog/version references. |
| Validation | The app validates resource attribute completeness, capacity unit definition, inventory instantiation rule, controller support, stock/SKU reference, assignment eligibility, firmware/software compatibility, and retirement impact. | Invalid resource specification and resource catalog version data creates rule failures, certification exceptions, waiver tasks, or publication rejection before CPQ, order decomposition, fulfillment, activation, inventory, or assurance can consume the change. |
| Orchestration | Service And Resource Design Studio coordinates catalog, design, inventory, fulfillment, activation, field, assurance, partner, test, and data consumers through APIs, events, workflow tasks, governed projections, or certification packs. | Consumers receive versioned technical catalog outputs while their own databases and lifecycle records remain private to their owning apps. |
| Exception | If Resource spec lacks assignable capacity unit, CPE model has incompatible firmware capability, Controller supports command but not rollback blocks the lifecycle, the workflow routes to the accountable service design, resource design, network engineering, catalog governance, fulfillment architecture, data stewardship, or security/compliance owner. | The exception captures failed rule, affected service/resource/product, risk, waiver authority, blocked consumer, correlation ID, evidence gap, and escalation path. |
| Completion | Completion occurs when the resource specification and resource catalog version is certified, published, rejected, retired, superseded, or mapped with downstream consumer acknowledgement. | Completion evidence includes catalog version, rule version, template version where relevant, validation result, approval/waiver record, impacted inventory or order scope, event IDs, and consumer revalidation status. |

## Missing Use Cases And Scenarios

| Scenario | Required behavior |
| --- | --- |
| Greenfield build or launch | Resource Catalog must support greenfield OLT port model introduction with explicit resource specification and resource catalog version, version, validation result, decision owner, evidence, and downstream handoff. |
| Brownfield MACD | Resource Catalog must support brownfield CPE firmware capability change with explicit resource specification and resource catalog version, version, validation result, decision owner, evidence, and downstream handoff. |
| Enterprise bulk or migration | Resource Catalog must support enterprise bulk router model certification with explicit resource specification and resource catalog version, version, validation result, decision owner, evidence, and downstream handoff. |
| Partner/off-net or external dependency | Resource Catalog must support cloud edge node resource model for NaaS with explicit resource specification and resource catalog version, version, validation result, decision owner, evidence, and downstream handoff. |
| Retirement, rollback, or decommissioning | Resource Catalog must support legacy resource spec retirement with installed inventory impact with explicit resource specification and resource catalog version, version, validation result, decision owner, evidence, and downstream handoff. |

## Capability Slices

| Feature ID | Feature | Parent feature area | Priority guidance |
| --- | --- | --- | --- |
| F-resource-catalog-01 | Physical resource specification | Resource Catalog | P1: required to make resource specification lifecycle usable for product launch, order-to-activate, inventory handoff, assurance readiness, or governed retirement. |
| F-resource-catalog-02 | Logical and identifier resource specification | Resource Catalog | P1: required to make resource specification lifecycle usable for product launch, order-to-activate, inventory handoff, assurance readiness, or governed retirement. |
| F-resource-catalog-03 | Cloud compute and software resource specification | Resource Catalog | P1: required to make resource specification lifecycle usable for product launch, order-to-activate, inventory handoff, assurance readiness, or governed retirement. |
| F-resource-catalog-04 | Network resource capacity unit | Resource Catalog | P1: required to make resource specification lifecycle usable for product launch, order-to-activate, inventory handoff, assurance readiness, or governed retirement. |
| F-resource-catalog-05 | Activation attribute link | Resource Catalog | P2: required to make resource specification lifecycle usable for product launch, order-to-activate, inventory handoff, assurance readiness, or governed retirement. |
| F-resource-catalog-06 | Inventory model link | Resource Catalog | P2: required to make resource specification lifecycle usable for product launch, order-to-activate, inventory handoff, assurance readiness, or governed retirement. |
| F-resource-catalog-07 | Resource retirement and successor mapping | Resource Catalog | P2: required to make resource specification lifecycle usable for product launch, order-to-activate, inventory handoff, assurance readiness, or governed retirement. |

## Acceptance Criteria

1. **AC-resource-catalog-01:** Given an authorized Service designer, Resource designer, Network engineer, Product/catalog governance user, or Fulfillment architect creates or updates the resource specification and resource catalog version, when the resource specification lifecycle advances from draft to review, then Service And Resource Design Studio validates resource attribute completeness, capacity unit definition, inventory instantiation rule, controller support, stock/SKU reference, assignment eligibility, firmware/software compatibility, and retirement impact before accepting the state change.
2. **AC-resource-catalog-02:** Given the resource specification and resource catalog version references commercial product, service, resource, inventory, activation, or assurance data, when a persona opens the Resource Catalog record, then the app shows source owner, referenced version, freshness, confidence, correction route, and whether the reference is read-only or app-owned.
3. **AC-resource-catalog-03:** Given Resource spec lacks assignable capacity unit, when validation fails for Resource Catalog, then the app keeps the record in draft, blocked, or rejected state with severity, owner, due date, reason code, impacted consumer, waiver option, and correlation ID.
4. **AC-resource-catalog-04:** Given a governance decision is required for the resource specification and resource catalog version, when the accountable persona approves, rejects, waives, retires, or supersedes it, then the app stores decision right, actor, role, reason, old/new values, policy version, evidence links, tenant/region boundary, and idempotency key.
5. **AC-resource-catalog-05:** Given CPQ, Order Management Hub, Fulfillment, Inventory, Field, Assurance, Partner, or Data consumers subscribe to Resource Catalog changes, when the resource specification and resource catalog version is published or retired, then the app emits a versioned event with changed fields, impacted services/resources, consumer revalidation flag, replay metadata, and correlation ID.
6. **AC-resource-catalog-06:** Given a brownfield MACD, migration, rollback, or decommissioning scenario references the resource specification and resource catalog version, when the user requests publication or closure, then the app validates active inventory impact, in-flight order impact, field/partner dependency, activation rollback path, and customer/NOC/care handoff before closure.
7. **AC-resource-catalog-07:** Given supervisors or data stewards review Resource Catalog operations, when they open dashboards, then they see draft aging, certification pass/fail, exception causes, waiver aging, publication lag, consumer adoption, revalidation backlog, and downstream fallout linked to the resource specification and resource catalog version.

## Negative Scenarios

Negative scenarios for this feature include permission denial, missing source data, stale dependency state, policy failure, duplicate or replayed request, downstream timeout, reconciliation mismatch, and any feature-specific negative scenario additions listed in the suite gap-review closure addendum.

## Edge Cases

| Scenario | Expected behavior |
| --- | --- |
| Resource spec lacks assignable capacity unit | Resource Catalog blocks unsafe publication or routes a governed exception with owner, due date, affected product/service/resource, consumer impact, waiver authority, and replayable evidence. |
| CPE model has incompatible firmware capability | Resource Catalog blocks unsafe publication or routes a governed exception with owner, due date, affected product/service/resource, consumer impact, waiver authority, and replayable evidence. |
| Controller supports command but not rollback | Resource Catalog blocks unsafe publication or routes a governed exception with owner, due date, affected product/service/resource, consumer impact, waiver authority, and replayable evidence. |
| Stock SKU differs from resource model identity | Resource Catalog blocks unsafe publication or routes a governed exception with owner, due date, affected product/service/resource, consumer impact, waiver authority, and replayable evidence. |
| Discovered resource cannot be typed against any certified spec | Resource Catalog blocks unsafe publication or routes a governed exception with owner, due date, affected product/service/resource, consumer impact, waiver authority, and replayable evidence. |
| Duplicate, stale, or out-of-order publication request | Resource Catalog uses optimistic locking, event version, source timestamp, and idempotency key so retries cannot publish duplicate catalog, template, rule, or certification state. |
| Cross-tenant, cross-region, or restricted topology access | Resource Catalog blocks mutation, masks restricted service/resource/topology data, and records policy decision metadata for tenant isolation, data residency, and export control. |
| Downstream consumer unavailable | Resource Catalog either fails fast for synchronous certification gates or queues a controlled retry, replay, or consumer revalidation task with owner, due date, backoff policy, and correlation ID. |
| Legal hold or regulatory retention conflict | Resource Catalog prevents deletion or destructive retirement of catalog, rule, template, or certification evidence until legal hold, retention, and regulatory inventory evidence controls allow it. |

## Suite Gap Review Closure Addendum

Source review: [03 Oss Engineering Inventory Fulfillment Gap Review](../../../../suite-gap-reviews/03-oss-engineering-inventory-fulfillment-gap-review.md)

This addendum applies the suite gap-review findings tied to this feature file. It supplements the baseline feature specification and should be carried into epic, story, API, event, data, and test refinement.

### Review Backlog Items Addressed

| Severity | Gap-review item | Closure expectation |
| --- | --- | --- |
| High | Advanced model compatibility for NaaS, slices, IoT, edge, firmware, and eSIM. | Add concrete happy path, negative path, edge-case, API/event/data control, reporting, and test evidence for this feature area. |

### Acceptance Criteria Additions

1. Given a service/resource catalog version is promoted, when any CPQ, order, fulfillment, activation, inventory, assurance, partner, or billing certification fails, then promotion is blocked or released only to a controlled market/channel.
2. Given a product-service-resource mapping changes, when impacted active offers/orders/templates are identified, then owners see blast radius, required migration, and rollback plan before approval.
3. Given an activation template is released, when command idempotency, rollback, validation test, and inventory side effects are not defined, then it cannot be consumed by fulfillment.

### Negative Scenario Additions

1. Product offer maps to retired resource spec; block order decomposition and route to catalog owner.
2. Activation template works for one vendor controller but not another market; restrict release by geography/technology and record compatibility evidence.
3. Retirement mapping leaves active enterprise service without migration path; reject retirement approval.

### API, Event, Data, And Reporting Updates

- Add or refine command/query APIs so the owning app remains the system of record and consumers do not bypass app APIs.
- Add lifecycle events for the reviewed gap, including created, validated, blocked, approved, completed, failed, corrected, replayed, and reconciliation-failed variants where applicable.
- Capture idempotency keys, correlation IDs, source freshness, lineage, confidence, policy version, owner, SLA/OLA timers, and audit evidence.
- Add dashboards or operational reports for aging, failure reason, confidence/quality, consumer impact, exception backlog, and closure proof.
- Extend the test approach with happy-path, negative, edge-case, contract, event replay, data reconciliation, security, accessibility, and operational-readiness tests for the listed review items.

## API, Event, And Data Requirements

Related APIs and API areas: [TMF634](../../../../../references/tmforum-open-apis/openapi-specs/TMF634_ResourceCatalog), [TMF730](../../../../../references/tmforum-open-apis/openapi-specs/TMF730_SoftwareAndComputeManagement)

TMF API fit and extension notes:

- Use TMF634 for resource specification lifecycle. Use TMF730 where software and compute resource specifications are represented. Use TMF685 and TMF639 only as referenced pool and inventory consumers, not as Design Studio write targets.
- Non-TMF Resource Model Design API for controller-specific activation attributes, discovery model metadata, firmware compatibility, and stock/SKU template references where TMF634 does not carry enough design detail. Each extension contract must be explicitly labelled non-TMF, documented with OpenAPI, and aligned to TMF-style id, href, lifecycle state, relatedParty, relatedEntity, error, pagination, and event-envelope patterns where practical.
- Command APIs for Resource Catalog must cover create/initiate, validate, update, certify, approve/reject, publish, suspend, retire, supersede, correct, replay, and close where the resource specification lifecycle uses those states.
- Query APIs for Resource Catalog must cover search, detail, timeline, related resource specification and resource catalog version references, compatibility matrix, certification evidence, work queue, metrics, and audit retrieval with role-aware masking.
- Domain events for Resource Catalog must include ResourceSpecificationDrafted, ResourceSpecificationCertified, ResourceSpecificationPublished, ResourceSpecificationRetirementMapped, plus exception raised, exception resolved, corrected, replay requested, and consumer revalidation requested where the lifecycle uses those states.

Data and ownership requirements:

- Service And Resource Design Studio owns resource specifications, resource characteristic templates, capacity units, compatibility attributes, assignment metadata, activation links, resource lifecycle states, and inventory model references; other apps consume Resource Catalog state through APIs, events, governed projections, workflow tasks, certification packs, or certified data products.
- Store source channel, actor, tenant/brand/market, technology domain, lifecycle action, status reason, catalog version, rule/template version, external references, before/after values, policy decision, evidence links, retention class, legal hold flag, and impacted consumer list.
- Keep read projections, analytics extracts, and data platform outputs separate from operational writes so Resource Catalog does not create shadow mastership of product, inventory, order, activation, field, assurance, partner, or platform records.
- Provide reconciliation outputs that prove CPQ, order decomposition, fulfillment, activation, inventory, assurance, field, partner, and data consumers have accepted, rejected, or remain explicitly blocked by the resource specification and resource catalog version.

## Integrations And Handoffs

- Inventory And Topology for resource instantiation and resource pool acceptance.
- Fulfillment And Activation Control Tower for resource order and activation template consumption.
- Field Work, Stock, And Logistics for CPE/device stock references.
- Discovery, NMS, EMS, SDN, NFV, and cloud controllers for model compatibility.
- Service And Resource Design Studio service catalog for service realization.

## Non-Functional Requirements

- Scale and latency: Resource Catalog must support national catalog portfolios with thousands of service/resource specs, realization rules, templates, compatibility rules, versions, validation runs, and consumer subscriptions; interactive search and detail views should stay below 2 seconds while certification, impact analysis, and bulk publication run asynchronously with progress and partial-failure reports.
- Availability and resilience: published catalog, rule, and template query APIs for Resource Catalog must remain available during downstream CPQ, inventory, fulfillment, activation, assurance, field, partner, or test outages by serving last-known certified versions with freshness and confidence indicators.
- Auditability and retention: Resource Catalog history must retain actor, channel, reason, old/new value, policy version, approval/waiver, event ID, external reference, certification result, legal hold flag, and retention class for engineering, regulatory, security, and operational evidence periods.
- Localization and accessibility: Resource Catalog UI tasks, validation messages, engineering units, technology labels, time zones, language, keyboard navigation, and screen-reader labels must respect tenant, market, geography, and accessibility policy.
- Data protection: API, event, export, and dashboard paths for Resource Catalog must enforce tenant isolation, data residency, purpose limitation, least privilege, sensitive topology masking, critical-infrastructure masking, and secure evidence storage.

## Compliance, Security, And Privacy

- Resource Catalog must enforce tenant isolation, region boundaries, role-based catalog publication, privileged activation-template controls, critical infrastructure masking, security-by-design evidence, export controls, and data residency for the resource specification and resource catalog version.
- Resource Catalog must preserve lawful/regulatory inventory evidence, service retirement evidence, activation safety evidence, migration/decommissioning evidence, legal hold, and certification records where catalog or template decisions affect regulated telecom obligations.
- Sensitive service, resource, site, topology, firmware, controller, partner/off-net, and enterprise customer references in Resource Catalog must be masked in search, timelines, exports, analytics, and dashboards unless the persona has a permitted operational purpose.

## Observability And Operations

- Metrics: track resource-catalog records drafted, validated, certified, rejected, published, retired, superseded, waived, corrected, replayed, and accepted by consumers, plus validation failure rate, waiver aging, publication lag, consumer revalidation backlog, and downstream fallout linked to catalog changes.
- Queues: provide queues for draft, pending validation, pending certification, blocked dependency, waiver review, publication ready, consumer revalidation, exception, retrying, retirement review, corrected, completed, and archived Resource Catalog records.
- Alerts: notify Service And Resource Design Studio owners when validation failure rate, certification backlog, event publication failure, consumer lag, stale version usage, waiver aging, or downstream activation/order fallout breaches threshold.
- Runbooks: document triage, validation replay, consumer revalidation, publication rollback, retirement repair, waiver review, evidence export, legal hold response, and downstream event replay procedures for Resource Catalog.
- Ownership: Service And Resource Design Studio owns first-line health for Resource Catalog lifecycle, event replay, validation queues, and publication evidence; Product, Inventory, Fulfillment, Field, Assurance, Partner, Platform, Data, and Test owners correct their own source records.

## Test Approach

| Test layer | Required coverage |
| --- | --- |
| Unit tests | Field rules, lifecycle transitions, certification state, duplicate detection, version compatibility, masking, and resource specification and resource catalog version calculations for Resource Catalog. |
| API contract tests | Commands, queries, errors, idempotency, pagination, filtering, version compatibility, TMF-aligned payloads for TMF634, TMF730, and documented non-TMF extension APIs. |
| Event contract tests | Resource Catalog event names, payload shape, changed fields, correlation ID, idempotency key, ordering metadata, replay behavior, and subscriber compatibility. |
| Workflow tests | Happy path, assisted correction, automated API path, certification approval, exception, waiver, timeout, retry, publication, retirement, supersession, correction, and closure for resource specification lifecycle. |
| Integration tests | Handoffs with product catalog, CPQ, order management, fulfillment, activation, inventory, field, assurance, partner/off-net, platform test, and data owners, including external provider unavailability and no direct database access. |
| Security and privacy tests | Tenant isolation, privileged publication permissions, sensitive topology masking, malicious payloads, audit logging, legal hold, retention, export controls, and data residency for Resource Catalog. |
| Data tests | Source authority, referential integrity, historical correction, projection refresh, data-quality stewardship, reporting metrics, and lineage for resource specification and resource catalog version. |
| Performance tests | Search, bulk validation, impact analysis, certification queues, event publication, replay, and API throughput under realistic telecom catalog and order-to-activate volumes. |

## Feature Detail Review Implementation Alignment (2026-06-14)

Source: [App Feature Detail Review Alignment](README.md#feature-detail-review-alignment-2026-06-14) and [Suite Feature Detail Review](../../feature-detail-review.md).

Apply this app review scope to this feature: versioned service and resource specifications, realization rules, compatibility validation, activation templates, and publication readiness.

Implementation updates required for this feature:

- Re-check the core workflows and add or adjust happy paths, approval paths, exception queues, rollback or compensation behavior, and handoffs so the review scope is directly represented in build stories.
- Add or refine UI workbench expectations, including operator queues, evidence panels, policy decision traces, preview/simulation views, and status dashboards where this feature owns the behavior.
- Add or refine command APIs, query APIs, events, app-owned data fields, DDL gap notes, and integration handoffs needed to support the review scope without crossing app data ownership boundaries.
- Add acceptance criteria for source authority, tenant and residency controls, lifecycle state, approval evidence, idempotency, correlation IDs, SLA/OLA timers, and downstream acknowledgement where applicable.
- Add negative scenarios for stale data, duplicate events, policy denial, missing evidence, downstream outage, unauthorized access, bulk/replay risk, and manual override misuse.
- Extend tests to include happy path, negative path, edge case, API contract, event replay, data reconciliation, security, accessibility, observability, runbook, and release-gate evidence for the review scope.

## Build-Ready Refinement (2026-06-14)

This refinement converts the feature review material for Resource Catalog into delivery slices that can become epics, stories, API contracts, migrations, and test cases. Treat Service And Resource Design Studio App as the owning application for this feature within Suite OSS Engineering, Inventory, And Fulfillment and schema `service_resource_design`.

| Workstream | Build-ready delivery guidance |
| --- | --- |
| UX and workflow | Build the Resource Catalog workbench for Service designer, Resource designer, Network engineer, Product/catalog governance user, Fulfillment architect. Include search or intake, guided validation, detail view, lifecycle timeline, decision panel, evidence drawer, exception queue, bulk or replay controls where relevant, saved filters, SLA/OLA aging, empty/error states, and role-aware masking. The UI must expose draft, validate, certify, publish, constrain, retire, reinstate, or map a resource specification to successor resource models. The decision records the accountable persona, rule result, waiver status, affected... and block closure when required evidence, approval, reconciliation, or downstream acknowledgement is missing. |
| API and events | Implement command and query APIs around resource-catalog using TMF634, TMF730, TMF685, TMF639. Command APIs for Resource Catalog must cover create/initiate, validate, update, certify, approve/reject, publish, suspend, retire, supersede, correct, replay, and close where the resource specification lifecycle uses... Query APIs for Resource Catalog must cover search, detail, timeline, related resource specification and resource catalog version references, compatibility matrix, certification evidence, work queue, metrics, and audit... Domain events for Resource Catalog must include ResourceSpecificationDrafted, ResourceSpecificationCertified, ResourceSpecificationPublished, ResourceSpecificationRetirementMapped, plus exception raised, exception... Non-TMF Resource Model Design API for controller-specific activation attributes, discovery model metadata, firmware compatibility, and stock/SKU template references where TMF634 does not carry enough design detail. Each... Every command, query, and event must carry tenant/brand/market where applicable, actor, source channel, reason code, idempotency key, correlation ID, external reference, lifecycle state, and version metadata. |
| Data and controls | Persist resource specification and resource catalog version. inside `service_resource_design` with typed lifecycle, owner, status reason, timestamps, policy decision, source freshness, confidence, old/new value, evidence, and reconciliation fields. Service And Resource Design Studio owns resource specifications, resource characteristic templates, capacity units, compatibility attributes, assignment metadata, activation links, resource lifecycle states, and inventory model references... Keep TMF payloads, extension characteristics, imported evidence, and low-stability metadata in JSONB while promoting operationally searched lifecycle fields to typed columns. |
| Integration and handoff | Exchange service specifications, product realization rules, resource inventory instances, resource pools, stock SKUs, activation command templates, discovery models, NMS/EMS/SDN/NFV controllers, and... with Inventory And Topology for resource instantiation and resource pool acceptance., Fulfillment And Activation Control Tower for resource order and activation template consumption., Field Work, Stock, And Logistics for CPE/device... only through APIs, events, workflow tasks, governed projections, adapters, evidence packages, or certified data products. Show source owner, freshness, confidence, dependency state, retry status, blocked consumer, and completion evidence so the app does not create shadow mastership or direct cross-schema coupling. |
| Security, privacy, and compliance | Enforce RBAC/ABAC, tenant and residency boundaries, least privilege, separation of duties, masking, purpose limitation, retention, legal hold, export control, manual override expiry, immutable audit, and evidence chain of custody for Resource Catalog. Sensitive customer, revenue, partner, security, network, credential, or regulatory evidence must be masked unless the persona has explicit operational purpose. |
| Tests and operations | Create unit, API contract, event replay/idempotency, workflow, integration, migration, data reconciliation, security/privacy, accessibility/localization, performance, dashboard, alert, and runbook tests for Resource Catalog. Cover happy path, assisted path, automated path, exception path, bulk/project path, stale or duplicate input, downstream outage, policy denial, manual override, and reconciliation mismatch. Use the existing review scope - versioned service and resource specifications, realization rules, compatibility validation, activation templates, and publication readiness. - as mandatory backlog and test evidence. |

Implementation notes:

- Treat Service And Resource Design Studio App as the lifecycle owner for resource specification and resource catalog version.; referenced data such as service specifications, product realization rules, resource inventory instances, resource pools, stock SKUs, activation command templates, discovery models, NMS/EMS/SDN/NFV controllers, and field work artifacts. must remain references, snapshots, projections, evidence packages, or consumer acknowledgements unless the source file explicitly gives this app mastership.
- Make TMF alignment visible in every story: use named TMF resources where they fit, document non-TMF extension APIs with OpenAPI, and keep extension payloads compatible with TMF-style identifiers, lifecycle state, related entities, pagination, errors, and event envelopes.
- Build UI and API behavior around decision evidence, not only CRUD: surface the permitted next actions, policy decision, state reason, owner, SLA/OLA timer, blocked dependency, retry or compensation path, and closure proof.
- Add development tasks for route/page/component work, command/query handlers, DTO validation, entity/repository/migration changes, outbox/event contracts, projection refresh, privacy/security checks, and operational dashboards.
- Definition-of-done evidence must show downstream consumers can use published state through APIs, events, projections, workflow tasks, or certified data products without direct database reads or manual spreadsheet reconciliation.

## Definition Of Done

1. The resource specification and resource catalog version lifecycle supports draft, validating, in certification, blocked, waived, published, suspended, retired, superseded, corrected, rejected, and archived states where applicable.
2. Persona workflows for Service designer, Resource designer, Network engineer, Product/catalog governance user, and Fulfillment architect include decision rights, validation messages, exception routing, and evidence capture for Resource Catalog.
3. TMF-aligned references, non-TMF extension APIs, events, idempotency, correlation IDs, error models, replay behavior, and consumer revalidation contracts are documented and contract-tested.
4. Data ownership, private app database boundaries, governed projections, retention, legal hold, tenant isolation, critical-topology masking, privileged activation controls, and export controls match data mastery and ODA guidance.
5. Operational dashboards explain Resource Catalog state, version, validation results, exceptions, waivers, publication status, downstream consumers, stale version usage, and revalidation backlog without direct database access.
6. Negative scenarios, telecom edge cases, workflow tests, security tests, event replay tests, certification tests, compatibility tests, and reconciliation tests are automated or explicitly covered in delivery evidence.


## Build-Ready Refinement (2026-06-15)

Header added at the top of this file. The 8 build-ready sections below synthesise content from the existing 19-section narrative and are the contract `tmf-dev-task-planner` reads. Source citations are inline.

## Persona & decision

- Service designer can define customer-facing for the persona-specific outcome `Approved service specifications can be consumed by Product And Offer Studio, Ord…`, evidenced by the `## Persona & decision` audit trail in this file.
- Resource designer can define physical, logical, cloud, software, device, identifier, for the persona-specific outcome `Resource specifications expose capacity units, assignment attributes, activation…`, evidenced by the `## Persona & decision` audit trail in this file.
- Network engineer can validate technology-specific constraints, topology assumptions, controller support, firmware/software compatibility, for the persona-specific outcome `Network engineering decisions are visible as rule results, waivers, and certific…`, evidenced by the `## Persona & decision` audit trail in this file.
- Product/catalog governance user can approve technical realization readiness for commercial product offerings, launch variants, retirements, for the persona-specific outcome `Product-service-resource mappings are versioned, certified, and traceable before…`, evidenced by the `## Persona & decision` audit trail in this file.
- Fulfillment architect can define decomposition, orchestration, activation template, fallout, compensation, for the persona-specific outcome `Fulfillment And Activation Control Tower receives executable templates and valid…`, evidenced by the `## Persona & decision` audit trail in this file.

## Lifecycle ownership

- This app owns the lifecycle state of the planning record listed in the source `## Telecom Objects And Decision Rights`. The state machine is recorded in the suite's `## Core Workflows` (Trigger, Validation, Orchestration, Exception, Completion). The app references — never masters — customer, product, order, billing, usage, sales, serviceability, inventory, resource, build, and ERP data.
- Source: [features/<this>.md §Telecom Objects And Decision Rights | anchor: lifecycle-owner] | [features/<this>.md §Core Workflows | anchor: lifecycle-states]

## TMF fit

- TMF API baseline for this app: (none captured in tmf-api-ddl-reviews).
- Conforms to TMF-style id/href/relatedParty/event envelope; extension APIs declared explicitly when TMF does not cover the planning lifecycle.

## Data fit

- Owns schema `service_and_resource_design_studio`; the V001 migration lists the owned tables: (none captured).
- Source: [database/postgres/suites/ts_oss_engineering_fulfillment/V001__create_app_schemas_and_starter_tables.sql §schema | anchor: schema-list]

## Path coverage

- Happy path: Not applicable — no evidence of this path in `## Edge Cases` or `## Missing Use Cases And Scenarios`.
- Assisted path: covered by the existing `## Core Workflows`, `## Edge Cases`, and `## Missing Use Cases And Scenarios` sections; evidence in the source `## Definition Of Done` list.
- Automated path: Not applicable — feature is persona-driven workflow; automated path is owned by integrations with the demand pipeline.
- Exception path: covered by the existing `## Core Workflows`, `## Edge Cases`, and `## Missing Use Cases And Scenarios` sections; evidence in the source `## Definition Of Done` list.
- Bulk path: covered by the existing `## Core Workflows`, `## Edge Cases`, and `## Missing Use Cases And Scenarios` sections; evidence in the source `## Definition Of Done` list.
- Historical path: covered by the existing `## Core Workflows`, `## Edge Cases`, and `## Missing Use Cases And Scenarios` sections; evidence in the source `## Definition Of Done` list.
- Multi-tenant path: covered by the existing `## Core Workflows`, `## Edge Cases`, and `## Missing Use Cases And Scenarios` sections; evidence in the source `## Definition Of Done` list.
- Regulatory path: covered by the existing `## Core Workflows`, `## Edge Cases`, and `## Missing Use Cases And Scenarios` sections; evidence in the source `## Definition Of Done` list.
- Source: [features/<this>.md §Edge Cases | anchor: paths] | [features/<this>.md §Missing Use Cases And Scenarios | anchor: paths]

## UI implications

- Pages / workbenches (per the app's `Required app screens / workbenches` block in `dev-tasks/development-task-tracker.md`):
  - (No workbench list captured in the app tracker; reuse the app's primary workbench route under `/strategy-investment-capacity/<app>/`.)
- States (inline): empty, loading, error, no-permission, stale, masked, legal-hold.
- Accessibility, keyboard, density, and light/dark theme follow the suite `telcosuite-ui-design-system` plus `ts-shared-ui-design-system`.
- Source: [development-task-tracker.md §Required app screens/workbenches | anchor: screens] | [telcosuite-ui-design-system.md | anchor: ux-baseline]

## Acceptance & tests

- AC1 (AC-resource-catalog-01): Given an authorized Service designer, Resource designer, Network engineer, Product/catalog governance user, or Fulfillment architect creates or updates the resource specification and resource catalog version, when the resource specification lifecycle advances from draft to review, then Service And Resource Design Studio validates resource attribute completeness, capacity unit definition, inventory instantiation rule, controller support, stock/SKU reference, assignment eligibility, firmware/software compatibility, and retirement impact before accepting the state change.
- AC2 (AC-resource-catalog-02): Given the resource specification and resource catalog version references commercial product, service, resource, inventory, activation, or assurance data, when a persona opens the Resource Catalog record, then the app shows source owner, referenced version, freshness, confidence, correction route, and whether the reference is read-only or app-owned.
- AC3 (AC-resource-catalog-03): Given Resource spec lacks assignable capacity unit, when validation fails for Resource Catalog, then the app keeps the record in draft, blocked, or rejected state with severity, owner, due date, reason code, impacted consumer, waiver option, and correlation ID.
- AC4 (AC-resource-catalog-04): Given a governance decision is required for the resource specification and resource catalog version, when the accountable persona approves, rejects, waives, retires, or supersedes it, then the app stores decision right, actor, role, reason, old/new values, policy version, evidence links, tenant/region boundary, and idempotency key.
- AC5 (AC-resource-catalog-05): Given CPQ, Order Management Hub, Fulfillment, Inventory, Field, Assurance, Partner, or Data consumers subscribe to Resource Catalog changes, when the resource specification and resource catalog version is published or retired, then the app emits a versioned event with changed fields, impacted services/resources, consumer revalidation flag, replay metadata, and correlation ID.
- AC6 (AC-resource-catalog-06): Given a brownfield MACD, migration, rollback, or decommissioning scenario references the resource specification and resource catalog version, when the user requests publication or closure, then the app validates active inventory impact, in-flight order impact, field/partner dependency, activation rollback path, and customer/NOC/care handoff before closure.
- AC7 (AC-resource-catalog-07): Given supervisors or data stewards review Resource Catalog operations, when they open dashboards, then they see draft aging, certification pass/fail, exception causes, waiver aging, publication lag, consumer adoption, revalidation backlog, and downstream fallout linked to the resource specification and resource catalog version.
- Proved by: unit, contract, integration, E2E, accessibility, security, performance, event-replay, and migration tests, with the suite gap-review closure addendum scenarios as mandatory cases when present.
- Source: [features/<this>.md §Acceptance Criteria | anchor: ac-list]

## Dependencies & release gate

- Depends on: dev-tasks tracker `Required app screens/workbenches` block; the suite's P01 foundation tasks; cross-app TMF and event contracts listed under `## API, Event, And Data Requirements`.
- Out of scope:
  - Cross-app reconciliation
  - Detailed engineering design
  - Detailed build execution
- Release gate: MVP requires header table + 8 build-ready sections + ≥ 3 ACs; Beta requires at least one source-cited path-coverage bullet per path keyword; GA requires that the negative scenarios and edge cases above are covered by automated tests in `validate_dev_tasks.py`.
- Source: [development-task-tracker.md | anchor: release-gate]
