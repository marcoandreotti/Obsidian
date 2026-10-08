# Avaliação

> **Estado:** proposta do cofre, **não implementada**. Verificado no checkout `6384863` (2026-10-07): não existe entidade, tabela, contrato, endpoint, VO `Rating` nem spec de avaliação em `src/`, `tests/` ou `openspec/specs/`. Regra central e jornada em [[Avaliações e Classificação]].

Registro pelo qual o consumidor que concluiu um pedido atribui **nota de 1 a 5** ao **estabelecimento** e aos **produtos** comprados, com **comentário obrigatório quando a nota é menor que 3**.

**Arquivo proposto:** `src/OrderHub.Domain/Reviews/Review.cs` · **Classe proposta:** `Review` (agregado raiz), no novo módulo de domínio `Reviews/`, ao lado de `Catalog/`, `Ordering/`, `Promotions/`. Escopo: `IEstablishmentScopedEntity` (`TenantId` + `EstablishmentId`), como `Product` e `Order` — ver [[Multi-tenancy]] e [[Entidades]].

## Por que um módulo novo

O módulo `Reviews/` não existe hoje; a proposta segue a organização atual (`src/OrderHub.Domain/<Módulo>/`). Alternativas consideradas: acrescentar a avaliação ao agregado `Order` (rejeitada: pedido é imutável após confirmação e não deve crescer com opinião do consumidor) e anexar ao `Catalog` (rejeitada: avaliação de produto depende de pedido, não de catálogo, e a de estabelecimento não é catálogo).

## Campos propostos

`Id` (Guid, `ValueGeneratedNever`, como as demais PKs), `TenantId`, `EstablishmentId`, `OrderId`, `OrderPublicReference`, `TargetKind` (`Establishment|Product`), `TargetId`, `Rating`, `Comment`, `AuthorCustomerId` (opcional), `Status` (`Published|Hidden`), `CreatedAt`, `UpdatedAt`, `EditedAt` (opcional), `ModerationReason` (opcional).

## Invariantes propostas (Domain)

Regra de negócio pertence ao domínio ([[Regras de Negócio]]); o repositório usa `DomainException` para invariante violada, com mensagem em inglês — ver `src/OrderHub.Domain/Exceptions/DomainException.cs`.

1. `Rating` é **inteiro de 1 a 5**; 0, 6, negativo ou fracionado são inválidos.
2. **Nota menor que 3 exige comentário** não vazio após normalização. Mensagem proposta: `Comment is required for ratings below 3.`
3. Comentário, quando presente, tem no máximo 1000 caracteres; quando obrigatório, no mínimo 10.
4. `TargetKind = Product` exige `TargetId` de produto da **mesma unidade e tenant** do pedido.
5. Pedido precisa estar `Completed` (`OrderStatus`); ver [[Fluxo de Pedido]].
6. Existe **no máximo uma avaliação por pedido e por alvo**; nova tentativa é conflito, não sobrescrita.
7. Administrador não altera nota nem exclui o registro: oculta com motivo e o registro permanece auditável.
8. `PublicReference` do pedido é a âncora pública (48 hex gerados em `Order.Confirm`), nunca o `Id` interno.

## Value object proposto

`Rating` (ex.: `readonly record struct Rating` com `Value` e `RequiresComment => Value < 3`), validado na criação. Observação de precedente: hoje os únicos VOs de valor são `Money`, `Quantity` (`src/OrderHub.Domain/SharedKernel/`), `Slug` (`Tenancy/`) e `Email` (`Identity/`); **não há VO numérico com faixa**. Alternativa a decidir: manter `int` com `HasCheckConstraint` no mapeamento EF e validação no agregado.

`Comment` pode permanecer `string?` com normalização no agregado; um VO próprio só se a regra crescer (ex.: filtro de conteúdo).

## Onde a regra roda

- **Domain:** nota, obrigatoriedade condicional do comentário, tamanho, coerência de escopo (`TenantId`/`EstablishmentId` iguais aos do alvo) e unicidade por alvo no agregado.
- **Application:** carrega o pedido pela referência pública, confirma `Completed` e que os alvos enviados **constam no pedido**; a pertinência ao pedido é decisão de caso de uso porque cruza agregados — o domínio não acessa `Ordering/`.
- **FluentValidation:** formato da entrada (nota presente e inteira, tamanho do texto, referência com 48 hex), como formato e não como regra. O repositório já usa validação condicional (`.When(...)`) em `PublicOrderingValidators.cs` — ver [[Validações]].

## Estado e ciclo de vida propostos

`Published` → `Hidden` (moderação, com `ModerationReason`) → `Published` (restauração). Ocultação altera a exibição pública e o cálculo de [[Classificação e Reputação]]; não apaga dado. Edição pelo autor dentro da janela proposta (7 dias) atualiza `EditedAt` e preserva histórico de moderação. Prazos de retenção e anonimização são **A confirmar** (LGPD).

## Eventos propostos

`ReviewPublished`, `ReviewUpdated`, `ReviewHidden`, `ReviewRestored` publicados via outbox (`[[ADR-003 - Transactional Outbox]]`) para atualizar o sumário de classificação. Alternativa: recalcular de forma síncrona na mesma transação. Decisão pendente — ver [[Proposta - Avaliações e Classificação]].

## Testes propostos

`tests/OrderHub.Domain.Tests/Reviews/ReviewTests.cs` (nota fora da faixa, comentário obrigatório ausente, alvo de outra unidade, segunda avaliação no mesmo alvo), `tests/OrderHub.Application.Tests/Reviews/` (pedido não concluído, alvo fora do pedido) e `tests/OrderHub.Integration.Tests/Reviews/` (unicidade, isolamento por unidade, idempotência).

## Relacionados

[[Classificação e Reputação]] · [[Avaliações e Classificação]] · [[Endpoints de Avaliação]] · [[Telas de Avaliação]] · [[Pedido]] · [[Produto]] · [[Estabelecimento]] · [[Cliente]] · [[Entidades de Pedido]] · [[Regras de Negócio]] · [[Multi-tenancy]]
