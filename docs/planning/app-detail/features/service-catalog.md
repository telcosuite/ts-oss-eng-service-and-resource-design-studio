# Service Catalog Feature Specification

Reviewed: 2026-06-07

Suite: OSS Engineering, Inventory, And Fulfillment

App: [Service And Resource Design Studio App](../README.md)

Source module detail: [Modules And Features](../modules-and-features.md)

Source gap review: [E2E Feature Gap Assessment](../../../e2e-feature-gap-assessment.md)

Feature area slug: `service-catalog`

E2E gap severity: Core

## Feature Intent

Manage customer-facing and resource-facing service specifications, service characteristics, relationships, dependencies, lifecycle states, versioning, product mapping, release, retirement, and compatibility so commercial offers can become orderable and supportable technical services. The Service Catalog feature produces a governed service specification and service catalog version outcome with versioned evidence, consumer readiness, and explicit ODA boundaries instead of spreadsheet-driven catalog or activation interpretation.

## Telecom Objects And Decision Rights

- Master entity: service specification and service catalog version. Service And Resource Design Studio owns customer-facing service specs, resource-facing service specs, service characteristics, service relationships, service lifecycle states, service compatibility notes, and service catalog publication evidence.
- Referenced entities: commercial product specifications, product offerings, geography/serviceability decisions, resource specifications, activation templates, service inventory instances, service tests, assurance rules, and order decomposition plans. Service And Resource Design Studio consumes these through APIs, events, governed projections, or certification packs and does not overwrite their operational masters.
- Primary decisions: draft, validate, certify, publish, suspend for correction, retire, reinstate, or map service specification versions to successor services. The decision records the accountable persona, rule result, waiver status, affected product/service/resource versions, consumer impact, and downstream handoff.
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
| Trigger | Service Catalog starts from new product launch, service redesign, MACD requirement, network build acceptance, assurance defect, service retirement, migration program, or catalog correction request. | The service specification and service catalog version opens with owner, tenant, market, technology scope, source trigger, lifecycle action, correlation ID, impacted consumer list, and required catalog/version references. |
| Validation | The app validates service characteristic completeness, CFS/RFS relationship validity, product mapping, resource realization, compatibility rule result, activation template reference, retirement impact, and assurance handoff readiness. | Invalid service specification and service catalog version data creates rule failures, certification exceptions, waiver tasks, or publication rejection before CPQ, order decomposition, fulfillment, activation, inventory, or assurance can consume the change. |
| Orchestration | Service And Resource Design Studio coordinates catalog, design, inventory, fulfillment, activation, field, assurance, partner, test, and data consumers through APIs, events, workflow tasks, governed projections, or certification packs. | Consumers receive versioned technical catalog outputs while their own databases and lifecycle records remain private to their owning apps. |
| Exception | If Missing RFS realization for a sellable product, Service characteristic conflicts with activation template parameter, Retired service spec still referenced by active service inventory blocks the lifecycle, the workflow routes to the accountable service design, resource design, network engineering, catalog governance, fulfillment architecture, data stewardship, or security/compliance owner. | The exception captures failed rule, affected service/resource/product, risk, waiver authority, blocked consumer, correlation ID, evidence gap, and escalation path. |
| Completion | Completion occurs when the service specification and service catalog version is certified, published, rejected, retired, superseded, or mapped with downstream consumer acknowledgement. | Completion evidence includes catalog version, rule version, template version where relevant, validation result, approval/waiver record, impacted inventory or order scope, event IDs, and consumer revalidation status. |

## Missing Use Cases And Scenarios

