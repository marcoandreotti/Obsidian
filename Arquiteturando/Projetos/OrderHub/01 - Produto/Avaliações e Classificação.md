# Avaliações e Classificação

> **Estado:** proposta do cofre, **não implementada**. Verificado no checkout `6384863` (2026-10-07): não foram encontrados código, tabela, endpoint ou tela de avaliação/rating/review/estrelas em `src/` nem `web/`, e nenhuma spec em `openspec/specs/`. Nada nesta nota é requisito vigente.

O **usuário público** que concluiu um pedido avalia o **estabelecimento** e os **produtos** comprados com nota de **1 a 5**. Regra central proposta: **nota menor que 3 exige comentário**; notas 3, 4 e 5 dispensam comentário.

## Regra central

| Nota | Comentário | Racional proposto |
|---:|---|---|
| 1 | **Obrigatório** | Nota baixa sem justificativa não é acionável para a unidade nem verificável. |
| 2 | **Obrigatório** | Idem. |
| 3 | Opcional | Nota neutra; comentário agrega, mas não é condição. |
| 4 | Opcional | Idem. |
| 5 | Opcional | Elogio sem texto continua válido. |

Consequências propostas: comentário obrigatório é texto **não vazio após normalização** (remover espaços nas bordas), com mínimo de 10 e máximo de 1000 caracteres; nota é **inteiro** de 1 a 5 — fracionada (ex.: 4,5) é inválida. O rótulo de cada nota é decisão de interface, não regra de domínio. Ver [[Avaliação]] para as invariantes e [[Validações]] para a divisão entre formato (FluentValidation) e regra de negócio (Domain).

## Quem avalia e âncora de identidade

O comprador público pode pedir **sem conta autenticada** (ver [[Usuários e Perfis]] e [[Cliente]]). O que identifica a compra é a **referência pública opaca do pedido** (`/order/track/{reference}`), não um usuário logado. Padrão proposto: a avaliação é vinculada a um **pedido concluído** da própria unidade — "compra verificada" — e cada alvo só pode ser avaliado **uma vez por pedido**.

Alternativa descartada no padrão proposto: avaliação livre, sem pedido. Motivo: sem âncora de compra não há como distinguir autor de terceiro, nem limitar repetição. Reabrir essa decisão exige ADR e registro em `openspec/decisions/`.

## O que é avaliado

- **Estabelecimento:** uma nota por pedido, com comentário opcional/obrigatório pela regra central.
- **Produto:** uma nota por **item comprado** no pedido, com a mesma regra de comentário. Produto removido ou inativo depois da compra continua podendo ser avaliado, porque a avaliação se refere ao que foi consumido, não ao catálogo atual.

Alvos são sempre da **mesma unidade** do pedido; nenhum alvo pode ser indicado pelo cliente fora do que consta no pedido (ver [[Multi-tenancy]]).

## Jornada pública proposta

1. Pedido atinge `Completed` (ver [[Fluxo de Pedido]]).
2. Tela de acompanhamento (`/order/track/{reference}`) passa a exibir convite "Avaliar pedido"; o convite não bloqueia nem substitui o acompanhamento.
3. Usuário atribui nota ao estabelecimento e aos produtos; ao escolher 1 ou 2, o comentário passa a ser exigido com indicação clara do motivo.
4. Envio é idempotente (mesma chave em retry, conforme padrão de confirmação de pedido); sucesso mostra a nota publicada e passa a alimentar [[Classificação e Reputação]].

Convite por notificação (canal de comunicações) é **A confirmar**; depende de `communications/customer-order-notifications` e do gateway de canais, hoje sandbox segundo `docs/notification-gateway.md`.

## Como a classificação aparece

- Página pública do estabelecimento: média, contagem e distribuição por nota.
- Catálogo/cardápio: média e contagem por produto no cartão e no detalhe.
- Administração: lista de avaliações recebidas, com filtro por nota e período.

Mínimo de avaliações para publicar média, ordenação por "melhor avaliado" e destaque de comentários são **A confirmar**. Média e contagem não são editáveis manualmente por administrador — ver [[Classificação e Reputação]].

## Integridade e moderação

- Uma avaliação por pedido e por alvo; repetição é rejeitada, não sobrescrita silenciosamente.
- Comentário público passa por validação de tamanho, normalização e verificação de conteúdo ofensivo/dados pessoais antes de publicar; o autor **não define** se aparece com nome, apelido ou anônimo por padrão (**A confirmar**, com implicação de LGPD).
- O estabelecimento **pode ocultar** um comentário com justificativa registrada, mas **não pode alterar nota** nem excluir o registro: ocultação sai da exibição pública e permanece auditável. Proposta de resposta pública da unidade fica para fase posterior.
- Abuso (várias avaliações do mesmo telefone/dispositivo, rajada em curto intervalo) é tratado por limite e por vínculo ao pedido, não por heurística de nota.

## Limites e riscos

- `PRODUCT.md` registra que o fluxo público ainda não foi validado por usuário real; a avaliação herda esse risco de validação — ver [[01 - Produto/Estado Atual do Produto|Estado do Produto]].
- Avaliação é conteúdo gerado por usuário: exige moderação, política de privacidade e retenção definidas **antes** do lançamento.
- Nota baixa obrigatória com comentário aumenta atrito; a decisão de produto é consciente (troca de volume por sinal acionável).

## Decisões a confirmar

- Exigir pedido `Completed` (padrão proposto) ou permitir avaliação após `Ready`/entrega.
- Janela para avaliar (proposta: 30 dias após a conclusão).
- Edição pelo autor depois de publicada (proposta: permitida em 7 dias, com histórico).
- Exibição do autor (anônimo por padrão ou nome abreviado).
- Mínimo de avaliações para exibir média pública.
- Resposta do estabelecimento e notificação de convite: fase 2.

## Relacionados

[[Avaliação]] · [[Classificação e Reputação]] · [[Endpoints de Avaliação]] · [[Telas de Avaliação]] · [[Proposta - Avaliações e Classificação]] · [[Pedido]] · [[Produto]] · [[Estabelecimento]] · [[Cliente]] · [[Fluxos Principais]]
