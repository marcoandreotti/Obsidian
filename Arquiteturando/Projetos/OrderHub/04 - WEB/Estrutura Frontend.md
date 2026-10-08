# Estrutura Frontend

Modelo de execução/estudo: Router lazy → route guard → layout de superfície → page/module → componentes e client/store locais → `boot/http.ts` / `http/client.ts` → API. Confirme imports reais da feature antes de alterar.

- `src/router/`: routes/access/index.
- `src/layouts/`: Public, Administration, Operations, Platform.
- `src/modules/administration/`: onboarding, users, catalog, availability, delivery, customers, coupons, payment methods, communications, reporting.
- `src/modules/operations/`: orders (actions/board/client/polling/realtime/store/types), kitchen (client/store/types/components).
- `src/modules/public-ordering/`: cart, checkout, client, theme, tracking, pages/components.
- `src/modules/session/`, `platform/`: sessão e provisionamento global.
- `src/components/`, `themes/`, `css/`: elementos shared/visual.

Feature clients/stores permanecem próximos às páginas. `composables/`, `services/`, `stores/`, `models/`, `modules/auth/`, `modules/public-menu/` contêm `.gitkeep`; camada efetiva futura ali **Não identificada no repositório**. Evite regra comercial autoritativa em view e camada de serviço/estado global presumida. Fonte visual: `docs/web-design-system.md`.

Relaciona: [[04 - WEB/WEB|WEB]], [[04 - WEB/Rotas|Rotas]], [[04 - WEB/Stores e Estado|Stores e Estado]], [[04 - WEB/Comunicação com a API|Comunicação com a API]], [[04 - WEB/Componentes e Design System|Design System]], [[Padrões de Frontend]].




> Caminhos iniciados em `src/` nesta nota são relativos a `web/OrderHub.Web/`; por exemplo, `src/router/routes.ts` corresponde a `web/OrderHub.Web/src/router/routes.ts` a partir da raiz do repositório.

