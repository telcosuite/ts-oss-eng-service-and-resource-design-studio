# Service And Resource Design Studio TMF API To DDL Review

Reviewed: 2026-06-14

Status: Complete for baseline app implementation. Endpoint-specific contract tests and final story-level field promotion still happen during build.

## Scope

This review covers `service_resource_design` in suite database `ts_oss_engineering_fulfillment`. It uses the local TMF Open API reference set, the suite data model, the API-to-DDL traceability matrix, and the V001 starter DDL.

The review confirms that the app can move into implementation with a V002 typed DDL baseline while preserving full TMF payload compatibility through validated `tmf_payload`, typed common TMF columns, and normalized support tables.

## TMF API Baseline Selection

| TMF API | Local baseline spec | Resources/path roots reviewed | V001 table groups |
| --- | --- | --- | --- |
| TMF633 | `references/tmforum-open-apis/openapi-specs/TMF633_ServiceCatalog/TMF633_Service_Catalog_Management_API_v4.0.0_swagger.json` | `exportJob`, `importJob`, `serviceCandidate`, `serviceCatalog`, `serviceCategory`, `serviceSpecification` | service_specification; partner_catalog_submission references |
| TMF620 | `references/tmforum-open-apis/openapi-specs/TMF620_ProductCatalog/TMF620-Product_Catalog_Management-v5.0.0.oas.yaml` | `category`, `exportJob`, `importJob`, `productCatalog`, `productOffering`, `productOfferingPrice`, `productSpecification` | product_specification; product_offering; product_bundle; marketplace_listing; partner_catalog_submission |
| TMF634 | `references/tmforum-open-apis/openapi-specs/TMF634_ResourceCatalog/TMF634-Resource_Catalog_Management-v5.0.0.oas.yaml` | `exportJob`, `importJob`, `resourceCandidate`, `resourceCatalog`, `resourceCategory`, `resourceSpecification` | resource_specification; capacity_model references |
| TMF730 | `references/tmforum-open-apis/openapi-specs/TMF730_SoftwareAndComputeManagement/TMF730_Software_And_Compute_Management_API_v4.0.0_swagger.json` | `resource`, `resourceSpecification` | resource_specification; capacity planning references |
| TMF701 | `references/tmforum-open-apis/openapi-specs/TMF701_ProcessFlow/TMF701-ProcessFlow-v4.0.0.swagger.json` | `processFlow` | process_definition; process_version; work_queue; task; provisioning_workflow_state |
| TMF645 | `references/tmforum-open-apis/openapi-specs/TMF645_ServiceQualification/TMF645-Service_Qualification_Management-v5.0.0.oas.yaml` | `checkServiceQualification`, `queryServiceQualification` | serviceability_rule; serviceability_decision; offering_qualification references |
| TMF679 | `references/tmforum-open-apis/openapi-specs/TMF679_ProductOfferingQualification/TMF679-Product_Offering_Qualification-v5.0.0.oas.yaml` | `checkProductOfferingQualification`, `queryProductOfferingQualification` | offering_qualification; serviceability_decision references |
| TMF662 | `references/tmforum-open-apis/openapi-specs/TMF662_EntityCatalog/TMF662_Entity_Catalog_Management_API_v4.0.0_swagger.json` | `association`, `associationSpecification`, `entityCatalog`, `entityCatalogItem`, `entityCategory`, `entitySpecification`, `exportJob`, `importJob` | entity_template |

## Current DDL Coverage

Current starter DDL is in `database/postgres/suites/ts_oss_engineering_fulfillment/V001__create_app_schemas_and_starter_tables.sql` under schema `service_resource_design`.

