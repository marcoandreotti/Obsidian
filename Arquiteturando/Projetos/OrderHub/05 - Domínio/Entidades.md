# Entidades e Conceitos

Índice dos conceitos centrais (código em `src/OrderHub.Domain/`). Relação de agregados é observada em classes/coleções; consulte mapeamento EF antes de afirmar tabela ou boundary.

- [[Tenant]] contém ou é dono de [[Estabelecimento]]s; mantém public code/estado.
- [[Estabelecimento]] tem slug, tema, fuso, onboarding; scopa catálogo, usuários vinculados, [[Disponibilidade]], cliente, [[Pedido]], pagamento/cupom e região.
- [[Usuário Administrativo]] pertence a Tenant e recebe papéis/acesso de estabelecimento; identidade de Platform é separada.
- [[Pedido]] preserva snapshot de item, contato, endereço, valor e transições/histórico.
- [[Produto]] pertence à unidade/categoria e agrega variações/imagens/grupos de modificadores.
- [[Cliente]] mantém contato/endereço dentro da unidade; visitante pode pedir sem login.
- [[Pagamento]] registra cobertura financeira sem substituir estado operacional do pedido.
- [[Cupom]] avalia desconto/uso associado ao pedido.
- [[Região de Entrega]] determina cobertura, tarifa e estimativa.

Value objects: `Money`, `Quantity`, `Email`, `Slug`, `EstablishmentTheme`, `ModifierPortion`; shared interfaces `ITenantScopedEntity`/`IEstablishmentScopedEntity`. Ver [[05 - Domínio/Glossário|Glossário]] e [[Regras de Negócio]].


