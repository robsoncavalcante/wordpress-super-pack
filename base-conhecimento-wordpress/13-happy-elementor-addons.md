# Happy Elementor Addons Free e Pro

## Escopo e inventário

Foram analisados os dois pacotes recebidos:

- Happy Elementor Addons Free;
- Happy Elementor Addons Pro 4.2.0.

O Pro contém áreas próprias de widgets, controls, extensions, conditions, templates, vendor, assets, mega menu, GSAP, charts, WooCommerce e EDD.

## 1. Papel arquitetural

Happy Addons é uma camada de extensão visual para Elementor. Ele adiciona widgets, efeitos, componentes de navegação, templates e integrações. Não deve ser tratado como substituto do WordPress Core, Elementor Pro, WooCommerce ou JetEngine.

## 2. Famílias de widgets observadas

- conteúdo e headings;
- accordion, tabs, toggle e timeline;
- grids, carousels, posts e produtos;
- pricing, comparison e shipping bar;
- charts e tabelas;
- mapas e hotspots;
- menus, nav, off-canvas e one-page navigation;
- popups, modal e sticky video;
- SVG, GSAP, scroll e animações;
- WooCommerce;
- Easy Digital Downloads;
- feeds sociais;
- loop grid e conteúdo dinâmico.

O número de widgets não justifica habilitar todos. Cada recurso deve ser ativado somente quando houver necessidade.

## 3. Extensions e condições

O Pro possui extensões como:

- display conditions;
- parallax e multi-layer effects;
- horizontal scroll;
- global badge;
- infinite marquee;
- global animation;
- particle effects;
- image trails;
- image masking;
- sticky pin element;
- designs manager.

Condições e efeitos operam na camada de apresentação. Não devem ser usados para esconder dados que exigem autorização.

## 4. Integrações e dependências

Validar antes de usar:

- versão mínima do Elementor;
- disponibilidade do Elementor Pro;
- WooCommerce ou EDD, quando aplicável;
- dependências de GSAP, chart libraries ou mapas;
- compatibilidade com JetEngine e Happy Loop Grid;
- assets e fontes carregadas;
- licença e atualização.

Widgets de WooCommerce e EDD devem respeitar as APIs oficiais dos respectivos sistemas.

## 5. Segurança

- Revisar widgets de Source Code, HTML, SVG e feeds externos.
- Sanitizar e escapar conteúdo dinâmico.
- Não expor tokens de APIs sociais no frontend.
- Validar URLs, imagens, embeds e iframes.
- Proteger formulários e AJAX com nonce/capability.
- Restringir condições administrativas.
- Revisar dados exibidos por Dynamic Tags e Loop Grid.
- Não confiar em display conditions para controle de acesso.
- Revisar vendor e dependências de terceiros.

Widgets como charts, maps, social feeds, remote carousel e source code podem introduzir requisições externas, conteúdo remoto, custo de performance e risco de privacidade.

## 6. Performance

- Habilitar somente widgets/extensões necessários.
- Carregar CSS/JS sob demanda.
- Limitar carousels, feeds e grids.
- Evitar várias bibliotecas de animação na mesma página.
- Respeitar `prefers-reduced-motion`.
- Otimizar imagens e vídeos.
- Evitar charts e mapas renderizando grandes datasets no navegador.
- Medir páginas com Loop Grid, WooCommerce e efeitos simultâneos.

## 7. Editabilidade e manutenção

- Usar controles nativos do widget.
- Evitar blocos monolíticos em Source Code para conteúdo editorial.
- Separar texto, imagem, botão e ícone em controles editáveis.
- Manter design tokens no sistema global do Elementor.
- Documentar IDs, condições, dependências e fallback.
- Não misturar vários plugins para a mesma função sem decisão explícita.

## 8. Sobreposição com a stack

| Função | Possíveis concorrentes |
|---|---|
| widgets visuais | Elementor Pro, JetElements, JetWidgets |
| popup | Elementor Pro, JetPopup |
| condições | JetEngine, Elementor Pro |
| loop/grid | Elementor Pro, JetEngine |
| WooCommerce | Elementor Pro, JetWooBuilder |
| menu | JetMenu, JetBlocks, Theme Builder |
| tabs/accordion | Elementor Pro, JetTabs |
| animações | Elementor, JetTricks, Happy Pro |
| charts/tables | JetEngine modules, Happy Pro |

Escolher uma fonte de verdade por função reduz conflitos de CSS, assets, markup e comportamento.

## 9. Checklist de ativação

1. Identificar widget ou extensão necessária.
2. Verificar se Elementor Pro ou Jet já resolve.
3. Confirmar dependências e licença.
4. Habilitar somente o recurso necessário.
5. Testar editor, preview e frontend.
6. Validar mobile, acessibilidade e reduced motion.
7. Revisar requisições externas e dados exibidos.
8. Medir performance.
9. Testar desativação e fallback.
10. Documentar a escolha.

## Limites

A inspeção estática não comprova comportamento em runtime, segurança de cada widget, licenciamento, compatibilidade exata com Elementor 4.3.5, conflitos com JetPlugins, custo real de assets ou comportamento de integrações externas.
