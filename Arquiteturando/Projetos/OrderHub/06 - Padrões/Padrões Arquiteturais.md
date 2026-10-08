# Padrões Arquiteturais

## Regra documentada

OrderHub é um monólito modular .NET com fronteiras por projeto/camada e dependências verificadas por testes de arquitetura. ADR-001 registra a decisão. Application usa CQRS com dispatchers próprios; escrita e leitura têm caminhos distintos. Infrastructure implementa portas/contratos e integrações. API compõe a aplicação; Vue WEB é cliente separado.

## Observação no código

Projects: Domain, Application, Contracts, Infrastructure, Api, Infrastructure.Migrations. Endpoints Minimal API agrupados por módulo. Application dispatchers: `src/OrderHub.Application/Dispatching/CommandDispatcher.cs`, `QueryDispatcher.cs`; read gateways Dapper e write repositories EF Core.

## Para novas mudanças

Siga `AGENTS.md`, `openspec/architecture.md` e os ADRs em `openspec/decisions/`; preserve direção de dependências e teste arquitetural. Não introduza microservices, MediatR ou AutoMapper: AGENTS proíbe MediatR/AutoMapper e ADR documenta modular monolith. Não mova regra de negócio para API/UI.

Relacionado: [[Dependências entre Camadas]], [[Camadas da API]], [[Padrões de Backend]], [[Decisões]].


