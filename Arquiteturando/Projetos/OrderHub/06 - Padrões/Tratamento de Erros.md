# Tratamento de Erros

API configura ProblemDetails e correlation id global; domínio expõe exceções para invariantes; validators retornam falhas de entrada por pipeline. Detalhes do mapeamento estão em `src/OrderHub.Api/` e `openspec/specs/architecture/` + `AGENTS.md` + ADRs.

WEB mostra falhas por componentes/mensagens de feature, incluindo `ProblemBanner.vue`; cliente centraliza tratamento HTTP e refresh. Mensagens localizadas têm change OpenSpec ativo; veja [[10 - Evolução/Estado Atual|Estado Atual]].

Não converter exceções em sucesso, não vazar detalhes internos e seguir o contrato existente. Responsabilidade/classificação exata de todos códigos HTTP por endpoint: A confirmar na spec correspondente.


