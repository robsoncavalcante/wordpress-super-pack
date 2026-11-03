# Base avançada de conhecimento WordPress

## Objetivo

Construir uma base técnica, verificável e reutilizável para criar landing pages, sites institucionais, lojas, portais e sistemas WordPress usando o Core, Elementor, Elementor Pro, Yoast SEO, JetPlugins e Happy Elementor Addons.

Esta base será a fonte de verdade para uma Skill compatível com Codex e Claude Code. A Skill será criada somente depois da validação dos padrões, riscos e limites documentados aqui.

## Princípios

- Evidência antes de regra: cada recomendação deve apontar para código, documentação ou teste correspondente.
- Segurança por padrão: autenticação, autorização, nonces, validação, sanitização, escape, SQL preparado, uploads e exposição REST são requisitos de primeira classe.
- Composição mínima: ativar somente os componentes necessários para o projeto.
- Separação de responsabilidades: conteúdo, apresentação, dados, integrações, infraestrutura e operação devem permanecer distinguíveis.
- Reversibilidade: mudanças devem ser testáveis em ambiente isolado, com backup e rollback.
- Licenciamento e procedência: nenhum pacote deve ser tratado como confiável apenas pelo nome do arquivo.
- Compatibilidade explícita: versões, PHP, banco, tema, plugins e dependências devem ser registrados antes da implementação.

## Domínios de conhecimento

1. WordPress Core: bootstrap, ciclo de requisição, hooks, opções, metadados, usuários, capacidades, REST, AJAX, cron, uploads, mídia, editor, temas, multisite e WP-CLI.
2. Elementor: editor, widgets, controls, documents, templates, dynamic tags, CSS, assets, responsive controls, data layer, REST e extensibilidade.
3. Elementor Pro: Theme Builder, forms, popups, loop/grid, dynamic tags, conditions, marketing, WooCommerce, payments, licensing e updater.
4. JetEngine: CPT, CCT, meta fields, relations, listings, macros, queries, forms, callbacks, visibility e integração com Elementor.
5. JetPlugins: filtros, busca, menus, booking, appointments, WooCommerce, tabelas, gráficos, reviews, popups e módulos complementares.
6. Yoast SEO: indexables, metadados, schema, sitemaps, breadcrumbs, redirects, integrações, CLI, Premium e riscos de conteúdo duplicado.
7. Happy Elementor Addons: widgets, extensões visuais, condições, animações, parallax, templates e sobreposição com Elementor Pro.
8. Segurança: superfície administrativa, REST/AJAX, CSRF, XSS, SQL injection, SSRF, upload, desserialização, privilege escalation, secrets, logs e hardening.
9. Performance: consultas, cache, assets, fontes, imagens, Core Web Vitals, object cache, cron, filas, CDN e degradação por plugins.
10. Engenharia de projetos: arquitetura, ambientes, versionamento, migrations, testes, observabilidade, deploy, rollback e documentação.
11. Agentes: decomposição de tarefas, delegação por domínio, revisão, aprovação humana, limites de escrita e critérios de parada.

## Método de estudo

Para cada componente será produzido um cartão técnico com:

- versão e origem do material;
- diretórios e arquivos de entrada;
- classes, interfaces e serviços principais;
- hooks, filtros, endpoints, comandos e pontos de extensão;
- dependências internas e externas;
- fluxo de dados e permissões;
- superfícies de entrada e saída;
- padrões de segurança observados;
- riscos e hipóteses ainda não validadas;
- exemplos seguros de uso;
- testes necessários antes de produção.

## Fases

### Fase 1 — Inventário e mapa arquitetural

Concluída parcialmente. Os anexos foram inventariados sem execução. O pacote JetPlugins contém 31 ZIPs internos; Happy e Yoast possuem variantes free/premium.

### Fase 2 — Core e ciclo de execução

Mapear WordPress Core, hooks, request lifecycle, REST/AJAX, permissões, banco, cron, uploads e APIs de extensão.

### Fase 3 — Camada visual

Mapear Elementor, Elementor Pro e Happy Addons, com foco em widgets, templates, dynamic data, condições, CSS e assets.

### Fase 4 — Dados e soluções Jet

Mapear JetEngine primeiro; depois filtros, busca, booking, menus, WooCommerce, tabelas, gráficos e módulos opcionais.

### Fase 5 — SEO e conteúdo

Mapear Yoast free/Premium, schema, indexables, sitemap, redirects, integração com tipos de conteúdo e governança editorial.

### Fase 6 — Segurança, performance e operação

Criar checklists, threat model, padrões de logging, testes, cache, backup, deploy e rollback.

### Fase 7 — Skill multiplataforma

Transformar somente conhecimento validado em `SKILL.md`, referências modulares, roteamento de tarefas, agentes especializados e protocolo de revisão para Codex e Claude Code.

## Critério de prontidão da Skill

A Skill só será considerada pronta quando houver:

- matriz de compatibilidade por componente;
- padrões seguros para as principais extensões;
- checklists de implementação e revisão;
- regras de quando delegar e quando exigir revisão humana;
- exemplos de LP, institucional, ecommerce, portal e sistema dinâmico;
- testes ou validações para os fluxos críticos;
- limites explícitos sobre licenças, procedência, runtime e produção.

## Limites atuais

A análise estática dos ZIPs não prova comportamento em runtime, compatibilidade, ausência de malware, validade de licenças, segurança da configuração do servidor ou desempenho. Esses pontos exigirão ambiente isolado, testes controlados e documentação dos resultados.