| Scenario | Required behavior |
| --- | --- |
| Greenfield build or launch | Service Catalog must support greenfield FTTH service spec launch with explicit service specification and service catalog version, version, validation result, decision owner, evidence, and downstream handoff. |
| Brownfield MACD | Service Catalog must support brownfield enterprise VPN change to add QoS tier with explicit service specification and service catalog version, version, validation result, decision owner, evidence, and downstream handoff. |
| Enterprise bulk or migration | Service Catalog must support bulk migration from legacy voice service to fiber voice profile with explicit service specification and service catalog version, version, validation result, decision owner, evidence, and downstream handoff. |
| Partner/off-net or external dependency | Service Catalog must support partner access service represented as an off-net service spec with explicit service specification and service catalog version, version, validation result, decision owner, evidence, and downstream handoff. |
| Retirement, rollback, or decommissioning | Service Catalog must support service retirement where installed inventory still references the old spec with explicit service specification and service catalog version, version, validation result, decision owner, evidence, and downstream handoff. |

## Capability Slices

| Feature ID | Feature | Parent feature area | Priority guidance |
| --- | --- | --- | --- |
| F-service-catalog-01 | Customer-facing service specification | Service Catalog | P1: required to make service specification lifecycle usable for product launch, order-to-activate, inventory handoff, assurance readiness, or governed retirement. |
| F-service-catalog-02 | Resource-facing service specification | Service Catalog | P1: required to make service specification lifecycle usable for product launch, order-to-activate, inventory handoff, assurance readiness, or governed retirement. |
| F-service-catalog-03 | Service characteristic and constraint model | Service Catalog | P1: required to make service specification lifecycle usable for product launch, order-to-activate, inventory handoff, assurance readiness, or governed retirement. |
| F-service-catalog-04 | CFS to RFS relationship model | Service Catalog | P1: required to make service specification lifecycle usable for product launch, order-to-activate, inventory handoff, assurance readiness, or governed retirement. |
| F-service-catalog-05 | Service dependency and ordering model | Service Catalog | P2: required to make service specification lifecycle usable for product launch, order-to-activate, inventory handoff, assurance readiness, or governed retirement. |
| F-service-catalog-06 | Product-service mapping reference | Service Catalog | P2: required to make service specification lifecycle usable for product launch, order-to-activate, inventory handoff, assurance readiness, or governed retirement. |
| F-service-catalog-07 | Service compatibility and retirement policy | Service Catalog | P2: required to make service specification lifecycle usable for product launch, order-to-activate, inventory handoff, assurance readiness, or governed retirement. |

## Acceptance Criteria

1. **AC-service-catalog-01:** Given an authorized Service designer, Resource designer, Network engineer, Product/catalog governance user, or Fulfillment architect creates or updates the service specification and service catalog version, when the service specification lifecycle advances from draft to review, then Service And Resource Design Studio validates service characteristic completeness, CFS/RFS relationship validity, product mapping, resource realization, compatibility rule result, activation template reference, retirement impact, and assurance handoff readiness before accepting the state change.
2. **AC-service-catalog-02:** Given the service specification and service catalog version references commercial product, service, resource, inventory, activation, or assurance data, when a persona opens the Service Catalog record, then the app shows source owner, referenced version, freshness, confidence, correction route, and whether the reference is read-only or app-owned.
3. **AC-service-catalog-03:** Given Missing RFS realization for a sellable product, when validation fails for Service Catalog, then the app keeps the record in draft, blocked, or rejected state with severity, owner, due date, reason code, impacted consumer, waiver option, and correlation ID.
4. **AC-service-catalog-04:** Given a governance decision is required for the service specification and service catalog version, when the accountable persona approves, rejects, waives, retires, or supersedes it, then the app stores decision right, actor, role, reason, old/new values, policy version, evidence links, tenant/region boundary, and idempotency key.
5. **AC-service-catalog-05:** Given CPQ, Order Management Hub, Fulfillment, Inventory, Field, Assurance, Partner, or Data consumers subscribe to Service Catalog changes, when the service specification and service catalog version is published or retired, then the app emits a versioned event with changed fields, impacted services/resources, consumer revalidation flag, replay metadata, and correlation ID.
6. **AC-service-catalog-06:** Given a brownfield MACD, migration, rollback, or decommissioning scenario references the service specification and service catalog version, when the user requests publication or closure, then the app validates active inventory impact, in-flight order impact, field/partner dependency, activation rollback path, and customer/NOC/care handoff before closure.
7. **AC-service-catalog-07:** Given supervisors or data stewards review Service Catalog operations, when they open dashboards, then they see draft aging, certification pass/fail, exception causes, waiver aging, publication lag, consumer adoption, revalidation backlog, and downstream fallout linked to the service specification and service catalog version.

