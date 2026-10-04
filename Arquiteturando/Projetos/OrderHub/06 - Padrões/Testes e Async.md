# Testes e Async

Projetos de teste: Domain, Application, Architecture, Integration; WEB usa Vitest. Siga convenção mais próxima e requisitos de AGENTS.md/Definition of Done. Não afirmar que suíte passou sem executá-la; a análise que produziu estas notas não executou testes.

Use async em I/O e propague CancellationToken conforme `AGENTS.md`; não bloquear com `.Result`/`.Wait()` em fluxo assíncrono. Teste lógica pura no Domain/Application, persistência/contratos em integração quando aplicável e fronteiras no Architecture.

Logging/configuração dependem das abstrações/configs existentes; não identificada uma convenção adicional universal. Relacionado: [[Checklist de Desenvolvimento]], [[10 - Evolução/Estado Atual|Estado Atual]].


