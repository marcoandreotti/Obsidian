# Regras de Negócio

Regras pertencem ao Domain; validação de formato/estrutura de entrada ao FluentValidation. `AGENTS.md`, `openspec/conventions.md` e `architecture/solution-foundation` estabelecem esse limite.

Exemplos confirmados no domínio:

- isolamento Tenant/unidade atravessa entidades e operações: [[Multi-tenancy]].
- [[Pedido]] protege composição no Draft, total/snapshot comercial e transições válidas.
- [[Produto]] exige categoria/grupos da mesma unidade; [[Cliente]] é estabelecimento-scoped.
- `Money` não negativo/arredonda a 2 casas; `Quantity` positivo/arredonda a 3.
- [[Disponibilidade]] combina estado da unidade, exceções, pausas, fuso e horários.
- [[Cupom]] avalia validade/elegibilidade/limites; domínio do pedido registra snapshot do desconto.
- [[Pagamento]] tem idempotência e estado financeiro próprio.

Exemplo errado: validator/endpoint decide que pedido pode transicionar; correto: `Order.StartPreparation()`/transição do agregado impõe regra. Valide códigos exatos em model/spec; não derive regra nova desta lista.


