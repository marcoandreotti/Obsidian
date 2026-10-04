# ADR-002 - Platform Identity and Authentication Bootstrap

## Contexto e decisão

[ADR-002 original](file:///C:/Users/marco/source/repos/OrderHub/openspec/decisions/ADR-002-platform-identity-and-authentication-bootstrap.md) registra identidade de plataforma separada da identidade administrativa e bootstrap/autenticação da plataforma.

## Motivo

Não extrapolar além do contexto escrito na fonte; consultar seção Context do original.

## Consequências

Separação aparece em APIs/áreas de identidade e autorização. Fluxo atual também inclui MFA administrativo; veja [[Autenticação e Autorização]]. Não confundir esses mecanismos.

## Alternativas

Estão no ADR original.

## Referências

`src/OrderHub.Application/Identity/`, `src/OrderHub.Api/Authentication/`, specs `openspec/specs/identity/` e `tenancy/`.