| Current table | TMF purpose | V002 decision |
| --- | --- | --- |
| `service_resource_design.service_specification` | Starter table for Service And Resource Design Studio; V002 promotes common TMF fields and keeps full validated payload support. | Keep and refine through `database/postgres/suites/ts_oss_engineering_fulfillment/V004__refine_service_resource_design_tmf_core.sql` |
| `service_resource_design.resource_specification` | Starter table for Service And Resource Design Studio; V002 promotes common TMF fields and keeps full validated payload support. | Keep and refine through `database/postgres/suites/ts_oss_engineering_fulfillment/V004__refine_service_resource_design_tmf_core.sql` |
| `service_resource_design.specification_version` | Starter table for Service And Resource Design Studio; V002 promotes common TMF fields and keeps full validated payload support. | Keep and refine through `database/postgres/suites/ts_oss_engineering_fulfillment/V004__refine_service_resource_design_tmf_core.sql` |
| `service_resource_design.realization_rule` | Starter table for Service And Resource Design Studio; V002 promotes common TMF fields and keeps full validated payload support. | Keep and refine through `database/postgres/suites/ts_oss_engineering_fulfillment/V004__refine_service_resource_design_tmf_core.sql` |
| `service_resource_design.technical_compatibility_rule` | Starter table for Service And Resource Design Studio; V002 promotes common TMF fields and keeps full validated payload support. | Keep and refine through `database/postgres/suites/ts_oss_engineering_fulfillment/V004__refine_service_resource_design_tmf_core.sql` |
| `service_resource_design.entity_template` | Starter table for Service And Resource Design Studio; V002 promotes common TMF fields and keeps full validated payload support. | Keep and refine through `database/postgres/suites/ts_oss_engineering_fulfillment/V004__refine_service_resource_design_tmf_core.sql` |
| `service_resource_design.event_outbox` | App outbox for domain and TMF notification events. | Keep and refine through `database/postgres/suites/ts_oss_engineering_fulfillment/V004__refine_service_resource_design_tmf_core.sql` |

## Resource To Table Decisions

