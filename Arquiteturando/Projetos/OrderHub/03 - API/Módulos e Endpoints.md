# Módulos e Endpoints

`Program.cs` registra Catalog, PublicOrdering, Administration, Onboarding, Administrative Users, Authentication, Platform Provisioning e hub SignalR. Cada módulo encaminha contratos a dispatchers Application.

| Área | Rota base | Código / acesso |
|---|---|---|
| Auth | `/api/auth` | `Authentication/AuthenticationEndpoints.cs`; begin/complete limitados. |
| Admin | `/api/admin/establishments/{establishmentId}` | `Administration/AdministrationEndpoints.cs`; policies por grupo. |
| Usuários | `.../{establishmentId}/users` | `Administration/AdministrativeUserEndpoints.cs`. |
| Configuração | mesmo prefixo: `/onboarding`, `/configuration`, `/theme`, `/business-hours`, `/tables`, `/availability/*` | `Administration/OnboardingEndpoints.cs`. |
| Catálogo admin | `.../{establishmentId}/catalog` | `Catalog/CatalogEndpoints.cs`, Management. Público: `/api/public/establishments/{slug}/catalog`. |
| Pedido público | `/api/public/ordering` | `/context`, `/schedule-slots`, `/customers`, `/simulate`, `/orders`, `/orders/{reference}`. Anônimo. |
| Platform | `/api/platform/tenants` | `Platform/PlatformProvisioningEndpoints.cs`, identidade global. |
| Notifications | `.../{establishmentId}/communications` | `Administration/NotificationEndpoints.cs`, Management. |
| Avaliações (proposto) | `/api/public/ordering/orders/{reference}/reviews`, `/api/public/establishments/{slug}/reviews`, `/api/admin/establishments/{establishmentId}/reviews` | **Não implementado**; desenho em [[Endpoints de Avaliação]]. |
| Realtime | `/hubs/order-updates` | `Program.cs`, OrderRead auth; subscription valida escopo. |

Admin subgrupos incluem reports/dashboard, order-scheduling, delivery-regions, customers, orders, coupons, payment-methods e payments. Consulte rota e response concreta antes de mudar cliente/contrato. Ver [[Endpoints de Pedido]], [[03 - API/Autenticação e Autorização|Autenticação]].


