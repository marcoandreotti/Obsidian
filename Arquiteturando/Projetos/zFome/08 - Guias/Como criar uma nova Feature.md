# Como criar uma nova Feature

1. Localize capability e leia spec vigente/changes; identifique domínio afetado.
2. Verifique módulo, ADR, exemplos e testes existentes.
3. Desenhe fronteiras API/Application/Domain/Infrastructure/WEB sem dependências invertidas.
4. Escreva/atualize spec e tasks pelo fluxo OpenSpec do repositório.
5. Implemente os slices necessários com validação, auth/tenant, persistência e UI apropriadas.
6. Teste por camada, atualize docs e confira Definition of Done em AGENTS.md.

Não presumir que toda feature precise de todas as camadas. Fontes: `AGENTS.md`, `.agents/skills/openspec-*`. Relacionado [[Diretrizes para Agentes]].


