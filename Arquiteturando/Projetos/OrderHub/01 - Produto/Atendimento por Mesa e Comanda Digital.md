# Atendimento por Mesa e Comanda Digital

> **Estado:** proposta de evolução mapeada no Cérebro; não implementada nem convertida em change OpenSpec. O vault registra fluxo de pedido do tipo `Table`, rota pública com `tableToken` e configuração de mesas/QR no onboarding. Esses registros não comprovam, por si só, comandas compartilhadas, divisão de conta ou controle de ocupação completo. Reconferir o checkout e as specs do OrderHub antes de especificar ou implementar.

## Visão

Evoluir o atendimento presencial para que o estabelecimento organize mesas e ocupação, receba pedidos digitais associados à mesa, acompanhe preparo e entrega, e feche uma ou mais contas de forma clara. A experiência deve funcionar bem em celular e manter operação assistida por equipe e caixa.

A solução atende restaurantes, bares, pizzarias, hamburguerias, padarias, lanchonetes, carrinhos de lanche, churrascarias, serviços de delivery e praças de alimentação. **Mesa e comanda são capacidades opcionais por modalidade e unidade**: delivery, retirada e operações sem mesas não devem ganhar etapas de salão.

## O que já aparece no Cérebro

- [[Fluxos Principais]] registra pedido público por mesa em `/order/{slug}/table/{tableToken}`.
- O onboarding da unidade já é descrito como incluindo mesas e QR.
- [[Pedido]] registra o tipo de serviço `Table` e os estados `Draft`, `Confirmed`, `Preparing`, `Ready`, `OutForDelivery`, `Completed`, `Cancelled` e `Rejected`.
- [[Pagamento]] documenta configuração de meios de pagamento, mas não identifica provedor externo nem confirma pagamento online.
- O snapshot de produto lista disponibilidade e relatórios, mas não comprova gestão de estoque por quantidade. Confirmar fontes atuais antes de planejar integração.

## Analogia com o rascunho e ajustes

| Ideia do rascunho | Ajuste recomendado |
| --- | --- |
| Atender vários tipos de alimentação | Configurar capacidades por unidade e modalidade: salão/mesa, balcão/retirada e delivery. Carrinhos e operações temporárias podem usar pedidos sem cadastro rígido de mesas. |
| QR para acompanhar gastos | O estabelecimento cria o QR de mesa; o cliente usa a câmera do próprio celular para escaneá-lo. O QR identifica a mesa e inicia uma sessão segura. Não é necessário o cliente gerar um QR. |
| QR seguro que muda a cada comanda | Separar o identificador físico da mesa da sessão de atendimento. Preferir QR fixo da mesa que não contenha dados pessoais ou de pagamento; após validar a mesa, o servidor emite um token opaco, limitado e revogável para a sessão/comanda ativa. Invalidar sessões ao encerrar ou reabrir conforme regra definida. QR dinâmico exibido pelo app do estabelecimento é alternativa para locais que tenham uma tela por mesa. |
| Número fixo e complemento por pessoa | Manter número/identificador estável da mesa e criar comandas ou contas vinculadas à visita ativa. Complementos são identificadores de conta/pessoa, não novos números físicos de mesa. |
| Mesa disponível quando todas as comandas fecharem | Controlar ciclo da visita/ocupação separadamente do estado de um pedido. Só liberar a mesa após todas as contas e pedidos vinculados serem encerrados, sem pagamentos pendentes e após confirmação da operação. |
| Dividir conta por quantidade de comandas | Permitir contas separadas por pessoa, divisão igualitária e divisão seletiva de itens. Definir como tratar itens compartilhados, taxas, descontos, gorjeta, pagamento parcial e alteração de pedidos após a primeira conta. |
| Lugares dinâmicos, adicionar cadeira ou juntar mesa | Registrar capacidade configurada e permitir ajuste operacional de lugares/união temporária de mesas com trilha de auditoria. Diferenciar capacidade física, lugares ocupados e quantidade de contas. |
| Total aparece no primeiro pedido | Exibir valores atualizados apenas às pessoas autorizadas pela sessão. Por padrão, cada cliente vê sua conta; total consolidado da mesa pode ser mostrado a quem iniciou ou coordena o fechamento. Definir privacidade e permissão antes de expor gastos de terceiros. |
| Cores por etapa do pedido | Usar o estado canônico do servidor, com texto e ícone além da cor para acessibilidade. Mapear rótulos de salão aos estados existentes; não criar estados redundantes sem necessidade validada. |
| Fechar conta envia ao app principal/caixa | Criar solicitação de fechamento que aparece na fila de caixa/operação com mesa, contas, total e situação. Pedido de fechamento não equivale a pagamento confirmado nem libera automaticamente a mesa. Confirmar se já existe módulo de caixa e como integra com pagamentos. |
| Cliente também pode pedir fechamento | Permitir solicitação pela sessão móvel da mesa; equipe/caixa revisa a conta e conclui conforme políticas da unidade. Evitar que uma solicitação do cliente altere diretamente estado financeiro. |

