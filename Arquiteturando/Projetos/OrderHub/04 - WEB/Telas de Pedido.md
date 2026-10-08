# Telas de Pedido

Rotas: `web/OrderHub.Web/src/router/routes.ts`; shell Public em `src/layouts/PublicLayout.vue`.

- `/order/:slug` e `/order/:slug/table/:tableToken` → `modules/public-ordering/PublicOrderingPage.vue`.
- `/order/track/:reference` → `modules/public-ordering/TrackingPage.vue`.
- Avaliação do pedido concluído (proposta não implementada): `/order/review/:reference` → `modules/public-ordering/ReviewPage.vue`; detalhes em [[Telas de Avaliação]].
- Fluxo e módulos: `cart.ts`, `checkout.ts`, `client.ts`, `theme.ts`, `tracking.ts`; componentes vizinhos `PublicProductCard.vue`, `PublicCategoryNavigation.vue`, `PublicCartAccess.vue`.
- Operação: `modules/operations/orders/OrdersDashboardPage.vue`; KDS `modules/operations/kitchen/KitchenDisplayPage.vue`.

`docs/user-journeys.md` documenta jornada. `PRODUCT.md` registra que tela pública existe mas não foi testada pelo usuário. Isso é limite de validação, não evidência de defeito.

Relaciona: [[Pedido]], [[Fluxo de Pedido]], [[Endpoints de Pedido]], [[04 - WEB/Componentes e Design System|Design System]].




> Caminhos iniciados em `src/` nesta nota são relativos a `web/OrderHub.Web/`; por exemplo, `src/router/routes.ts` corresponde a `web/OrderHub.Web/src/router/routes.ts` a partir da raiz do repositório.

