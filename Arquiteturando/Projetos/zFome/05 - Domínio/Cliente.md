# Cliente

Registro de cliente é escopado ao estabelecimento e pode conter endereços usados em pedidos. Código: `src/ZFome.Domain/Customers/`; aplicação/persistência em `src/ZFome.Application/Customers/` e `src/ZFome.Infrastructure/`; UI em `web/ZFome.Web/src/modules/administration/customers/`.

Relaciona-se a [[Pedido]], [[Estabelecimento]] e, na proposta de [[Avaliação]], à referência pública do pedido como âncora da compra. Spec `openspec/specs/customers/customer-records/spec.md`; testes `CustomerApplicationTests`, `CustomerTests`, `CustomerPersistenceTests` e `customers.test.ts`. Não inferir que exista CRM externo; não identificado no repositório.



Relacionado: [[Fidelidade]] — ideia de status atribuído pelo restaurante; escopo e implementação ainda não definidos.
