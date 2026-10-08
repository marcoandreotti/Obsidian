# Contextos de Negócio

Mapa de capability → spec → implementation/test references. A presença de classe/teste não prova todos os requisitos concluídos.

| Contexto | Spec(s) | Código e testes encontrados |
|---|---|---|
| Foundation/persistence | `architecture/solution-foundation`; `persistence/core-postgresql-schema` | `src/OrderHub.*`; tests `ArchitectureDependencyTests`, `ApiFoundationTests`, `PostgreSqlPersistenceTests`, `ModelConventionsTests`. |
| Tenancy/onboarding/platform | `tenancy/establishment-management`, `establishment-onboarding`, `platform-tenant-provisioning` | Domain `Tenancy/`; Application Tenancy; API Platform; Web onboarding/platform; tests `TenantTests`, `OnboardingTests`, `OnboardingApiTests`, PlatformProvisioning*, Tenancy*. |
| Identity/admin | `identity/administrative-authentication`, `administrative-users`; `administration/administration-api` | Domain Identity, API Authentication/Admin, Web session/users; tests auth/user mgmt/context/persistence. |
| Catalog | `catalog/product-catalog`; `administration/administration-web` | Domain/Application Catalog, API Catalog, Web administration/catalog & public ordering; Catalog application/API/persistence/domain tests, Web catalog tests. |
| Customers | `customers/customer-records` | Domain Customers, Application/Infrastructure Customers, Web administration/customers; `CustomerApplicationTests`, `CustomerTests`, `CustomerPersistenceTests`, `customers.test.ts`. |
| Service configuration | `operations/service-configuration`; `tenancy/establishment-onboarding` | Domain Operations, Application Availability, API onboarding, Web availability; `OperationsTests`, `availability.test.ts`. |
| Orders/scheduling/public | `ordering/order-management`, `order-scheduling`, `public-ordering-api`, `public-ordering-web` | Domain Ordering; Application Ordering/PublicOrdering; API PublicOrdering/Admin; Web public-ordering/operations; Order, PublicOrdering and scheduling tests .NET/Web. |
| Operations/KDS/realtime | `operations/order-operations-dashboard`, `kitchen-display-system`, `realtime-order-updates` | API Realtime/Admin, Infrastructure read gateways, Web operations/orders/kitchen; OperationsPersistence, KitchenDisplayEndToEnd, RealtimeOrderNotification + Web tests. |
| Delivery | `delivery/delivery-management` | Domain Delivery, app/infra Delivery, Web admin/delivery; `DeliveryRegionTests`. Persistence-specific delivery test name: **Não identificado no repositório**. |
| Payments | `payments/order-payments` | Domain/Application Payments, Infrastructure read/write, Web payment-methods; Payment application/domain/persistence + promotions-payments Web tests. |
| Promotions | `promotions/coupon-management` | Domain/Application Promotions, Web coupons; Coupon application/domain/persistence + promotions-payments Web tests. |
| Reporting | `reporting/business-dashboard` | Application Reporting, `BusinessDashboardReadGateway`, Web reporting; `BusinessDashboardValidationTests`, `BusinessDashboardReportingTests`. |
| Communications/outbox | `communications/notification-gateway`, `customer-order-notifications`; `architecture/transactional-outbox` | Application Communications, Infrastructure/Outbox/worker, Web communications; Notification validation/gateway/provider and outbox integration tests. |
| Avaliações e classificação (proposta) | capability nova `reviews/customer-reviews`; **não implementada** | [[Avaliação]], [[Classificação e Reputação]], [[Endpoints de Avaliação]], [[Telas de Avaliação]]; nenhum código/spec existe no checkout `6384863`. |
| Web conventions | `openspec/specs/web/action-controls/spec.md`, `openspec/specs/web/appearance-preferences/spec.md` | Quasar components/themes; Web layout/navigation/page tests; `docs/web-design-system.md`. |

Paths completos das specs começam `openspec/specs/<context>/<capability>/spec.md`; tabela usa sufixo para legibilidade. Para endpoint/page files, ver [[03 - API/Módulos e Endpoints|API]] e [[04 - WEB/Rotas|Rotas]]. O teste real de entrega encontrado é `tests/OrderHub.Domain.Tests/Delivery/DeliveryRegionTests.cs`.

Changes em andamento: [[10 - Evolução/Estado Atual|Estado Atual]].


