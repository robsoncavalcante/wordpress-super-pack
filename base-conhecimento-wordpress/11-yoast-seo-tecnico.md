# Yoast SEO e SEO técnico

## Escopo e evidência

Baseado na inspeção estática dos pacotes Yoast SEO 28.8 e Yoast SEO Premium 28.8. Foram identificadas estruturas de indexables, metadados, schema, sitemaps, breadcrumbs, redirects, importações, CLI e integrações.

## 1. Papel do Yoast

Yoast organiza sinais SEO e metadados do WordPress. Ele não substitui arquitetura de conteúdo, performance, acessibilidade, links internos ou qualidade editorial.

Camadas principais:

- metadados de página;
- indexables;
- títulos e descriptions;
- canonical;
- robots;
- Open Graph e social metadata;
- schema graph;
- XML sitemaps;
- breadcrumbs;
- redirects Premium;
- integrações com post types, taxonomias e usuários.

## 2. Indexables

Indexables são uma representação otimizada de entidades indexáveis e suas relações. Devem ser tratados como dados derivados, não como fonte editorial primária.

Ao criar CPT ou alterar taxonomias:

- definir se o tipo deve ser indexável;
- definir single, archive e sitemap;
- revisar canonical;
- revisar relações e links internos;
- regenerar ou validar dados derivados;
- evitar duplicidade entre CPT, CCT e taxonomia.

Não indexar automaticamente CCTs operacionais, registros privados, localizações sem conteúdo editorial ou endpoints internos.

## 3. CPT, CCT e Elementor

### CPT

É normalmente o candidato para páginas individuais indexáveis, com título, slug, conteúdo, taxonomias e template Single.

### CCT

Pode alimentar listings, mapas e tabelas sem representar uma página editorial. Só deve ser indexado quando houver estratégia explícita de URL, conteúdo único, canonical, sitemap e template público.

### Elementor e JetEngine

O template visual não garante SEO correto. Validar:

- título real no HTML;
- headings semânticos;
- conteúdo presente no HTML inicial quando necessário;
- links rastreáveis;
- imagem e alt text;
- canonical;
- schema coerente;
- ausência de conteúdo duplicado entre Listing, archive e single.

## 4. Schema

Schema deve representar o conteúdo real, não ser usado para declarar dados que a página não comprova.

Revisar:

- tipo de entidade;
- propriedades obrigatórias;
- autor e organização;
- imagem;
- datas;
- breadcrumbs;
- produto, oferta, review ou evento quando aplicável;
- duplicação de schema por tema, Elementor, WooCommerce e Yoast.

Não criar schema de produto, review ou evento para uma página que apenas lista itens ou não possui dados verificáveis.

## 5. Sitemap e robots

O sitemap deve conter somente URLs que o projeto deseja tornar descobríveis. Revisar:

- CPTs públicos;
- taxonomias úteis;
- mídia;
- arquivos e autores;
- páginas de filtro;
- URLs expiradas;
- parâmetros e buscas;
- conteúdo duplicado ou fino.

Robots e noindex não corrigem arquitetura ruim. Uma URL privada também precisa de autenticação e controle de acesso.

## 6. Redirects Premium

Redirects devem ser tratados como migração controlada:

- origem exata;
- destino canônico;
- código apropriado;
- ausência de loop;
- preservação de parâmetros quando necessário;
- revisão de cadeias;
- logs e data de criação;
- remoção somente após evidência.

Não apagar redirects históricos sem backup ou análise de tráfego.

## 7. Breadcrumbs e links internos

Breadcrumbs precisam refletir a hierarquia real, sem forçar categorias inexistentes. Em CPTs relacionados a CCTs, manter a empresa, produto ou entidade editorial como página principal e usar CCT para dados auxiliares quando apropriado.

Links internos devem ser criados por intenção editorial e navegação útil, não apenas para satisfazer contadores do plugin.

## 8. Segurança e privacidade

- Não expor metadados privados no schema.
- Não inserir dados pessoais em title, description ou Open Graph.
- Validar campos dinâmicos antes de gerar schema.
- Escapar valores e URLs.
- Revisar endpoints de importação e exportação.
- Proteger comandos WP-CLI e operações administrativas por capability.
- Não armazenar tokens ou segredos em campos SEO.

## 9. Fluxo recomendado

1. Definir intenção e tipo de conteúdo.
2. Escolher entidade indexável.
3. Definir URL, canonical e relacionamento.
4. Configurar template Elementor.
5. Criar metadados editoriais.
6. Configurar schema verificável.
7. Revisar sitemap e robots.
8. Testar HTML, links, dados estruturados e mobile.
9. Validar redirects e migrações.
10. Monitorar indexação e erros após publicação.

## 10. Checklist por projeto

- cada CPT tem regra index/noindex;
- cada CCT tem decisão explícita de exposição;
- páginas de busca e filtros não criam indexação infinita;
- listings não duplicam singles sem propósito;
- títulos e descriptions não são gerados de campos vazios;
- schema não é duplicado;
- sitemap não contém URLs privadas ou expiradas;
- redirects têm origem e destino testados;
- breadcrumbs representam a hierarquia;
- imagens têm alt coerente;
- dados dinâmicos são escapados e revisados.

## Limites

Ainda falta validar o comportamento real da versão 28.8 em runtime, a interação com os templates Elementor/JetEngine instalados, a regeneração de indexables, o schema efetivamente renderizado e os endpoints de redirects/importação.
