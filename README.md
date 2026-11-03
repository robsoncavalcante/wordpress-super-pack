# WordPress Super Pack

Base avançada para desenvolvimento seguro de soluções WordPress com WordPress Core, Elementor, Elementor Pro, JetEngine, JetPlugins, Yoast SEO e Happy Elementor Addons.

## Conteúdo

- `skill-wordpress-solutions/`: Skill multiplataforma para Codex e Claude Code.
- `base-conhecimento-wordpress/`: inventário técnico, arquitetura, segurança e padrões reutilizáveis.

## Objetivo

Orientar a criação e manutenção de landing pages, sites institucionais, ecommerce, catálogos, portais e sistemas de reservas com composição mínima de plugins, segurança, compatibilidade, performance, testes e rollback.

## Princípios

- Um plugin por função quando possível.
- Separação entre dados, apresentação, transações e integrações.
- Validação server-side, autorização, sanitização e escape.
- Não usar visibilidade visual como autorização.
- Não ativar toda a suíte sem necessidade.
- Backup, validação e rollback antes de alterações reais.

## Estado

A Skill está em evolução inicial e foi validada estruturalmente com o validador oficial de Skills. A inspeção dos pacotes foi estática; comportamento em runtime, compatibilidade, licenciamento, performance e segurança de configuração exigem testes isolados.

## Uso

Leia `skill-wordpress-solutions/SKILL.md` e carregue apenas as referências necessárias ao tipo de tarefa. Consulte os cenários em `skill-wordpress-solutions/tests/SCENARIOS.md` antes de considerar a Skill pronta para produção.

## Licenciamento e procedência

Este repositório contém documentação e instruções próprias. Os plugins citados pertencem aos respectivos fornecedores e não são redistribuídos aqui.
