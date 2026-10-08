# Serviços e Integrações

Não há diretório `services/` implementado: clients ficam dentro do módulo feature. Exemplos: administration catalog/users/availability/communications/customers/delivery/onboarding/payment-methods/reporting/coupons; operations orders/kitchen; platform; public-ordering.

Integrações Web: Axios client; SignalR client `@microsoft/signalr` no painel operacional; Quasar/Vue/Pinia; package inclui `qrcode`. API base vem de `VITE_API_BASE_URL`; realtime aceita `VITE_REALTIME_BASE_URL`.

SMTP e Meta WhatsApp são chamados no backend/Infrastructure, não no browser. PostgreSQL é persistência API. Nenhum provider externo de pagamento foi confirmado. Busca de CEP externa: BrasilAPI, em `web/OrderHub.Web/src/modules/public-ordering/PublicOrderingPage.vue` (fato observado no repositório: `https://brasilapi.com.br/api/cep/v1/{cep}`).

Evite segunda camada genérica de serviços sem convenção local ou necessidade. Referências: `web/OrderHub.Web/src/modules/*/client.ts`, `package.json`, `docs/notification-gateway.md`. Ver [[Infraestrutura]], [[Comunicação com a API]].


