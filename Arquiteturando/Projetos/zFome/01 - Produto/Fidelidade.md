# Fidelidade

> **Estado:** ideia de produto mapeada no Cérebro; não implementada e ainda sem change OpenSpec. Esta nota registra o conceito inicial, não define requisitos vigentes.

## Ideia

A **Fidelidade** representa um status associado ao cliente e atribuído pelo restaurante. A intenção é permitir que a unidade reconheça e acompanhe clientes que participam de seu relacionamento de fidelidade.

Em uma fase futura, o restaurante poderá associar benefícios a essa experiência, como descontos exclusivos, brindes ou itens gratuitos. Esses exemplos são possibilidades, não benefícios prometidos nem regras aprovadas.

## Escopo inicial conhecido

- O restaurante é quem adiciona ou atribui o status de fidelidade ao cliente.
- A ideia se relaciona ao cadastro de [[Cliente]] e à área de produto de relacionamento com clientes.
- Os benefícios são uma possibilidade futura, fora do escopo definido desta ideia inicial.

## Decisões em aberto

Antes de transformar a ideia em requisito ou implementação, ainda é necessário definir:

- O que caracteriza um cliente com status de fidelidade e quais status existirão.
- Se o status é manual, automático ou admite os dois caminhos. A atribuição pelo restaurante é a intenção inicial registrada; qualquer automação futura precisa ser definida.
- Quem, dentro do restaurante, pode atribuir, alterar ou remover o status.
- Se o status pertence ao cliente dentro de uma unidade, a todo o tenant ou a outro escopo.
- Como identificar o cliente com consistência entre pedidos e canais.
- Quais informações e histórico devem ser registrados, e como o cliente será informado.
- Se e como benefícios serão configurados, concedidos, limitados e auditados.
- Como evitar concessões indevidas e como tratar cancelamentos, reembolsos ou abuso.

## Relação com Avaliações

[[Avaliações e Classificação]] trata da opinião do cliente sobre o estabelecimento e os produtos. Fidelidade trata de um status de relacionamento atribuído pelo restaurante. As duas ideias podem coexistir no contexto do cliente, mas uma avaliação não concede nem altera automaticamente o status de fidelidade conforme o escopo atualmente conhecido.

## Próximos passos

Quando houver definição de regras e prioridade, validar o conceito de produto, verificar o cadastro e a identidade de [[Cliente]], e então propor uma change OpenSpec seguindo o processo vigente do repositório ZFome. Registrar a implementação e atualizar esta nota somente após confirmar o comportamento nas fontes oficiais.

## Relacionados

[[Cliente]] · [[Avaliações e Classificação]] · [[Melhorias Identificadas]] · [[Estado Atual do Produto]]