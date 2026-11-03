# Arquitetura e seleção

## Ordem de decisão

1. WordPress Core e tema resolvem?
2. Elementor ou Elementor Pro resolvem?
3. JetEngine é necessário para dados dinâmicos?
4. WooCommerce ou booking já é a fonte transacional?
5. JetSmartFilters/JetSearch são necessários para descoberta?
6. Yoast é necessário para SEO técnico?
7. Happy ou outros Jet adicionam capacidade que não existe?

Escolha uma fonte de verdade por função: template global, popup, widget, query, schema, preço, estoque, disponibilidade e autorização.

## Modelos

- CPT para conteúdo editorial com single/archive, autor, taxonomia ou revisão.
- CCT para dados tabulares e grandes volumes sem ciclo editorial completo.
- Relations para vínculos explícitos.
- Meta fields para atributos com tipo e chave estáveis.
- WooCommerce para dados transacionais de ecommerce.
- Booking/appointments para disponibilidade, slots, status e conflitos.

## Entrega

Toda proposta deve listar componentes necessários, componentes evitados, dependências, modelo de dados, riscos, testes, rollback e pontos de aprovação.
