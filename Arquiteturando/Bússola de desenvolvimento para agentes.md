# Bússola de desenvolvimento para agentes

> Ponto de entrada do **Cérebro do OrderHub** para agentes de programação. Esta nota descreve o **método** de uso do cofre; as regras detalhadas ficam na seção [[09 - Agentes/Diretrizes para Agentes|09 - Agentes]] e o conteúdo vinculante continua no repositório (`AGENTS.md`, specs, ADRs e código). Levantamento em 2026-10-07.

## Para que serve este cofre

O cofre reúne produto, domínio, arquitetura, API, WEB, padrões, decisões e evolução do OrderHub em notas conectadas por wikilinks. Use-o **no início da tarefa** para recuperar contexto, intenção, histórico e vocabulário — e navegue apenas pelas notas relacionadas ao pedido.

O cofre **não é autoridade**: em conflito, valem `AGENTS.md`, `openspec/`, ADRs, specs e o código atual. Toda afirmação relevante nas notas traz caminho de arquivo justamente para você conferir na fonte.

## Níveis de evidência (leia antes de agir)

| Marcador na nota | O que significa para você |
|---|---|
| Fato observado | Encontrado no checkout citado, com caminho de arquivo. Ainda assim, confirme no código atual. |
| Decisão documentada | Registrada em ADR/spec do repositório; a nota do cofre é retrospectiva, não a decisão. |
| Proposta do cofre | Desenho **não implementado** (ex.: [[Avaliações e Classificação]]). Não é requisito e não deve ser implementado por conta própria. |
| **A confirmar** / **Não identificado no repositório** | Não comprovado nas fontes consultadas. Não transforme em regra nem em premissa. |

## Por onde começar, conforme a tarefa

- **Entender o produto:** [[Visão Geral]] → [[Objetivo do Produto]] → [[Fluxos Principais]].
- **Entender o domínio:** [[Domínio]] → [[Contextos de Negócio]] → [[Pedido]] → [[Regras de Negócio]].
- **Backend e API:** [[Arquitetura]] → [[Fluxo de uma Requisição]] → [[API]] → [[Módulos e Endpoints]] → [[Backend - Guia do Agente]].
- **Frontend:** [[WEB]] → [[Estrutura Frontend]] → [[Rotas]] → [[Comunicação com a API]] → [[Frontend - Guia do Agente]].
- **Propor uma mudança:** [[Como criar uma nova Feature]] → [[Checklist de Desenvolvimento]] → [[Diretrizes para Agentes]].
- **Saber o que está em andamento:** [[10 - Evolução/Estado Atual|Estado Atual]] → [[Backlog Técnico]] → [[Dívidas Técnicas]].
- **Não sabe onde está:** [[Como navegar no cofre]] e [[Mapa do Projeto]].

## Protocolo de trabalho

1. **Ordem das fontes:** `AGENTS.md` (e instruções mais próximas do arquivo) → `openspec/architecture.md`, ADRs em `openspec/decisions/` e `openspec/conventions.md` → spec vigente e change ativa → código e testes atuais → notas do cofre como índice.
2. **Localize o análogo** antes de criar: siga o padrão do módulo vizinho (comando, handler, validador, configuração EF, read gateway, página, teste).
3. **Respeite as fronteiras:** invariante no Domain, caso de uso na Application, endpoint fino na API, EF Core só na escrita e Dapper só na leitura.
4. **Não infira regra de negócio** a partir da interface, do nome de uma policy ou de uma nota do cofre; confirme na spec e no código.
5. **Multi-tenancy sempre:** a unidade vem do contexto validado no servidor, nunca de identificador enviado pelo cliente.
6. **Diferencie requisito vigente de proposta:** change ativa complementa a spec, não a substitui; change arquivada não prova entrega.
7. **Valide de fato e relate:** execute os testes/verificações pertinentes e informe o que rodou, o que não rodou e o que permanece **A confirmar**.
8. **Atualize a fonte certa:** requisito e decisão pelo fluxo OpenSpec/ADR do repositório; o cofre é índice, não destino de decisão.

## Regras que não podem ser quebradas

- Sem MediatR e sem AutoMapper — há teste arquitetural que proíbe os pacotes.
- FluentValidation para entrada; invariante de negócio no Domain.
- Domain não referencia camadas externas.
- Sem segredo real em nota, log ou resposta.
- Não declare validação executada sem tê-la executado.

Detalhamento e exceções: [[Regras Obrigatórias]] e [[Antes de Alterar o Código]].

## Limites do cofre

- O levantamento é **datado**: cada nota registra o checkout conferido (atual `6384863`, de 2026-10-06, com reconferências em 2026-10-07). Item volátil exige nova conferência.
- Presença de código ou teste não comprova produção; checklist concluído não comprova release.
- Propostas do cofre aguardam o fluxo OpenSpec do repositório antes de virarem requisito.

## Navegação

[[00 - Home/Home|Home]] · [[Como navegar no cofre]] · [[Mapa do Projeto]] · [[Diretrizes para Agentes]] · [[Regras Obrigatórias]] · [[Antes de Alterar o Código]] · [[Backend - Guia do Agente]] · [[Frontend - Guia do Agente]] · [[Guias]] · [[Padrões]] · [[Decisões]] · [[10 - Evolução/Estado Atual|Estado Atual]]
