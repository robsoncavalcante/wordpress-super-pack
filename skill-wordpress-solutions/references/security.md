# Segurança

## Entrada e saída

Receba, valide tipo e allowlist, autorize, sanitize, processe, escape conforme contexto e registre somente o necessário.

## REST, AJAX e formulários

- Toda rota REST deve ter `permission_callback`.
- Nonces protegem CSRF, mas não substituem capabilities.
- Não confiar em hidden fields para ownership, status, preço, permissões ou IDs.
- Limitar paginação, filtros, uploads, datas, ranges e payloads.
- Não aceitar meta keys, tabelas, operadores ou orderby arbitrários.

## Dados e cache

Revisar exposição por HTML, REST, AJAX, logs, sitemap, schema e cache. Dados privados exigem autorização server-side e cache compatível com contexto.

## Integrações

Usar secrets fora do código, timeout, retry controlado, idempotência, validação de webhook e logs sem tokens ou dados pessoais.