| TMF API/resource | Master or anchor table | Path coverage | Promoted field candidates | Field handling strategy |
| --- | --- | --- | --- | --- |
| TMF633 `exportJob` | `service_resource_design.service_specification` | `/exportJob`, `/exportJob/{id}` | `id`, `href`, `completionDate`, `contentType`, `creationDate`, `errorLog`, `path`, `query` | Promote common TMF lifecycle/reference fields; store remaining validated resource fields in tmf_payload and characteristics tables. |
| TMF633 `importJob` | `service_resource_design.service_specification` | `/importJob`, `/importJob/{id}` | `id`, `href`, `completionDate`, `contentType`, `creationDate`, `errorLog`, `path`, `url` | Promote common TMF lifecycle/reference fields; store remaining validated resource fields in tmf_payload and characteristics tables. |
| TMF633 `serviceCandidate` | `service_resource_design.service_specification` | `/serviceCandidate`, `/serviceCandidate/{id}` | `id`, `href`, `description`, `lastUpdate`, `lifecycleStatus`, `name`, `version`, `category` | Promote common TMF lifecycle/reference fields; store remaining validated resource fields in tmf_payload and characteristics tables. |
| TMF633 `serviceCatalog` | `service_resource_design.service_specification` | `/serviceCatalog`, `/serviceCatalog/{id}` | `id`, `href`, `description`, `lastUpdate`, `lifecycleStatus`, `name`, `version`, `category` | Promote common TMF lifecycle/reference fields; store remaining validated resource fields in tmf_payload and characteristics tables. |
| TMF633 `serviceCategory` | `service_resource_design.service_specification` | `/serviceCategory`, `/serviceCategory/{id}` | `id`, `href`, `description`, `isRoot`, `lastUpdate`, `lifecycleStatus`, `name`, `parentId` | Promote common TMF lifecycle/reference fields; store remaining validated resource fields in tmf_payload and characteristics tables. |
| TMF633 `serviceSpecification` | `service_resource_design.service_specification` | `/serviceSpecification`, `/serviceSpecification/{id}` | `id`, `href`, `description`, `isBundle`, `lastUpdate`, `lifecycleStatus`, `name`, `version` | Promote common TMF lifecycle/reference fields; store remaining validated resource fields in tmf_payload and characteristics tables. |
| TMF620 `category` | `service_resource_design.service_specification` | `/category`, `/category/{id}` | Common TMF metadata plus payload validation | Promote common TMF metadata; store resource-specific fields in tmf_payload until query patterns justify additional typed columns. |
| TMF620 `exportJob` | `service_resource_design.service_specification` | `/exportJob`, `/exportJob/{id}` | Common TMF metadata plus payload validation | Promote common TMF metadata; store resource-specific fields in tmf_payload until query patterns justify additional typed columns. |
| TMF620 `importJob` | `service_resource_design.service_specification` | `/importJob`, `/importJob/{id}` | Common TMF metadata plus payload validation | Promote common TMF metadata; store resource-specific fields in tmf_payload until query patterns justify additional typed columns. |
| TMF620 `productCatalog` | `service_resource_design.service_specification` | `/productCatalog`, `/productCatalog/{id}` | Common TMF metadata plus payload validation | Promote common TMF metadata; store resource-specific fields in tmf_payload until query patterns justify additional typed columns. |
| TMF620 `productOffering` | `service_resource_design.service_specification` | `/productOffering`, `/productOffering/{id}` | Common TMF metadata plus payload validation | Promote common TMF metadata; store resource-specific fields in tmf_payload until query patterns justify additional typed columns. |
| TMF620 `productOfferingPrice` | `service_resource_design.service_specification` | `/productOfferingPrice`, `/productOfferingPrice/{id}` | Common TMF metadata plus payload validation | Promote common TMF metadata; store resource-specific fields in tmf_payload until query patterns justify additional typed columns. |
| TMF620 `productSpecification` | `service_resource_design.service_specification` | `/productSpecification`, `/productSpecification/{id}` | Common TMF metadata plus payload validation | Promote common TMF metadata; store resource-specific fields in tmf_payload until query patterns justify additional typed columns. |
| TMF634 `exportJob` | `service_resource_design.resource_specification` | `/exportJob`, `/exportJob/{id}` | Common TMF metadata plus payload validation | Promote common TMF metadata; store resource-specific fields in tmf_payload until query patterns justify additional typed columns. |
| TMF634 `importJob` | `service_resource_design.resource_specification` | `/importJob`, `/importJob/{id}` | Common TMF metadata plus payload validation | Promote common TMF metadata; store resource-specific fields in tmf_payload until query patterns justify additional typed columns. |
| TMF634 `resourceCandidate` | `service_resource_design.resource_specification` | `/resourceCandidate`, `/resourceCandidate/{id}` | Common TMF metadata plus payload validation | Promote common TMF metadata; store resource-specific fields in tmf_payload until query patterns justify additional typed columns. |
| TMF634 `resourceCatalog` | `service_resource_design.resource_specification` | `/resourceCatalog`, `/resourceCatalog/{id}` | Common TMF metadata plus payload validation | Promote common TMF metadata; store resource-specific fields in tmf_payload until query patterns justify additional typed columns. |
| TMF634 `resourceCategory` | `service_resource_design.resource_specification` | `/resourceCategory`, `/resourceCategory/{id}` | Common TMF metadata plus payload validation | Promote common TMF metadata; store resource-specific fields in tmf_payload until query patterns justify additional typed columns. |
| TMF634 `resourceSpecification` | `service_resource_design.resource_specification` | `/resourceSpecification`, `/resourceSpecification/{id}` | Common TMF metadata plus payload validation | Promote common TMF metadata; store resource-specific fields in tmf_payload until query patterns justify additional typed columns. |
| TMF730 `resource` | `service_resource_design.resource_specification` | `/resource`, `/resource/{id}` | `id`, `href`, `category`, `description`, `endOperatingDate`, `isDistributedCurrent`, `lastUpdate`, `name` | Promote common TMF lifecycle/reference fields; store remaining validated resource fields in tmf_payload and characteristics tables. |
| TMF730 `resourceSpecification` | `service_resource_design.resource_specification` | `/resourceSpecification`, `/resourceSpecification/{id}` | `id`, `href`, `buildNumber`, `category`, `description`, `isBundle`, `isDistributable`, `isExperimental` | Promote common TMF lifecycle/reference fields; store remaining validated resource fields in tmf_payload and characteristics tables. |
| TMF701 `processFlow` | `service_resource_design.service_specification` | `/processFlow`, `/processFlow/{id}`, `/processFlow/{processFlowId}/taskFlow` | `id`, `href`, `processFlowDate`, `processFlowSpecification`, `channel`, `characteristic`, `relatedEntity`, `relatedParty` | Promote common TMF lifecycle/reference fields; store remaining validated resource fields in tmf_payload and characteristics tables. |
| TMF645 `checkServiceQualification` | `service_resource_design.service_specification` | `/checkServiceQualification`, `/checkServiceQualification/{id}` | Common TMF metadata plus payload validation | Promote common TMF metadata; store resource-specific fields in tmf_payload until query patterns justify additional typed columns. |
| TMF645 `queryServiceQualification` | `service_resource_design.service_specification` | `/queryServiceQualification`, `/queryServiceQualification/{id}` | Common TMF metadata plus payload validation | Promote common TMF metadata; store resource-specific fields in tmf_payload until query patterns justify additional typed columns. |
| TMF679 `checkProductOfferingQualification` | `service_resource_design.service_specification` | `/checkProductOfferingQualification`, `/checkProductOfferingQualification/{id}` | Common TMF metadata plus payload validation | Promote common TMF metadata; store resource-specific fields in tmf_payload until query patterns justify additional typed columns. |
| TMF679 `queryProductOfferingQualification` | `service_resource_design.service_specification` | `/queryProductOfferingQualification`, `/queryProductOfferingQualification/{id}` | Common TMF metadata plus payload validation | Promote common TMF metadata; store resource-specific fields in tmf_payload until query patterns justify additional typed columns. |
| TMF662 `association` | `service_resource_design.entity_template` | `/association`, `/association/{id}` | `description`, `lastUpdate`, `lifecycleStatus`, `name`, `validFor`, `version`, `associationSpec`, `associationRole` | Promote common TMF lifecycle/reference fields; store remaining validated resource fields in tmf_payload and characteristics tables. |
| TMF662 `associationSpecification` | `service_resource_design.service_specification` | `/associationSpecification`, `/associationSpecification/{id}` | `description`, `lastUpdate`, `lifecycleStatus`, `name`, `validFor`, `version`, `constraint`, `associationRoleSpec` | Promote common TMF lifecycle/reference fields; store remaining validated resource fields in tmf_payload and characteristics tables. |
| TMF662 `entityCatalog` | `service_resource_design.entity_template` | `/entityCatalog`, `/entityCatalog/{id}` | `id`, `href`, `description`, `lastUpdate`, `lifecycleStatus`, `name`, `version`, `category` | Promote common TMF lifecycle/reference fields; store remaining validated resource fields in tmf_payload and characteristics tables. |
| TMF662 `entityCatalogItem` | `service_resource_design.entity_template` | `/entityCatalogItem`, `/entityCatalogItem/{id}` | `id`, `href`, `description`, `lastUpdate`, `lifecycleStatus`, `name`, `version`, `category` | Promote common TMF lifecycle/reference fields; store remaining validated resource fields in tmf_payload and characteristics tables. |
| TMF662 `entityCategory` | `service_resource_design.entity_template` | `/entityCategory`, `/entityCategory/{id}` | `id`, `href`, `description`, `isRoot`, `lastUpdate`, `lifecycleStatus`, `name`, `parentId` | Promote common TMF lifecycle/reference fields; store remaining validated resource fields in tmf_payload and characteristics tables. |
| TMF662 `entitySpecification` | `service_resource_design.entity_template` | `/entitySpecification`, `/entitySpecification/{id}` | `id`, `href`, `description`, `isBundle`, `lastUpdate`, `lifecycleStatus`, `name`, `version` | Promote common TMF lifecycle/reference fields; store remaining validated resource fields in tmf_payload and characteristics tables. |
| TMF662 `exportJob` | `service_resource_design.entity_template` | `/exportJob`, `/exportJob/{id}` | `id`, `href`, `completionDate`, `contentType`, `creationDate`, `errorLog`, `path`, `query` | Promote common TMF lifecycle/reference fields; store remaining validated resource fields in tmf_payload and characteristics tables. |
| TMF662 `importJob` | `service_resource_design.entity_template` | `/importJob`, `/importJob/{id}` | `id`, `href`, `completionDate`, `contentType`, `creationDate`, `errorLog`, `path`, `url` | Promote common TMF lifecycle/reference fields; store remaining validated resource fields in tmf_payload and characteristics tables. |