## Negative Scenarios

Negative scenarios for this feature include permission denial, missing source data, stale dependency state, policy failure, duplicate or replayed request, downstream timeout, reconciliation mismatch, and any feature-specific negative scenario additions listed in the suite gap-review closure addendum.

## Edge Cases

| Scenario | Expected behavior |
| --- | --- |
| Missing RFS realization for a sellable product | Service Catalog blocks unsafe publication or routes a governed exception with owner, due date, affected product/service/resource, consumer impact, waiver authority, and replayable evidence. |
| Service characteristic conflicts with activation template parameter | Service Catalog blocks unsafe publication or routes a governed exception with owner, due date, affected product/service/resource, consumer impact, waiver authority, and replayable evidence. |
| Retired service spec still referenced by active service inventory | Service Catalog blocks unsafe publication or routes a governed exception with owner, due date, affected product/service/resource, consumer impact, waiver authority, and replayable evidence. |
| Assurance test rule absent for a critical enterprise service | Service Catalog blocks unsafe publication or routes a governed exception with owner, due date, affected product/service/resource, consumer impact, waiver authority, and replayable evidence. |
| Cross-tenant service version reused without approval | Service Catalog blocks unsafe publication or routes a governed exception with owner, due date, affected product/service/resource, consumer impact, waiver authority, and replayable evidence. |
| Duplicate, stale, or out-of-order publication request | Service Catalog uses optimistic locking, event version, source timestamp, and idempotency key so retries cannot publish duplicate catalog, template, rule, or certification state. |
| Cross-tenant, cross-region, or restricted topology access | Service Catalog blocks mutation, masks restricted service/resource/topology data, and records policy decision metadata for tenant isolation, data residency, and export control. |
| Downstream consumer unavailable | Service Catalog either fails fast for synchronous certification gates or queues a controlled retry, replay, or consumer revalidation task with owner, due date, backoff policy, and correlation ID. |
| Legal hold or regulatory retention conflict | Service Catalog prevents deletion or destructive retirement of catalog, rule, template, or certification evidence until legal hold, retention, and regulatory inventory evidence controls allow it. |

## API, Event, And Data Requirements

Related APIs and API areas: [TMF633](../../../../../references/tmforum-open-apis/openapi-specs/TMF633_ServiceCatalog), [TMF620](../../../../../references/tmforum-open-apis/openapi-specs/TMF620_ProductCatalog), [TMF645](../../../../../references/tmforum-open-apis/openapi-specs/TMF645_ServiceQualification), [TMF701](../../../../../references/tmforum-open-apis/openapi-specs/TMF701_ProcessFlow)

TMF API fit and extension notes:

- Use TMF633 for service specification resources and catalog lifecycle. Use TMF620 only as a referenced commercial product catalog source. Use TMF645 and TMF701 patterns for qualification and decomposition process links where service rules affect feasibility or order decomposition.
- Non-TMF Service Design Rule API for CFS/RFS realization constraints, rollback notes, assurance handoff metadata, and service retirement impact summaries. Each extension contract must be explicitly labelled non-TMF, documented with OpenAPI, and aligned to TMF-style id, href, lifecycle state, relatedParty, relatedEntity, error, pagination, and event-envelope patterns where practical.
- Command APIs for Service Catalog must cover create/initiate, validate, update, certify, approve/reject, publish, suspend, retire, supersede, correct, replay, and close where the service specification lifecycle uses those states.
- Query APIs for Service Catalog must cover search, detail, timeline, related service specification and service catalog version references, compatibility matrix, certification evidence, work queue, metrics, and audit retrieval with role-aware masking.
- Domain events for Service Catalog must include ServiceSpecificationDrafted, ServiceSpecificationCertified, ServiceSpecificationPublished, ServiceSpecificationRetirementMapped, plus exception raised, exception resolved, corrected, replay requested, and consumer revalidation requested where the lifecycle uses those states.

