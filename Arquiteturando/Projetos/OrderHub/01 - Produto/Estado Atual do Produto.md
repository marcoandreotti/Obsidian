# Estado Atual do Produto

Snapshot do repo em 2026-10-04: commit `2c6de5b`, working tree limpo.

Reconferência em 2026-10-07: checkout `6384863` (2026-10-06), árvore limpa.

Código e referências de teste encontrados para catálogo/modificadores, clientes, MFA/sessões, gestão por capacidade, tenancy/onboarding/provisionamento, disponibilidade, pedidos públicos/admin, pagamentos configuráveis, cupons, entrega, dashboard operacional, KDS, agendamento, SignalR/polling, relatórios e comunicações/outbox. Presença de código/teste não atesta produção.

Limites documentados: `PRODUCT.md` diz que o fluxo público ainda não foi testado pelo usuário. `docs/notification-gateway.md`/ADR-004 descrevem credenciais sandbox compartilhadas para canais iniciais e ausência de webhook de entrega final. Forma de pagamento configurada não prova processamento online; provedor externo de pagamento **Não identificado no repositório**.

Avaliações de restaurante e de produtos pelo usuário público (nota 1–5, comentário obrigatório abaixo de 3) **não existem** no checkout `6384863` (2026-10-07): nenhum código, spec, tabela ou tela. Desenho em [[Avaliações e Classificação]].

Changes ativas e tarefas em [[10 - Evolução/Estado Atual|Estado técnico do projeto]] (Evolução). Dívidas comprovadas vs itens a confirmar: [[Dívidas Técnicas]].


