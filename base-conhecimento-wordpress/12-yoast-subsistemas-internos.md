# Yoast SEO — subsistemas internos e pontos de extensão

## 1. Conclusão do inventário

O Yoast recebido não é um conjunto de dezenas de plugins instaláveis. É composto por dois plugins principais:

- Yoast SEO Free 28.8;
- Yoast SEO Premium 28.8.

Dentro deles existem diversos subsistemas, bibliotecas Composer, componentes administrativos, integrações e recursos de IA.

## 2. Yoast SEO Free

### Núcleo e inicialização

`src/initializers`, `src/generated`, `src/context`, `src/config` e os arquivos `wp-seo.php`/`wp-seo-main.php` organizam carregamento, configuração, contêiner e inicialização.

### Indexação

`src/actions/indexables`, `src/actions/indexing`, `src/models`, `src/repositories` e migrations relacionadas sustentam indexables, hierarquia e dados derivados.

Risco: alterações de CPT, taxonomia, slug ou migração podem deixar dados derivados desatualizados, duplicados ou órfãos.

### Schema e apresentação

`src/generators/schema`, `src/helpers/schema`, `src/presenters`, `src/helpers/open-graph` e `src/helpers/twitter` geram dados estruturados e metadados sociais.

Risco: duplicidade com tema, WooCommerce, Elementor ou plugins de schema; valores dinâmicos incorretos; exposição de dados pessoais.

### Integrações

`src/integrations` possui áreas administrativas, frontend, blocos, watchers e integrações de terceiros. Há integração dedicada com Elementor e outras plataformas.

Regra: qualquer alteração de template dinâmico deve ser validada no HTML final, não apenas no painel do Yoast.

### IA e serviços remotos

O pacote possui áreas de autenticação, autorização, consentimento, gerador, content planner e requisições HTTP relacionadas a recursos de IA.

Riscos:

- envio de conteúdo para serviço externo;
- consentimento inadequado;
- tokens ou sessões;
- limites e falhas de API;
- dados sensíveis em prompts;
- dependência de disponibilidade externa.

### Importação e configuração

As áreas de importing, configuration e migrations podem alterar opções, indexables e conteúdo derivado. Importações devem ser feitas com backup, validação e possibilidade de rollback.

### Outros subsistemas

- bulk editor;
- analytics e tracking;
- alerts;
- content-type visibility;
- expiring store;
- logs e memoizers;
- plans e addons;
- llms-txt;
- abilities;
- comandos.

Esses componentes não são plugins separados; são módulos internos com efeitos próprios.

## 3. Yoast SEO Premium

### Redirects

O Premium possui classes, rotas e comandos WP-CLI para criar, atualizar, listar, seguir e excluir redirects.

Toda operação deve ser autorizada e auditável. Redirects não devem formar loops ou cadeias desnecessárias.

### IA Premium

O Premium adiciona:

- AI Optimize;
- sugestões em lote;
- sumarização;
- pós-processamento de sugestões;
- rotas e integrações administrativas.

Revisar consentimento, conteúdo enviado, permissões, custo, limite, fallback e aprovação humana. Sugestões de IA não devem publicar ou substituir conteúdo automaticamente sem controle editorial.

### Prominent words e análise

Há tarefas e integrações relacionadas a palavras proeminentes, análise de conteúdo, cornerstone content e bulk editor.

Esses recursos são auxiliares editoriais; não devem ser confundidos com garantia de ranking ou qualidade de conteúdo.

### Integrações de terceiros

O Premium inclui integrações com Elementor Premium, EDD, Algolia, Wincher, Mastodon, TranslationPress e outras áreas de terceiros.

Cada integração deve ser tratada como superfície adicional de compatibilidade, credenciais, requisições e privacidade.

### Schema organizacional e Open Graph

O Premium amplia integrações de organização, arquivos, autores, tipos de post e termos. Revisar duplicidade e coerência com tema e ecommerce.

## 4. Vendor e bibliotecas

`vendor` e `vendor_prefixed` contêm dependências PHP e classes isoladas para reduzir colisões. Não são plugins instaláveis e não devem ser editados diretamente.

Riscos:

- vulnerabilidades em dependências;
- divergência de autoload;
- atualização parcial;
- conflito com outra cópia da mesma biblioteca;
- falsa impressão de que alterar vendor é uma extensão suportada.

## 5. Pontos de extensão seguros

- filtros e actions documentados pelo Yoast;
- APIs de schema e presenters;
- integração de post types e taxonomias;
- filtros de metadados com escape;
- integração de breadcrumbs;
- controle de indexação por entidade;
- APIs de redirects com autorização;
- extensões de análise sem alterar dados transacionais.

Evitar:

- editar arquivos em `vendor`;
- alterar migrations existentes;
- escrever diretamente nas tabelas de indexables sem entender o repositório;
- desativar verificações de licença ou consentimento;
- interceptar IA para enviar dados sem transparência;
- duplicar schema sem verificar o HTML final.

## 6. Threat model resumido

| Área | Risco | Controle |
|---|---|---|
| Indexables | dados órfãos/duplicados | migrations, regeneração e backup |
| Schema | markup falso/duplicado | fonte única e validação do HTML |
| Redirects | loop, cadeia ou perda de tráfego | teste, logs e rollback |
| IA | envio de conteúdo sensível | consentimento, minimização e aprovação |
| CLI | alteração administrativa | capability, ambiente e auditoria |
| Integrações | credencial ou API exposta | secrets, timeout, logs seguros |
| Vendor | dependência vulnerável | atualização integral e auditoria |

## 7. Fluxo de uso na Skill

1. Identificar entidade e objetivo SEO.
2. Definir index/noindex.
3. Configurar título, description, canonical e schema.
4. Validar template Elementor/JetEngine renderizado.
5. Revisar sitemap, breadcrumbs e links.
6. Usar Premium somente quando a capacidade for necessária.
7. Em IA, exigir consentimento e revisão humana.
8. Em redirects/importações, fazer backup e teste.
9. Monitorar indexação e erros.

## Limites

A análise permanece estática. Ainda não foi verificado runtime, contratos exatos de todos os hooks, permissões efetivas das rotas, comportamento de IA, chamadas remotas, queries de indexables ou compatibilidade com cada versão de Elementor, JetEngine e WooCommerce.
