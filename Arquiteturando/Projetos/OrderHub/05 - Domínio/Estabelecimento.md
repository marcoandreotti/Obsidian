# Estabelecimento

**Arquivo:** `src/OrderHub.Domain/Tenancy/Establishment.cs` · **Classe:** `Establishment` (unidade operacional).

Possui `TenantId`, nome comercial, `Slug`, `EstablishmentTheme`, fuso (`America/Sao_Paulo` default observado), estado active, onboarding completed timestamp. Tema/slug/timezone podem ser alterados; obtenção de public theme exige unidade ativa. A unidade é scope de catálogo, operação e acesso.

**Relacionados:** [[Tenant]], [[Produto]], [[Pedido]], [[Disponibilidade]], [[Região de Entrega]], [[Usuário Administrativo]], [[Avaliação]] e [[Classificação e Reputação]] (proposta do cofre, não implementada). Specs `tenancy/establishment-management`, `establishment-onboarding`; API config/onboarding e Platform; UI onboarding/Platform. Testes `EstablishmentScopeResolverTests`, `OnboardingTests`, `PlatformProvisioningApplicationTests`, `OnboardingApiTests`.

Public theme pertence à unidade, mas Web Design System limita customização visual a Public. Ver `docs/web-design-system.md`.


