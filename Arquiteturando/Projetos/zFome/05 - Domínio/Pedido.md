# Pedido

Pedido é o agregado central do fluxo de venda. Código: `src/ZFome.Domain/Ordering/Order.cs`; aplicação em `src/ZFome.Application/Ordering/`; persistência em Infrastructure; rotas públicas e administrativas na API; interfaces em módulos WEB public-ordering e operations.

## Conceitos relacionados

[[Fluxo de Pedido]] · [[Entidades de Pedido]] · [[Regras de Pedido]] · [[Endpoints de Pedido]] · [[Telas de Pedido]] · [[Cliente]] · [[Produto]] · [[Disponibilidade]] · [[Pagamento]] · [[Região de Entrega]]

## Fatos observados

O pedido preserva snapshots relevantes de itens/preços e dados de entrega; alterações de itens estão limitadas a Draft; transições registram histórico. Estados encontrados: Draft, Confirmed, Preparing, Ready, OutForDelivery, Completed, Cancelled, Rejected. Tipos de serviço: Table, Pickup, Delivery. Confira spec `openspec/specs/ordering/order-management/spec.md` e testes antes de alterar; mudanças ativas podem complementar requisitos (ver [[10 - Evolução/Estado Atual|Estado Atual]]).

## Referências

Código: `src/ZFome.Domain/Ordering/Order.cs` (que declara `Order`, `OrderItem` e o enum `OrderStatus`); specs em `openspec/specs/ordering/`; testes `tests/ZFome.Domain.Tests/Ordering/`, `tests/ZFome.Application.Tests/Ordering/`, API/Integration tests de public ordering e operações; WEB `web/ZFome.Web/src/modules/public-ordering/` e `modules/operations/orders/`.


