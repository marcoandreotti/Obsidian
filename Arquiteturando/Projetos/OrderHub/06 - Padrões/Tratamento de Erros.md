# Tratamento de Erros

API configura ProblemDetails e correlation id global; domínio expõe exceções para invariantes; validators retornam falhas de entrada por pipeline. Detalhes do mapeamento estão em `src/OrderHub.Api/Middleware/GlobalExceptionMiddleware.cs` e `src/OrderHub.Api/Middleware/CorrelationIdMiddleware.cs`; o contrato consta em `openspec/specs/architecture/solution-foundation/spec.md`, `AGENTS.md` e `openspec/conventions.md`.

WEB mostra falhas por componentes/mensagens de feature, incluindo `ProblemBanner.vue`; cliente centraliza tratamento HTTP e refresh. Mensagens localizadas estão na spec `openspec/specs/web/portuguese-user-interface/`; a change `2026-10-06-localize-user-facing-messages` foi arquivada — veja [[10 - Evolução/Estado Atual|Estado Atual]].

Não converter exceções em sucesso, não vazar detalhes internos e seguir o contrato existente. Responsabilidade/classificação exata de todos códigos HTTP por endpoint: A confirmar na spec correspondente.

Relacionado: [[Padrões de Backend]], [[Validações]], [[Padrões Arquiteturais]], [[Segurança]].


