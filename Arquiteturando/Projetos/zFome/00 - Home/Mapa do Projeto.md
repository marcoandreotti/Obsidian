# Mapa do Projeto

Raiz do repositório: `C:\Users\marco\source\repos\zFome`.

| Caminho | Responsabilidade |
|---|---|
| `AGENTS.md` | Regras para agentes, hierarquia de fontes, DoD. |
| `PRODUCT.md`, `README.md` | Propósito, execução local. |
| `openspec/` | Specs, decisões, arquitetura, convenções, changes e arquivo. |
| `docs/` | Jornadas, inventários, Design System e guias operacionais. |
| `src/` | Projetos .NET. |
| `tests/` | Testes .NET por camada/tipo. |
| `web/ZFome.Web/` | SPA Vue 3/Quasar/TypeScript. |
| `docker/`, `docker-compose*.yml` | Imagens, serviços e topologia local. |
| `.agents/skills/` | Procedimentos OpenSpec locais. |

## Projetos .NET

- `src/ZFome.Domain/`: modelo/invariantes — Catalog, Customers, Delivery, Identity, Operations, Ordering, Payments, Promotions, Tenancy, SharedKernel.
- `src/ZFome.Application/`: casos de uso, Commands/Queries, dispatchers, handlers, validators e portas.
- `src/ZFome.Contracts/`: contratos externos.
- `src/ZFome.Infrastructure/`: persistência EF/Dapper, adapters, integrações e worker Outbox.
- `src/ZFome.Api/`: Minimal APIs, middleware, autenticação, tenancy, realtime e composição em `Program.cs`.
- `src/ZFome.Infrastructure.Migrations/`: executável isolado de migrations.

Testes: `tests/ZFome.Domain.Tests/`, `tests/ZFome.Application.Tests/`, `tests/ZFome.Architecture.Tests/`, `tests/ZFome.Integration.Tests/`. Web organizada em `src/router/`, `layouts/`, `modules/`, `components/`, `http/`, `boot/`, `themes/`, `css/`; testes em `web/ZFome.Web/tests/`.

Configuração importante: `Directory.Build.props`, `.csproj`, `ZFome.sln`, `appsettings*.json`, `.env.example`, Compose, Dockerfiles, `package.json`, Quasar/Vitest configs e scripts Web. O `.env` local não foi lido nem copiado para o cofre.

Detalhes: [[03 - API/Módulos e Endpoints|Módulos e Endpoints]] · [[04 - WEB/Estrutura Frontend|Estrutura Frontend]].




> Caminhos iniciados em `src/` nesta nota são relativos a `web/ZFome.Web/`; por exemplo, `src/router/routes.ts` corresponde a `web/ZFome.Web/src/router/routes.ts` a partir da raiz do repositório.


