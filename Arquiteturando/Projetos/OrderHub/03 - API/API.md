# API

Backend HTTP em `src/OrderHub.Api/`, ASP.NET Core/.NET 10. `Program.cs` compõe Application, Infrastructure, autenticação, policies, middleware, rate limiter, CORS, health, OpenAPI e SignalR. Os endpoints são Minimal APIs agrupadas por contexto; diretório `Controllers/` existe, mas não foram identificados controllers de rota implementados.

## Estude por

1. [[03 - API/Camadas da API|Camadas da API]]: Domain → Application → adapters → borda HTTP.
2. [[03 - API/Módulos e Endpoints|Módulos e Endpoints]] e [[Endpoints de Pedido]].
3. [[03 - API/Autenticação e Autorização|Autenticação e Autorização]] e [[03 - API/Endpoints de Avaliação|Endpoints de Avaliação]] (proposta).
4. [[03 - API/Persistência|Persistência]] e [[03 - API/Infraestrutura|Infraestrutura]].

Stack confirmado: C#/.NET 10, FluentValidation, EF Core/Npgsql (escrita), Dapper/Npgsql (leitura), ProblemDetails, ASP.NET Core auth e SignalR. MediatR/AutoMapper proibidos; sem microservices no desenho atual.


