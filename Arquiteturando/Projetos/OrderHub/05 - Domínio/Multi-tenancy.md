# Multi-tenancy

OrderHub separa Tenant (cliente SaaS) e Estabelecimento (unidade operacional). Administradores pertencem a tenant e acesso pode ser limitado por unidade; usuário de plataforma é identidade distinta. Isolamento deve ser verificado na autorização, contexto da requisição, query, escrita, jobs e outbox conforme `AGENTS.md` e specs.

Fontes: `src/OrderHub.Domain/Tenancy/Tenant.cs`, `Establishment.cs`, `src/OrderHub.Application/Identity/`, `src/OrderHub.Api/`; specs `openspec/specs/tenancy/`, `identity/`; ADR-002. Relacionado: [[Tenant]], [[Estabelecimento]], [[Usuário Administrativo]], [[Provisionamento de Tenant]], [[Segurança]].


