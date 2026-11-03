# WordPress Core — mapa técnico inicial

## Escopo e evidência

Baseado na listagem estática do pacote `wordpress-7.1.4-pt_BR.zip`. Nenhum arquivo PHP foi executado. O documento descreve a arquitetura observada e padrões gerais de extensão; não substitui testes em uma instalação isolada.

## 1. Ciclo de execução

O fluxo de uma requisição WordPress pode ser modelado assim:

1. O servidor web entrega um entry point (`index.php`, `wp-admin/*`, `wp-login.php`, `xmlrpc.php`, `wp-cron.php` ou um endpoint REST/AJAX).
2. O bootstrap carrega `wp-config.php`, constantes, ambiente e banco.
3. `wp-settings.php` inicializa o Core, carrega plugins ativos, tema e arquivos de configuração.
4. Plugins e tema registram hooks, tipos de conteúdo, rotas, shortcodes, widgets e serviços.
5. A requisição é roteada para o front controller, REST, AJAX, administração ou cron.
6. O WordPress consulta opções, usuários, posts, termos, metadados e transientes.
7. A resposta passa por filtros de conteúdo, headers, cache e serialização.

Regra de projeto: código de plugin deve registrar comportamento em hooks apropriados, evitando executar lógica pesada no carregamento global do arquivo.

## 2. Superfícies principais de extensão

### Plugins

- arquivo principal com cabeçalho do plugin;
- hooks de ativação, desativação e desinstalação;
- actions e filters;
- registro de opções, menus e capabilities;
- post types, taxonomias, metadados e shortcodes;
- REST routes, AJAX actions e WP-CLI commands;
- enqueue de scripts e estilos;
- integração com cron e transients.

### Temas

- `functions.php` e hooks de tema;
- templates e template parts;
- `theme.json`, estilos e blocos;
- suporte a menus, thumbnails, HTML5 e recursos do editor;
- filtros de renderização e conteúdo.

### Dados

- posts e post types;
- postmeta;
- terms e termmeta;
- users e usermeta;
- options e site options;
- comentários;
- tabelas próprias somente quando o volume e o modelo justificarem.

## 3. APIs que a Skill deve conhecer

### Conteúdo e dados

- `register_post_type()` e `register_taxonomy()`;
- `register_post_meta()`;
- `get_post_meta()`, `update_post_meta()` e APIs de opções;
- `WP_Query`, `WP_Term_Query`, `WP_User_Query`;
- `wp_insert_post()`, `wp_update_post()` e APIs de termos;
- `$wpdb` com `prepare()` para SQL parametrizado.

### HTTP e integração

- HTTP API (`wp_remote_get()`, `wp_remote_post()`);
- REST API com `register_rest_route()`;
- autenticação e permission callbacks;
- webhooks com validação de assinatura;
- timeouts, retries, idempotência e logs sem segredos.

### Interface e assets

- Settings API;
- `add_menu_page()` e menus de administração;
- `wp_enqueue_script()` e `wp_enqueue_style()`;
- dependências, versões, `wp_localize_script()`/dados estruturados;
- editor de blocos e registro de blocos.

### Execução assíncrona

- `wp_ajax_{action}` e `wp_ajax_nopriv_{action}`;
- REST para operações públicas ou autenticadas;
- WP-Cron para tarefas pequenas e recorrentes;
- Action Scheduler quando o ecossistema WooCommerce já o fornece;
- processamento em lotes, checkpoints e reexecução segura.

## 4. Segurança obrigatória

Toda entrada externa deve seguir o fluxo:

`receber → validar tipo/permitidos → autorizar → sanitizar → processar → escapar na saída → registrar resultado seguro`

Checklist mínimo:

- verificar capability, não apenas login;
- usar nonce contra CSRF em formulários e AJAX;
- usar `permission_callback` em toda rota REST;
- aplicar `sanitize_*()` na entrada e `esc_*()` na saída;
- usar `$wpdb->prepare()` para valores dinâmicos;
- restringir uploads por tipo, tamanho, MIME e capacidade;
- não confiar em nomes de arquivos, IDs ou parâmetros vindos do cliente;
- impedir exposição involuntária por REST, AJAX, logs e mensagens de erro;
- nunca armazenar tokens, senhas ou chaves em código, posts ou opções públicas;
- validar webhooks e aplicar idempotência;
- evitar desserialização de dados controlados pelo usuário;
- limitar operações administrativas a capabilities específicas.

## 5. Performance e confiabilidade

- Evitar consultas dentro de loops quando uma consulta agregada resolver o caso.
- Não executar importações grandes em uma única requisição web.
- Dividir tarefas em lotes pequenos, com checkpoint e cron próprio.
- Usar cache de objeto e transients somente com invalidação definida.
- Enfileirar assets apenas onde são necessários.
- Não carregar todos os módulos de plugins em todas as páginas sem necessidade.
- Medir consultas, tempo de resposta, memória e tamanho dos assets.
- Tratar cron como eventualmente executado: tarefas devem ser reentrantes.
- Fazer backup antes de migrations, limpeza ou alteração em dados reais.

## 6. Riscos específicos para projetos com Elementor e JetEngine

- Exposição de campos privados através da REST API ou listings.
- Queries dinâmicas sem limites, filtros ou paginação.
- Formulários que gravam posts/meta sem capability adequada.
- Callbacks e macros que executam consultas repetidas.
- AJAX público sem rate limit ou validação de origem.
- Templates que exibem HTML não escapado.
- Importação de JSON/XML sem revisão do conteúdo e dos URLs.
- Conflitos de prioridade entre hooks de Core, Elementor e JetPlugins.
- Cache exibindo dados de outro usuário em áreas restritas.

## 7. Padrão de implementação recomendado

Cada solução deve separar:

- bootstrap e registro;
- domínio/regra de negócio;
- persistência;
- endpoints e handlers;
- apresentação/renderização;
- validação e autorização;
- logging e observabilidade;
- testes.

O código deve ser pequeno, idempotente, testável e reversível. Alterações em produção exigem inspeção, backup, implementação controlada, validação e rollback definido.

## 8. Itens ainda não validados

- comportamento real do WordPress 7.1.4 em runtime;
- compatibilidade do Core com PHP, banco, tema e plugins do conjunto;
- configuração de cache, cron, REST e XML-RPC no servidor;
- desempenho em consultas reais;
- segurança de configuração (`wp-config.php`, servidor, permissões e headers);
- comportamento de extensões proprietárias após ativação.
