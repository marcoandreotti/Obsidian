# Usuários e Perfis

`PRODUCT.md`/`openspec/project.md` citam cliente, atendente, cozinha, entregador, gerente, administrador, proprietário e superusuário da plataforma.

Papéis implementados (`src/OrderHub.Domain/Identity/AdministrativeRole.cs`): `Owner=1`, `Admin=2`, `Manager=3`, `Attendant=4`, `Kitchen=5`, `Delivery=6`. `src/OrderHub.Application/Identity/AdministrativePolicies.cs` mapeia esses papéis a capacidades como management, administration, order-read/kitchen/delivery, customer-operations, promotion-management e payment-management. Consulte o mapa: não suponha equivalência a partir do nome do papel.

Identidade Platform é separada do usuário Tenant (ADR-002). Especificação de cliente público permite comprar sem conta autenticada (`customers/customer-records`). Detalhes em `openspec/specs/identity/` e `administration/administration-api/spec.md`; código em `src/OrderHub.Domain/Identity/`, `src/OrderHub.Api/Authentication/`, Web `modules/session/`, `modules/administration/users/`, `modules/platform/`.

Perfis humanos além do enum e policy: confirmar nas specs, não inferir. Ver [[Usuário Administrativo]] e [[Autenticação e Autorização]].