## Jornada recomendada

1. A unidade habilita atendimento de salão, configura mesas, capacidade e regras de conta.
2. Um QR é associado a cada mesa. O cliente escaneia e acessa o cardápio web móvel da unidade, sem instalação obrigatória de app.
3. O servidor valida o QR e cria ou associa o cliente à visita/comanda ativa da mesa, emitindo uma sessão com escopo restrito e expiração/revogação definidas.
4. O cliente envia um pedido de mesa. O pedido entra na operação e no KDS usando o fluxo existente; a equipe entrega à mesa.
5. A sessão permite acompanhar os próprios itens e valores. A equipe pode organizar contas individuais ou agrupadas conforme regras da unidade.
6. Cliente ou atendente solicita fechamento. O caixa recebe uma tarefa, revisa as contas e registra pagamento/fechamento pelos meios realmente suportados.
7. Após todas as contas e pedidos serem encerrados, a equipe finaliza a visita. A mesa retorna a disponível.

## Escopo inicial sugerido

**Primeiro recorte:** experiência web responsiva para cliente e equipe; associação segura de pedido à mesa; visita ativa; acompanhamento do pedido; contas individuais e consolidadas com divisão simples; solicitação e tratamento de fechamento; transições de ocupação auditáveis.

**Deixar para etapa posterior:** pagamento dividido entre vários meios, transferência de itens entre contas, união dinâmica de mesas com mapa visual, QR rotativo em tela dedicada, inventário quantitativo integrado, fidelidade e relatórios avançados de salão.

Controle de estoque exige definição própria de insumos, receitas, baixa por venda, perdas, ajustes e inventário. O rascunho menciona estoque e relatórios completos, mas isso não está especificado aqui como consequência automática da comanda.

## Segurança, confiabilidade e operação

- Tokens de mesa não devem ser previsíveis, conter PII, preço ou autorização de pagamento; validar tenant/unidade/mesa/sessão no servidor.
- Aplicar expiração, revogação ao fechar a visita, limitação de tentativas e proteção contra reenvio duplicado de pedidos/solicitações.
- Garantir isolamento entre unidades e não permitir que o cliente escolha livremente uma mesa fora do QR validado.
- Registrar quem abriu, alterou, dividiu, fechou ou reabriu conta; exigir permissão de equipe para ajustes financeiros e de ocupação.
- Preservar consistência entre estado do pedido, conta, pagamento e visita de mesa. Definir recuperação de falha de rede e ações repetidas.
- Exibir estados com rótulo e acessibilidade; usar atualizações em tempo real quando disponíveis e estratégia de atualização de fallback.
- Projetar primeiro para uso em celular e telas pequenas. PWA/nativo é decisão posterior; o escopo não deve exigir instalação do cliente.

## Decisões em aberto

- Uma visita de mesa pode conter um pedido único, vários pedidos ou ambos? Como pedidos se agrupam numa conta?
- A primeira abertura da visita é feita por atendente, pelo primeiro pedido autenticado pelo QR ou por ambos?
- Como identificar clientes sem exigir conta, e como reconciliar sua identidade com [[Cliente]]?
- Como suportar adolescente/criança, visitante sem celular, conexão indisponível e pedidos feitos por atendente?
- Quem pode ver o total da mesa e iniciar divisão/fechamento?
- Quais regras valem para taxa de serviço, couvert, gorjeta, descontos, cancelamentos e pagamentos parciais?
- O que significa exatamente “entregue” para pedido de mesa, e o estado atual por pedido é suficiente ou itens precisam de estados próprios?
- Como refletir capacidade/união de mesas sem criar conflito com a configuração física?
- Qual é a fronteira entre comanda, conta, pedido e pagamento no modelo atual?
- Quais relatórios de salão são prioritários e quais dados de estoque são necessários?
- A unidade possui um caixa operacional existente ou isso exige novo módulo? Há integração de pagamento disponível?

## Próximos passos

Validar o fluxo com atendentes, caixa e clientes em celular; confirmar no código/specs atuais o comportamento de `Table`, `tableToken`, QR do onboarding, status e pagamento; fechar as decisões que afetam domínio e segurança; então propor change OpenSpec com requisitos e cenários testáveis. Não tratar este rascunho como especificação ativa.

## Relacionados

[[Fluxos Principais]] · [[Pedido]] · [[Fluxo de Pedido]] · [[Pagamento]] · [[Telas de Pedido]] · [[Cliente]] · [[Estado Atual do Produto]]