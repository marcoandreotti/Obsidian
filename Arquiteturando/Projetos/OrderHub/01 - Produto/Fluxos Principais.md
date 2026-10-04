# Fluxos Principais

Síntese de `docs/user-journeys.md`; contratos e regras detalhados nas fontes referidas.

1. **Consumidor:** `/order/{slug}` ou QR `/order/{slug}/table/{tableToken}` → catálogo/composição → carrinho → simulação/checkout → confirmação idempotente → `/order/track/{reference}`. Cancelamento só quando estado permite.
2. **Preparar unidade:** login e onboarding em etapas salvas/retomáveis: dados/slug, tema, horários, mesas/QR, acessos e revisão. Unidade também precisa de catálogo e modalidades disponíveis.
3. **Administrar:** login/MFA → unidade autorizada → telas habilitadas por capacidade: catálogo, equipe, disponibilidade, entrega, clientes, cupons, pagamentos, comunicações, relatórios.
4. **Operar:** `/operations`, `/operations/kitchen`, `/operations/delivery`; ações respeitam papel e estado servidor; realtime preferido e polling de fallback.
5. **Provisionar:** PlatformSuperUser → `/platform` → cria Tenant, unidade e primeiro Owner; Owner usa código do Tenant, MFA, troca senha e continua onboarding.

Fontes: `docs/user-journeys.md`, `docs/platform-tenant-provisioning.md`, specs de cada contexto. Ver [[Fluxo de Pedido]], [[Comunicação com a API]], [[Infraestrutura]].