Data and ownership requirements:

- Service And Resource Design Studio owns customer-facing service specs, resource-facing service specs, service characteristics, service relationships, service lifecycle states, service compatibility notes, and service catalog publication evidence; other apps consume Service Catalog state through APIs, events, governed projections, workflow tasks, certification packs, or certified data products.
- Store source channel, actor, tenant/brand/market, technology domain, lifecycle action, status reason, catalog version, rule/template version, external references, before/after values, policy decision, evidence links, retention class, legal hold flag, and impacted consumer list.
- Keep read projections, analytics extracts, and data platform outputs separate from operational writes so Service Catalog does not create shadow mastership of product, inventory, order, activation, field, assurance, partner, or platform records.
- Provide reconciliation outputs that prove CPQ, order decomposition, fulfillment, activation, inventory, assurance, field, partner, and data consumers have accepted, rejected, or remain explicitly blocked by the service specification and service catalog version.

## Integrations And Handoffs

- Product And Offer Studio for product specification and offering references.
- Order Management Hub for service decomposition input.
- Fulfillment And Activation Control Tower for executable service order templates.
- Inventory And Topology for service inventory model acceptance.
- NOC And Assurance and Performance/SLA for service test and monitoring readiness.

## Non-Functional Requirements

- Scale and latency: Service Catalog must support national catalog portfolios with thousands of service/resource specs, realization rules, templates, compatibility rules, versions, validation runs, and consumer subscriptions; interactive search and detail views should stay below 2 seconds while certification, impact analysis, and bulk publication run asynchronously with progress and partial-failure reports.
- Availability and resilience: published catalog, rule, and template query APIs for Service Catalog must remain available during downstream CPQ, inventory, fulfillment, activation, assurance, field, partner, or test outages by serving last-known certified versions with freshness and confidence indicators.
- Auditability and retention: Service Catalog history must retain actor, channel, reason, old/new value, policy version, approval/waiver, event ID, external reference, certification result, legal hold flag, and retention class for engineering, regulatory, security, and operational evidence periods.
- Localization and accessibility: Service Catalog UI tasks, validation messages, engineering units, technology labels, time zones, language, keyboard navigation, and screen-reader labels must respect tenant, market, geography, and accessibility policy.
- Data protection: API, event, export, and dashboard paths for Service Catalog must enforce tenant isolation, data residency, purpose limitation, least privilege, sensitive topology masking, critical-infrastructure masking, and secure evidence storage.

## Compliance, Security, And Privacy

- Service Catalog must enforce tenant isolation, region boundaries, role-based catalog publication, privileged activation-template controls, critical infrastructure masking, security-by-design evidence, export controls, and data residency for the service specification and service catalog version.
- Service Catalog must preserve lawful/regulatory inventory evidence, service retirement evidence, activation safety evidence, migration/decommissioning evidence, legal hold, and certification records where catalog or template decisions affect regulated telecom obligations.
- Sensitive service, resource, site, topology, firmware, controller, partner/off-net, and enterprise customer references in Service Catalog must be masked in search, timelines, exports, analytics, and dashboards unless the persona has a permitted operational purpose.

## Observability And Operations

- Metrics: track service-catalog records drafted, validated, certified, rejected, published, retired, superseded, waived, corrected, replayed, and accepted by consumers, plus validation failure rate, waiver aging, publication lag, consumer revalidation backlog, and downstream fallout linked to catalog changes.
- Queues: provide queues for draft, pending validation, pending certification, blocked dependency, waiver review, publication ready, consumer revalidation, exception, retrying, retirement review, corrected, completed, and archived Service Catalog records.
- Alerts: notify Service And Resource Design Studio owners when validation failure rate, certification backlog, event publication failure, consumer lag, stale version usage, waiver aging, or downstream activation/order fallout breaches threshold.
- Runbooks: document triage, validation replay, consumer revalidation, publication rollback, retirement repair, waiver review, evidence export, legal hold response, and downstream event replay procedures for Service Catalog.
- Ownership: Service And Resource Design Studio owns first-line health for Service Catalog lifecycle, event replay, validation queues, and publication evidence; Product, Inventory, Fulfillment, Field, Assurance, Partner, Platform, Data, and Test owners correct their own source records.

