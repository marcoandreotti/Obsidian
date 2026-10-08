# Glossário

| Termo | Significado no projeto |
|---|---|
| Tenant | Cliente organizacional SaaS, com `PublicCode`, nome/estado; ver [[Tenant]]. |
| Estabelecimento / unidade | Unidade operacional pertencente a Tenant, identificada publicamente por slug; [[Estabelecimento]]. |
| Escopo tenant-scoped | Registro/consulta pertencente a um Tenant. |
| Escopo establishment-scoped | Registro/consulta pertencente a unidade, normalmente também Tenant. |
| Owner/Admin/Manager/Attendant/Kitchen/Delivery | Enum `AdministrativeRole`, não nomes de claims livres. |
| Capability/Policy | Permissão nomeada aplicada na API, mapeada de papéis em `AdministrativePolicies`. |
| Command | Request Application que altera estado. |
| Query | Request Application de leitura apenas. |
| Read model | Projeção para resposta/query; pode ser Dapper DTO. |
| Outbox | Mensagem persistida na mesma transação de negócio, processada depois. |
| Referência pública | Token opaco do pedido, distinto de ID interno/sequência. |
| KDS | Kitchen Display System, fila de produção da cozinha. |
| Surface | Contexto visual/operacional Public, Administration, Operations, KDS ou Platform. |
| Idempotency key | Chave estável para evitar duplicação lógica em confirmações/retries. |
| ProblemDetails | Formato padronizado `application/problem+json` para erro HTTP. |
| Avaliação | Nota de 1 a 5 dada pelo consumidor ao estabelecimento ou a produto de um pedido concluído; comentário obrigatório abaixo de 3. Proposta do cofre, não implementada; [[Avaliação]]. |
| Nota | Inteiro de 1 a 5 atribuído a um alvo avaliado. Proposta do cofre, não implementada. |
| Comentário obrigatório | Texto exigido quando a nota é 1 ou 2; não vazio após normalização, 10 a 1000 caracteres na proposta. |
| Classificação / Reputação | Média, contagem e distribuição das avaliações publicadas de uma unidade ou de um produto; proposta do cofre, não implementada; [[Classificação e Reputação]]. |

Termos em inglês usados por contracts/specs permanecem técnicos; não inferir domínio além da definição da fonte.


