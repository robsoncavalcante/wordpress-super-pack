# QA e critérios de aceite

## Matriz mínima

### Funcional

- fluxo principal completo;
- estados vazio, inválido, duplicado e expirado;
- usuário anônimo e autenticado;
- roles e ownership;
- mobile e desktop;
- fallback quando dependência está ausente.

### Segurança

- nonce/CSRF;
- capability e permission callback;
- sanitização e escape;
- SQL preparado;
- upload e MIME;
- REST/AJAX;
- cache contextual;
- logs sem tokens ou dados desnecessários.

### Performance

- quantidade de assets;
- consultas e paginação;
- payload AJAX;
- imagens e fontes;
- cache;
- cron e tarefas longas;
- comportamento em catálogo grande.

### SEO e acessibilidade

- title, canonical, robots e schema;
- sitemap e redirects;
- headings e landmarks;
- teclado e foco;
- labels e mensagens;
- alt text;
- reduced motion;
- contraste e leitura.

## Critério de aceite

Uma entrega só está pronta quando:

1. o fluxo solicitado funciona;
2. dados e permissões estão corretos;
3. erros são tratados de forma compreensível;
4. testes críticos foram executados;
5. o diff foi revisado;
6. dependências e versões estão registradas;
7. rollback é possível;
8. limitações remanescentes foram declaradas.

## Parar e pedir decisão

Pare antes de executar quando houver:

- ambiguidade que muda o modelo de dados;
- risco de apagar ou sobrescrever dados reais;
- mudança de pagamento, credencial, DNS ou produção;
- licença/procedência não comprovada;
- incompatibilidade de versão;
- necessidade de publicar sem aceite;
- segurança crítica não mitigada.
