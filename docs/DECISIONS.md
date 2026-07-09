# DECISIONS — Registro de Decisões (ADR)

> Formato herdado da guia `hiria_pro`: append-only — entradas nunca são editadas;
> uma decisão que muda gera novo ADR que **supersede** o anterior.
> Campos: Data · Contexto · Decisão · Justificativa · Alternativas rejeitadas · Status
> (`immutable` | `active` | `revisable` | `deprecated`).

---

## ADR-001 — Stack: Java (backend) + React (frontend)

- **Data:** 2026-07-07
- **Contexto:** escolha de stack no kickoff do projeto.
- **Decisão:** backend em Java, frontend em React.
- **Justificativa:** definição direta do CEO (domínio da equipe).
- **Alternativas rejeitadas:** não discutidas — premissa do projeto.
- **Status:** `immutable`

## ADR-002 — Repositório exclusivo de documentação

- **Data:** 2026-07-07
- **Contexto:** o CEO fará a implementação depois, via LLMs guiadas por micro-tarefas.
- **Decisão:** `wc-gool` contém somente documentação; código de aplicação em repositório(s) separado(s).
- **Justificativa:** separar a fonte da verdade (regras/tarefas) do código gerado.
- **Status:** `immutable`

## ADR-003 — Método: informação → alinhamento → regras de negócio → specs → micro-tarefas

- **Data:** 2026-07-07
- **Contexto:** risco de escrever documentação sólida sobre premissas erradas.
- **Decisão:** fases sequenciais com gates de aprovação do CEO (ver CONSTITUTION §5).
- **Status:** `immutable`

## ADR-004 — Pilar central do MVP: gráficos + ideias (modelo TradingView)

- **Data:** 2026-07-09
- **Contexto:** o domínio tem ~10 pilares possíveis; um MVP precisa de um núcleo único
  (ver `00-descoberta/03-analise-concorrentes.md` §4).
- **Decisão:** núcleo = gráficos profissionais + ideias sociais publicadas (imutáveis, com reputação).
- **Alternativas rejeitadas:** rede social pura estilo StockTwits (menos defensável);
  paper trading + ranking como núcleo (vira candidato a v2).
- **Status:** `active`

## ADR-005 — Mercados v1: somente criptomoedas

- **Data:** 2026-07-09
- **Contexto:** dados de ações/B3 em tempo real têm custo e licenciamento proibitivos para MVP;
  cripto tem WebSocket gratuito e sem royalties.
- **Decisão:** v1 cobre apenas pares cripto spot (fonte primária proposta: Binance, pares USDT).
- **Alternativas rejeitadas:** ações US delayed (v2), foco B3 (dados difíceis), multi-mercado (caro).
- **Status:** `active`

## ADR-006 — Público global, UI em inglês

- **Data:** 2026-07-09
- **Contexto:** definir idioma da plataforma e mercado-alvo.
- **Decisão:** produto global com UI em inglês (EN-US); i18n PT/ES em fase posterior;
  textos centralizados desde o início.
- **Alternativas rejeitadas:** LatAm/espanhol e Brasil/português como foco inicial.
- **Status:** `active`

## ADR-007 — Estrutura de documentação própria (provisória)

- **Data:** 2026-07-09
- **Contexto:** a guia `hiria_pro` estava privada e inacessível na sessão.
- **Decisão:** seguir com estrutura própria (`docs/00-descoberta`, `01-alinhamento`, `02-regras-de-negocio`).
- **Status:** `deprecated` — superseded por ADR-008.

## ADR-008 — Adoção do padrão de governança da guia `hiria_pro`

- **Data:** 2026-07-09
- **Contexto:** o repositório `hiria_pro` foi tornado público, permitindo estudar a guia:
  `docs/CONSTITUTION.md` (regras imutáveis) + `CONTEXT_GLOBAL.md` (memória viva) +
  `DECISIONS.md` (ADRs append-only) + `US_BySteps/Etapa-XXX/` (micro-tarefas por etapa).
- **Decisão:** adotar esse padrão em `wc-gool`, mantendo as pastas de descoberta e regras de
  negócio já criadas como acervo das Fases 0–1. Nomenclatura de US adaptada:
  `US-XXXX-B/F/D` (backend/frontend/docs).
- **Supersede:** ADR-007.
- **Status:** `active`
