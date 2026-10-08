# ADR-003 - Transactional Outbox

## Contexto e decisão

O original em `openspec/decisions/ADR-003-transactional-outbox.md` registra uso do padrão Transactional Outbox para encaminhar mensagens de forma confiável após persistência transacional.

## Motivo

A fonte descreve o contexto e a motivação; esta nota não presume garantias além das consequências documentadas no ADR e implementação.

## Consequências

Implementação observada em `src/OrderHub.Infrastructure/Persistence/OutboxProcessingWorker.cs` e `src/OrderHub.Infrastructure/Persistence/Write/OutboxMessageStager.cs`, com testes em `tests/OrderHub.Integration.Tests/TransactionalOutboxPersistenceTests.cs`. Relaciona-se a notificações; veja [[Persistência]], [[Fluxo de Pedido]] e [[10 - Evolução/Estado Atual|Estado Atual]].

## Alternativas

Ver ADR original.

## Referências

`openspec/specs/architecture/transactional-outbox/`, `docs/transactional-outbox.md`, `AGENTS.md`.


