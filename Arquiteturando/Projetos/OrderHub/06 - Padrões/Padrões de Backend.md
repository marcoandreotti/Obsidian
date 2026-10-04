# Padrões de Backend

- CQRS: Commands alteram estado; Queries leem projeções. Dispatchers próprios em `Application/Dispatching/`; handlers em módulos Application.
- Domain: invariantes nos agregados/value objects; exemplos `Ordering/Order.cs`, `Catalog/ModifierCompositionCalculator.cs`.
- Validação: FluentValidation junto aos request/handlers conforme padrão documentado; ver [[Validações]].
- Persistência: EF Core/PostgreSQL no caminho de escrita; Dapper/PostgreSQL nos read gateways. Transações e outbox conforme [[Persistência]] e ADR-003.
- HTTP: Minimal APIs em `Api/Endpoints`, sem controller com lógica de negócio; resposta de erro global ProblemDetails e correlation id.
- Async: propague `CancellationToken` em I/O assíncrono conforme AGENTS.md. Consulte [[Testes e Async]].

Exemplos são observações de implementação; `AGENTS.md`, arquitetura e specs definem obrigações. Evitar acesso a dados diretamente em endpoint, duplicação de regra na API, handler que contorna dispatcher/pipeline.


