# Service And Resource Design Studio App Feature Specifications

Reviewed: 2026-06-07

This folder contains detailed feature specifications for the Service And Resource Design Studio app. The app owns service specifications, resource specifications, technical realization rules, compatibility rules, entity templates, activation template definitions, and catalog certification evidence; it does not own commercial product catalog records, active inventory, service/resource order execution, activation execution, field work, stock, assurance, or platform security records.

Parent app: [Service And Resource Design Studio App](../README.md)

## Feature Specification Index

| Feature specification | OSS engineering intent | Primary TMF anchors | Gap priority |
| --- | --- | --- | --- |
| [Service Catalog](service-catalog.md) | Manage customer-facing and resource-facing service specifications, service characteristics, relationships, dependencies, lifecycle states, versioning, product mapping, release, retirement, and compatibility so commercial offers can become orderable and supportable technical services. | TMF633, TMF620, TMF645, TMF701 | Core |
| [Resource Catalog](resource-catalog.md) | Manage physical, logical, compute, software, device, cloud, network, identifier, and capacity resource specifications so Inventory And Topology can instantiate resources and Fulfillment can request assignments with valid activation attributes. | TMF634, TMF730 | Core |
| [Product-Service-Resource Mapping](product-service-resource-mapping.md) | Define how BSS commercial products and offerings decompose into customer-facing services, resource-facing services, resource orders, activation tasks, inventory reservations, field work, partner work, and billing/assurance handoffs across fiber, mobile, fixed wireless, enterprise VPN, IoT, NaaS, cloud connectivity, and off-net products. | TMF620, TMF633, TMF634, TMF701, TMF641, TMF652 | Core |
| [Technical Compatibility And Design Rule](technical-compatibility-and-design-rule.md) | Define technical compatibility and design rules across products, services, resources, technologies, locations, customer types, topology, serviceability, capacity pools, activation platforms, and regulatory constraints so CPQ, order decomposition, engineering, and fulfillment can reject unsafe combinations early. | TMF645, TMF679, TMF633, TMF634 | Core |
| [Entity Catalog](entity-catalog.md) | Define reusable entity types, metadata templates, relationship patterns, extension points, naming standards, and versioning rules shared across service catalog, resource catalog, inventory, topology, fulfillment, activation, and assurance models. | TMF662, TMF633, TMF634 | Core |
| [Fulfillment And Activation Template Design](fulfillment-and-activation-template-design.md) | Design decomposition templates, service order templates, resource order templates, activation command templates, configuration profiles, validation rules, compensation steps, and test handoffs that Fulfillment And Activation Control Tower can execute safely. | TMF633, TMF634, TMF641, TMF652, TMF640, TMF664, TMF760 | High E2E gap closure |
| [Advanced Network Cloud And Device Resource Models](advanced-network-cloud-and-device-resource-models.md) | Model network slices, SDN/NFV functions, cloud and edge resources, CPE firmware, IoT device capabilities, SIM/eSIM enablement attributes, and resource-function activation metadata for modern telecom services. | TMF634, TMF730, TMF640, TMF664 | High E2E gap closure |
| [Catalog Version Certification And Retirement Mapping](catalog-version-certification-and-retirement-mapping.md) | Govern service/resource catalog version compatibility, certification evidence, release gates, retirement mappings, migration paths, and backward compatibility policies so catalog changes do not break CPQ, order decomposition, fulfillment, inventory, activation, assurance, or partner journeys. | TMF633, TMF634, TMF704, TMF707, TMF760, TMF701 | High E2E gap closure |

## App-Level Control Scope

- Design Studio masters technical catalog and template definitions: service specifications, resource specifications, realization rules, compatibility rules, entity templates, fulfillment/activation templates, certification packs, retirement mappings, and publication events.
- Design Studio references BSS product and offer versions, geography/serviceability decisions, inventory/topology state, service/resource orders, activation evidence, field work, assurance tests, and platform policy through APIs, events, governed projections, or certification packs.
- Design Studio must never become the active product inventory, service inventory, resource inventory, service order, resource order, activation execution, work order, stock, shipment, assurance ticket, customer, billing, or partner lifecycle master.

## Cross-App Handoffs To Prove

| Handoff | Required evidence |
| --- | --- |
| Product/offer to technical realization | Product specification and offering version, mapped service/resource specs, compatibility decision, certification evidence, and launch readiness status. |
| Design to order decomposition | Realization rule, lifecycle action matrix, service/resource order template, field/partner handoff requirement, rollback behavior, and consumer event ID. |
| Design to activation | Activation template version, parameter schema, controller compatibility, rollback command, service test handoff, and privileged approval record. |
| Design to inventory/topology | Resource specification, inventory model link, assignment attributes, entity template, topology relationship rule, and data stewardship route. |
| Design to assurance/NOC | Service test rule, monitoring readiness, service/resource relationship, impact metadata, and retirement or migration notification. |
| Design to compliance/data | Tenant, region, data residency, legal hold, critical topology masking, retention class, lineage, and certification evidence. |

## How To Use These Feature Specs

- Use each feature specification as the starting point for epics, user stories, API contracts, event contracts, certification tests, operational dashboards, runbooks, and data-quality controls.
- Confirm the master entity, referenced entities, TMF API fit, non-TMF extension APIs, events, private database boundary, and consumer revalidation behavior before implementation starts.
- Keep app-owned writes inside the Service And Resource Design Studio boundary; cross-app work must use APIs, events, governed projections, workflow tasks, certification packs, or certified data products.
- Validate every feature against order-to-activate, plan-to-build handoff, lead-to-order feasibility, assure-to-optimize feedback, trouble-to-resolve support, partner/off-net delivery, and govern-to-comply evidence journeys.

## Feature Detail Review Alignment (2026-06-14)

Source: [Suite Feature Detail Review](../../feature-detail-review.md) and [Critical Feature Review Enhancements](../modules-and-features.md#critical-feature-review-enhancements-2026-06-14).

The 2026-06-14 review upgrades this app feature set with required scope: versioned service and resource specifications, realization rules, compatibility validation, activation templates, and publication readiness.

Apply this scope when refining the feature specifications in this folder:

- Add or update epics, stories, UI workbenches, APIs, events, app-owned data fields, DDL gaps, test cases, observability, runbooks, and definition-of-done evidence for the review scope.
- Preserve the app data ownership boundary. Cross-app access must use APIs, events, workflow tasks, governed projections, or certified data products rather than direct database sharing.
- If this scope needs technology beyond Angular, Spring Boot, PostgreSQL, and PrimeNG, offer open-source options with pros, cons, and a recommendation before implementation.
