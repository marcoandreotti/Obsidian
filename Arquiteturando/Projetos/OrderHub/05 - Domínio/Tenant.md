# Tenant

**Arquivo:** `src/OrderHub.Domain/Tenancy/Tenant.cs` · **Classe:** `Tenant`.

Representa a organização cliente na plataforma. Propriedades observadas: `Id`, `Name`, `PublicCode`, `IsActive`, timestamps. Factory `Create`; rename/activate/deactivate e normalização do public code. Um Tenant possui estabelecimentos/unidades no modelo; consultar `Establishment.TenantId` e persistência para relações concretas.

**Regras relacionadas:** código público normalizado uppercase e 3–50 letras/números/hífen; nome 1–150 caracteres; estado Tenant afeta operação. `Tenant` não é identidade do usuário global Platform (ADR-002).

**Relacionado a:** [[Estabelecimento]], [[Usuário Administrativo]], [[Multi-tenancy]], [[Provisionamento de Tenant]]. Specs `openspec/specs/tenancy/establishment-management/spec.md`, `platform-tenant-provisioning/spec.md`; tests `tests/OrderHub.Domain.Tests/Tenancy/TenantTests.cs`, `tests/OrderHub.Integration.Tests/TenancyPersistenceTests.cs`.


