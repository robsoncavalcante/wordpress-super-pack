# Módulos complementares do JetEngine

## Escopo

Este módulo cobre os pacotes complementares identificados no conjunto: Dynamic Charts Module 1.1.0, Dynamic Tables Module 1.3.0, Custom Visibility Conditions, External Modules, Layout Switcher, Post Expiration Period, Attachment Link Callback e Trim Callback.

## 1. Dynamic Charts

Usado para transformar consultas em gráficos. Antes de publicar, definir:

- origem dos dados;
- agregação;
- filtros permitidos;
- período e timezone;
- limite de pontos;
- fallback sem dados;
- cache e invalidação;
- acessibilidade textual.

Não expor dados privados apenas porque um gráfico não mostra o registro individualmente. O endpoint ou payload ainda pode conter os valores.

## 2. Dynamic Tables

Tabelas dinâmicas são adequadas para dados estruturados, mas precisam de:

- paginação server-side;
- limite de linhas;
- ordenação por allowlist;
- escape de células;
- filtros autorizados;
- tratamento de colunas sensíveis;
- exportação protegida;
- fallback para datasets vazios.

Evitar carregar milhares de registros no navegador. Não permitir que o usuário escolha livremente coluna, tabela ou expressão SQL.

## 3. Custom Visibility Conditions

Condições customizadas controlam apresentação. Não substituem autorização, ownership ou proteção de endpoint.

Boas práticas:

- uma condição por regra clara;
- evitar duplicação de condições;
- documentar precedência;
- testar ausência, zero, falso e valor inválido;
- revisar cache;
- garantir que o dado não seja exposto em HTML, REST ou AJAX.

## 4. External Modules

Módulos externos ampliam o JetEngine, mas elevam risco de procedência e compatibilidade. Antes de habilitar:

- identificar origem e licença;
- revisar dependências;
- verificar hooks e endpoints;
- conferir escrita no banco;
- confirmar suporte à versão do JetEngine;
- testar ativação e desativação;
- manter rollback.

Nenhum módulo externo deve ser tratado como confiável apenas porque aparece no painel do plugin.

## 5. Layout Switcher

Alterna entre layouts ou apresentações. Deve preservar:

- mesma fonte de dados;
- filtros e paginação;
- estado de URL quando necessário;
- acessibilidade;
- performance;
- contexto do usuário.

Evitar duplicar queries para cada layout. O switcher deve trocar apresentação, não regra de negócio.

## 6. Post Expiration Period

Expiração altera estado de conteúdo ao longo do tempo. Definir:

- timezone;
- evento de expiração;
- status após expirar;
- impacto em relações e listings;
- notificações;
- reversão;
- comportamento no cache;
- auditoria.

Cron pode atrasar. O frontend não deve assumir que uma tarefa agendada executou exatamente no horário; queries devem considerar a data de expiração quando necessário.

## 7. Attachment Link Callback

Callbacks de anexos devem validar:

- post e attachment;
- ownership e capability;
- tipo de arquivo;
- URL gerada;
- acesso público ou privado;
- escape no atributo e no HTML.

Não transformar callback de link em mecanismo de autorização. Arquivo privado exige controle server-side e URL temporária quando aplicável.

## 8. Trim Callback

Truncamento deve ser feito no contexto correto:

- texto simples;
- HTML permitido;
- caracteres versus palavras;
- idioma e acentuação;
- preservação de entidades;
- acessibilidade;
- link “ler mais”.

Não truncar HTML bruto sem estratégia, pois isso pode quebrar tags ou exibir conteúdo incorretamente. Quando o plugin não oferecer corte por caracteres, considerar transformação segura no backend ou CSS/JS apenas para apresentação, conforme o caso.

## 9. Riscos transversais

- queries duplicadas e caras;
- exposição por payload mesmo com widget oculto;
- cache de dado contextual;
- cron atrasado ou executado duas vezes;
- callbacks sem contrato;
- módulos externos sem revisão;
- exportações sem autorização;
- inconsistência entre CPT, CCT e tabelas de relations.

## 10. Checklist de ativação

1. Registrar finalidade do módulo.
2. Confirmar dependências e versão.
3. Revisar entradas, saídas e permissões.
4. Definir fallback e rollback.
5. Testar com dados vazios, grandes e inválidos.
6. Testar usuário anônimo e autenticado.
7. Verificar REST, AJAX, cache e cron.
8. Medir impacto de consulta e assets.
9. Documentar configuração.
10. Só então habilitar em produção.

## Limites

Ainda falta validar cada módulo em runtime e confirmar seus contratos internos, especialmente permissões, cron, tabelas auxiliares, endpoints, exportação e comportamento sob cache.
