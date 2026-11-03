# JetEngine e descoberta de dados

Use JetEngine para modelar CPT, CCT, meta fields, relations, listings, queries e forms. Defina ownership e ciclo de vida antes do schema.

- Query: fonte, filtros allowlist, ordenação, limite, paginação e contexto.
- Listing: apresentação editável, fallback e escape.
- Relation: origem, destino, cardinalidade, direção e exclusão.
- Form: nonce, capability, validação, ownership, idempotência e estado inicial.
- Dynamic Visibility controla apresentação, nunca autorização.
- JetSmartFilters e JetSearch devem compartilhar provider e contexto de query.
- Não expor CCT operacional, meta privado ou relation por REST/HTML/cache sem decisão explícita.