## V002 DDL Refinement

Migration: `database/postgres/suites/ts_oss_engineering_fulfillment/V004__refine_service_resource_design_tmf_core.sql`

The migration adds this implementation baseline for the app:

| Area | Decision |
| --- | --- |
| Common TMF fields | Add reusable typed columns such as `tmf_id`, `tmf_href`, `tmf_type`, `tmf_base_type`, `tmf_schema_location`, `tmf_referred_type`, `tmf_name`, `tmf_description`, `tmf_lifecycle_status`, `tmf_state`, dates, priority, and external ID to every V001 app table. |
| Full TMF compatibility | Keep the V001 `tmf_payload` column as the complete validated TMF resource snapshot for fields that are not yet promoted to typed columns. |
| Characteristics and references | Add normalized `tmf_characteristic`, `tmf_resource_reference`, `tmf_external_identifier`, `tmf_related_party`, `tmf_note`, `tmf_attachment`, and `tmf_relationship` support tables. |
| API/resource map | Add `tmf_api_resource_map` rows for the selected local TMF APIs and resource roots. |
| Event contracts | Add baseline event contract rows for create, update, state-change, and delete events per reviewed API resource. |
| Privacy and audit | Add table-level privacy, retention, legal-hold, residency, masking, and audit policy rows. |
| High-volume candidates | `service_resource_design.event_outbox` |

