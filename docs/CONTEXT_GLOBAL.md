# CONTEXT_GLOBAL — Memória viva do projeto

> Padrão da guia `hiria_pro`: memória institucional do projeto, atualizada ao fim de cada
> rodada de trabalho. Leitura obrigatória (após `CONSTITUTION.md`) antes de qualquer tarefa.
> Última atualização: 2026-07-09 (2ª rodada).

---

## 1. Estado atual do projeto

**Status:** Fase 1 — Regras de Negócio (pontos em aberto resolvidos; falta validação final do escopo)

- Fase 0 (descoberta + alinhamento) concluída: pesquisa de domínio feita, decisões de
  produto tomadas (ADR-004 a ADR-006, ADR-008).
- Fase 1: regras de negócio dos 6 módulos escritas e **todos os pontos em aberto Q-M*
  resolvidos pelo CEO (ADR-009)** — destaque: tema claro + escuro desde a v1 (RT-07).
- Nenhum código existe. Nenhuma Etapa de US foi criada ainda (Fase 3).

## 2. O produto em uma frase

Plataforma web global (inglês) de gráficos cripto em tempo real + rede social de ideias de
trade com reputação verificável — modelo TradingView, sem dinheiro real.

## 3. Stack (referência rápida)

Ver CONSTITUTION §3 para a lista completa e o que é imutável.

- Backend: **Java** (proposta: Java 21 + Spring Boot 3.x)
- Frontend: **React** (proposta: React 18 + TypeScript + Vite)
- Dados: proposta PostgreSQL + TimescaleDB + Redis; fonte v1 Binance
- Gráficos: proposta TradingView Lightweight Charts

## 4. Mapa da documentação

| Caminho | Conteúdo | Fase |
|---|---|---|
| `docs/CONSTITUTION.md` | Regras imutáveis e governança | — |
| `docs/CONTEXT_GLOBAL.md` | Este arquivo | — |
| `docs/DECISIONS.md` | ADRs (append-only) | — |
| `docs/00-descoberta/` | Pesquisa: TradingView, concorrentes, considerações técnicas | 0 ✅ |
| `docs/01-alinhamento/duvidas-e-decisoes.md` | Dúvidas abertas (as respondidas viram ADR) | 0/contínuo |
| `docs/02-regras-de-negocio/` | Escopo do MVP + regras dos módulos M1–M6 | 1 🔄 |
| `docs/03-especificacao-tecnica/` | (a criar) arquitetura, modelo de dados, contratos de API | 2 ⏳ |
| `US_BySteps/` | (a popular) micro-tarefas por Etapa | 3 ⏳ |

## 5. Módulos do MVP

M1 Usuários/perfis · M2 Dados de mercado (cripto) · M3 Gráficos · M4 Ideias ·
M5 Social/feed/moderação · M6 Watchlists. Alertas = v1.1; screener/paper trading = v2.
Detalhes: `docs/02-regras-de-negocio/00-escopo-mvp.md`.

## 6. Decisões que regem o estado atual

ADR-001 (Java+React) · ADR-002 (repo só docs) · ADR-003 (método por fases) ·
ADR-004 (pilar: gráficos+ideias) · ADR-005 (só cripto) · ADR-006 (global/inglês) ·
ADR-008 (padrão hiria_pro). Histórico completo: `docs/DECISIONS.md`.

## 7. Pendências que bloqueiam a próxima fase

1. Validação final do CEO do escopo do MVP (`00-escopo-mvp.md`) como contrato de escopo —
   gate da passagem para a Fase 2 (CONSTITUTION §7).
2. Dúvidas 🟠 restantes (não bloqueiam a Fase 2, mas ajudam): N-05 (monetização), N-06 (nome do
   produto), P-02 (idioma da doc), P-03 (granularidade das US), T-05 (hospedagem/orçamento —
   necessária ANTES de fechar a spec técnica).

## 8. Riscos ativos

1. Rate limits da fonte de dados gratuita (validar cedo — RN-M2-16).
2. Desenhos no gráfico são implementação própria sobre Lightweight Charts (custo alto — M3 §4).
3. Licença da Charting Library completa do TradingView: pedir cedo; muda o custo de M3 (Q-M3-B).
4. Moderação de conteúdo com um único admin (Q-M5-A).

## 9. Histórico de atualizações

| Data | Mudança |
|---|---|
| 2026-07-07 | Criação do repositório de docs; Fase 0 iniciada |
| 2026-07-09 | Decisões de produto tomadas (ADR-004..006); regras M1–M6 escritas; adoção do padrão hiria_pro (ADR-008) |
| 2026-07-09 | Pontos em aberto Q-M* resolvidos (ADR-009); tema claro+escuro na v1 (RT-07/RN-M3-18) |
