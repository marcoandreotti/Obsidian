# Segurança

Autenticação administrativa inclui senha + desafio MFA por email e cookies HttpOnly; refresh, CSRF cookie/header, rate limiting para início/conclusão de autenticação. Middleware inclui ProblemDetails/correlation e proteção contra alteração de senha temporária. Authorization policies e escopo por tenant/unidade estão em Application/Identity.

Identidade da plataforma é distinta da identidade administrativa por ADR-002. Isolamento tenant deve acompanhar leitura, escrita, autorização e jobs. Não ler nem copiar `.env`; `.env.example` é documentação de nomes/configuração, não segredo.

Fontes: `AGENTS.md`, ADR-002, `src/OrderHub.Api/Authentication/`, `Application/Identity/AdministrativePolicies.cs`, specs identity/tenancy. Relacionado: [[Autenticação e Autorização]], [[Tenant]].


