# Validações

AGENTS.md exige FluentValidation para inputs, associada aos casos Application; regras invariantes pertencem ao Domain e não devem ser duplicadas no endpoint. Entrada de UI ajuda usabilidade, mas API/domain permanecem autoritativos.

Exemplos: validators de ordering, onboarding, pagamentos, notification; `ModifierCompositionCalculator` valida seleção e composição. Localize por módulo em `src/OrderHub.Application/` e `src/OrderHub.Domain/`; testes em projetos equivalentes.

Ao alterar: confira spec, validator/teste existente, domínio e tratamento de erro. Não deslocar regras para controller/componente. Relacionado: [[Padrões de Backend]], [[Pedido]].


