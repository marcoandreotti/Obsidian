# Infraestrutura

Compose define PostgreSQL 17 com volume/healthcheck, Mailpit local, migration job, API e Web; `api` espera migrations completadas. Ports defaults PostgreSQL 5432, API 8080, Web 9000, SMTP Mailpit 1025/UI 8025. Rede Docker `orderhub`.

Produção Web Docker: Node 22.22 para Quasar build e Nginx 1.29 para SPA, fallback `/index.html`, proxy WebSocket `/hubs/`. Override local monta Web e executa `npm ci`/`quasar dev` na porta 9000 com polling. API/migrations usam .NET 10 SDK/runtime.

`.env.example` nomeia configuração DB/ports, Web origin, Platform bootstrap, SMTP, notification SMTP, Meta WhatsApp, retry e realtime. `appsettings.Development.json` aponta Mailpit localhost; API Compose aponta service `mailpit`. `.env` real não foi lido.

Integrações confirmadas: SMTP auth/notification; Meta WhatsApp Cloud API por adapter; PostgreSQL; SignalR. Docs dizem credenciais iniciais Notification são sandbox, nível implantação e compartilhadas por Tenant; webhook de entrega final não incluído. Payment provider externo: **Não identificado no repositório**. CEP provider: **A confirmar**.

README: `dotnet restore/build/test`, `dotnet run --project src/OrderHub.Api`, `npm run dev`, `docker compose up --build`. Migrations doc em `src/OrderHub.Infrastructure/Persistence/Write/Migrations/README.md`.


