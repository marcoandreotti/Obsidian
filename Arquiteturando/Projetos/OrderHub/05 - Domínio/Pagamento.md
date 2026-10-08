# Pagamento

O projeto modela métodos e operações/estados de pagamento associados a pedidos. Domínio e aplicação: `src/OrderHub.Domain/Payments/`, `src/OrderHub.Application/Payments/`; infraestrutura read/write; configurações WEB em `modules/administration/payment-methods/`.

Spec `openspec/specs/payments/order-payments/spec.md`. Testes de domínio, aplicação e persistência foram identificados. Configurar meios de pagamento não prova processamento online: provedor de pagamento externo **Não identificado no repositório**.

Relaciona-se a [[Pedido]], [[Estabelecimento]] e [[Fluxo de Pedido]].


