# Contribuição

## Princípios

Contribuições devem preservar composição mínima, segurança por padrão, editabilidade, compatibilidade explícita e rollback.

## Antes de alterar

1. Identifique a regra ou lacuna.
2. Consulte a base de conhecimento existente.
3. Evite duplicar referências.
4. Declare se a informação é evidência estática, comportamento validado ou hipótese.

## Alterações na Skill

- Mantenha `SKILL.md` curto e roteie detalhes para `references/`.
- Atualize cenários quando uma regra nova mudar decisões.
- Não adicione instruções genéricas que não alterem comportamento.
- Não inclua credenciais, tokens, dados pessoais ou ZIPs proprietários.
- Rode o validador de Skills antes de publicar.

## Segurança

Qualquer mudança envolvendo REST, AJAX, uploads, formulários, pagamentos, reservas, dados reais, produção ou dependências externas exige revisão de segurança e critérios de rollback.

## Commits

Use mensagens convencionais: `feat:`, `fix:`, `docs:`, `test:`, `chore:` ou `refactor:`.
