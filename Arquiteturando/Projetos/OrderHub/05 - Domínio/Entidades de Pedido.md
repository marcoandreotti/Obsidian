# Entidades de Pedido

Inventário inicial, baseado em `src/OrderHub.Domain/Ordering/` e arquivos em `Catalog`, `Customers`, `Payments` e `Delivery`:

- `Order`: agregado; status, serviço, cliente/endereço, linhas, histórico e snapshots.
- `OrderItem`: linha e escolhas de catálogo associadas.
- Value objects/enums e tipos de suporte: inspecionar pasta Ordering para nomes atuais antes de referenciar em alteração.
- Pagamento, cupom, região e produto têm modelos/contextos próprios; não são automaticamente parte do agregado Order.

Specs: ordering/order-management, order-scheduling, payments/order-payments, promotions/coupon-management. Relacionado: [[Pedido]], [[Produto]], [[Cliente]], [[Pagamento]], [[Cupom]]. Consulte modelo e migrations antes de supor cardinalidade.


