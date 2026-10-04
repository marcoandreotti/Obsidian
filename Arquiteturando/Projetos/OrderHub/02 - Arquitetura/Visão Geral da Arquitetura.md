# Visão Geral da Arquitetura

Esta nota registra fronteiras e nível de evidência. Para navegação, use [[Arquitetura]]; para sequência, [[Fluxo de uma Requisição]]; para detalhe API/Web, [[API]] e [[WEB]].

## Decisões documentadas

- Modular monolith: ADR-001.
- Separação de identidade de plataforma: ADR-002.
- Outbox transacional: ADR-003.
- Adapters de canal de notificação: ADR-004.
- Regras de dependências, CQRS e testes: `AGENTS.md`, `openspec/specs/architecture/` + `AGENTS.md` + ADRs.

## Observações inferidas do código

A API expõe Minimal APIs e compõe módulos no startup; Application hospeda handlers e regras de orquestração; Domain define modelo/invariantes; Infrastructure implementa persistência e gateways; WEB comunica por HTTP e, em operações, SignalR para invalidação. Esses fatos descrevem o estado observado, não substituem as regras oficiais.

## Fronteiras

Domain não deve depender de API/Infrastructure; Application referencia Domain e define casos/portas; Infrastructure implementa persistência/integrações; API trata HTTP/auth/composição. WEB é cliente independente e não compartilha acesso ao banco. Confira `openspec/specs/architecture/` + `AGENTS.md` + ADRs e teste `tests/OrderHub.Architecture.Tests/` para restrições exatas.


