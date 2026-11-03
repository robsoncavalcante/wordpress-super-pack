# JetSmartFilters — filtros, queries e atualização dinâmica

## Escopo e evidência

Baseado na inspeção estática do `jet-smart-filters-3.8.6.3.zip`, com aproximadamente 672 arquivos. Foram identificados filtros de busca, select, checkbox, radio, range, rating, data, hierárquico, sorting, paginação, AJAX, providers e integração com Elementor/Bricks.

## 1. Papel arquitetural

JetSmartFilters não é a fonte de dados. Ele controla parâmetros de filtragem e atualiza um provider, normalmente:

- Listing Grid do JetEngine;
- Archive Grid do Elementor;
- Map Listing;
- resultados de busca;
- providers compatíveis de terceiros.

Modelo:

`filtro → parâmetros → provider/query → resultados → paginação/mapa/listing`

Se o filtro e o provider não compartilham o mesmo contexto, os controles podem parecer funcionar enquanto os resultados permanecem errados.

## 2. Tipos observados

- Search;
- Select;
- Checkboxes;
- Radio;
- Range e Check Range;
- Rating;
- Date Range e Date Period;
- Hierarchical;
- Alphabet;
- Sorting;
- Color/Image;
- Hidden;
- Remove Filters;
- Apply Filters;
- Pagination, Load More e navegação dinâmica.

Cada tipo exige fonte de dados, formato de valor, regra de comparação e comportamento quando não há resultados.

## 3. Query e provider

Antes de configurar um filtro, registrar:

- Query ID;
- provider;
- fonte de dados;
- campo filtrado;
- tipo do campo;
- operador;
- relação com outros filtros;
- paginação;
- modo de atualização;
- URL/state, se aplicável.

Regra crítica: filtros que trabalham com relations, CCT, taxonomias e posts não devem ser misturados sem confirmar que a query entende a mesma origem.

## 4. AJAX, URL e estado

Atualização AJAX melhora UX, mas cria requisitos adicionais:

- estado inicial reproduzível por URL;
- fallback quando JavaScript falha;
- debounce para busca textual;
- limite de resultados;
- proteção contra abuso;
- sincronização com paginação e sorting;
- invalidação de cache;
- acessibilidade para anunciar atualização;
- não expor dados privados no payload.

O estado de filtro deve ser idempotente: repetir a mesma combinação deve produzir o mesmo resultado para o mesmo contexto.

## 5. Relations, CCT e mapas

Em dados relacionais, o filtro precisa apontar para a query correta. Um caso comum de falha é o filtro enviar o valor correto, mas o Map Listing ou Listing Grid usar outro provider ou outra fonte.

Checklist:

- confirmar a fonte da query;
- confirmar Query ID exatamente, inclusive maiúsculas e minúsculas;
- verificar cardinalidade da relation;
- garantir que o provider é compatível com CCT;
- aplicar os mesmos filtros ao mapa e à lista;
- limpar markers antigos quando a resposta muda;
- testar combinação vazia e múltiplos filtros.

## 6. Filtros dependentes

Filtros dependentes, como Estado → Cidade → Categoria, devem ser baseados nos resultados disponíveis, não apenas em todos os termos cadastrados.

O fluxo seguro é:

1. selecionar o primeiro filtro;
2. recalcular opções válidas do segundo;
3. remover valores incompatíveis;
4. atualizar listing/mapa;
5. preservar somente estado ainda válido.

Não apresentar opções sem resultados, salvo quando houver decisão explícita de UX.

## 7. Segurança

- Validar e normalizar valores recebidos por URL, AJAX e formulários.
- Não aceitar meta keys, table names ou operadores arbitrários do usuário.
- Usar allowlists para campos e ordenações.
- Aplicar capabilities e ownership antes de filtrar dados restritos.
- Não usar filtros para substituir autorização.
- Revisar payloads AJAX e respostas REST.
- Limitar range numérico e datas.
- Escapar labels e valores exibidos.
- Aplicar rate limiting ou mitigação para busca pública.
- Não revelar existência de registros privados por contagem ou mensagens.

## 8. Performance

- Criar índices e campos adequados ao volume.
- Limitar paginação e número de markers.
- Evitar consultas SQL avançadas sem plano de execução.
- Debounce em Search Filter.
- Não atualizar simultaneamente múltiplos providers sem necessidade.
- Evitar filtros hierárquicos que carreguem toda a taxonomia em grandes volumes.
- Medir tempo de resposta AJAX e tamanho do payload.
- Revisar cache após mudanças de estado.

## 9. Padrão de implementação

1. Definir entidade, ownership e fonte.
2. Criar e testar a query sem filtro.
3. Criar Listing/Grid/Map provider.
4. Testar paginação.
5. Adicionar um filtro simples.
6. Validar Query ID e provider.
7. Adicionar filtros dependentes gradualmente.
8. Habilitar AJAX somente depois do modo básico funcionar.
9. Testar URL, cache, mobile, ausência de resultados e usuário anônimo.
10. Registrar configuração e rollback.

## 10. Limites ainda não validados

- contratos exatos de todos os providers da versão 3.8.6.3;
- compatibilidade de cada filtro com CCT e SQL avançado;
- comportamento em mapas com grande volume;
- sanitização completa de todos os parâmetros em runtime;
- impacto de cache e CDN;
- suporte real a cada integração de terceiros.
