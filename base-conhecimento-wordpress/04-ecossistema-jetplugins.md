# Ecossistema JetPlugins — inventário e plano técnico

## Resposta direta

Até o documento anterior, somente o JetEngine principal 3.9.0.2 havia sido analisado. Os demais ZIPs não foram tratados como se fossem parte do Core. Este documento inicia o inventário separado dos 31 pacotes relacionados.

## 1. Componentes identificados

### Dados, consultas e extensões do JetEngine

- JetEngine 3.9.0.2 — CPT, CCT, meta fields, relations, listings, queries e forms.
- JetEngine Dynamic Charts Module 1.1.0 — visualização de dados.
- JetEngine Dynamic Tables Module 1.3.0 — tabelas dinâmicas.
- JetEngine Attachment Link Callback — callback de anexos.
- JetEngine Custom Visibility Conditions — condições de visibilidade.
- JetEngine External Modules — módulos externos.
- JetEngine Layout Switcher — alternância de layout.
- JetEngine Post Expiration Period — expiração de posts.
- JetEngine Trim Callback — callback de truncamento.

Esses módulos devem ser avaliados junto do JetEngine e não instalados indiscriminadamente. Callbacks, condições e expiração podem alterar renderização, estado e dados.

### Conteúdo e interface Elementor

- JetElements 2.9.2.6 — widgets Elementor.
- JetWidgets for Elementor 1.0.21 — widgets adicionais.
- JetWoo Widgets for Elementor 1.1.9 — widgets WooCommerce.
- JetBlocks 1.5.2.2 — header, footer e elementos de navegação.
- JetTabs 2.3.5 — abas e acordeões.
- JetBlog 2.4.11 — layouts de blog.
- JetTricks 2.0.1 — efeitos e interações.
- JetParallax — efeitos de parallax.
- JetGuten — integração com Gutenberg.
- JetStyleManager 1.3.9 — controles e estilo.

Risco principal: sobreposição funcional com Elementor Pro e Happy Addons, aumento de assets e conflitos de controles.

### Navegação, busca e filtros

- JetMenu 3.0.3 — mega menus e navegação.
- JetSearch 3.6.3.1 — busca.
- JetSmartFilters 3.8.6.3 — filtros, AJAX e integração com listings.

Esses componentes dependem de contexto correto de query, Listing, paginação e fonte de dados. Filtros de posts, CCT, relations e mapas não são intercambiáveis automaticamente.

### WooCommerce

- JetWooBuilder 2.3.5 — templates WooCommerce.
- JetWooProductGallery 2.4.0 — galeria de produtos.
- JetWooWidgets 1.1.9 — widgets WooCommerce.
- JetCompareWishlist 1.5.13 — comparação e wishlist.

Exigem validação de sessão, carrinho, cache, endpoints, permissões e compatibilidade com o fluxo oficial do WooCommerce.

### Reservas e agenda

- JetBooking 4.1.2.2 — reservas.
- JetAppointments Booking 2.5.1.1 — agendamentos.

Não devem ser tratados como simples formulários. É necessário modelar disponibilidade, timezone, concorrência, status, conflitos, notificações, cancelamento e idempotência.

### Popups, tema e avaliações

- JetPopup 2.2.3.3 — popups e triggers.
- JetThemeCore 2.3.4 — templates de tema.
- JetReviews 3.1.1 — avaliações.

Esses plugins podem interferir em templates globais, cache, conteúdo enviado por usuários e exposição de dados.

## 2. Relações prováveis

`JetEngine → Listings / Queries / Relations → JetSmartFilters / JetSearch / Maps / Elementor`

`WooCommerce → JetWooBuilder / JetWooWidgets / Gallery / CompareWishlist`

`Elementor → JetElements / JetBlocks / JetTabs / JetBlog / JetPopup / JetThemeCore`

`JetBooking ou JetAppointments → usuários / calendário / notificações / pagamentos`

Essas relações são arquiteturais e precisam ser confirmadas por headers, dependências declaradas e testes de ativação controlada.

## 3. Regra de instalação

Não instalar o pacote inteiro por padrão. Escolher por capacidade:

- dados dinâmicos: JetEngine;
- filtros: JetSmartFilters;
- busca: JetSearch;
- menus: JetMenu;
- ecommerce: somente módulos WooCommerce necessários;
- agenda: JetBooking ou JetAppointments, conforme o domínio;
- visual: somente widgets que não sejam cobertos nativamente pelo Elementor Pro.

## 4. Matriz de risco

| Grupo | Risco dominante | Validação necessária |
|---|---|---|
| JetEngine e módulos | exposição ou alteração de dados | permissions, REST, forms, queries e migrations |
| Filtros e busca | queries caras e resultados inconsistentes | paginação, índices, AJAX, cache e contexto |
| Widgets | assets e conflitos visuais | editor, frontend, responsivo e performance |
| WooCommerce | quebra de checkout ou sessão | carrinho, checkout, webhooks e cache |
| Booking | dupla reserva e timezone | concorrência, status, cancelamento e idempotência |
| Popups/tema | template errado ou bloqueio UX | condições, prioridade, cache e acessibilidade |
| Reviews | conteúdo malicioso | sanitização, moderação e permissões |

## 5. Plano de estudo individual

Cada plugin deverá receber uma ficha com:

- versão e arquivo principal;
- dependências declaradas;
- módulos ativáveis;
- hooks e filtros;
- endpoints e AJAX;
- tabelas, options e postmeta;
- capabilities e nonces;
- assets carregados;
- integrações;
- riscos;
- conflito potencial;
- teste mínimo de ativação e desativação.

## 6. Critério para a Skill

A Skill não deverá recomendar “use JetPlugins” genericamente. Ela deverá selecionar o menor conjunto de plugins que atende ao requisito, explicar dependências e exigir validação específica para dados, ecommerce, reservas, filtros e conteúdo de usuários.

## Limites atuais

Este documento é um inventário arquitetural. Ainda falta a ficha individual de cada ZIP, incluindo leitura dos arquivos principais, dependências declaradas, hooks, endpoints, options, tabelas e controles de segurança.
