# Proposta — Avaliações e Classificação

> **Estado:** proposta do cofre. **Não é uma change OpenSpec criada** e não há implementação. Verificado no checkout `6384863` (2026-10-07): nenhuma dessas rotas, agregados, tabelas ou specs existe. A change descrita precisa seguir o processo do repositório (`.agents/skills/openspec-propose` → `openspec-apply-change` → `openspec-archive-change`).

Objetivo: permitir que o **usuário público que concluiu um pedido** avalie o **estabelecimento** e os **produtos** com **nota de 1 a 5**, exigindo **comentário quando a nota for menor que 3**. Regra, jornada e limites em [[Avaliações e Classificação]]; modelo em [[Avaliação]] e [[Classificação e Reputação]]; contratos em [[Endpoints de Avaliação]]; interface em [[Telas de Avaliação]].

## Change proposta

- **Nome proposto:** `add-customer-reviews` (padrão `add-*` usado no repositório).
- **Capability nova proposta:** `reviews/customer-reviews` — o contexto `reviews` não existe em `openspec/specs/` (são 15 contextos hoje). Contexto novo criado por change tem precedente (`customer-service` em `add-ai-customer-agent`, `security` em `add-audit-trail`).
- **Capabilities possivelmente modificadas:** `catalog/product-catalog` (expor média por produto no catálogo público) e `ordering/public-ordering-web` (convite de avaliação na jornada pública). **A confirmar** — só modificar se o requisito vigente realmente mudar; caso contrário, manter tudo na capability nova.
- **Artefatos esperados:** `.openspec.yaml`, `proposal.md` (`## Why` / `## What Changes` / `## Capabilities` / `## Impact`), `design.md` (`## Context` / `## Goals / Non-Goals` / `## Decisions` / `## Risks / Trade-offs` / `## Migration Plan`) e `tasks.md`; delta em `specs/reviews/customer-reviews/spec.md`.
- **Comandos do fluxo:** `openspec new change "add-customer-reviews"` → `openspec status --change add-customer-reviews --json` → `openspec instructions <artifact-id> --change add-customer-reviews --json`.

## Delta de spec proposto (rascunho)

Formato do repositório: `## ADDED Requirements` + `### Requirement:` (SHALL/MUST/MAY) + `#### Scenario:` com `- **WHEN**` / `- **THEN**`.

### Requirement: Nota de avaliação é inteiro de 1 a 5
O sistema SHALL aceitar, por alvo avaliado, apenas nota inteira entre 1 e 5 e MUST rejeitar valores fora dessa faixa.

#### Scenario: Nota fora da faixa
- **WHEN** o consumidor envia nota 0, 6 ou fracionada para o estabelecimento ou para um produto
- **THEN** a avaliação MUST ser rejeitada com erro de validação e nenhum registro MUST ser criado

### Requirement: Nota inferior a 3 exige comentário
Avaliação com nota 1 ou 2 SHALL exigir comentário não vazio; avaliação com nota 3, 4 ou 5 MAY ser enviada sem comentário.

#### Scenario: Nota baixa sem comentário
- **WHEN** o consumidor envia nota 2 sem comentário ou apenas com espaços
- **THEN** a API MUST rejeitar por regra de negócio não atendida e MUST NOT criar a avaliação

#### Scenario: Nota baixa com comentário
- **WHEN** o consumidor envia nota 1 com comentário de tamanho válido
- **THEN** a avaliação MUST ser registrada e publicada

### Requirement: Avaliação exige pedido concluído da mesma unidade
Uma avaliação SHALL referenciar pedido da mesma unidade e tenant, com status `Completed`, e MUST NOT aceitar alvo que não conste no pedido.

#### Scenario: Pedido ainda não concluído
- **WHEN** o consumidor tenta avaliar pedido em `Confirmed`, `Preparing`, `Ready` ou `OutForDelivery`
- **THEN** a API MUST rejeitar por regra de negócio não atendida

