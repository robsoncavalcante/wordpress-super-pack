# JetEngine — arquitetura de dados dinâmica

## Escopo e evidência

Baseado na inspeção estática do `jet-engine-3.9.0.2.zip`, com aproximadamente 1.977 arquivos. O pacote apresenta áreas de CPT, CCT, meta fields, relations, listings, queries, forms, dynamic data, macros, mapas, visibilidade, REST/AJAX e integração com Elementor.

## 1. Modelo de dados

### CPT

Usar CPT quando o registro precisa participar do ecossistema de posts do WordPress: permalink, autor, status, revisões, taxonomias, busca e templates single/archive.

Exemplos: produtos, imóveis, parceiros, cases, artigos e serviços.

### CCT

Usar CCT quando há grande volume de registros estruturados e o modelo não precisa do ciclo completo de posts. A escolha reduz custo de postmeta, mas exige atenção especial a queries, permissões, REST, exportação e backup.

Exemplos: localizações, eventos, logs operacionais e registros de matriz.

### Meta fields

Meta fields armazenam atributos do objeto principal. Devem ter chave estável, tipo coerente, valor padrão, regra de obrigatoriedade e tratamento explícito para vazio.

Não usar um campo livre quando o valor será filtrado, ordenado ou usado por condições. Nesses casos, preferir tipo estruturado, select, switcher, relação ou taxonomia.

### Relations

Relations modelam vínculos entre entidades. Antes de criar uma relation, definir:

- origem e destino;
- cardinalidade;
- direção de navegação;
- comportamento ao excluir;
- como a relação será consultada;
- como será exibida no Listing;
- permissões de leitura e edição.

## 2. Listings e apresentação

Listing é a camada de apresentação repetível. Deve receber um contexto de item e renderizar campos, links, imagens, relações e ações com fallback.

Padrão recomendado:

`fonte de dados → query limitada → listing → template Elementor → filtros/paginação`

O Listing não deve esconder regras críticas de negócio. Queries, permissões e transformação de dados devem ser identificáveis e testáveis separadamente.

## 3. Queries

Queries devem declarar:

- fonte: posts, CCT, terms, users ou relation;
- filtros permitidos;
- ordenação;
- paginação;
- limite máximo;
- contexto do usuário;
- cache e invalidação;
- comportamento quando não há resultado.

Evitar queries abertas baseadas diretamente em parâmetros de URL. Filtrar e validar cada parâmetro; nunca concatenar SQL ou meta keys sem allowlist.

## 4. Dynamic Data, macros e callbacks

Dados dinâmicos conectam campos, relações e contexto ao Elementor. Macros e callbacks são poderosos, mas podem:

- executar consultas repetidas;
- expor metadados privados;
- produzir HTML não escapado;
- aceitar parâmetros inesperados;
- gerar links inseguros;
- criar dependência difícil de migrar.

Todo callback deve possuir contrato de entrada, saída, fallback e regra de escape. Não usar callback para esconder uma operação de negócio grande dentro de um template.

## 5. Forms e gravação

Formulários JetEngine podem criar ou editar posts, CCT, usuários, meta fields e relações. Cada ação precisa definir:

- quem pode enviar;
- quais campos são aceitos;
- quais campos são somente leitura;
- validação por tipo e regra de negócio;
- nonce e proteção CSRF;
- anti-spam e rate limit;
- estado inicial do registro;
- mensagens sem vazamento de dados;
- logs e idempotência;
- rollback ou compensação em falha parcial.

Nunca confiar em hidden fields para autorização, preço, proprietário, status ou ID de relacionamento.

## 6. Visibilidade e contexto

Dynamic Visibility deve ser usada para apresentação condicional, não como substituto de autorização. Ocultar um widget não impede que o dado exista ou seja acessado por REST, HTML, cache ou endpoint.

Para áreas restritas, aplicar autorização no servidor e revisar cache de página, cache de objeto, REST e AJAX.

## 7. Mapas, filtros e busca

Mapas e filtros introduzem riscos de custo e consistência:

- coordenadas devem ser validadas;
- resultados devem ter limite e paginação;
- relation filters precisam de query compatível com a fonte;
- filtros CCT e filtros de posts não são automaticamente equivalentes;
- IDs de query devem ser estáveis e documentados;
- AJAX público deve possuir mitigação de abuso;
- não expor endereço ou dados privados sem regra explícita.

## 8. Escolha CPT versus CCT

| Necessidade | Preferência |
|---|---|
| Single/archive, autor, revisões, taxonomias | CPT |
| Grande volume tabular sem ciclo de post | CCT |
| Relação editorial com conteúdo | CPT + relation |
| Matriz de unidades/localizações | CCT + relation |
| Busca e filtros públicos | Modelo com query limitada e índices adequados |
| Dados sensíveis ou restritos | Qualquer modelo com autorização server-side e cache revisado |

## 9. Integração com Elementor

- usar Dynamic Field/Image/Terms/Link para manter editabilidade;
- criar fallback para campos vazios;
- separar Listing Item, Single e Archive;
- documentar Query ID e contexto;
- evitar lógica de negócio em HTML widget;
- testar AJAX, filtros e paginação após cada atualização;
- verificar se o cache não mistura usuários ou contextos.

## 10. Checklist de segurança

- CPT/CCT e campos sensíveis não ficam públicos por padrão;
- REST possui permissões e campos expostos revisados;
- forms verificam nonce, capability e ownership;
- IDs recebidos são validados e autorizados;
- uploads têm MIME, extensão, tamanho e destino controlados;
- callbacks escapam saída conforme o contexto;
- queries têm allowlist, paginação e limite;
- relation updates são transacionais ou compensáveis;
- logs não registram dados pessoais ou tokens;
- exportação e backup incluem o modelo escolhido;
- exclusões e alterações de schema têm migração reversível.

## 11. Padrão arquitetural recomendado

1. Modelar entidades e ownership.
2. Escolher CPT, CCT, taxonomy, meta ou relation.
3. Definir estado, permissões e ciclo de vida.
4. Criar campos com tipos e chaves estáveis.
5. Criar queries pequenas e nomeadas.
6. Criar Listings com fallback e escape.
7. Conectar Elementor por Dynamic Data.
8. Adicionar filtros e AJAX somente quando necessário.
9. Testar dados vazios, duplicados, inválidos, anônimos e autorizados.
10. Documentar migração, backup e rollback.

## Limites ainda não validados

- contratos exatos das APIs internas JetEngine 3.9.0.2;
- desempenho real entre CPT, CCT e relations;
- exposição REST padrão de cada modelo;
- comportamento dos módulos adicionais;
- compatibilidade com JetSmartFilters, JetSearch e Elementor nas versões recebidas;
- segurança de configurações feitas pelo painel;
- comportamento em cache e produção.
