# WooCommerce e plugins Jet — arquitetura de ecommerce

## Escopo

Este módulo cobre JetWooBuilder 2.3.5, JetWooWidgets 1.1.9, JetWooProductGallery 2.4.0 e JetCompareWishlist 1.5.13 como camadas de apresentação e interação sobre WooCommerce.

## 1. Princípio central

Esses plugins devem compor a experiência visual e a descoberta de produtos. Não devem substituir as regras oficiais do WooCommerce para:

- preço;
- estoque;
- impostos;
- carrinho;
- checkout;
- pedidos;
- pagamentos;
- cupons;
- webhooks;
- sessões;
- permissões.

Qualquer customização precisa respeitar os objetos e hooks do WooCommerce e evitar gravações paralelas que criem divergência.

## 2. Componentes

### JetWooBuilder

Permite construir templates de loja, produto, arquivo, categorias, carrinho e outras áreas. Deve ser usado com condições explícitas e fallback para templates nativos.

Riscos: template global incorreto, prioridade sobre páginas críticas, incompatibilidade com checkout e cache de conteúdo contextual.

### JetWooWidgets

Fornece widgets para produtos, categorias, carrinho e elementos comerciais. Cada widget deve ser avaliado por consulta, assets, compatibilidade com variações e comportamento sem estoque.

### JetWooProductGallery

Controla galeria, imagens, zoom e mídia do produto. Deve manter alt text, proporções, lazy loading e fallback de imagem, sem expor mídia privada.

### JetCompareWishlist

Introduz estado de comparação e lista de desejos. É necessário definir se o estado é por cookie, sessão, usuário ou armazenamento persistente, além de política de privacidade e limpeza.

## 3. Fluxos críticos

### Produto

`produto → variações/opções → preço/estoque → adicionar ao carrinho`

Não confiar em preço ou ID de variação vindos do navegador. O servidor deve recalcular e validar.

### Carrinho

`produto → sessão/carrinho → totais → cupons/frete → checkout`

Cache de página não pode servir carrinho, totais ou mensagens personalizadas de outro usuário.

### Checkout

O checkout exige validação server-side, nonce, sanitização, regras de estoque, cálculo de totais e integração oficial com gateway. Widgets visuais não autorizam pedido nem pagamento.

### Wishlist/comparação

IDs recebidos precisam ser validados. Itens removidos, privados ou sem estoque devem ter comportamento definido.

## 4. Segurança

- Não expor preços, descontos ou regras comerciais como fonte confiável no JavaScript.
- Validar produto, variação, quantidade e disponibilidade no servidor.
- Respeitar capabilities e ownership em listas persistentes.
- Proteger AJAX e endpoints com nonce e autorização adequada.
- Escapar títulos, atributos, URLs, reviews e conteúdo de usuários.
- Sanitizar reviews, nomes e campos de checkout.
- Não registrar dados completos de cartão, tokens ou informações desnecessárias.
- Revisar webhooks, redirecionamentos e retorno de pagamento.
- Impedir cache compartilhado de dados de sessão.

## 5. Performance

- Consultas de produto devem possuir limite, paginação e ordenação definida.
- Galerias devem usar imagens dimensionadas e lazy loading.
- Assets dos widgets devem carregar somente quando usados.
- Evitar filtros ou queries em postmeta sem necessidade.
- Medir variações, atributos e widgets em catálogos grandes.
- Invalidar cache após produto, estoque, preço ou template mudar.
- Testar com usuário anônimo, cliente autenticado e carrinho ativo.

## 6. Compatibilidade com Elementor e JetEngine

- Produtos devem usar o modelo WooCommerce, não um CPT paralelo para preço/estoque.
- JetEngine pode complementar catálogo com campos editoriais, mas não deve duplicar dados transacionais.
- Dynamic Tags precisam ter fallback para produto sem campo personalizado.
- Templates de archive, single e loja devem ter condições documentadas.
- JetSmartFilters deve filtrar a fonte correta sem alterar regras comerciais.
- JetSearch deve apontar para produtos e taxonomias apropriados.

## 7. Testes obrigatórios

- produto simples;
- produto variável;
- produto sem estoque;
- produto com preço promocional;
- carrinho anônimo;
- cliente autenticado;
- cupom válido e inválido;
- frete e imposto;
- checkout com erro de validação;
- pagamento aprovado, recusado e pendente;
- webhook repetido;
- cache ativo;
- mobile e acessibilidade;
- wishlist/comparação em cookie e usuário persistente.

## 8. Padrão de implementação

1. Definir modelo de produto e regras oficiais do WooCommerce.
2. Criar templates visuais com fallback.
3. Adicionar widgets somente onde o núcleo não atende.
4. Manter dados editoriais separados dos transacionais.
5. Testar carrinho, checkout e pagamento antes de otimizar estética.
6. Revisar cache, sessão, AJAX e webhooks.
7. Documentar condições, dependências e rollback.

## Limites

Ainda falta validar em runtime os hooks específicos de cada versão, compatibilidade com gateways, comportamento de sessão, variações, HPOS, cache e temas WooCommerce concretos.
