# ADR-003 - Transactional Outbox

## Contexto e decisão

[ADR-003 original](file:///C:/Users/marco/source/repos/OrderHub/openspec/decisions/ADR-003-transactional-outbox.md) registra uso do padrão Transactional Outbox para encaminhar mensagens de forma confiável após persistência transacional.

## Motivo

A fonte descreve o contexto e a motivação; esta nota não presume garantias além das consequências documentadas no ADR e implementação.

## Consequências

Implementação observada em Infrastructure/Outbox e worker, com testes de integração. Relaciona-se a notificações; veja [[Persistência]], [[Fluxo de Pedido]] e [[10 - Evolução/Estado Atual|Estado Atual]].

## Alternativas

Ver ADR original.