## Test Approach

| Test layer | Required coverage |
| --- | --- |
| Unit tests | Field rules, lifecycle transitions, certification state, duplicate detection, version compatibility, masking, and service specification and service catalog version calculations for Service Catalog. |
| API contract tests | Commands, queries, errors, idempotency, pagination, filtering, version compatibility, TMF-aligned payloads for TMF633, TMF620, TMF645, TMF701, and documented non-TMF extension APIs. |
| Event contract tests | Service Catalog event names, payload shape, changed fields, correlation ID, idempotency key, ordering metadata, replay behavior, and subscriber compatibility. |
| Workflow tests | Happy path, assisted correction, automated API path, certification approval, exception, waiver, timeout, retry, publication, retirement, supersession, correction, and closure for service specification lifecycle. |
| Integration tests | Handoffs with product catalog, CPQ, order management, fulfillment, activation, inventory, field, assurance, partner/off-net, platform test, and data owners, including external provider unavailability and no direct database access. |
| Security and privacy tests | Tenant isolation, privileged publication permissions, sensitive topology masking, malicious payloads, audit logging, legal hold, retention, export controls, and data residency for Service Catalog. |
| Data tests | Source authority, referential integrity, historical correction, projection refresh, data-quality stewardship, reporting metrics, and lineage for service specification and service catalog version. |
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

This refinement converts the feature review material for Service Catalog into delivery slices that can become epics, stories, API contracts, migrations, and test cases. Treat Service And Resource Design Studio App as the owning application for this feature within Suite OSS Engineering, Inventory, And Fulfillment and schema `service_resource_design`.

| Workstream | Build-ready delivery guidance |
| --- | --- |
| UX and workflow | Build the Service Catalog workbench for Service designer, Resource designer, Network engineer, Product/catalog governance user, Fulfillment architect. Include search or intake, guided validation, detail view, lifecycle timeline, decision panel, evidence drawer, exception queue, bulk or replay controls where relevant, saved filters, SLA/OLA aging, empty/error states, and role-aware masking. The UI must expose draft, validate, certify, publish, suspend for correction, retire, reinstate, or map service specification versions to successor services. The decision records the accountable persona, rule result, waiver status... and block closure when required evidence, approval, reconciliation, or downstream acknowledgement is missing. |
| API and events | Implement command and query APIs around service-catalog using TMF633, TMF620, TMF645, TMF701. Command APIs for Service Catalog must cover create/initiate, validate, update, certify, approve/reject, publish, suspend, retire, supersede, correct, replay, and close where the service specification lifecycle uses... Query APIs for Service Catalog must cover search, detail, timeline, related service specification and service catalog version references, compatibility matrix, certification evidence, work queue, metrics, and audit... Domain events for Service Catalog must include ServiceSpecificationDrafted, ServiceSpecificationCertified, ServiceSpecificationPublished, ServiceSpecificationRetirementMapped, plus exception raised, exception resolved... Non-TMF Service Design Rule API for CFS/RFS realization constraints, rollback notes, assurance handoff metadata, and service retirement impact summaries. Each extension contract must be explicitly labelled non-TMF... Every command, query, and event must carry tenant/brand/market where applicable, actor, source channel, reason code, idempotency key, correlation ID, external reference, lifecycle state, and version metadata. |
| Data and controls | Persist service specification and service catalog version. inside `service_resource_design` with typed lifecycle, owner, status reason, timestamps, policy decision, source freshness, confidence, old/new value, evidence, and reconciliation fields. Service And Resource Design Studio owns customer-facing service specs, resource-facing service specs, service characteristics, service relationships, service lifecycle states, service compatibility notes, and service catalog publication... Keep TMF payloads, extension characteristics, imported evidence, and low-stability metadata in JSONB while promoting operationally searched lifecycle fields to typed columns. |
| Integration and handoff | Exchange commercial product specifications, product offerings, geography/serviceability decisions, resource specifications, activation templates, service inventory instances, service tests... with Product And Offer Studio for product specification and offering references., Order Management Hub for service decomposition input., Fulfillment And Activation Control Tower for executable service order templates., Inventory And... only through APIs, events, workflow tasks, governed projections, adapters, evidence packages, or certified data products. Show source owner, freshness, confidence, dependency state, retry status, blocked consumer, and completion evidence so the app does not create shadow mastership or direct cross-schema coupling. |
| Security, privacy, and compliance | Enforce RBAC/ABAC, tenant and residency boundaries, least privilege, separation of duties, masking, purpose limitation, retention, legal hold, export control, manual override expiry, immutable audit, and evidence chain of custody for Service Catalog. Sensitive customer, revenue, partner, security, network, credential, or regulatory evidence must be masked unless the persona has explicit operational purpose. |
| Tests and operations | Create unit, API contract, event replay/idempotency, workflow, integration, migration, data reconciliation, security/privacy, accessibility/localization, performance, dashboard, alert, and runbook tests for Service Catalog. Cover happy path, assisted path, automated path, exception path, bulk/project path, stale or duplicate input, downstream outage, policy denial, manual override, and reconciliation mismatch. Use the existing review scope - versioned service and resource specifications, realization rules, compatibility validation, activation templates, and publication readiness. - as mandatory backlog and test evidence. |

