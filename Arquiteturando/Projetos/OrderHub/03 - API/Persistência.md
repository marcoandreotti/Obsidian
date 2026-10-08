# Persistência

PostgreSQL é store principal, usado por caminhos separados de leitura e escrita.

- Write: port da Application → repository/gateway Infrastructure → `OrderHubDbContext`/EF Core/Npgsql → transaction. Mapeamentos em `Persistence/Write/Configurations/`; repositories em `Write/Repositories/` e adapters específicos.
- Read: gateways em `Persistence/Read/` → `NpgsqlReadConnectionFactory`/`IReadConnectionFactory` → Dapper/SQL → read model/DTO.
- Scope: entidades implementam `ITenantScopedEntity`/`IEstablishmentScopedEntity` conforme contexto; convenções EF em `TenantModelConventions.cs`, gateways filtram Tenant/unidade e testes cobrem isolamento.
- Migrations isoladas em `OrderHub.Infrastructure.Migrations`; Compose aguarda sucesso antes de iniciar API.

Specs: `openspec/specs/persistence/core-postgresql-schema/spec.md`, `architecture/solution-foundation/spec.md`. Exemplos: `OrderHubDbContext.cs`, `OrderRepository.cs`, `OrderReadGateway.cs`. Ver [[Multi-tenancy]], [[Pedido]], [[ADR-003 - Transactional Outbox]].



