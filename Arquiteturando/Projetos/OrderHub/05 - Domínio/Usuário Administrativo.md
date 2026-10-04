# Usuário Administrativo

**Arquivo:** `src/OrderHub.Domain/Identity/AdministrativeUser.cs` · tipo `AdministrativeUser`.

Registro tenant-scoped com Email, hash senha, flag de troca obrigatória, estado, papéis e acessos a estabelecimentos. Methods `GrantRole`, `RevokeRole`, `GrantEstablishmentAccess`, `RevokeEstablishmentAccess`, `Activate/Deactivate`, `ChangePassword`. Factory para Owner provisionado requer troca de senha.

Enum/policy: `AdministrativeRole.cs`; `Application/Identity/AdministrativePolicies.cs`. Regras especiais de gestão de Owner/último usuário em `AdministrativeUserManagementRules.cs` e Application transaction.

**Não confundir** com identidade Platform global, separada no ADR-002. Relacionados: [[Tenant]], [[Estabelecimento]], [[Autenticação e Autorização]]. Specs identity auth/users e administration API; testes Identity/Authentication/Application e Integration. Telas Web `modules/administration/users/`, sessão em `modules/session/`.


