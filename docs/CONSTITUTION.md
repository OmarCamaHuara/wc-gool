# CONSTITUTION — wc-gool

> Documento de governança do projeto, no padrão da guia `hiria_pro`.
> Seções marcadas **IMUTÁVEL** não podem ser alteradas por agentes/LLMs sem aprovação
> explícita do CEO (Omar). Última atualização: 2026-07-09.

---

## 1. Missão

Construir uma plataforma web global (UI em inglês) de análise de mercados cripto e rede social
de traders, inspirada no TradingView: gráficos profissionais em tempo real + publicação de
ideias de trade com reputação verificável.

## 2. Valores

1. **Accountability em primeiro lugar** — ideias publicadas são imutáveis; o track record
   público é a moeda da plataforma (RT-02).
2. **Nenhum dinheiro real** — a plataforma não executa ordens, não custodia fundos e não
   promete lucro. Qualquer mudança nisso é decisão constitucional (regulatória).
3. **Documentação antes de código** — nenhuma feature é implementada sem regra de negócio
   escrita e micro-tarefa aprovada.
4. **Rastreabilidade** — toda decisão relevante vira ADR em `docs/DECISIONS.md` (append-only).

## 3. Stack Tecnológica — IMUTÁVEL

| Camada | Tecnologia | Status |
|---|---|---|
| Backend | **Java** | Imutável (ADR-001) |
| Frontend | **React** | Imutável (ADR-001) |
| Versões/frameworks (Java 21 + Spring Boot 3.x; React 18 + TS + Vite) | proposta | Revisável até a Fase 2 (T-01) |
| Banco relacional + séries temporais (PostgreSQL + TimescaleDB) | proposta | Revisável até a Fase 2 (T-02) |
| Gráficos (TradingView Lightweight Charts) | proposta | Revisável até a Fase 2 (T-03) |
| Fonte de dados v1 (Binance WebSocket/REST) | proposta | Revisável até a Fase 2 (T-04) |

Agentes **não questionam** as linhas imutáveis; as linhas "proposta" são fechadas por ADR
na Fase 2 (especificação técnica).

## 4. Escopo deste Repositório — IMUTÁVEL

Este repositório contém **somente documentação** (ADR-002): regras de negócio, especificações,
decisões e micro-tarefas (`US_BySteps/`). Código de aplicação viverá em repositório(s) próprio(s).
Nenhum agente cria código de aplicação aqui.

## 5. Método de Trabalho — IMUTÁVEL

Fases sequenciais; não se avança com pendência 🔴 aberta na fase anterior:

```
Fase 0 — Descoberta e alinhamento   (docs/00-descoberta, docs/01-alinhamento)  ✅
Fase 1 — Regras de negócio          (docs/02-regras-de-negocio)                🔄
Fase 2 — Especificação técnica      (docs/03-especificacao-tecnica)            ⏳
Fase 3 — Milestones e micro-tarefas (US_BySteps/Etapa-XXX)                     ⏳
Fase 4 — Implementação              (fora deste repo, guiada pelas Etapas)     ⏳
```

## 6. Regras para Micro-tarefas (US) — IMUTÁVEL

Padrão herdado da guia `hiria_pro`, adaptado:

- Nomenclatura: `US-XXXX-B` (backend), `US-XXXX-F` (frontend), `US-XXXX-D` (docs/infra),
  numeração global zero-padded, organizadas em `US_BySteps/Etapa-XXX/`.
- Cada US deve ser executável por **qualquer LLM sem contexto além dos documentos referenciados**:
  contém objetivo, contexto mínimo, critérios de aceitação verificáveis, arquivos afetados
  e definição de pronto (testes incluídos).
- Uma US = um PR pequeno (alvo: ≤ ~2 h de trabalho de um dev).
- Leitura obrigatória do agente antes de qualquer US:
  `CONSTITUTION.md` → `CONTEXT_GLOBAL.md` → regra de negócio do módulo → a própria US.

## 7. O que o CEO aprova

- Emendas a esta constituição e a qualquer seção IMUTÁVEL.
- Fechamento das decisões técnicas "proposta" da Seção 3.
- Passagem de fase (Fase 1 → 2 → 3).
- Mudanças de escopo do MVP (`docs/02-regras-de-negocio/00-escopo-mvp.md`).
- Qualquer funcionalidade que toque dinheiro real, execução de ordens ou dados pessoais sensíveis.

## 8. Idiomas — ativo

- Documentação: **PT-BR** (revisável — dúvida P-02).
- Produto (UI): **inglês** (ADR-006).

## 9. Disposições Imutáveis

Não mudam sem aprovação do CEO: esta constituição; Seções 3 (linhas imutáveis), 4, 5 e 6;
o princípio "nenhum dinheiro real" (Seção 2.2); o formato append-only de `docs/DECISIONS.md`.
