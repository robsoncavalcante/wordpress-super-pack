# JetThemeCore, JetPopup e widgets Jet — camada de apresentação

## Escopo

Este módulo reúne JetThemeCore 2.3.4, JetPopup 2.2.3.3, JetMenu 3.0.3, JetBlocks 1.5.2.2, JetTabs 2.3.5, JetElements 2.9.2.6, JetBlog 2.4.11, JetTricks 2.0.1 e JetStyleManager 1.3.9.

## 1. Divisão de responsabilidades

- JetThemeCore: templates globais e condições de tema.
- JetPopup: popups, triggers, condições e frequência.
- JetMenu: menus, mega menus e navegação.
- JetBlocks: header, footer e elementos de navegação.
- JetTabs: abas, acordeões e conteúdo alternável.
- JetElements: widgets visuais para Elementor.
- JetBlog: layouts e componentes de conteúdo.
- JetTricks: efeitos, animações e interações.
- JetStyleManager: controles e estilo compartilhado.

Esses plugins não devem duplicar indiscriminadamente recursos existentes no Elementor Pro ou no tema.

## 2. ThemeCore e templates globais

Templates de header, footer, single, archive e 404 precisam de:

- condição explícita;
- prioridade conhecida;
- fallback;
- teste em usuário anônimo e autenticado;
- teste em páginas, posts, CPT, archives e 404;
- verificação de cache;
- documentação de qual template vence em conflito.

Condições visuais não substituem autorização. Um template que não exibe um dado não impede acesso por REST, HTML pré-cacheado ou endpoint.

## 3. Popups

Definir antes de publicar:

- trigger;
- condição de página;
- frequência e cookie;
- fechamento por teclado;
- foco e retorno de foco;
- comportamento mobile;
- consentimento, se houver coleta;
- integração com formulário;
- exclusão de usuários já convertidos.

Popups não devem bloquear navegação, esconder conteúdo essencial ou criar loops de abertura.

## 4. Menus e blocos de tema

Menus devem preservar:

- navegação por teclado;
- foco visível;
- hierarquia semântica;
- estado expandido corretamente anunciado;
- fallback sem JavaScript;
- links escapados e destinos válidos;
- comportamento mobile previsível.

Mega menus podem aumentar muito o DOM e os assets. Carregar conteúdo dinâmico apenas quando necessário.

## 5. Tabs, blog e conteúdo alternável

Abas e acordeões devem:

- possuir headings e labels claros;
- indicar estado ativo;
- funcionar por teclado;
- não esconder conteúdo essencial de mecanismos de busca sem intenção;
- não duplicar IDs;
- preservar links profundos quando necessário.

Cards de blog e listings devem escapar títulos, excerpts, imagens e URLs, com fallback para campos ausentes.

## 6. Widgets e estilo

Widgets Jet devem ser usados quando agregarem capacidade real. Para cada widget, validar:

- dependência Elementor/Pro;
- controles editáveis;
- responsividade;
- HTML semântico;
- assets carregados;
- CSS global versus escopado;
- compatibilidade com tema;
- acessibilidade;
- impacto de performance.

Regra: texto, botões, imagens e ícones devem permanecer em widgets e controles nativos sempre que possível; HTML monolítico reduz manutenção e editabilidade.

## 7. Animações e efeitos

- Respeitar `prefers-reduced-motion`.
- Não usar animação como única forma de comunicar estado.
- Evitar listeners globais e cálculos contínuos sem necessidade.
- Desativar efeitos pesados em mobile quando apropriado.
- Testar scroll, teclado, touch e baixa performance.
- Não inserir dependências externas sem avaliar procedência e custo.

## 8. Conflitos com Elementor Pro e Happy Addons

Possíveis duplicidades:

- Theme Builder;
- Popup;
- widgets de blog;
- tabs e accordion;
- mega menu;
- condições de exibição;
- animações;
- controles de estilo.

Escolher uma fonte de verdade por função. Misturar recursos equivalentes aumenta risco de prioridades conflitantes, CSS duplicado, assets e dificuldade de manutenção.

## 9. Checklist de segurança e qualidade

- condições globais documentadas;
- HTML escapado e sem conteúdo arbitrário;
- links e atributos seguros;
- formulários protegidos pelo componente responsável;
- assets carregados sob demanda;
- CSS escopado para evitar vazamento global;
- foco e teclado testados;
- reduced motion respeitado;
- cache testado por contexto;
- templates desativados sem deixar página quebrada;
- importações de templates revisadas antes de aplicar.

## 10. Padrão de implementação

1. Definir a função visual necessária.
2. Verificar se Elementor Pro ou tema já resolve.
3. Escolher um único plugin responsável.
4. Criar template/widget mínimo e editável.
5. Configurar condições e fallback.
6. Escopar CSS e carregar assets sob demanda.
7. Testar acessibilidade e responsividade.
8. Validar cache, performance e desativação.
9. Documentar dependências e rollback.

## Limites

Ainda falta analisar cada plugin individualmente em código, confirmar hooks e dependências das versões recebidas e validar comportamento em runtime com temas, Elementor Pro, Happy Addons e cache reais.
