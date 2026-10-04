# Backend - Guia do Agente

Estude nesta ordem: `AGENTS.md` → `openspec/specs/architecture/` + `AGENTS.md` + ADRs e ADR → spec OpenSpec → exemplo do módulo → testes. Fluxo típico observado: Endpoint Minimal API → contrato/dispatcher Application → validator/handler → Domain → portas → Infrastructure write EF ou read Dapper → PostgreSQL; resposta mapeada pelo endpoint.

Localize endpoints em `src/OrderHub.Api/` (endpoints agrupados por módulo); casos de uso em `src/OrderHub.Application/`; invariantes em Domain; implementação persistência em `src/OrderHub.Infrastructure/`; migrations em `src/OrderHub.Infrastructure.Migrations/`. Use conceitos de [[Camadas da API]], [[Dependências entre Camadas]], [[Persistência]], [[Segurança]], [[Testes e Async]].

Manter endpoint fino, regras no Domain/Application conforme papel, queries tenant-filtered, async/cancellation, validators e testes da camada. Confirmar nomes concretos localmente; este fluxo é orientativo e pode variar por caso.


