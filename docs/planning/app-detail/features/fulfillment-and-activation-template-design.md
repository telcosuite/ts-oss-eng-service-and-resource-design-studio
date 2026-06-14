# Fulfillment And Activation Template Design Feature Specification

Reviewed: 2026-06-07

Suite: OSS Engineering, Inventory, And Fulfillment

App: [Service And Resource Design Studio App](../README.md)

Source module detail: [Modules And Features](../modules-and-features.md)

Source gap review: [E2E Feature Gap Assessment](../../../e2e-feature-gap-assessment.md)

Feature area slug: `fulfillment-and-activation-template-design`

E2E gap severity: High E2E gap closure

## Feature Intent

Design decomposition templates, service order templates, resource order templates, activation command templates, configuration profiles, validation rules, compensation steps, and test handoffs that Fulfillment And Activation Control Tower can execute safely. The Fulfillment And Activation Template Design feature produces a governed fulfillment and activation template definition outcome with versioned evidence, consumer readiness, and explicit ODA boundaries instead of spreadsheet-driven catalog or activation interpretation.

## Telecom Objects And Decision Rights

- Master entity: fulfillment and activation template definition. Service And Resource Design Studio owns decomposition templates, activation command templates, configuration profiles, validation rules, rollback/compensation rules, catalog-to-fulfillment certification evidence, lifecycle states, and publication events.
- Referenced entities: service specs, resource specs, realization rules, product configuration models, service orders, resource orders, activation systems, inventory reservation/assignment rules, service tests, network controller capabilities, and partner/off-net templates. Service And Resource Design Studio consumes these through APIs, events, governed projections, or certification packs and does not overwrite their operational masters.
- Primary decisions: certify, publish, reject, suspend, retire, or supersede a fulfillment or activation template for a service/resource specification and lifecycle action. The decision records the accountable persona, rule result, waiver status, affected product/service/resource versions, consumer impact, and downstream handoff.
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
| Trigger | Fulfillment And Activation Template Design starts from new realization rule, activation fallout, controller onboarding, product launch certification, MACD path design, rollback defect, or test-and-turn-up readiness requirement. | The fulfillment and activation template definition opens with owner, tenant, market, technology scope, source trigger, lifecycle action, correlation ID, impacted consumer list, and required catalog/version references. |
| Validation | The app validates template parameter completeness, catalog version compatibility, controller capability, idempotency support, rollback command availability, inventory update rule, service test handoff, and fallout queue owner. | Invalid fulfillment and activation template definition data creates rule failures, certification exceptions, waiver tasks, or publication rejection before CPQ, order decomposition, fulfillment, activation, inventory, or assurance can consume the change. |
| Orchestration | Service And Resource Design Studio coordinates catalog, design, inventory, fulfillment, activation, field, assurance, partner, test, and data consumers through APIs, events, workflow tasks, governed projections, or certification packs. | Consumers receive versioned technical catalog outputs while their own databases and lifecycle records remain private to their owning apps. |
| Exception | If Template omits mandatory controller parameter, Rollback command cannot restore prior configuration, Activation response cannot map to inventory update blocks the lifecycle, the workflow routes to the accountable service design, resource design, network engineering, catalog governance, fulfillment architecture, data stewardship, or security/compliance owner. | The exception captures failed rule, affected service/resource/product, risk, waiver authority, blocked consumer, correlation ID, evidence gap, and escalation path. |
| Completion | Completion occurs when the fulfillment and activation template definition is certified, published, rejected, retired, superseded, or mapped with downstream consumer acknowledgement. | Completion evidence includes catalog version, rule version, template version where relevant, validation result, approval/waiver record, impacted inventory or order scope, event IDs, and consumer revalidation status. |

## Missing Use Cases And Scenarios

| Scenario | Required behavior |
| --- | --- |
| Greenfield build or launch | Fulfillment And Activation Template Design must support zero-touch broadband activation template for ONT and speed profile with explicit fulfillment and activation template definition, version, validation result, decision owner, evidence, and downstream handoff. |
| Brownfield MACD | Fulfillment And Activation Template Design must support manual fallout path for missing VLAN or IP parameter with explicit fulfillment and activation template definition, version, validation result, decision owner, evidence, and downstream handoff. |
| Enterprise bulk or migration | Fulfillment And Activation Template Design must support rollback template for failed SDN service activation with explicit fulfillment and activation template definition, version, validation result, decision owner, evidence, and downstream handoff. |
| Partner/off-net or external dependency | Fulfillment And Activation Template Design must support partner/off-net handoff template with evidence requirement with explicit fulfillment and activation template definition, version, validation result, decision owner, evidence, and downstream handoff. |
| Retirement, rollback, or decommissioning | Fulfillment And Activation Template Design must support bulk enterprise VPN activation template with site-level sequencing with explicit fulfillment and activation template definition, version, validation result, decision owner, evidence, and downstream handoff. |

