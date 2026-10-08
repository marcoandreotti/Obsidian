# Fluxo de uma Requisição

## Escrita

```mermaid
sequenceDiagram
 participant W as Web feature client
 participant E as Minimal API endpoint
 participant D as CommandDispatcher
 participant V as FluentValidation
 participant H as CommandHandler
 participant M as Domain
 participant R as Write adapter
 participant DB as PostgreSQL
 W->>E: HTTP request / contrato
 E->>D: ICommand
 D->>V: valida entrada
 D->>H: executar
 H->>M: aplicar regra/invariante
 H->>R: porta de persistência
 R->>DB: EF Core/transação
 E-->>W: response ou ProblemDetails
```

## Leitura

Web → endpoint → `IQueryDispatcher` → validação quando necessária → QueryHandler → read gateway → Dapper → PostgreSQL → DTO/read model.

Endpoints observados em `src/OrderHub.Api/*/*Endpoints.cs` são Minimal APIs. `src/OrderHub.Application/Dispatching/` contém dispatchers próprios; endpoints encaminham caso de uso, sem carregar regra de negócio. Contracts converte borda; Domain não vaza para HTTP.

Pedido público: API resolve unidade, preços, disponibilidade, entrega/cupom/slots; Domain calcula e protege transições; confirmação usa idempotency key. Ver [[Fluxo de Pedido]], [[Endpoints de Pedido]].


