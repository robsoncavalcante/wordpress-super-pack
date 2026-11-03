# Cenários de validação da Skill WordPress Solutions

## Como avaliar

Para cada cenário, a resposta da Skill deve separar arquitetura, componentes, segurança, testes, riscos e autorização. Uma resposta não deve presumir versão, licença, dados ou produção.

## S1 — Landing page com lead

### Entrada

Criar LP com formulário, WhatsApp, pixel, SEO e versão mobile.

### Deve recomendar

- Elementor/Elementor Pro conforme necessidade;
- formulário protegido e consentimento;
- tracking sem dados sensíveis;
- performance, acessibilidade e validação mobile;
- Yoast se houver necessidade de SEO administrável.

### Falhas a detectar

- colocar token no JavaScript;
- publicar sem validar domínio de tracking;
- usar HTML monolítico;
- ignorar spam, nonce ou consentimento.

## S2 — Site institucional com serviços e cases

### Entrada

Site com páginas, serviços, equipe, cases e blog.

### Deve recomendar

- CPT somente para conteúdo editorial recorrente;
- Elementor/Pro para templates;
- Yoast para indexação, schema e sitemap;
- governança de templates e redirects.

### Falhas a detectar

- criar CCT para tudo;
- indexar entidades auxiliares sem estratégia;
- duplicar Theme Builder com JetThemeCore;
- publicar schema não comprovado.

## S3 — Catálogo com estados e filtros

### Entrada

Catálogo com categorias, campos, relações, busca, filtros AJAX e mapa.

### Deve recomendar

- CPT/CCT conforme ciclo editorial e volume;
- relations e ownership;
- JetEngine, JetSmartFilters e JetSearch com provider coerente;
- paginação, limites, cache e testes anônimo/autenticado.

### Falhas a detectar

- filtros sem Query ID/provider;
- Dynamic Visibility como segurança;
- query sem limite;
- expor CCT privado por REST ou cache.

## S4 — Ecommerce

### Entrada

Loja com produtos variáveis, carrinho, checkout, pagamento, wishlist e comparação.

### Deve recomendar

- WooCommerce como fonte transacional;
- JetWoo/Elementor apenas como apresentação;
- validação server-side;
- webhook, sessão e cache revisados;
- testes de variação, estoque e pagamento.

### Falhas a detectar

- confiar em preço do browser;
- alterar status por retorno do frontend;
- cachear carrinho;
- duplicar dados de estoque no JetEngine.

## S5 — Reservas

### Entrada

Agenda com recursos, horários, pagamento, cancelamento e notificações.

### Deve recomendar

- JetBooking ou JetAppointments conforme domínio;
- timezone explícito;
- revalidação server-side;
- lock/idempotência;
- estados e webhook;
- política de cancelamento.

### Falhas a detectar

- confirmar pelo calendário visual;
- ignorar concorrência;
- misturar timezones;
- reenviar notificação ou cobrança em retry.

## S6 — Migração/redesign

### Entrada

Trocar tema, templates e plugins mantendo SEO e dados reais.

### Deve recomendar

- inventário e backup verificável;
- ambiente isolado;
- migração incremental;
- redirects e sitemap;
- validação de amostra;
- rollback e aprovação antes de produção.

### Falhas a detectar

- apagar dados históricos;
- alterar produção sem backup;
- assumir compatibilidade;
- remover redirects sem evidência.

## Rubrica

Pontuação por cenário:

- 2 pontos: arquitetura e escolha de componentes corretas;
- 2 pontos: segurança e permissões;
- 2 pontos: testes e critérios de aceite;
- 2 pontos: riscos e limites declarados;
- 1 ponto: rollback e reversibilidade;
- 1 ponto: delegação adequada.

Meta: pelo menos 8/10 em cada cenário e zero falhas críticas de segurança.
