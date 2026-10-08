# Telas de Avaliação

> **Estado:** proposta do cofre, **não implementada**. Verificado no checkout `6384863` (2026-10-07): `web/OrderHub.Web/src/modules/public-ordering/` tem 13 arquivos e nenhum componente, tipo ou chamada de avaliação/estrela; o Design System não possui componente de nota.

Contexto atual relevante: a jornada pública vive em **uma página** (`PublicOrderingPage.vue`) com máquina de estados `catalog → cart → checkout → receipt`, sem store Pinia — o carrinho é estado reativo de módulo com `localStorage` versionado por slug. Rotas públicas (`/order/:slug`, `/order/:slug/table/:tableToken`, `/order/track/:reference`) não têm `meta` nem guard. Ver [[Telas de Pedido]], [[Rotas]] e [[Estrutura Frontend]].

## Superfície pública (proposta)

| Onde | O quê |
|---|---|
| `TrackingPage.vue` (`/order/track/:reference`) | Bloco "Avaliar pedido" exibido quando o status é `Completed`; some nos demais estados, inclusive `Cancelled`/`Rejected`. |
| Nova `ReviewPage.vue` em `modules/public-ordering/` | Nota e comentário do estabelecimento + de cada produto do pedido; rota proposta `/order/review/:reference`, público e sem `meta` (coerente com as rotas públicas atuais). |
| `PublicUnitContext.vue` | Média e contagem da unidade no contexto público. |
| `PublicProductCard.vue` / detalhe do produto | Média e contagem do produto no cartão; sem média quando não há avaliação publicada. |
| `PublicOrderingPage.vue` (opcional) | Seção/rota `/order/:slug/reviews` com comentários publicados da unidade. |

Alternativa ao `ReviewPage.vue`: `q-dialog` dentro de `TrackingPage.vue`, como já ocorre na composição de produto em `PublicOrderingPage.vue`. Página dedicada foi a preferida por permitir link compartilhável e recarregamento; decisão final **A confirmar**.

## Componentes propostos

`PublicRatingStars.vue` (exibição de média) e `PublicRatingInput.vue` (entrada 1–5) em `modules/public-ordering/`, construídos sobre Quasar (`q-rating`, `q-input`, `q-banner`, `q-btn`) e tokens de tema. O Design System hoje expõe apenas `ProblemBanner.vue` e `AppearanceControl.vue`, e `docs/web-design-system.md` declara a inexistência de componentes oficiais como `AppButton`/`AppCard`/`AppDialog` — **não inventar biblioteca nova**: ver [[Componentes e Design System]].

Requisitos de interface propostos:

- Comentário obrigatório aparece **no momento em que a nota 1 ou 2 é escolhida**, com o motivo textual (não apenas campo em vermelho).
- Nota não enviada como ausente silenciosamente: envio com alvo sem nota é bloqueado com mensagem por alvo.
- Erro do servidor exibido com `ProblemDetails` traduzido (`ProblemBanner`), sem perder o texto digitado.
- Estados de carregamento, vazio ("ainda sem avaliações") e envio em andamento; envio repetido reutiliza a `Idempotency-Key` até haver mudança material, como no checkout.

## Acessibilidade

Rótulo por estrela (`aria-label="Nota 3 de 5"`), operação por teclado, texto equivalente à nota numérica, `role="alert"` para a exigência de comentário e contraste conforme tema público. Ver [[Padrões de Frontend]].

## Administração (proposta)

`modules/administration/reviews/ReviewsPage.vue` na rota `/administration/reviews` com `meta.capability: 'management'` (padrão das rotas administrativas): lista paginada, filtro por nota/período/estado, distribuição da unidade, ocultar e restaurar **com motivo obrigatório**. Sem edição de nota e sem exclusão — ver [[Avaliação]].

## Integração e dados

- Estender `modules/public-ordering/client.ts` e `types.ts`; **não há tipos gerados de API** no projeto, os tipos são escritos à mão por módulo.
- Cliente público é instância axios própria (sem `withCredentials`, CSRF injetado se o cookie existir) — manter esse isolamento e não transportar `TenantId`/`EstablishmentId` do cliente, como já ocorre hoje.
- Ver [[Comunicação com a API]] e [[Serviços e Integrações]].

## Testes propostos

`web/OrderHub.Web/tests/public-ordering-reviews.test.ts` (nota < 3 exige comentário; envio idempotente; sem média quando não há avaliação) e `tests/administration-reviews.test.ts` (ocultar com motivo). Padrão Vitest com `@vue/test-utils`, nomes kebab-case, executado por `npm run test` e `npm run typecheck` em `web/OrderHub.Web/`.

## Limites

`PRODUCT.md` registra que a superfície pública ainda não foi validada por usuário real; não existe script de verificação em navegador para a superfície pública, ao contrário da administração e do KDS. Isso é limite de validação, não defeito.

## Relacionados

[[Avaliações e Classificação]] · [[Avaliação]] · [[Classificação e Reputação]] · [[Endpoints de Avaliação]] · [[Telas de Pedido]] · [[Rotas]] · [[Componentes e Design System]] · [[Padrões de Frontend]]
