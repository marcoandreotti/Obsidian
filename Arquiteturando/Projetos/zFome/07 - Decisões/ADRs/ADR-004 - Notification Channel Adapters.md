# ADR-004 - Notification Channel Adapters

## Contexto e decisão

O original em `openspec/decisions/ADR-004-notification-channel-adapters.md` registra arquitetura de adapters para canais de notificação.

## Motivo

Consultar motivação explicitamente registrada no ADR; nenhuma explicação histórica adicional é atribuída nesta nota.

## Consequências

Há abstrações e implementação de canais incluindo SMTP e integração WhatsApp Cloud API; detalhes de configuração/entrega em `docs/notification-gateway.md`. Mensagem aceita pelo provedor não equivale a confirmação de entrega. Relacionado: [[Padrões de Backend]], [[10 - Evolução/Estado Atual|Estado Atual]].

## Alternativas

Ver ADR original.

## Referências

`openspec/specs/communications/notification-gateway/`, `docs/notification-gateway.md`.