## Capability Slices

| Feature ID | Feature | Parent feature area | Priority guidance |
| --- | --- | --- | --- |
| F-fulfillment-and-activation-template-design-01 | Service decomposition template | Fulfillment And Activation Template Design | P1: required to make activation template lifecycle usable for product launch, order-to-activate, inventory handoff, assurance readiness, or governed retirement. |
| F-fulfillment-and-activation-template-design-02 | Resource order template | Fulfillment And Activation Template Design | P1: required to make activation template lifecycle usable for product launch, order-to-activate, inventory handoff, assurance readiness, or governed retirement. |
| F-fulfillment-and-activation-template-design-03 | Activation command template | Fulfillment And Activation Template Design | P1: required to make activation template lifecycle usable for product launch, order-to-activate, inventory handoff, assurance readiness, or governed retirement. |
| F-fulfillment-and-activation-template-design-04 | Configuration profile | Fulfillment And Activation Template Design | P1: required to make activation template lifecycle usable for product launch, order-to-activate, inventory handoff, assurance readiness, or governed retirement. |
| F-fulfillment-and-activation-template-design-05 | Validation and rollback rule | Fulfillment And Activation Template Design | P2: required to make activation template lifecycle usable for product launch, order-to-activate, inventory handoff, assurance readiness, or governed retirement. |
| F-fulfillment-and-activation-template-design-06 | Catalog-to-fulfillment certification | Fulfillment And Activation Template Design | P2: required to make activation template lifecycle usable for product launch, order-to-activate, inventory handoff, assurance readiness, or governed retirement. |
| F-fulfillment-and-activation-template-design-07 | Service test handoff rule | Fulfillment And Activation Template Design | P2: required to make activation template lifecycle usable for product launch, order-to-activate, inventory handoff, assurance readiness, or governed retirement. |

## Acceptance Criteria

1. **AC-fulfillment-and-activation-template-design-01:** Given an authorized Service designer, Resource designer, Network engineer, Product/catalog governance user, or Fulfillment architect creates or updates the fulfillment and activation template definition, when the activation template lifecycle advances from draft to review, then Service And Resource Design Studio validates template parameter completeness, catalog version compatibility, controller capability, idempotency support, rollback command availability, inventory update rule, service test handoff, and fallout queue owner before accepting the state change.
2. **AC-fulfillment-and-activation-template-design-02:** Given the fulfillment and activation template definition references commercial product, service, resource, inventory, activation, or assurance data, when a persona opens the Fulfillment And Activation Template Design record, then the app shows source owner, referenced version, freshness, confidence, correction route, and whether the reference is read-only or app-owned.
3. **AC-fulfillment-and-activation-template-design-03:** Given Template omits mandatory controller parameter, when validation fails for Fulfillment And Activation Template Design, then the app keeps the record in draft, blocked, or rejected state with severity, owner, due date, reason code, impacted consumer, waiver option, and correlation ID.
4. **AC-fulfillment-and-activation-template-design-04:** Given a governance decision is required for the fulfillment and activation template definition, when the accountable persona approves, rejects, waives, retires, or supersedes it, then the app stores decision right, actor, role, reason, old/new values, policy version, evidence links, tenant/region boundary, and idempotency key.
5. **AC-fulfillment-and-activation-template-design-05:** Given CPQ, Order Management Hub, Fulfillment, Inventory, Field, Assurance, Partner, or Data consumers subscribe to Fulfillment And Activation Template Design changes, when the fulfillment and activation template definition is published or retired, then the app emits a versioned event with changed fields, impacted services/resources, consumer revalidation flag, replay metadata, and correlation ID.
6. **AC-fulfillment-and-activation-template-design-06:** Given a brownfield MACD, migration, rollback, or decommissioning scenario references the fulfillment and activation template definition, when the user requests publication or closure, then the app validates active inventory impact, in-flight order impact, field/partner dependency, activation rollback path, and customer/NOC/care handoff before closure.
7. **AC-fulfillment-and-activation-template-design-07:** Given supervisors or data stewards review Fulfillment And Activation Template Design operations, when they open dashboards, then they see draft aging, certification pass/fail, exception causes, waiver aging, publication lag, consumer adoption, revalidation backlog, and downstream fallout linked to the fulfillment and activation template definition.

