# Produto

Produto de catálogo pertence a um tenant, estabelecimento e categoria. Implementação: `src/ZFome.Domain/Catalog/Product.cs`; contexto [[Produto e Catálogo]]. Está relacionado a [[Pedido]], a [[Avaliação]] e [[Classificação e Reputação]] (proposta não implementada) e aos fluxos [[Fluxos Principais]].

Produtos comportam variações, imagens e grupos de adicionais; grupos/composições têm restrições de seleção e modos de preço. `ModifierCompositionCalculator`, em `src/ZFome.Domain/Ordering/ModifierComposition.cs`, concentra o cálculo e a compatibilidade. Fontes: `src/ZFome.Domain/Catalog/`, `src/ZFome.Application/Catalog/`, `openspec/specs/catalog/product-catalog/spec.md`, testes Domain/Application/Infrastructure e WEB `web/ZFome.Web/src/modules/administration/catalog/` e `modules/public-ordering/`.

Verifique as specs e exemplos existentes antes de mudar o modelo.


