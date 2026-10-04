# Dívidas Técnicas

Esta nota registra lacunas evidenciadas, não uma auditoria de qualidade completa.

| Item | Evidência | Estado/limite |
|---|---|---|
| UX de ordering público ainda não validada por usuário | `PRODUCT.md` | Risco explicitamente registrado; não tratar como bug de código confirmado. |
| Observabilidade proposta | OpenSpec `add-observability` | Change ativa; tasks abertas no snapshot; health/correlation já existem parcialmente. |
| Auditoria proposta | OpenSpec `add-audit-trail` | Tasks abertas; falta implementação segundo proposta. |
| Integração de agente cliente IA | OpenSpec `add-ai-customer-agent` | 0/7 tarefas concluídas no snapshot. |
| Provedor de pagamento online | Não identificado | Não inferir que processamento online está disponível. |
| Teste específico de persistência de delivery | Não identificado pelo levantamento | Confirmar nova busca antes de concluir ausência definitiva. |
| Credenciais reais/prod | Não avaliadas | `.env` não foi lido; nada inferido sobre ambiente. |

Ver [[10 - Evolução/Estado Atual|Estado Atual]], [[Backlog Técnico]], [[Melhorias Identificadas]].