#### Scenario: Alvo de outra unidade ou fora do pedido
- **WHEN** o payload indica produto de outra unidade ou produto ausente do pedido
- **THEN** o sistema MUST rejeitar e MUST NOT criar avaliação

### Requirement: Uma avaliação por pedido e alvo
O sistema SHALL permitir no máximo uma avaliação publicada por pedido e por alvo.

#### Scenario: Segunda avaliação no mesmo alvo
- **WHEN** o consumidor reenvia avaliação do mesmo pedido para o mesmo alvo
- **THEN** a API MUST responder conflito e MUST NOT alterar a avaliação existente

### Requirement: Envio idempotente
A criação de avaliação SHALL exigir chave de idempotência e MUST NOT duplicar registros em repetição.

#### Scenario: Repetição com a mesma chave
- **WHEN** o consumidor repete a requisição com a mesma chave de idempotência e o mesmo payload
- **THEN** o sistema MUST devolver o resultado já produzido, sem criar segunda avaliação

### Requirement: Classificação publicada reflete apenas avaliações publicadas
Média, contagem e distribuição SHALL considerar somente avaliações publicadas e MUST ser recalculadas ao publicar, ocultar ou restaurar avaliação.

#### Scenario: Ocultação remove do cálculo
- **WHEN** o administrador oculta uma avaliação com motivo
- **THEN** a média e a distribuição públicas MUST deixar de contá-la e o registro MUST permanecer auditável

### Requirement: Administrador modera sem alterar nota
A moderação SHALL permitir ocultar e restaurar com motivo registrado e MUST NOT permitir alterar nota ou excluir o registro.

#### Scenario: Tentativa de editar nota
- **WHEN** um administrador procura alterar a nota de uma avaliação
- **THEN** nenhuma operação desse tipo MUST existir na API e o dado MUST permanecer inalterado

### Requirement: Isolamento por tenant e unidade
Leitura e escrita SHALL respeitar escopo de tenant e estabelecimento, e a unidade MUST ser resolvida a partir do pedido/referência, nunca a partir do cliente.

#### Scenario: Leitura cruzando unidades
- **WHEN** uma consulta pública usa slug de outra unidade ou referência de outro estabelecimento
- **THEN** o sistema MUST NOT retornar dados de avaliação de outra unidade

## Tasks propostas

### 1. Proposta e spec
- [ ] 1.1 Criar a change `add-customer-reviews` com proposal, design e delta spec; verificar com `openspec status --change add-customer-reviews --json`.
- [ ] 1.2 Fechar as decisões abertas (janela de avaliação, edição pelo autor, anonimato, mínimo para exibir média) no `design.md`; verificar que cada uma está registrada como decisão, não como suposição.

### 2. Domain (`Reviews`)
- [ ] 2.1 Criar `src/OrderHub.Domain/Reviews/Review.cs` com `Review`, `ReviewTargetKind`, `ReviewStatus` e o VO `Rating`; verificar `tests/OrderHub.Domain.Tests/Reviews/ReviewTests.cs`.
- [ ] 2.2 Implementar as invariantes de nota, comentário obrigatório e coerência de escopo; verificar testes de nota fora da faixa, comentário ausente e alvo de outra unidade.

### 3. Application
- [ ] 3.1 Criar comando e validador de publicação de avaliação (`Reviews/`), registrados em `DependencyInjection.cs`; verificar `tests/OrderHub.Application.Tests/Reviews/`.
- [ ] 3.2 Implementar consultas de situação do pedido, listagem pública e sumário de classificação; verificar que a pertinência do alvo ao pedido é checada no caso de uso.
- [ ] 3.3 Implementar moderação (ocultar/restaurar com motivo); verificar que não existe caminho de edição de nota.