Implementation notes:

- Treat Service And Resource Design Studio App as the lifecycle owner for service specification and service catalog version.; referenced data such as commercial product specifications, product offerings, geography/serviceability decisions, resource specifications, activation templates, service inventory instances, service tests, assurance rules, and order... must remain references, snapshots, projections, evidence packages, or consumer acknowledgements unless the source file explicitly gives this app mastership.
- Make TMF alignment visible in every story: use named TMF resources where they fit, document non-TMF extension APIs with OpenAPI, and keep extension payloads compatible with TMF-style identifiers, lifecycle state, related entities, pagination, errors, and event envelopes.
- Build UI and API behavior around decision evidence, not only CRUD: surface the permitted next actions, policy decision, state reason, owner, SLA/OLA timer, blocked dependency, retry or compensation path, and closure proof.
- Add development tasks for route/page/component work, command/query handlers, DTO validation, entity/repository/migration changes, outbox/event contracts, projection refresh, privacy/security checks, and operational dashboards.
- Definition-of-done evidence must show downstream consumers can use published state through APIs, events, projections, workflow tasks, or certified data products without direct database reads or manual spreadsheet reconciliation.

## Definition Of Done

1. The service specification and service catalog version lifecycle supports draft, validating, in certification, blocked, waived, published, suspended, retired, superseded, corrected, rejected, and archived states where applicable.
2. Persona workflows for Service designer, Resource designer, Network engineer, Product/catalog governance user, and Fulfillment architect include decision rights, validation messages, exception routing, and evidence capture for Service Catalog.
3. TMF-aligned references, non-TMF extension APIs, events, idempotency, correlation IDs, error models, replay behavior, and consumer revalidation contracts are documented and contract-tested.
4. Data ownership, private app database boundaries, governed projections, retention, legal hold, tenant isolation, critical-topology masking, privileged activation controls, and export controls match data mastery and ODA guidance.
5. Operational dashboards explain Service Catalog state, version, validation results, exceptions, waivers, publication status, downstream consumers, stale version usage, and revalidation backlog without direct database access.
6. Negative scenarios, telecom edge cases, workflow tests, security tests, event replay tests, certification tests, compatibility tests, and reconciliation tests are automated or explicitly covered in delivery evidence.
