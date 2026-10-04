# Regras Obrigatórias

Resumo de `AGENTS.md`; confirme o texto oficial antes de cada mudança.

- Preservar monólito modular e dependências permitidas; Domain não referencia camadas externas.
- CQRS com dispatcher próprio; proibido MediatR e AutoMapper conforme instrução do repositório.
- FluentValidation para validação de entrada; invariantes no Domain; controllers/endpoints finos.
- EF Core em escrita, Dapper em leitura conforme arquitetura, com escopo tenant.
- Seguir autorização/policies, tenant context e proteção contra CSRF/auth existentes.
- API não deve duplicar regras nem acessar dados diretamente fora da abstração prevista.
- WEB segue Vue/TypeScript/Quasar, rotas e Design System, acessibilidade e estrutura por feature.
- I/O assíncrono e CancellationToken conforme aplicável.
- Testes pertinentes e Definition of Done da raiz/spec; documentação e specs atualizadas conforme fluxo.

Fontes: `AGENTS.md`; `openspec/specs/architecture/` + `AGENTS.md` + ADRs; `docs/web-design-system.md`; `openspec/decisions/`; spec/change aplicável. É resumo, não substitui redação oficial.