## Negative Scenarios

Negative scenarios for this feature include permission denial, missing source data, stale dependency state, policy failure, duplicate or replayed request, downstream timeout, reconciliation mismatch, and any feature-specific negative scenario additions listed in the suite gap-review closure addendum.

## Edge Cases

| Scenario | Expected behavior |
| --- | --- |
| Template omits mandatory controller parameter | Fulfillment And Activation Template Design blocks unsafe publication or routes a governed exception with owner, due date, affected product/service/resource, consumer impact, waiver authority, and replayable evidence. |
| Rollback command cannot restore prior configuration | Fulfillment And Activation Template Design blocks unsafe publication or routes a governed exception with owner, due date, affected product/service/resource, consumer impact, waiver authority, and replayable evidence. |
| Activation response cannot map to inventory update | Fulfillment And Activation Template Design blocks unsafe publication or routes a governed exception with owner, due date, affected product/service/resource, consumer impact, waiver authority, and replayable evidence. |
| Template certified against stale service spec version | Fulfillment And Activation Template Design blocks unsafe publication or routes a governed exception with owner, due date, affected product/service/resource, consumer impact, waiver authority, and replayable evidence. |
| Zero-touch path lacks manual fallout owner | Fulfillment And Activation Template Design blocks unsafe publication or routes a governed exception with owner, due date, affected product/service/resource, consumer impact, waiver authority, and replayable evidence. |
| Duplicate, stale, or out-of-order publication request | Fulfillment And Activation Template Design uses optimistic locking, event version, source timestamp, and idempotency key so retries cannot publish duplicate catalog, template, rule, or certification state. |
| Cross-tenant, cross-region, or restricted topology access | Fulfillment And Activation Template Design blocks mutation, masks restricted service/resource/topology data, and records policy decision metadata for tenant isolation, data residency, and export control. |
| Downstream consumer unavailable | Fulfillment And Activation Template Design either fails fast for synchronous certification gates or queues a controlled retry, replay, or consumer revalidation task with owner, due date, backoff policy, and correlation ID. |
| Legal hold or regulatory retention conflict | Fulfillment And Activation Template Design prevents deletion or destructive retirement of catalog, rule, template, or certification evidence until legal hold, retention, and regulatory inventory evidence controls allow it. |

## Suite Gap Review Closure Addendum

Source review: [03 Oss Engineering Inventory Fulfillment Gap Review](../../../../suite-gap-reviews/03-oss-engineering-inventory-fulfillment-gap-review.md)

This addendum applies the suite gap-review findings tied to this feature file. It supplements the baseline feature specification and should be carried into epic, story, API, event, data, and test refinement.

### Review Backlog Items Addressed

| Severity | Gap-review item | Closure expectation |
| --- | --- | --- |
| Critical | Cross-domain catalog and activation-template certification harness. | Add concrete happy path, negative path, edge-case, API/event/data control, reporting, and test evidence for this feature area. |
| Medium | Activation template safety profile with rollback and idempotency metadata. | Add concrete happy path, negative path, edge-case, API/event/data control, reporting, and test evidence for this feature area. |

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

Related APIs and API areas: [TMF633](../../../../../references/tmforum-open-apis/openapi-specs/TMF633_ServiceCatalog), [TMF634](../../../../../references/tmforum-open-apis/openapi-specs/TMF634_ResourceCatalog), [TMF641](../../../../../references/tmforum-open-apis/openapi-specs/TMF641_ServiceOrder), [TMF652](../../../../../references/tmforum-open-apis/openapi-specs/TMF652_ResourceOrderManagement), [TMF640](../../../../../references/tmforum-open-apis/openapi-specs/TMF640_ActivationConfiguration), [TMF664](../../../../../references/tmforum-open-apis/openapi-specs/TMF664_ResourceFunctionActivationConfiguration), [TMF760](../../../../../references/tmforum-open-apis/openapi-specs/TMF760_ProductConfigurationManagement)

TMF API fit and extension notes:

