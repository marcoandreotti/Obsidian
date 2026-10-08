# Padrões de Frontend

Vue 3 + TypeScript + Quasar. Rotas explicitadas em `src/router/routes.ts`, controle de acesso em `router/access.ts`; páginas e componentes pertencem aos módulos de feature. HTTP via `src/http/client.ts` e clientes locais às features; estado durável de sessão no Pinia. SignalR é sinal de invalidação; HTTP continua fonte de leitura.

Design System em `docs/web-design-system.md`: tokens em `src/themes/_tokens.scss`, aparência e superfícies distintas (pública do tenant, administração/operação, plataforma). Reutilizar componentes compartilhados existentes e padrões por feature. Evitar criar componente genérico global sem necessidade/sem seguir DS; não inventar APIs de componente ausentes.

Referências: [[Estrutura Frontend]], [[Rotas]], [[Componentes e Design System]], [[Stores e Estado]], [[Comunicação com a API]].




> Caminhos iniciados em `src/` nesta nota são relativos a `web/OrderHub.Web/`; por exemplo, `src/router/routes.ts` corresponde a `web/OrderHub.Web/src/router/routes.ts` a partir da raiz do repositório.

