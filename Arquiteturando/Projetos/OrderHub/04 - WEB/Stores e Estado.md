# Stores e Estado

Pinia está em `package.json`; estado observado é feature-scoped:

- `modules/session/store.ts`: consulta `/api/auth/context`, contexto de sessão, unidade selecionada e revisão. `sessionStorage` mantém `oh-unit`, revalidado com resposta do servidor; cookies de sessão não são lidos pelo JS (`docs/administration-web-foundation.md`).
- `modules/operations/orders/store.ts`: fila operacional e coordenação com polling/realtime.
- `modules/operations/kitchen/store.ts`: fila KDS.
- `modules/platform/store.ts`: estado da área Platform.
- `modules/public-ordering/cart.ts`: carrinho por slug/local persistence; é intenção, não autoridade de preço.

Helpers de domínio UI em `modules/operations/orders/{actions,board,polling,realtime}.ts` e `modules/public-ordering/{cart,checkout,tracking}.ts`. `src/stores/` e `src/composables/` só têm `.gitkeep`; store/composable global implementado **Não identificado no repositório**.

Antes de criar estado novo, procure módulo equivalente. Não confie em carrinho/cache para autorização, preço, disponibilidade ou transições. Ver [[04 - WEB/Estrutura Frontend|Estrutura Frontend]], [[Comunicação com a API]].




> Caminhos iniciados em `src/` nesta nota são relativos a `web/OrderHub.Web/`; por exemplo, `src/router/routes.ts` corresponde a `web/OrderHub.Web/src/router/routes.ts` a partir da raiz do repositório.