- Use TMF633 and TMF634 for service/resource specification references, TMF641 and TMF652 for downstream service/resource order consumers, TMF640 and TMF664 for activation/configuration patterns, and TMF760 for product configuration references. Template authoring and certification remains an app-owned design capability.
- Non-TMF Activation Template Design API for parameter schemas, command safety rules, rollback/compensation scripts, dry-run profiles, and catalog-to-fulfillment certification packs. Each extension contract must be explicitly labelled non-TMF, documented with OpenAPI, and aligned to TMF-style id, href, lifecycle state, relatedParty, relatedEntity, error, pagination, and event-envelope patterns where practical.
- Command APIs for Fulfillment And Activation Template Design must cover create/initiate, validate, update, certify, approve/reject, publish, suspend, retire, supersede, correct, replay, and close where the activation template lifecycle uses those states.
- Query APIs for Fulfillment And Activation Template Design must cover search, detail, timeline, related fulfillment and activation template definition references, compatibility matrix, certification evidence, work queue, metrics, and audit retrieval with role-aware masking.
- Domain events for Fulfillment And Activation Template Design must include ActivationTemplateDrafted, ActivationTemplateCertified, ActivationTemplatePublished, ActivationTemplateSuspended, plus exception raised, exception resolved, corrected, replay requested, and consumer revalidation requested where the lifecycle uses those states.

Data and ownership requirements:

- Service And Resource Design Studio owns decomposition templates, activation command templates, configuration profiles, validation rules, rollback/compensation rules, catalog-to-fulfillment certification evidence, lifecycle states, and publication events; other apps consume Fulfillment And Activation Template Design state through APIs, events, governed projections, workflow tasks, certification packs, or certified data products.
- Store source channel, actor, tenant/brand/market, technology domain, lifecycle action, status reason, catalog version, rule/template version, external references, before/after values, policy decision, evidence links, retention class, legal hold flag, and impacted consumer list.
- Keep read projections, analytics extracts, and data platform outputs separate from operational writes so Fulfillment And Activation Template Design does not create shadow mastership of product, inventory, order, activation, field, assurance, partner, or platform records.
- Provide reconciliation outputs that prove CPQ, order decomposition, fulfillment, activation, inventory, assurance, field, partner, and data consumers have accepted, rejected, or remain explicitly blocked by the fulfillment and activation template definition.

## Integrations And Handoffs

- Fulfillment And Activation Control Tower for executable template consumption.
- Inventory And Topology for reservation, assignment, and inventory update rules.
- Service Test and NOC/Assurance for test-and-turn-up handoff.
- Network controllers, SDN/NFV, EMS, NMS, and cloud managers for capability validation.
- Order Management Hub for decomposition readiness.

## Non-Functional Requirements

- Scale and latency: Fulfillment And Activation Template Design must support national catalog portfolios with thousands of service/resource specs, realization rules, templates, compatibility rules, versions, validation runs, and consumer subscriptions; interactive search and detail views should stay below 2 seconds while certification, impact analysis, and bulk publication run asynchronously with progress and partial-failure reports.
- Availability and resilience: published catalog, rule, and template query APIs for Fulfillment And Activation Template Design must remain available during downstream CPQ, inventory, fulfillment, activation, assurance, field, partner, or test outages by serving last-known certified versions with freshness and confidence indicators.
- Auditability and retention: Fulfillment And Activation Template Design history must retain actor, channel, reason, old/new value, policy version, approval/waiver, event ID, external reference, certification result, legal hold flag, and retention class for engineering, regulatory, security, and operational evidence periods.
- Localization and accessibility: Fulfillment And Activation Template Design UI tasks, validation messages, engineering units, technology labels, time zones, language, keyboard navigation, and screen-reader labels must respect tenant, market, geography, and accessibility policy.
- Data protection: API, event, export, and dashboard paths for Fulfillment And Activation Template Design must enforce tenant isolation, data residency, purpose limitation, least privilege, sensitive topology masking, critical-infrastructure masking, and secure evidence storage.

## Compliance, Security, And Privacy

- Fulfillment And Activation Template Design must enforce tenant isolation, region boundaries, role-based catalog publication, privileged activation-template controls, critical infrastructure masking, security-by-design evidence, export controls, and data residency for the fulfillment and activation template definition.
- Fulfillment And Activation Template Design must preserve lawful/regulatory inventory evidence, service retirement evidence, activation safety evidence, migration/decommissioning evidence, legal hold, and certification records where catalog or template decisions affect regulated telecom obligations.
- Sensitive service, resource, site, topology, firmware, controller, partner/off-net, and enterprise customer references in Fulfillment And Activation Template Design must be masked in search, timelines, exports, analytics, and dashboards unless the persona has a permitted operational purpose.

## Observability And Operations

