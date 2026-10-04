# Como criar um novo Endpoint

Leia endpoint semelhante em `src/OrderHub.Api/` (endpoints agrupados por módulo) e `AGENTS.md`. Confirme contrato/spec, grupo/rota e política de autorização. Endpoint deve permanecer fino: validação/use case pelo Application dispatcher, regra no Domain, dados por abstração apropriada. Para leitura use query/read gateway; para escrita command e fluxo transacional existente. Propague cancellation; mapeie erro conforme ProblemDetails/contrato. Adicione teste apropriado (API/integration) e teste do caso de uso. WEB consumidor deve usar cliente local e cliente HTTP comum.

Ver [[Camadas da API]], [[Endpoints de Pedido]], [[Autenticação e Autorização]], [[Checklist de Desenvolvimento]].


