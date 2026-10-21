# OrderHub — Home

> Cérebro técnico e funcional do OrderHub. Levantamento em **2026-10-04**. Resumos com links às fontes; repositório é autoridade.

OrderHub é uma aplicação SaaS multi-tenant voltada a estabelecimentos de alimentação para configurar unidade/cardápio, receber pedidos e acompanhar preparação/retirada/entrega. Problema-alvo: centralizar o fluxo de pedido online e operação da unidade. Esse propósito vem de `README.md`, `PRODUCT.md` e código; validação comercial/usuários: ver [[Visão Geral]].

## Comece por aqui

1. [[Visão Geral]] e [[Objetivo do Produto]]
2. [[Mapa do Projeto]]
3. [[Arquitetura]] → [[Fluxo de uma Requisição]] → [[API]] / [[WEB]]
4. [[Domínio]] → [[Contextos de Negócio]] → [[Pedido]]
5. [[Padrões]] e [[Diretrizes para Agentes]]
6. [[Decisões]] e [[10 - Evolução/Estado Atual|Estado Atual]]
7. Para agentes de programação: [[Bússola de desenvolvimento para agentes|Bússola]] → [[Diretrizes para Agentes]]

## Áreas do conhecimento

- Proposta em avaliação: [[Atendimento por Mesa e Comanda Digital]]


- Produto: [[Visão Geral]], [[Usuários e Perfis]], [[Fluxos Principais]], [[01 - Produto/Estado Atual do Produto|Estado do Produto]]
- Arquitetura: [[Arquitetura]], [[Mapa de Componentes]], [[Dependências entre Camadas]]
- [[API]] · [[WEB]] · [[Domínio]] · [[Padrões]] · [[Decisões]] · [[Guias]]
- Agentes: [[Diretrizes para Agentes]] · [[Antes de Alterar o Código]]
- Evolução: [[10 - Evolução/Estado Atual|Estado Atual]], [[Dívidas Técnicas]], [[Melhorias Identificadas]]
- Avaliações e classificação: [[Avaliações e Classificação]] · [[Avaliação]] · [[Classificação e Reputação]]
- Fidelidade — ideia de produto, ainda não implementada: [[Fidelidade]]

## Estado rápido

Solução inclui onboarding/tenancy, autenticação, catálogo, ordering, avaliações, operações/KDS, clientes, entrega, pagamentos, promoções, reporting e notifications. Mudanças OpenSpec ainda ativas: [[Backlog Técnico]]. A capability de avaliações de restaurante e produtos foi implementada no change `add-customer-reviews`, com moderação pendente, classificação publicada e isolamento por unidade — ver [[Avaliações e Classificação]]. Primeiro commit disponível 2026-09-02; janela aferida de 32 dias até HEAD 2026-10-04 (33 commits); não prova início real.

Reconferência em 2026-10-07: checkout `6384863` (2026-10-06), árvore limpa, 35 commits e janela de 34 dias desde 2026-09-02. O snapshot de 2026-10-04 acima permanece como registro.

## Confiança

Em caso de conflito, leia `AGENTS.md`, documentação/ADRs/specs/código atuais. Ver [[Como navegar no cofre]].