- Metrics: track fulfillment-and-activation-template-design records drafted, validated, certified, rejected, published, retired, superseded, waived, corrected, replayed, and accepted by consumers, plus validation failure rate, waiver aging, publication lag, consumer revalidation backlog, and downstream fallout linked to catalog changes.
- Queues: provide queues for draft, pending validation, pending certification, blocked dependency, waiver review, publication ready, consumer revalidation, exception, retrying, retirement review, corrected, completed, and archived Fulfillment And Activation Template Design records.
- Alerts: notify Service And Resource Design Studio owners when validation failure rate, certification backlog, event publication failure, consumer lag, stale version usage, waiver aging, or downstream activation/order fallout breaches threshold.
- Runbooks: document triage, validation replay, consumer revalidation, publication rollback, retirement repair, waiver review, evidence export, legal hold response, and downstream event replay procedures for Fulfillment And Activation Template Design.
- Ownership: Service And Resource Design Studio owns first-line health for Fulfillment And Activation Template Design lifecycle, event replay, validation queues, and publication evidence; Product, Inventory, Fulfillment, Field, Assurance, Partner, Platform, Data, and Test owners correct their own source records.

## Test Approach

| Test layer | Required coverage |
| --- | --- |
| Unit tests | Field rules, lifecycle transitions, certification state, duplicate detection, version compatibility, masking, and fulfillment and activation template definition calculations for Fulfillment And Activation Template Design. |
| API contract tests | Commands, queries, errors, idempotency, pagination, filtering, version compatibility, TMF-aligned payloads for TMF633, TMF634, TMF641, TMF652, TMF640, TMF664, TMF760, and documented non-TMF extension APIs. |
| Event contract tests | Fulfillment And Activation Template Design event names, payload shape, changed fields, correlation ID, idempotency key, ordering metadata, replay behavior, and subscriber compatibility. |
| Workflow tests | Happy path, assisted correction, automated API path, certification approval, exception, waiver, timeout, retry, publication, retirement, supersession, correction, and closure for activation template lifecycle. |
| Integration tests | Handoffs with product catalog, CPQ, order management, fulfillment, activation, inventory, field, assurance, partner/off-net, platform test, and data owners, including external provider unavailability and no direct database access. |
| Security and privacy tests | Tenant isolation, privileged publication permissions, sensitive topology masking, malicious payloads, audit logging, legal hold, retention, export controls, and data residency for Fulfillment And Activation Template Design. |
| Data tests | Source authority, referential integrity, historical correction, projection refresh, data-quality stewardship, reporting metrics, and lineage for fulfillment and activation template definition. |
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

This refinement converts the feature review material for Fulfillment And Activation Template Design into delivery slices that can become epics, stories, API contracts, migrations, and test cases. Treat Service And Resource Design Studio App as the owning application for this feature within Suite OSS Engineering, Inventory, And Fulfillment and schema `service_resource_design`.

