# <span style="color: red;">Pedido</span>

Pedido é o agregado central do fluxo de venda. Código: `src/OrderHub.Domain/Ordering/Order.cs`; aplicação em `src/OrderHub.Application/Ordering/`; persistência em Infrastructure; rotas públicas e administrativas na API; interfaces em módulos WEB public-ordering e operations.

## Conceitos relacionados

[[Fluxo de Pedido]] · [[Entidades de Pedido]] · [[Regras de Pedido]] · [[Endpoints de Pedido]] · [[Telas de Pedido]] · [[Cliente]] · [[Produto]] · [[Disponibilidade]] · [[Pagamento]] · [[Região de Entrega]]

## Fatos observados

O pedido preserva snapshots relevantes de itens/preços e dados de entrega; alterações de itens estão limitadas a Draft; transições registram histórico. Estados encontrados: Draft, Confirmed, Preparing, Ready, OutForDelivery, Completed, Cancelled, Rejected. Tipos de serviço: Table, Pickup, Delivery. Confira spec `openspec/specs/ordering/order-management/spec.md` e testes antes de alterar; mudanças ativas podem complementar requisitos (ver [[10 - Evolução/Estado Atual|Estado Atual]]).

## Referências

Código: `src/OrderHub.Domain/Ordering/Order.cs`, `OrderItem.cs`, `OrderStatus.cs`; specs em `openspec/specs/ordering/`; testes `tests/OrderHub.Domain.Tests/Ordering/`, `tests/OrderHub.Application.Tests/Ordering/`, API/Integration tests de public ordering e operações; WEB `web/OrderHub.Web/src/modules/public-ordering/` e `modules/operations/orders/`.


