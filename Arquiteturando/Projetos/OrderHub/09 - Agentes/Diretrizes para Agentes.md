# Diretrizes para Agentes

Manual de navegação e execução para agentes que atuam no OrderHub. **As fontes oficiais do repositório prevalecem sobre este resumo**; consulte-as antes de implementar mudanças e verifique se mudaram.

## Ordem das fontes

1. `AGENTS.md` e instruções mais próximas do arquivo alterado.
2. ADRs em `openspec/decisions/`, especificações arquiteturais em `openspec/specs/architecture/`, convenções e Design System em `docs/web-design-system.md`.
3. Spec vigente em `openspec/specs/` e mudanças propostas em `openspec/changes/`. Diferencie requisito vigente de proposta em andamento.
4. Código, testes e configuração atuais como evidência da implementação.
5. Notas do cofre como índice; nunca como autoridade em conflito.

## Fluxo recomendado

**Entender → Localizar exemplos → Identificar camada → Avaliar impacto → Implementar → Validar padrões → Testar → Documentar → Relatar**

1. Identifique o contexto de negócio e leia a spec/change aplicável.
2. Localize código e testes análogos antes de abstrair algo.
3. Trace o fluxo completo e determine responsabilidades API, Application, Domain, Infrastructure e WEB.
4. Avalie efeitos nas camadas e dados tocados: API, WEB, domínio, banco/migrations, permissões, tenants, notificações e relatórios, conforme aplicável.
5. Siga a arquitetura e o padrão local; evite duplicar regra, abstração ou integração.
6. Preserve tenancy, autorização, validações e transações/outbox onde aplicáveis.
7. Execute verificações e Definition of Done prescritas; reporte exatamente o que foi executado e o que ficou pendente.
8. Atualize spec/docs/ADR quando o fluxo OpenSpec exigir ou quando uma decisão arquitetural for tomada.

## Regras de trabalho

- **CQRS:** use dispatchers próprios; Commands e Queries mantêm responsabilidades distintas. Não introduza MediatR nem AutoMapper (`AGENTS.md`).
- **Domain:** invariantes e regras de negócio no domínio; sem lógica autoritativa em endpoints ou componentes visuais.
- **Application:** casos de uso, handlers/validators e coordenação; não contorne o pipeline existente.
- **Persistência:** respeite EF Core para escrita e Dapper para leitura conforme arquitetura atual; mantenha consultas tenant-scoped. Antes de alterar schema/dados, revise migrations e os padrões de compatibilidade já usados.
- **API:** Minimal API/endpoint fino; autenticação, autorização e respostas seguem configurações e políticas existentes.
- **Multi-tenancy:** não confie em identificador vindo apenas do cliente; use o contexto/escopo validado pelo fluxo atual e teste isolamento.
- **WEB:** siga módulos, layouts, rota/access, cliente HTTP, tokens e componentes do Design System. Consulte [[Frontend - Guia do Agente]].
- **Assíncrono:** use async I/O e propague CancellationToken conforme instruções.
- **Testes/DoD:** siga `AGENTS.md` e checklist da spec. Não declare validação executada sem executá-la.
- **Segredos:** não copie credenciais para notas, logs ou respostas. Use configuração de exemplo; não leia nem exponha `.env`.
- **Documentação:** não converta observação em decisão. Siga o processo ADR/OpenSpec vigente.

## Incertezas e decisões

Quando requisito, regra de negócio ou motivação histórica não estiverem comprovados, sinalize **A confirmar** ou **Não identificado no repositório**. Não escolha silenciosamente uma interpretação que altere comportamento; consulte a spec, exemplos e responsáveis disponíveis no fluxo de trabalho.

Antes de encerrar uma change, siga o processo OpenSpec do repositório para revisar specs e tarefas. Uma lista de tarefas concluída, por si só, não comprova integração, release ou implantação.

Registre um ADR quando uma decisão arquitetural for efetivamente tomada e o processo do repositório exigir esse registro. Não crie ADR para transformar uma observação em decisão, nem invente a motivação de uma decisão passada.

## Relatório de conclusão

Ao finalizar, informe de forma verificável:

- arquivos e áreas alterados;
- specs, ADRs e padrões consultados;
- comandos/testes executados e seus resultados;
- verificações não executadas, limitações e pontos ainda **A confirmar**.

## Navegação

Detalhes por área: [[Regras Obrigatórias]], [[Antes de Alterar o Código]], [[Backend - Guia do Agente]], [[Frontend - Guia do Agente]]. Complementos: [[Arquitetura]], [[Padrões]], [[Guias]], [[Checklist de Desenvolvimento]].
