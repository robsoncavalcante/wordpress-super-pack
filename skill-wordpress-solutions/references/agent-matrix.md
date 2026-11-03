# Matriz de agentes

| Tarefa | Responsável principal | Revisores | Entrega mínima |
|---|---|---|---|
| Descoberta e escopo | Planner | Architect | objetivo, restrições, riscos, aceite |
| Modelo CPT/CCT/relations | JetEngine | Security, QA | schema, ownership, queries, migration |
| Template Elementor | Elementor | UX, QA | template editável, responsivo, fallback |
| Widget/plugin PHP | WordPress | Security, Reviewer | arquivos, hooks, validação, testes |
| Filtros e busca | JetEngine/Discovery | Performance, QA | provider, Query ID, paginação, AJAX |
| Ecommerce | Commerce | Security, QA | fluxo WooCommerce, sessão, webhook |
| Booking | Booking | Security, QA | disponibilidade, lock, estados, idempotência |
| SEO | SEO | Content, QA | indexação, metadata, schema, sitemap |
| Performance | Performance | QA | métricas antes/depois e regressões |
| Auditoria de segurança | Security | Reviewer | achados priorizados e correções |
| Validação final | QA | Security, Owner | evidências, limitações, aceite |

## Regras de delegação

- Divida por responsabilidade ou arquivos sem sobreposição.
- Dê ao agente contexto mínimo suficiente, não conclusões prontas.
- Exija evidências e arquivos alterados.
- Não delegue publicação, pagamento, credenciais, exclusão ou produção sem autorização.
- O agente que implementa não é o único responsável pela aprovação.
- Segurança e QA podem rodar em paralelo à implementação quando não dependem do resultado final.
- Reunir resultados antes de integrar mudanças que alterem schema ou dados.

## Coordenação Codex/Claude Code

O Codex deve concentrar planejamento, escopo, prompts completos, revisão e validação. O Claude Code pode implementar no repositório quando essa divisão for escolhida, sempre recebendo critérios de aceite e limites claros.
