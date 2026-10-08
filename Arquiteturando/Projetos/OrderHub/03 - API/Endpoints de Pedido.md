# Endpoints de Pedido

Fontes: `src/OrderHub.Api/PublicOrdering/PublicOrderingEndpoints.cs`, `Administration/AdministrationEndpoints.cs`, `Realtime/OrderUpdatesHub.cs`; specs Ordering/Operations.

## Público — anônimo

Prefixo `/api/public/ordering`: `GET /{slug}/context`, `GET /{slug}/schedule-slots`; `POST /{slug}/customers`, `POST /{slug}/simulate`, `POST /{slug}/orders`; `GET /orders/{reference}` e `POST /orders/{reference}/cancel`. Confirmação usa `Idempotency-Key`. Catálogo público: `GET /api/public/establishments/{slug}/catalog`.

API resolve unidade e cálculos comerciais; não usa preço do cliente como autoridade. Referência pública opaca, sem ID interno. Ver [[Fluxo de Pedido]], [[Pedido]].

## Administração/operação — sessão e escopo

Prefixo `/api/admin/establishments/{establishmentId}`: leitura `/orders`, `/orders/{orderId}`, `/kitchen`; mutações POST `/orders/{orderId}/prepare|ready|dispatch|complete|cancel|reject` com policy por ação. Scheduling, delivery, reports, coupons, payment methods e payments são subgrupos.

Avaliação de pedido concluído (nota 1–5, comentário obrigatório abaixo de 3) é proposta **não implementada**: [[Endpoints de Avaliação]].

Hub `/hubs/order-updates`: inscrição `SubscribeAsync(establishmentId)`, evento `OrderUpdated` V1. Evento informa mudança, não é estado autoritativo; query HTTP recompõe snapshot.

Specs: `openspec/specs/ordering/{order-management,public-ordering-api,public-ordering-web}`, `operations/{order-operations-dashboard,realtime-order-updates}`. Testes: `tests/OrderHub.Integration.Tests/{PublicOrderingApiTests,PublicOrderingPersistenceTests,OrderPersistenceTests,RealtimeOrderNotificationTests}.cs`.


