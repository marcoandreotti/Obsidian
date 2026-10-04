# Rotas

Fonte `web/OrderHub.Web/src/router/routes.ts`, guard `src/router/access.ts`. Rotas importam páginas lazy sob layouts.

| URL | Página/superfície | Guard declarado |
|---|---|---|
| `/order/track/:reference` | Public / TrackingPage | público |
| `/order/:slug`, `/order/:slug/table/:tableToken` | Public / PublicOrderingPage | público |
| `/login`, `/access-denied`, `/` | Public shell / session ou FoundationPage | público |
| `/change-password` | ChangePasswordPage | requiresSession |
| `/platform` | PlatformTenantsPage | requiresSession + platformOnly |
| `/operations` | OrdersDashboardPage | `order-read` |
| `/operations/kitchen` | KitchenDisplayPage | `order-kitchen` |
| `/operations/delivery` | OrdersDashboardPage | `order-delivery` |
| `/administration` | HomePage | `management` |
| `/administration/onboarding/:step?`, `/users` | OnboardingPage, UsersPage | `administration` |
| `/administration/catalog`, `/delivery-regions` | CatalogPage, DeliveryRegionsPage | `management` |
| `/administration/availability` | AvailabilityPage | `administration` |
| `/administration/customers` | CustomersPage | `customer-operations` |
| `/administration/coupons`, `/payment-methods` | CouponsPage, PaymentMethodsPage | promotion/payment-management |
| `/administration/communications` | CommunicationsPage | `management` |

Rota `/administration/foundation` existe. Guard hidrata session context e redireciona; código comenta que autorização efetiva continua servidor. `docs/user-journeys.md` cobre navegação por perfil. Ver [[Telas de Pedido]], [[Autenticação e Autorização]].




> Caminhos iniciados em `src/` nesta nota são relativos a `web/OrderHub.Web/`; por exemplo, `src/router/routes.ts` corresponde a `web/OrderHub.Web/src/router/routes.ts` a partir da raiz do repositório.

