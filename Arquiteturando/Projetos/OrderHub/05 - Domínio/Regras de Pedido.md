# Regras de Pedido

Regras confirmadas por código/spec: estados e transições modelados no Domain; itens editáveis enquanto Draft; transição cria registro de histórico; snapshots mantêm dados/valores relevantes do momento do pedido; horários futuros permitidos para Pickup/Delivery conforme scheduling; composição de adicionais valida limites, compatibilidade e preço.

As regras específicas evoluem via specs. Não assumir regras não observadas (ex.: política de cancelamento por perfil ou pagamento obrigatório). Fontes: `Order.cs`, `ModifierComposition.cs` (classe `ModifierCompositionCalculator`), `openspec/specs/ordering/`, testes `Order*`, `PublicOrdering*`, `ModifierComposition*`.

Relacionados: [[Pedido]], [[Fluxo de Pedido]], [[Produto]], [[Disponibilidade]], [[Pagamento]].


