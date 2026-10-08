# Frontend - Guia do Agente

Leia `AGENTS.md`, `docs/web-design-system.md`, route/access existentes e módulo análogo antes de alterar. Estruture página/feature no `web/OrderHub.Web/src/modules/`; registre rota em `router/routes.ts` e acesso conforme `router/access.ts` quando necessário. Mantenha chamadas HTTP nos serviços/clientes de módulo via `src/http/client.ts`; use Pinia/composable conforme exemplos.

Siga as cinco superfícies (Public, Administration, Operations, KDS, Platform) e os quatro layouts existentes, tokens, temas, acessibilidade e componentes documentados. Não assumir componentes globais inexistentes. Trate erros no padrão local. SignalR atual é aviso de invalidação; recarregue dado via HTTP conforme fluxo implementado.

Fontes: `docs/web-design-system.md`, `web/OrderHub.Web/src/`, testes Vitest. Veja [[Rotas]], [[Componentes e Design System]], [[Comunicação com a API]], [[Stores e Estado]].




> Caminhos iniciados em `src/` nesta nota são relativos a `web/OrderHub.Web/`; por exemplo, `src/router/routes.ts` corresponde a `web/OrderHub.Web/src/router/routes.ts` a partir da raiz do repositório.

