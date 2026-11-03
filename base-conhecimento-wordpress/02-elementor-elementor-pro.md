# Elementor e Elementor Pro — mapa técnico inicial

## Escopo e evidência

Baseado na inspeção estática dos pacotes Elementor 4.3.5 e Elementor Pro 4.3.2. Nenhum plugin foi instalado ou executado. A análise identifica superfícies de extensão e padrões de projeto; compatibilidade real deve ser validada em ambiente isolado.

## 1. Separação de responsabilidades

### Elementor

O pacote base concentra o editor visual, widgets fundamentais, controles, documentos, sistema de dados, assets, responsividade, templates, renderização e integração com o Core.

### Elementor Pro

O pacote Pro amplia o editor com Theme Builder, Dynamic Tags, formulários, popups, loops, recursos de marketing, integrações WooCommerce, pagamentos, condições e serviços de licença/atualização.

Regra: uma extensão deve declarar explicitamente se depende do Elementor base, do Pro ou de outro plugin. Não se deve assumir que uma API Pro existe em instalações gratuitas.

## 2. Modelo mental do editor

Uma página Elementor é composta por:

- documento;
- árvore de elementos;
- containers/seções/colunas;
- widgets;
- controles e configurações;
- valores dinâmicos;
- condições de renderização;
- estilos responsivos;
- CSS e JavaScript gerados;
- metadados persistidos no post.

O editor permite separar estrutura, conteúdo e apresentação. A Skill deve preservar essa editabilidade e evitar transformar toda a interface em um bloco HTML monolítico.

## 3. Pontos de extensão

### Widgets

Um widget customizado normalmente precisa definir:

- identificação e categoria;
- controles editáveis;
- valores padrão;
- renderização segura;
- estilos e scripts necessários;
- dependências de assets;
- suporte a conteúdo dinâmico;
- condições de disponibilidade;
- compatibilidade com editor e frontend.

### Controles

Controles devem representar propriedades editáveis pelo usuário: texto, link, imagem, repetidores, cores, tipografia, espaçamento, responsividade e campos dinâmicos.

Regra: usar controles nativos sempre que possível. Isso preserva editabilidade, responsividade, acessibilidade e compatibilidade com templates.

### Dynamic Tags

Dynamic Tags conectam controles a dados externos ou contextuais, como título, imagem destacada, campos personalizados, autor, termos e URLs.

Riscos:

- exibir dados privados;
- gerar links sem escape;
- executar queries em excesso;
- ignorar contexto de usuário;
- confiar em valores dinâmicos sem validação.

### Conditions e Theme Builder

Theme Builder e condições permitem selecionar templates para header, footer, single, archive, 404, produtos e outros contextos.

Toda condição deve ser testada com:

- usuário anônimo;
- usuário autenticado;
- diferentes roles;
- páginas sem dados;
- archives e singles;
- dispositivos móveis;
- cache ativo.

## 4. Elementor Pro por domínio

### Forms

Os formulários devem ser tratados como fronteira de segurança. A implementação precisa validar campos, limitar spam, proteger AJAX, controlar armazenamento, redirecionamento, webhook e envio de e-mail.

Nunca enviar credenciais ou tokens em campos ocultos. Webhooks devem usar autenticação, timeout, retry controlado e idempotência.

### Popups

Popups dependem de condições, triggers, cookies, frequência e contexto de página. Devem ser testados para não bloquear navegação, acessibilidade ou consentimento.

### Loop e conteúdo dinâmico

Loops devem ter query limitada, paginação e campos escapados. Evitar consultas repetidas por item e validar exposição de meta fields.

### WooCommerce e pagamentos

Elementor pode apresentar e compor fluxos WooCommerce, mas não deve substituir as garantias de checkout, autorização, webhook e persistência do próprio ecommerce.

Pagamentos exigem ambiente de teste, verificação de assinatura e nenhuma manipulação manual de status sem autorização explícita.

## 5. Assets, CSS e JavaScript

- Enfileirar assets somente quando o widget ou recurso existir na página.
- Declarar dependências e versões.
- Evitar scripts globais que assumam IDs ou classes frágeis.
- Não inserir segredos em JavaScript enviado ao navegador.
- Escapar URLs e atributos.
- Testar editor, preview e frontend separadamente.
- Verificar regeneração de CSS após alteração de templates.
- Medir impacto de fontes, ícones, animações, Lottie e bibliotecas externas.

## 6. Arquitetura de uma extensão segura

Separar:

1. bootstrap e verificação de dependências;
2. registro de widgets/controls/tags;
3. domínio e validação;
4. renderização;
5. assets;
6. endpoints e integrações;
7. compatibilidade/migrações;
8. testes.

O bootstrap deve falhar de forma controlada quando Elementor ou Elementor Pro não estiver disponível, sem fatal error e sem deixar estado parcialmente registrado.

## 7. Padrões para projetos

- Textos, botões, imagens e ícones devem usar widgets nativos e controles editáveis.
- HTML deve ser reservado para elementos realmente decorativos ou casos em que a editabilidade não seja necessária.
- Design tokens devem ser ligados às cores e tipografias globais do Elementor, não duplicados como hexadecimais espalhados.
- Templates devem ter responsabilidade única e condições documentadas.
- Conteúdo deve permanecer separado da estrutura visual sempre que o projeto exigir manutenção frequente.
- Campos JetEngine/ACF devem alimentar Dynamic Tags ou widgets apropriados, com fallback para ausência de valor.

## 8. Checklist de revisão

- A extensão verifica dependências e versões?
- Os controles são editáveis e responsivos?
- A saída HTML está escapada?
- URLs, atributos e CSS são seguros?
- Existe capability e nonce nos fluxos administrativos?
- Endpoints REST possuem `permission_callback`?
- AJAX público tem rate limiting ou mitigação adequada?
- Dados dinâmicos respeitam privacidade e contexto?
- Assets são carregados sob demanda?
- Há fallback para plugin desativado ou campo vazio?
- Migrações são reversíveis?
- O fluxo foi testado no editor e no frontend?

## 9. Limites ainda não validados

- APIs internas exatas e estabilidade entre versões;
- comportamento de widgets premium em runtime;
- compatibilidade específica com cada JetPlugin;
- desempenho em páginas com muitos widgets e loops;
- comportamento com cache, minificação e CDN;
- segurança de integrações externas e licenciamento;
- acessibilidade real em templates produzidos.
