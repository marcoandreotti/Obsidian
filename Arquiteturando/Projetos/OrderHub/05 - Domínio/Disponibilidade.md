# Disponibilidade

Configuração de horários de funcionamento, pausas, exceções, fuso horário e estado ativo da unidade condiciona disponibilidade do pedido agendado e atendimento. Código em Domain Operations e Application Availability; UI `web/OrderHub.Web/src/modules/administration/availability/` (confirmar arquivos específicos no checkout).

Relaciona [[Estabelecimento]], [[Pedido]] e [[Fluxo de Pedido]]. Spec `openspec/specs/operations/service-configuration/spec.md`; também onboarding. Fuso padrão observado em `Establishment.cs`: `America/Sao_Paulo`/São Paulo (consulte valor literal no código). Testes `OperationsTests` e `availability.test.ts`.


