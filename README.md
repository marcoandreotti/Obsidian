# Cérebro do Arquiteto

Este repositório é um cofre Obsidian para organizar o conhecimento de arquitetura e produto do **OrderHub**. Ele funciona como um mapa navegável do projeto: reúne conceitos, fluxos, decisões e orientações para que pessoas e agentes de desenvolvimento encontrem contexto antes de propor ou fazer mudanças.

> O cofre documenta e conecta o conhecimento do projeto. O repositório de código, as especificações e as decisões oficiais continuam sendo as fontes de verdade.

## Ideias que orientam o cofre

- **Contexto antes da mudança:** entender produto, domínio e arquitetura ajuda a tomar decisões coerentes.
- **Conhecimento conectado:** notas e índices (MOCs) organizam os assuntos e ligam conceitos relacionados por wikilinks do Obsidian.
- **Decisões rastreáveis:** ADRs registram escolhas arquiteturais e apontam para suas fontes originais.
- **Orientação para agentes:** guias e regras ajudam agentes de programação a inspecionar o projeto, respeitar fronteiras e seguir os processos definidos.
- **Evidência explícita:** as notas distinguem decisões documentadas, observações inferidas do código e pontos que ainda precisam de confirmação.
- **Documentação viva:** o estado descrito pode mudar; confirme informações voláteis no checkout e nas fontes atuais.

## Projeto documentado: OrderHub

O OrderHub é descrito como uma plataforma SaaS multi-tenant para estabelecimentos de alimentação. A visão reúne três frentes principais:

- **Experiência pública:** cardápio, carrinho, checkout, confirmação e acompanhamento de pedidos.
- **Gestão e operação:** configuração do estabelecimento, catálogo, equipe, pedidos, cozinha, entrega, pagamentos e comunicações.
- **Plataforma:** identidade e provisionamento de tenants e unidades.

A documentação de produto também registra limites do que está validado: informações como pesquisa de mercado, métricas e clientes pagantes podem não estar identificadas nas fontes do repositório.

## Como navegar

Abra `Arquiteturando/Projetos/OrderHub/00 - Home/Home.md` no Obsidian para começar. A partir daí, siga os índices por assunto:

| Área | O que reúne |
| --- | --- |
| Produto | Objetivos, perfis de usuário e fluxos principais |
| Arquitetura | Componentes, camadas, dependências e fluxo de requisição |
| API e Web | Endpoints, autenticação, persistência, rotas, estado e integrações |
| Domínio | Contextos de negócio, entidades, regras e ciclo do pedido |
| Padrões | Convenções, segurança, validações, erros e testes |
| Decisões | Índice de ADRs e decisões arquiteturais registradas |
| Guias | Passos para criar features, endpoints, regras e telas |
| Agentes | Diretrizes e orientações específicas para backend e frontend |
| Evolução | Estado atual, backlog, melhorias e dívidas técnicas |

Comece por `Arquiteturando/Bússola de desenvolvimento para agentes.md`, o ponto de entrada do cofre para agentes; as regras detalhadas ficam em `Arquiteturando/Projetos/OrderHub/09 - Agentes/`. As notas de navegação explicam como seguir os wikilinks e como interpretar os níveis de evidência.

## Como interpretar as notas

- **Decisão documentada** aponta para uma fonte oficial, como um ADR ou especificação.
- **Observado no código** descreve a implementação encontrada e não define, por si só, uma regra arquitetural.
- **Inferência** é uma interpretação derivada das fontes e deve ser lida como tal.
- **A confirmar** ou **não identificado no repositório** sinaliza que a informação não foi comprovada nas fontes consultadas.
- Uma mudança OpenSpec ativa representa trabalho especificado ou em andamento; isso não significa necessariamente que já foi entregue.

Em caso de divergência, consulte primeiro as instruções `AGENTS.md`, as especificações, os ADRs e o código atual do OrderHub.

## Usando com Obsidian

Clone ou baixe o repositório e abra a pasta como um cofre no Obsidian. Os links `[[wikilink]]` funcionam como navegação interna no Obsidian; no GitHub, use a árvore de arquivos para abrir as notas.

## Atualização

As notas indicam a data do levantamento quando relevante. Antes de usar uma descrição para tomar decisões, confira a fonte e o estado atual do repositório do OrderHub.