| Workstream | Build-ready delivery guidance |
| --- | --- |
| UX and workflow | Build the Fulfillment And Activation Template Design workbench for Service designer, Resource designer, Network engineer, Product/catalog governance user, Fulfillment architect. Include search or intake, guided validation, detail view, lifecycle timeline, decision panel, evidence drawer, exception queue, bulk or replay controls where relevant, saved filters, SLA/OLA aging, empty/error states, and role-aware masking. The UI must expose certify, publish, reject, suspend, retire, or supersede a fulfillment or activation template for a service/resource specification and lifecycle action. The decision records the accountable persona, rule result, waiver... and block closure when required evidence, approval, reconciliation, or downstream acknowledgement is missing. |
| API and events | Implement command and query APIs around fulfillment-and-activation-template-design using TMF633, TMF634, TMF641, TMF652, TMF640, TMF664, TMF760. Command APIs for Fulfillment And Activation Template Design must cover create/initiate, validate, update, certify, approve/reject, publish, suspend, retire, supersede, correct, replay, and close where the activation... Query APIs for Fulfillment And Activation Template Design must cover search, detail, timeline, related fulfillment and activation template definition references, compatibility matrix, certification evidence, work queue... Domain events for Fulfillment And Activation Template Design must include ActivationTemplateDrafted, ActivationTemplateCertified, ActivationTemplatePublished, ActivationTemplateSuspended, plus exception raised... Non-TMF Activation Template Design API for parameter schemas, command safety rules, rollback/compensation scripts, dry-run profiles, and catalog-to-fulfillment certification packs. Each extension contract must be... Every command, query, and event must carry tenant/brand/market where applicable, actor, source channel, reason code, idempotency key, correlation ID, external reference, lifecycle state, and version metadata. |
| Data and controls | Persist fulfillment and activation template definition. inside `service_resource_design` with typed lifecycle, owner, status reason, timestamps, policy decision, source freshness, confidence, old/new value, evidence, and reconciliation fields. Service And Resource Design Studio owns decomposition templates, activation command templates, configuration profiles, validation rules, rollback/compensation rules, catalog-to-fulfillment certification evidence, lifecycle states, and... Keep TMF payloads, extension characteristics, imported evidence, and low-stability metadata in JSONB while promoting operationally searched lifecycle fields to typed columns. |
| Integration and handoff | Exchange service specs, resource specs, realization rules, product configuration models, service orders, resource orders, activation systems, inventory reservation/assignment rules, service tests... with Fulfillment And Activation Control Tower for executable template consumption., Inventory And Topology for reservation, assignment, and inventory update rules., Service Test and NOC/Assurance for test-and-turn-up handoff., Network... only through APIs, events, workflow tasks, governed projections, adapters, evidence packages, or certified data products. Show source owner, freshness, confidence, dependency state, retry status, blocked consumer, and completion evidence so the app does not create shadow mastership or direct cross-schema coupling. |
| Security, privacy, and compliance | Enforce RBAC/ABAC, tenant and residency boundaries, least privilege, separation of duties, masking, purpose limitation, retention, legal hold, export control, manual override expiry, immutable audit, and evidence chain of custody for Fulfillment And Activation Template Design. Sensitive customer, revenue, partner, security, network, credential, or regulatory evidence must be masked unless the persona has explicit operational purpose. |
| Tests and operations | Create unit, API contract, event replay/idempotency, workflow, integration, migration, data reconciliation, security/privacy, accessibility/localization, performance, dashboard, alert, and runbook tests for Fulfillment And Activation Template Design. Cover happy path, assisted path, automated path, exception path, bulk/project path, stale or duplicate input, downstream outage, policy denial, manual override, and reconciliation mismatch. Use the existing review scope - versioned service and resource specifications, realization rules, compatibility validation, activation templates, and publication readiness. - as mandatory backlog and test evidence. |

Implementation notes:

- Treat Service And Resource Design Studio App as the lifecycle owner for fulfillment and activation template definition.; referenced data such as service specs, resource specs, realization rules, product configuration models, service orders, resource orders, activation systems, inventory reservation/assignment rules, service tests, network controller... must remain references, snapshots, projections, evidence packages, or consumer acknowledgements unless the source file explicitly gives this app mastership.
- Make TMF alignment visible in every story: use named TMF resources where they fit, document non-TMF extension APIs with OpenAPI, and keep extension payloads compatible with TMF-style identifiers, lifecycle state, related entities, pagination, errors, and event envelopes.
- Build UI and API behavior around decision evidence, not only CRUD: surface the permitted next actions, policy decision, state reason, owner, SLA/OLA timer, blocked dependency, retry or compensation path, and closure proof.
- Add development tasks for route/page/component work, command/query handlers, DTO validation, entity/repository/migration changes, outbox/event contracts, projection refresh, privacy/security checks, and operational dashboards.
- Definition-of-done evidence must show downstream consumers can use published state through APIs, events, projections, workflow tasks, or certified data products without direct database reads or manual spreadsheet reconciliation.

## Definition Of Done

1. The fulfillment and activation template definition lifecycle supports draft, validating, in certification, blocked, waived, published, suspended, retired, superseded, corrected, rejected, and archived states where applicable.
2. Persona workflows for Service designer, Resource designer, Network engineer, Product/catalog governance user, and Fulfillment architect include decision rights, validation messages, exception routing, and evidence capture for Fulfillment And Activation Template Design.
3. TMF-aligned references, non-TMF extension APIs, events, idempotency, correlation IDs, error models, replay behavior, and consumer revalidation contracts are documented and contract-tested.
4. Data ownership, private app database boundaries, governed projections, retention, legal hold, tenant isolation, critical-topology masking, privileged activation controls, and export controls match data mastery and ODA guidance.
5. Operational dashboards explain Fulfillment And Activation Template Design state, version, validation results, exceptions, waivers, publication status, downstream consumers, stale version usage, and revalidation backlog without direct database access.
6. Negative scenarios, telecom edge cases, workflow tests, security tests, event replay tests, certification tests, compatibility tests, and reconciliation tests are automated or explicitly covered in delivery evidence.
