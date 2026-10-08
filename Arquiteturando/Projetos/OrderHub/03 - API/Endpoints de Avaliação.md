# Endpoints de Avaliação

> **Estado:** proposta do cofre, **não implementada**. Verificado no checkout `6384863` (2026-10-07): os grupos públicos existentes são apenas `/api/public/ordering` (`src/OrderHub.Api/PublicOrdering/PublicOrderingEndpoints.cs`) e o catálogo público (`src/OrderHub.Api/Catalog/CatalogEndpoints.cs`), ambos `AllowAnonymous()`; não há rota de avaliação.

Convenções a seguir: Minimal APIs em `internal static class <X>Endpoints` com `Map<X>Endpoints`, registro em `Program.cs`, DTOs `sealed record` em `src/OrderHub.Contracts/<Módulo>/` (nunca entidades), metadados `.Produces*` e erros pelo `GlobalExceptionMiddleware`. Ver [[Módulos e Endpoints]] e [[Camadas da API]].

## Superfície pública — anônima

| Método e rota proposta | Uso |
|---|---|
| `GET /api/public/ordering/orders/{reference}/reviews` | Situação do pedido: o que já foi avaliado e o que falta avaliar; monta a tela. |
| `POST /api/public/ordering/orders/{reference}/reviews` | Cria avaliação do estabelecimento e dos produtos do pedido; exige `Idempotency-Key`. |
| `GET /api/public/establishments/{slug}/reviews` | Lista paginada das avaliações publicadas da unidade. |
| `GET /api/public/establishments/{slug}/rating-summary` | Média, contagem e distribuição da unidade e por produto. |

Corpo proposto do `POST`: nota do estabelecimento, comentário do estabelecimento e coleção de itens de produto com `productId`, nota e comentário. A unidade é resolvida **pelo pedido/referência**, nunca aceita do cliente — mesmo critério de tenancy dos endpoints atuais ([[Multi-tenancy]]).

Idempotência segue o padrão de `PublicOrderRequest` (`src/OrderHub.Domain/Ordering/PublicOrderRequest.cs`): chave de 8–100 caracteres, hash SHA-256 do payload e unicidade por `(TenantId, EstablishmentId, Key)`; repetir a mesma chave devolve o mesmo resultado, sem segunda avaliação. Proposta: registro análogo `ReviewRequest` no módulo `Reviews`, não reutilizar a tabela de pedido.

## Superfície administrativa — sessão e policy

Prefixo proposto `/api/admin/establishments/{establishmentId:guid}/reviews`:

| Método e rota proposta | Policy proposta |
|---|---|
| `GET /reviews` | `Management`; filtros por nota, período e estado; resposta `PagedResponse<T>`. |
| `POST /reviews/{reviewId:guid}/hide` | `Management`; exige motivo. |
| `POST /reviews/{reviewId:guid}/restore` | `Management`. |

Não há endpoint de edição de nota nem de exclusão. Aplicar `Management` reutiliza o mapa existente (`src/OrderHub.Application/Identity/AdministrativePolicies.cs`); criar uma capacidade dedicada (ex.: `review-moderation`) exigiria alterar o `RoleMap` e é **A confirmar**.

## Erros mapeados (ProblemDetails)

| Situação | Status esperado | Origem |
|---|---|---|
| Nota ausente, fora de 1–5, comentário fora do tamanho | 400 com `errors` por campo | `ValidationException` via FluentValidation |
| Referência/pedido ou alvo inexistente | 404 | `NotFoundException` |
| Pedido já avaliado no mesmo alvo | 409 | `ConflictException` |
| Pedido não concluído, alvo fora do pedido, nota < 3 sem comentário | 422 | `DomainException` ("Regra de negócio não atendida") |

Os códigos seguem o middleware atual; validar contra o comportamento real antes de escrever a spec, pois o `GlobalExceptionMiddleware` é a autoridade do formato (`status`, `title`, `detail`, `instance`, `traceId`, `errors`).

## Validação e abuso

- FluentValidation para formato: nota inteira presente, faixa 1–5, tamanho do comentário, referência com 48 hex minúsculos (`^[a-f0-9]{48}$`) e presença de ao menos um alvo. A obrigatoriedade condicional do comentário é **invariante de domínio**; o validator pode antecipá-la para melhorar a mensagem, sem substituí-la — ver [[Validações]].
- Hoje o único rate limit é `authentication-attempts` (20/min por IP) aplicado a `/api/auth/begin|complete`. Endpoint público de avaliação sem limite é risco de abuso; proposta de política própria (por IP e por referência) é **A confirmar**.

## Testes propostos

`tests/OrderHub.Integration.Tests/Reviews/PublicReviewsApiTests.cs` e `AdminReviewsApiTests.cs` (WebApplicationFactory, ambiente `Testing`), seguindo o padrão de `PublicOrderingApiTests.cs`: casos de nota inválida, comentário obrigatório ausente, pedido não concluído, segunda avaliação, idempotência e isolamento entre unidades.

## Relacionados

[[Avaliação]] · [[Classificação e Reputação]] · [[Avaliações e Classificação]] · [[Endpoints de Pedido]] · [[Autenticação e Autorização]] · [[Tratamento de Erros]] · [[03 - API/Módulos e Endpoints|Módulos e Endpoints]]
