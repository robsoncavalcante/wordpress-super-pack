# JetSearch — busca AJAX e resultados dinâmicos

## Escopo e evidência

Baseado na inspeção estática do `jet-search-3.6.3.1.zip`, com aproximadamente 365 arquivos. O pacote possui widgets/blocos de busca, sugestões, resultados AJAX, handlers, token manager, integrações de compatibilidade e templates próprios.

## 1. Papel no ecossistema

JetSearch resolve a experiência de busca, não substitui o modelo de conteúdo do WordPress ou JetEngine.

Fluxo principal:

`termo → handler/token → consulta → sugestões/resultados → template Elementor/Listing → página completa`

Pode haver duas experiências diferentes:

- sugestões rápidas durante a digitação;
- página completa de resultados.

As duas devem usar regras consistentes de fonte, post types, campos pesquisáveis, taxonomias e permissões.

## 2. Componentes identificados

- Jet Ajax Search;
- Search Suggestions;
- templates de formulário e resultados;
- popup de resultados;
- contagem de resultados;
- botão de submit;
- integração com Elementor;
- integração com blocos;
- handlers AJAX;
- token manager;
- configurações administrativas;
- compatibilidade com outros plugins.

## 3. Configuração correta

Antes de publicar uma busca, definir:

- post types permitidos;
- taxonomias incluídas;
- campos pesquisáveis;
- quantidade máxima de resultados;
- número de sugestões;
- ordem e relevância;
- template dos itens;
- link para resultado completo;
- comportamento sem resultados;
- idioma e normalização;
- cache e invalidação.

Não permitir que a busca exponha drafts, conteúdos privados, meta fields sensíveis ou objetos que o usuário não poderia acessar.

## 4. Integração com JetEngine

Para buscar conteúdo criado no JetEngine, confirmar:

- CPT está publicamente consultável quando necessário;
- CCT possui integração suportada pelo componente escolhido;
- Listing usado nos resultados corresponde à entidade;
- campos do card possuem fallback;
- resultado completo usa template próprio;
- paginação e filtros preservam o mesmo contexto.

Uma busca AJAX pode retornar sugestões corretas e, ainda assim, abrir uma página completa com template errado. O template de resultados precisa ser criado e condicionado explicitamente.

## 5. Segurança

- Validar e limitar o termo de busca.
- Escapar termo, labels, links e HTML de resultados.
- Não aceitar post type, meta key ou orderby arbitrários vindos do cliente.
- Garantir que handlers AJAX respeitem visibilidade e status do conteúdo.
- Aplicar rate limit, debounce e limite de payload.
- Evitar mensagens que revelem dados privados.
- Não colocar tokens ou credenciais em JavaScript público.
- Usar cache sem compartilhar resposta personalizada entre usuários.
- Revisar endpoints e ações AJAX expostos.

## 6. Performance

- Definir mínimo de caracteres antes de iniciar AJAX.
- Aplicar debounce na digitação.
- Limitar sugestões e campos consultados.
- Evitar busca indiscriminada em postmeta de alto volume.
- Preferir taxonomias e campos indexáveis para filtros frequentes.
- Medir tempo do handler e tamanho da resposta.
- Cancelar ou ignorar respostas antigas quando o usuário continua digitando.
- Não carregar assets de busca em páginas sem o widget.

## 7. UX e acessibilidade

- Indicar carregamento sem bloquear o campo.
- Permitir teclado e leitores de tela.
- Usar labels claros e foco previsível.
- Exibir estado sem resultados.
- Não depender apenas de ícones ou cor.
- Manter link para ver todos os resultados.
- Preservar busca e filtros na URL quando a página for compartilhável.
- Testar mobile, conexão lenta e JavaScript desabilitado.

## 8. Padrão para catálogo ou portal

1. Definir entidades pesquisáveis.
2. Criar uma query controlada.
3. Criar Listing visual da sugestão.
4. Criar Listing/template da página completa.
5. Configurar provider e campos.
6. Validar conteúdo vazio, privado e inexistente.
7. Integrar com JetSmartFilters sem duplicar lógica.
8. Testar paginação e URL.
9. Medir AJAX e consultas.
10. Validar cache e permissões.

## Limites ainda não validados

- comportamento real do token manager em todos os fluxos;
- suporte completo a CCT;
- relevância e indexação interna da versão 3.6.3.1;
- compatibilidade com cada provider Elementor/JetEngine;
- segurança de configurações administrativas após ativação;
- performance em bases grandes.
