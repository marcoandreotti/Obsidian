# Mapa de Componentes

```mermaid
flowchart LR
 Browser --> Web[Vue 3 + Quasar SPA]
 Web -->|HTTP cookies / CSRF| API[ASP.NET Core API]
 Web -->|SignalR WebSocket| Hub[Order Updates Hub]
 API --> App[Application: dispatchers, handlers, validators]
 App --> Domain[Domain: regras/invariantes]
 App --> Infra[Infrastructure: adapters]
 Infra -->|write EF Core| PG[(PostgreSQL)]
 Infra -->|read Dapper| PG
 Worker[Outbox worker no processo API] --> PG
 Worker --> Providers[SMTP / Meta WhatsApp]
 Migrations[Migrations executable] --> PG
 Nginx[Nginx SPA / local Quasar] --> Web
```

**Documentado:** monólito modular; sem broker externo; Outbox/worker local no monólito. **Implementado/configurado:** Compose contém `postgres`, `mailpit`, `migrations`, `api`, `web`; `Program.cs` registra SignalR e serviços; Nginx encaminha `/hubs/`. Fontes `docker-compose.yml`, `docker/web/nginx.conf`, `src/OrderHub.Infrastructure.Migrations/Program.cs`.

Ver [[03 - API/Infraestrutura|Infraestrutura]], [[04 - WEB/Comunicação com a API|Comunicação com a API]], [[ADR-003 - Transactional Outbox]].



