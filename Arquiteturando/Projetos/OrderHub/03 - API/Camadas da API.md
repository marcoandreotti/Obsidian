# Camadas da API

Ordem de estudo: Domain → Application → Infrastructure → API/composition → Contracts/testes. Ordem de execução de escrita: endpoint → Dispatcher → validator → handler → Domain → port/repository → adapter/DB.

| Camada | Objetivo, exemplos | Pode depender | Evitar |
|---|---|---|---|
| Domain | invariantes: `Domain/Ordering/Order.cs`, `Catalog/Product.cs`, `Tenancy/Tenant.cs` | BCL e tipos próprios | EF, Dapper, SQL, HTTP, Infrastructure |
| Application | casos de uso/ports: `Application/Dispatching/`, contextos, validators | Domain, FluentValidation | persistência concreta; regra de negócio em validator |
| Infrastructure | `Persistence/Write/`, `Persistence/Read/`, adapters e worker | Application/Domain, EF, Dapper, Npgsql, clients externos | SQL/EF no Domain; Controllers com acesso direto |
| API | `Api/Program.cs`, `*Endpoints.cs`, middleware | Application, Infrastructure, Contracts, ASP.NET Core | regra de negócio, acesso DB direto, entidade na response |
| Contracts | `src/OrderHub.Contracts/` | tipos neutros externos | entidade de domínio/EF |
| Migrations | `src/OrderHub.Infrastructure.Migrations/` | Infrastructure/EF tooling | ser referência de camadas internas |

Referências `.csproj`, `openspec/conventions.md`, `AGENTS.md`, `tests/OrderHub.Architecture.Tests/`. Ver [[02 - Arquitetura/Dependências entre Camadas|Dependências entre Camadas]].