## Event Contract Baseline

Events are registered in `service_resource_design.event_contract` using `service_resource_design.event_outbox` as the publication basis. Consumers must be added when integrations are designed; no app should directly write another app schema.

## Privacy, Retention, And Audit Baseline

| Table | Data classification | Retention class | Audit level |
| --- | --- | --- | --- |
| `service_resource_design.service_specification` | internal | domain_lifecycle | standard |
| `service_resource_design.resource_specification` | internal | domain_lifecycle | standard |
| `service_resource_design.specification_version` | internal | domain_lifecycle | standard |
| `service_resource_design.realization_rule` | internal | domain_lifecycle | standard |
| `service_resource_design.technical_compatibility_rule` | internal | domain_lifecycle | standard |
| `service_resource_design.entity_template` | internal | domain_lifecycle | standard |
| `service_resource_design.event_outbox` | internal | operational_telemetry | standard |

## Build Gate Result

| Gate item | Result |
| --- | --- |
| API/resource review | Complete for baseline implementation |
| V002 typed DDL | Complete: `database/postgres/suites/ts_oss_engineering_fulfillment/V004__refine_service_resource_design_tmf_core.sql` |
| Event contract register | Baseline complete |
| Privacy/retention/audit classification | Baseline complete |
| Remaining implementation control | Validate exact endpoint operations and contract tests as Angular/Spring Boot features are built |