### 4. Infrastructure
- [ ] 4.1 Mapear o módulo em `Persistence/Write/Configurations/ReviewsConfiguration.cs` e criar schema `reviews`; verificar `ModelConventionsTests`.
- [ ] 4.2 Criar migration no projeto `OrderHub.Infrastructure.Migrations` com índices únicos de unicidade por pedido/alvo e `tenant_id` primeiro; verificar aplicação em banco limpo.
- [ ] 4.3 Implementar read gateways Dapper de listagem e sumário; verificar ausência de N+1 no catálogo público.

### 5. API
- [ ] 5.1 Registrar endpoints públicos e administrativos com policies e metadados `.Produces*`; verificar 400/404/409/422 conforme [[Endpoints de Avaliação]].
- [ ] 5.2 Verificar idempotência de publicação e isolamento entre unidades nos testes de integração.

### 6. WEB — público
- [ ] 6.1 Criar componentes de exibição e entrada de nota com acessibilidade; verificar rótulos, teclado e contraste.
- [ ] 6.2 Adicionar convite na tela de acompanhamento e a página de avaliação; verificar que apenas pedido `Completed` oferece o convite.
- [ ] 6.3 Exibir média e contagem no contexto da unidade e nos produtos; verificar ausência de média quando não há avaliação publicada.

### 7. WEB — administração
- [ ] 7.1 Criar a tela de avaliações com filtros e moderação; verificar ocultar/restaurar com motivo e ausência de edição de nota.

### 8. Fechamento
- [ ] 8.1 Atualizar specs, docs afetados e este cofre; verificar Definition of Done de `AGENTS.md` e [[Checklist de Desenvolvimento]].

## Impacto

- **Domain:** novo módulo `Reviews` (nenhum módulo atual é alterado nos requisitos propostos).
- **Application / Infrastructure:** novos comandos, consultas, repositório, read gateways, schema `reviews` e migrations.
- **API:** dois grupos novos (público anônimo e administrativo autenticado).
- **WEB:** `modules/public-ordering/` e `modules/administration/reviews/`, mais rotas.
- **Specs/docs:** nova capability `reviews/customer-reviews`; eventual modificação de `catalog/product-catalog` e `ordering/public-ordering-web`.

## Riscos e trade-offs

- **Conteúdo gerado por usuário:** exige moderação, política de privacidade e retenção definidas antes do lançamento (LGPD); comentário público é dado pessoal em potencial.
- **Sem identidade de consumidor:** não há login de usuário final; a âncora contra abuso é a referência do pedido e o telefone normalizado do `Customer` (escopado por unidade). Limite de requisições por IP/referência passa a ser necessário.
- **Atrito:** exigir comentário em nota 1–2 reduz volume de respostas; é decisão de produto consciente.
- **Consistência do sumário:** recálculo síncrono é mais simples, porém acopla a escrita ao agregado de classificação; a via por outbox introduz defasagem visível e exige idempotência.
- **Volume de migrations:** novo schema e tabelas novas; migrations destrutivas não estão previstas.
- **Risco herdado:** a superfície pública ainda não foi validada por usuário real (`PRODUCT.md`).

## Reconferência do snapshot do cofre

Em 2026-10-07 o repositório está em `6384863`, com árvore limpa, dois commits depois do snapshot do cofre (`2c6de5b`, 2026-10-04). O commit `6384863` ("Ajustes mensagens e arquivando changes") arquivou três changes em 2026-10-06: `improve-kitchen-display`, `improve-operations-order-filtering` e `localize-user-facing-messages`. As changes ativas passam a ser `add-ai-customer-agent`, `add-audit-trail` e `add-observability`. As notas [[10 - Evolução/Estado Atual|Estado Atual]] e [[Backlog Técnico]] registram essa reconferência.

## Relacionados

[[Avaliações e Classificação]] · [[Avaliação]] · [[Classificação e Reputação]] · [[Endpoints de Avaliação]] · [[Telas de Avaliação]] · [[Backlog Técnico]] · [[Melhorias Identificadas]] · [[Como criar uma nova Feature]] · [[Diretrizes para Agentes]]
