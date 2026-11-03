---
name: wordpress-solutions
description: Planejar, construir, auditar e revisar soluções WordPress com Elementor, Elementor Pro, JetEngine, JetPlugins, Yoast SEO e Happy Elementor Addons, priorizando arquitetura, segurança, compatibilidade, performance e rollback.
metadata:
  short-description: Desenvolvimento seguro de soluções WordPress
---

# WordPress Solutions

Use esta Skill quando a tarefa envolver criação, evolução, auditoria ou diagnóstico de landing pages, sites institucionais, ecommerce, catálogos, portais, reservas ou sistemas dinâmicos baseados em WordPress e nos componentes da stack analisada.

## Resultado esperado

Entregar uma solução proporcional ao pedido, com arquitetura explícita, menor conjunto necessário de plugins, riscos conhecidos, validação adequada e plano de rollback.

## Regras essenciais

- Inspecione o projeto e o estado atual antes de propor mudanças.
- Consulte a documentação de referência relevante antes de decidir entre Core, Elementor, JetEngine, WooCommerce, Yoast, Jet ou Happy.
- Separe conteúdo, dados, apresentação, transações, integrações e operação.
- Use um plugin por função quando possível; não ative toda a suíte por conveniência.
- Nunca trate visibilidade visual como autorização.
- Valide, autorize, sanitize e escape toda entrada e saída.
- REST exige `permission_callback`; AJAX exige nonce, capability quando aplicável e limites.
- Queries devem ter fonte, allowlist, limite, paginação e contexto documentados.
- Dados transacionais permanecem sob a fonte oficial do WooCommerce ou do sistema de reservas.
- Mudanças em dados reais exigem backup, validação, rollback e aprovação proporcional ao risco.
- Não edite `vendor`, migrations existentes ou arquivos de terceiros para criar extensões.

## Roteamento

Leia somente as referências necessárias:

- Arquitetura e seleção de plugins: [references/architecture.md](references/architecture.md)
- Segurança: [references/security.md](references/security.md)
- Dados JetEngine: [references/jetengine.md](references/jetengine.md)
- Elementor e addons visuais: [references/elementor.md](references/elementor.md)
- Ecommerce e reservas: [references/commerce-booking.md](references/commerce-booking.md)
- SEO Yoast: [references/yoast.md](references/yoast.md)
- Delegação e revisão: [references/agents.md](references/agents.md)
- Fluxos por solução: [references/workflows.md](references/workflows.md)
- QA e critérios de aceite: [references/qa.md](references/qa.md)
- Matriz de agentes: [references/agent-matrix.md](references/agent-matrix.md)
- Exemplos de handoff: [references/examples.md](references/examples.md)

## Fluxo padrão

1. Classifique o tipo de solução e o risco.
2. Inspecione versões, estrutura, dados, integrações e estado atual.
3. Modele entidades, ownership, ciclo de vida e fonte de verdade.
4. Selecione o menor conjunto de componentes.
5. Produza plano e critérios de aceite antes de mudanças amplas.
6. Implemente incrementalmente, preservando editabilidade e reversibilidade.
7. Faça revisão de segurança, compatibilidade, performance e UX.
8. Teste vazio, inválido, anônimo, autenticado, mobile, cache e falhas de integração.
9. Revise o diff e documente decisões, limitações e rollback.

## Entrega por tipo de projeto

Quando o pedido envolver um tipo específico de produto, leia o fluxo correspondente em `references/workflows.md` e adapte-o ao contexto. Não pule modelagem, segurança ou critérios de aceite apenas porque a entrega é visual.

## Limites

Não invente APIs, compatibilidade ou comportamento de runtime com base apenas no nome de um plugin. Quando a versão, licença, procedência, servidor ou comportamento não estiver comprovado, declare a incerteza e proponha validação isolada.
