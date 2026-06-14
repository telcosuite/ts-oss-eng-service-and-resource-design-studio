# Service And Resource Design Studio App Detail Pack

Reviewed: 2026-06-06

This folder expands the concise app overview into build-ready module, feature, persona, and user journey planning. The concise source overview remains at [service-and-resource-design-studio.md](../service-and-resource-design-studio.md).

Suite: OSS Engineering, Inventory, And Fulfillment

## Build Intent

Define how commercial products become technical services, resource assignments, activation patterns, and fulfillment workflows.

## Detail Documents

- [Modules And Features](modules-and-features.md)
- [Feature Specifications](features/README.md)
- [Personas And User Journeys](personas-and-user-journeys.md)

## Primary Personas

- Service designer: models customer-facing and resource-facing service specifications.
- Resource designer: models reusable physical, logical, cloud, software, and network resources.
- Network engineer: validates technology-specific design and compatibility.
- Product/catalog governance user: confirms product-service-resource mapping before offer launch.
- Fulfillment architect: defines decomposition and activation patterns.

## Core Operating Flow

1. Define service specifications and resource specifications.
2. Map product offerings to service and resource realization patterns.
3. Define add, modify, suspend, resume, disconnect, transfer, migrate, and rollback behaviors.
4. Validate technical compatibility by location, product, service, resource, topology, and capacity.
5. Publish design models to CPQ, order decomposition, fulfillment, activation, inventory, and assurance.

## Module Map

| Module | Feature focus | Related APIs |
| --- | --- | --- |
| Service Catalog | Manage customer-facing and resource-facing service specs, characteristics, relationships, dependencies, lifecycle, versioning, product mapping, release, retirement, and compatibility. | [TMF633](../../../../references/tmforum-open-apis/openapi-specs/TMF633_ServiceCatalog), [TMF620](../../../../references/tmforum-open-apis/openapi-specs/TMF620_ProductCatalog) |
| Resource Catalog | Manage physical, logical, compute, software, and network resource specs | [TMF634](../../../../references/tmforum-open-apis/openapi-specs/TMF634_ResourceCatalog), [TMF730](../../../../references/tmforum-open-apis/openapi-specs/TMF730_SoftwareAndComputeManagement) |
| Product-Service-Resource Mapping | Define how products decompose into services and resources across fiber, mobile, fixed wireless, enterprise VPN, IoT, NaaS, cloud connectivity, and partner products | [TMF620](../../../../references/tmforum-open-apis/openapi-specs/TMF620_ProductCatalog), [TMF633](../../../../references/tmforum-open-apis/openapi-specs/TMF633_ServiceCatalog), [TMF634](../../../../references/tmforum-open-apis/openapi-specs/TMF634_ResourceCatalog), [TMF701](../../../../references/tmforum-open-apis/openapi-specs/TMF701_ProcessFlow) |
| Technical Compatibility And Design Rule | Define compatibility rules across products, services, resources, technologies, locations, customer types, topology, serviceability, and capacity pools | [TMF645](../../../../references/tmforum-open-apis/openapi-specs/TMF645_ServiceQualification), [TMF679](../../../../references/tmforum-open-apis/openapi-specs/TMF679_ProductOfferingQualification) |
| Entity Catalog | Define reusable entity types, metadata, templates, relationships, extension points, and versioning shared across service, resource, inventory, and assurance models. | [TMF662](../../../../references/tmforum-open-apis/openapi-specs/TMF662_EntityCatalog) |

## Data Ownership

Owns service specifications, resource specifications, realization rules, technical compatibility rules, design templates, and entity templates. It does not own active inventory or customer product instances.

## First Release Scope

Deliver service catalog, resource catalog, product-service-resource mapping, and basic compatibility validation for the first supported products. Add advanced model extension and technology-specific design automation over time.

## Build Notes

- Treat this app as an API-first product surface. UI screens, automations, partner access, and internal integrations should use the same app-owned APIs.
- Keep the app database private to this app or its module owners. Other apps should consume APIs, events, governed read models, or data products.
- Create backlog items at feature level, but preserve module ownership so roadmap, permissions, observability, and data stewardship remain clear.

## Implementation Guidance

- [Implementation File Usage](implementation-file-usage.md)
