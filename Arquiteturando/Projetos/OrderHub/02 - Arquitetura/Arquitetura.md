# Arquitetura

OrderHub é um monólito modular SaaS multi-tenant. Backend .NET 10 é organizado em camadas/contextos; PostgreSQL é o store primário. A Web Vue/Quasar é SPA separada. Usa DDD/CQRS e dispatchers próprios. HTTP conecta browser à API; SignalR serve invalidação/atualização operacional com query HTTP para reconciliação.

Escrita: endpoint → CommandDispatcher → FluentValidation → handler → Domain → write repository → EF Core → PostgreSQL. Leitura: endpoint → QueryDispatcher → handler → read gateway → Dapper → PostgreSQL → read model. Não misturar caminhos.

**Documentado:** monólito, limites, stack e CQRS em `openspec/architecture.md`, `openspec/conventions.md`, `AGENTS.md` e ADRs. **Observado:** Minimal APIs, `Program.cs` composition root, Web clients/Pinia e SignalR no código. Observação não cria regra oficial.

Ver [[02 - Arquitetura/Mapa de Componentes|Mapa de Componentes]], [[02 - Arquitetura/Fluxo de uma Requisição|Fluxo de uma Requisição]], [[02 - Arquitetura/Dependências entre Camadas|Dependências entre Camadas]], [[03 - API/API|API]], [[04 - WEB/WEB|WEB]].


