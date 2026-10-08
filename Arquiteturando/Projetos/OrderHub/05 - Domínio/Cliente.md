# Cliente

Registro de cliente é escopado ao estabelecimento e pode conter endereços usados em pedidos. Código: `src/OrderHub.Domain/Customers/`; aplicação/persistência em `src/OrderHub.Application/Customers/` e `src/OrderHub.Infrastructure/`; UI em `web/OrderHub.Web/src/modules/administration/customers/`.

Relaciona-se a [[Pedido]], [[Estabelecimento]] e, na proposta de [[Avaliação]], à referência pública do pedido como âncora da compra. Spec `openspec/specs/customers/customer-records/spec.md`; testes `CustomerApplicationTests`, `CustomerTests`, `CustomerPersistenceTests` e `customers.test.ts`. Não inferir que exista CRM externo; não identificado no repositório.


