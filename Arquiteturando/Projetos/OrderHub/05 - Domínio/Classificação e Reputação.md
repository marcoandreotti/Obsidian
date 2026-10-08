# Classificação e Reputação

> **Estado:** proposta do cofre, **não implementada**. Verificado no checkout `6384863` (2026-10-07): não existe coluna, tabela, read model ou campo de média/contagem de avaliação em `src/` nem em `openspec/specs/`.

Classificação é a **agregação das avaliações publicadas** de um alvo — estabelecimento ou produto — em média, contagem e distribuição por nota. Reputação é o uso dessa classificação na exibição pública; nenhum dos dois altera estado operacional do pedido. Regra de origem em [[Avaliação]].

## Estrutura proposta

`RatingSummary` derivado, com dois níveis:

| Alvo | Chave proposta | Conteúdo |
|---|---|---|
| Estabelecimento | `(EstablishmentId)` | média, contagem, distribuição 1–5 |
| Produto | `(EstablishmentId, ProductId)` | média, contagem, distribuição 1–5 |

Proposta de persistência: tabela `reviews.rating_summary` (schema novo `reviews`, ao lado de `catalog`, `orders`, `customers` em `src/OrderHub.Infrastructure/Persistence/DatabaseSchemas.cs`), média com precisão 2 casas e distribuição em cinco contadores. Escrita por EF Core e leitura por Dapper, respeitando a divisão vigente (`openspec/conventions.md`) — ver [[Persistência]].

## Regras propostas

- Somente avaliações `Published` entram no cálculo; ocultar remove do cálculo e restaurar devolve.
- Média e contagem **não são editáveis** por administrador em nenhuma superfície.
- Produto sem avaliação publicada aparece **sem média** — não aparece com nota zero nem com "0 de 5".
- Contagem e média são do par (unidade, produto): a mesma nota não transborda para outra unidade nem para o produto em outro tenant.
- Mínimo de avaliações para exibir média pública, arredondamento exibido e destaque de "melhor avaliado" são **A confirmar**.

## Consistência

Duas opções, com trade-off explícito:

1. **Síncrona (proposta padrão):** o handler que publica a avaliação recalcula o sumário na mesma transação. Simples de raciocinar; mantém leitura imediatamente coerente.
2. **Por evento:** `ReviewPublished`/`ReviewHidden` via outbox atualizam o sumário de forma eventual ([[ADR-003 - Transactional Outbox]]). Menos acoplamento na escrita, porém a média pública pode ficar defasada por instantes e exige idempotência no consumidor.

Se a opção 2 for escolhida, o comportamento observável (quanto tempo a média demora a refletir) precisa constar da spec.

## Exibição pública

- Página do estabelecimento (`/order/:slug`): média, contagem e distribuição no contexto da unidade.
- Catálogo: média e contagem por produto no cartão e no detalhe.
- A média por produto deve vir **no mesmo read model** do catálogo público (`CatalogReadGateway.GetPublicAsync`, Dapper) ou em consulta agregada equivalente; calcular por produto em requisição separada criaria N+1 no cardápio.
- Lista textual de comentários publicados e paginação: ver [[Telas de Avaliação]].

## Reputação não é estado operacional

Nota baixa **não** cancela, bloqueia nem reclassifica pedido, produto ou unidade; nenhuma transição de `OrderStatus` depende de classificação. Ganchos automáticos (ex.: desativar produto com média baixa) **não** fazem parte da proposta.

## Relacionados

[[Avaliação]] · [[Avaliações e Classificação]] · [[Endpoints de Avaliação]] · [[Telas de Avaliação]] · [[Produto]] · [[Estabelecimento]] · [[Persistência]] · [[Multi-tenancy]] · [[ADR-003 - Transactional Outbox]]
