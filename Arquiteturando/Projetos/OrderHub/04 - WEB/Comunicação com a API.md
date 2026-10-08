# Comunicação com a API

`src/http/client.ts` cria Axios com `withCredentials`; injeta `X-Correlation-ID` e `X-CSRF-Token`; bloqueia respostas de revisão de sessão obsoleta; coordena refresh de 401 concorrente e repete uma vez quando permitido. `ApiError` interpreta ProblemDetails/erros de campo. `boot/http.ts` liga hooks de sessão e roteador.

Clients de feature constroem rotas conforme unidade ou contexto (Public/Platform). `establishmentId` na URL não autoriza acesso; API valida principal/policy/unidade. Sessão usa cookies; mutações precisam CSRF; CORS/origem/credentials devem alinhar deployment.

Operations usa SignalR `/hubs/order-updates`; evento V1 é aviso/invalidação, query HTTP continua autoritativa. Reconexão recarrega snapshot; polling com backoff é fallback, pausa em tab oculta. Nginx encaminha WebSocket `/hubs/`; Quasar dev configura proxy.

Refs: `src/http/client.ts`, `boot/http.ts`, `modules/session/store.ts`, `modules/operations/orders/realtime.ts`, `docs/realtime-order-notifications.md`. Ver [[Endpoints de Pedido]], [[Autenticação e Autorização]].




> Caminhos iniciados em `src/` nesta nota são relativos a `web/OrderHub.Web/`; por exemplo, `src/router/routes.ts` corresponde a `web/OrderHub.Web/src/router/routes.ts` a partir da raiz do repositório.

