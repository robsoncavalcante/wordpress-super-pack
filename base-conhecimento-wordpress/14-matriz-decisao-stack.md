# Matriz de decisão da stack WordPress

## 1. Princípio de composição

Começar pelo menor conjunto de componentes que resolve o requisito. Cada plugin adicional aumenta superfície de segurança, assets, consultas, atualizações e possibilidade de conflito.

## 2. Matriz principal

| Necessidade | Primeira escolha | Complemento possível | Evitar |
|---|---|---|---|
| Conteúdo editorial | WordPress Core + Elementor | Yoast | CPT duplicado sem necessidade |
| Layout visual | Elementor | Elementor Pro | HTML monolítico |
| Theme Builder | Elementor Pro | JetThemeCore | duas fontes globais sem decisão |
| CPT e campos | JetEngine | ACF se já adotado | duplicar o mesmo campo em plugins |
| Grande volume tabular | JetEngine CCT | Dynamic Tables | carregar tudo no browser |
| Relações | JetEngine Relations | queries específicas | relation sem ownership |
| Listing dinâmico | JetEngine + Elementor | JetWidgets/Happy | lógica de negócio no template |
| Filtros | JetSmartFilters | query do JetEngine | filtro sem provider coerente |
| Busca | JetSearch | busca nativa/externa | busca sem limite ou debounce |
| SEO | Yoast SEO | Premium quando necessário | schema duplicado |
| Ecommerce | WooCommerce | JetWoo/Elementor Pro | regras transacionais em widgets |
| Reserva | JetBooking | gateway/notificações | formulário sem lock/idempotência |
| Agendamento | JetAppointments | calendário/notificações | slot confirmado apenas no frontend |
| Widgets adicionais | Elementor Pro | Happy ou Jet, um por função | ativar todos |
| Popup | Elementor Pro | JetPopup ou Happy, um por função | múltiplos sistemas concorrentes |
| Menu | tema/Elementor Pro | JetMenu/JetBlocks | markup duplicado |
| Animação | CSS/Elementor | JetTricks/Happy | várias bibliotecas globais |

## 3. Dependências por camada

```text
WordPress Core
├── Elementor
│   └── Elementor Pro
├── JetEngine
│   ├── Listings / Queries / Relations
│   ├── JetSmartFilters
│   ├── JetSearch
│   └── módulos complementares
├── WooCommerce
│   └── JetWoo / widgets ecommerce
├── JetBooking ou JetAppointments
├── Yoast SEO
└── Happy Elementor Addons
```

As linhas representam dependências conceituais, não garantia de compatibilidade de versões.

## 4. Matriz de risco

| Camada | Entrada crítica | Risco | Controle mínimo |
|---|---|---|---|
| Core | REST/AJAX/forms | CSRF, XSS, privilege escalation | nonce, capability, sanitização, escape |
| Elementor | Dynamic Tags/HTML | exposição e markup inseguro | controles, escape, fallback |
| JetEngine | meta/CCT/relations | dados expostos ou query cara | ownership, limite, permission, paginação |
| Filters/Search | URL/AJAX | abuso, inconsistência, leak | allowlist, debounce, limite, provider |
| WooCommerce | preço/estoque/carrinho | fraude ou sessão cruzada | servidor, sessão, cache, webhook |
| Booking | slot/status | dupla reserva | lock, revalidação, idempotência |
| Yoast | schema/indexables | duplicidade ou dados falsos | fonte única, HTML final, migração |
| Happy/Jet UI | assets/HTML remoto | XSS, performance | escopo, dependências, carga condicional |

## 5. Fluxo de seleção de plugins

1. Descrever requisito de negócio.
2. Identificar entidade e ownership.
3. Separar conteúdo, apresentação e transação.
4. Verificar capacidade nativa do Core/Elementor/WooCommerce.
5. Escolher um plugin por função.
6. Confirmar dependência e versão.
7. Mapear dados, endpoints, assets e cache.
8. Definir testes e rollback.
9. Implementar em ambiente isolado.
10. Só então promover para produção.

## 6. Regras de não combinação automática

- Elementor Pro, JetThemeCore e Happy Theme/Theme widgets não devem controlar o mesmo template sem governança.
- Elementor Pro, JetPopup, Happy Modal e JetPopup não devem controlar o mesmo popup sem motivo.
- Elementor Pro, JetElements, JetWidgets e Happy não devem duplicar widgets sem necessidade.
- JetEngine CCT não deve duplicar dados transacionais do WooCommerce.
- Yoast, tema e plugins de schema não devem gerar o mesmo tipo de schema simultaneamente.
- JetSmartFilters e JetSearch devem compartilhar contexto de query e provider.
- Dynamic Visibility nunca deve ser a única proteção de dado.

## 7. Ambientes e promoção

### Desenvolvimento

Usar cópia isolada, dados fictícios controlados, logs detalhados e acesso externo mínimo.

### Homologação

Reproduzir permissões, cache, cron, integrações e volumes relevantes. Validar fluxos críticos com dados não sensíveis.

### Produção

Backup, janela de mudança, rollback, monitoramento e registro de versões. Não limpar ou substituir dados reais sem autorização específica.

## 8. Critério para a futura Skill

A Skill deverá retornar, para cada solicitação:

- arquitetura recomendada;
- plugins necessários e plugins dispensáveis;
- entidades e modelo de dados;
- dependências e versões;
- riscos e controles;
- estratégia de testes;
- plano de rollback;
- agentes adequados;
- pontos que exigem aprovação humana.

## Limites

Esta matriz é uma regra de decisão arquitetural baseada na inspeção estática e em padrões anteriores. Compatibilidade específica de versão, comportamento de runtime e desempenho devem ser confirmados em ambiente de teste.
