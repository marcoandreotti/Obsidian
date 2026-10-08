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

## Regras propostas (não implementadas)

- [[Avaliação]]: nota inteira de 1 a 5 por alvo; **nota menor que 3 exige comentário** não vazio; uma avaliação por pedido e por alvo; alvo da mesma unidade; pedido precisa estar `Completed`.
- [[Classificação e Reputação]]: média, contagem e distribuição consideram apenas avaliações publicadas e não são editáveis por administrador.

Proposta do cofre registrada em 2026-10-07; nada disso é regra vigente até passar pelo fluxo OpenSpec do repositório.


