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

## Áreas do conhecimento

- Produto: [[Visão Geral]], [[Usuários e Perfis]], [[Fluxos Principais]], [[01 - Produto/Estado Atual|Estado do Produto]]
- Arquitetura: [[Arquitetura]], [[Mapa de Componentes]], [[Dependências entre Camadas]]
- [[API]] · [[WEB]] · [[Domínio]] · [[Padrões]] · [[Decisões]] · [[Guias]]
- Agentes: [[Diretrizes para Agentes]] · [[Antes de Alterar o Código]]
- Evolução: [[10 - Evolução/Estado Atual|Estado Atual]], [[Dívidas Técnicas]], [[Melhorias Identificadas]]
- Proposta em estudo, não implementada: [[Avaliações e Classificação]] · [[Avaliação]] · [[Proposta - Avaliações e Classificação]]

## Estado rápido

Solução inclui onboarding/tenancy, autenticação, catálogo, ordering, operações/KDS, clientes, entrega, pagamentos, promoções, reporting e notifications. Mudanças OpenSpec ainda ativas: [[Backlog Técnico]]. Avaliações de restaurante e de produtos pelo usuário público (nota 1–5, comentário obrigatório abaixo de 3) são **proposta do cofre**, sem implementação — ver [[Avaliações e Classificação]]. Primeiro commit disponível 2026-09-02; janela aferida de 32 dias até HEAD 2026-10-04; não prova início real.

## Confiança

Em caso de conflito, leia `AGENTS.md`, documentação/ADRs/specs/código atuais. Ver [[Como navegar no cofre]].



