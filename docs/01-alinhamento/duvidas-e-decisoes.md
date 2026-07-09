# Dúvidas de Alinhamento e Registro de Decisões

**Como usar este documento**: cada dúvida tem um ID. Responda no chat ou editando este arquivo.
Quando uma dúvida for respondida, a resposta vira uma **Decisão numerada** na seção final e a
dúvida é marcada como ✅. Nenhum documento de regra de negócio será escrito com dúvidas 🔴 abertas.

Legenda de prioridade: 🔴 bloqueia o planejamento · 🟠 importante, mas tem default razoável · 🟢 pode esperar

---

## P — Processo e documentação

### P-01 ✅ Acesso à guia `hiria_pro`
**Respondida em 2026-07-09 → ADR-007, superseded por ADR-008**: o repositório foi tornado
público no mesmo dia; a guia foi estudada e seu padrão adotado (CONSTITUTION + CONTEXT_GLOBAL +
DECISIONS em ADR + `US_BySteps/Etapa-XXX`).

### P-02 🟠 Idioma da documentação
Estou escrevendo em PT-BR. Confirma? (Alternativas: espanhol, inglês, ou PT para negócio +
inglês para specs técnicas — inglês costuma render melhor com LLMs na hora de codar.)

### P-03 🟠 Granularidade das micro-tarefas
Você pediu tarefas que "qualquer LLM possa fazer". Para calibrar: uma micro-tarefa ideal para você é
algo como **"criar endpoint `GET /api/watchlists/{id}` retornando X, com teste"** (1–2 h de trabalho,
um PR pequeno)? Ou ainda menor (ex.: "criar a entidade JPA `Watchlist` com os campos X, Y")?

### P-04 🟢 Ferramenta de gestão das tarefas
Os milestones/micro-tarefas viverão onde? (a) arquivos Markdown neste repo; (b) GitHub Issues +
Milestones deste repo; (c) GitHub Projects. Sugestão: (a) como fonte da verdade + (b) gerado a partir de (a).

---

## N — Negócio e produto

### N-01 ✅ Qual é o pilar central do produto?
**Respondida em 2026-07-09 → D-004**: modelo TradingView — **gráficos excelentes + ideias sociais**
(análises publicadas com gráfico anotado) em volta.

### N-02 ✅ Quais mercados/ativos na v1?
**Respondida em 2026-07-09 → D-005**: **somente cripto** na v1 (dados em tempo real gratuitos).

### N-03 ✅ Público-alvo e idioma da plataforma
**Respondida em 2026-07-09 → D-006**: **global, UI em inglês**, com i18n para PT/ES em fase posterior.

### N-04 🟠 Copy trading / execução real está no horizonte?
Mesmo que não seja MVP: o plano de longo prazo inclui executar ordens ou copy trading com dinheiro
real? A resposta muda decisões de arquitetura e a estratégia regulatória desde já
(ver análise de concorrentes, seção 4.1). Minha recomendação: manter fora do horizonte v1–v2.

### N-05 🟠 Modelo de monetização pretendido
(a) Freemium com assinatura (padrão do setor); (b) grátis por enquanto, monetiza depois;
(c) ads; (d) marketplace/criadores. Precisa estar claro cedo porque limites de plano
(nº de alertas, watchlists etc.) entram nas regras de negócio.

### N-06 🟠 Nome do produto
"wc-gool" é o nome do repositório — é também o nome do produto? Tem marca/nome em mente?
(Impacta domínio, textos da documentação e identidade visual.)

### N-08 🟠 Quais features de IA entram na v1?
A investigação [`00-descoberta/05-ia-nos-concorrentes.md`](../00-descoberta/05-ia-nos-concorrentes.md)
mostrou que o setor virou "AI-first" em 2025–2026 e mapeou 6 candidatas (F-IA-1 a F-IA-6).
**Proposta**: v1 leva **F-IA-1 (TL;DR de ideia)** e **F-IA-5 (moderação assistida)** — as duas
mais baratas e que usam nosso dado proprietário; copiloto de gráfico (F-IA-3) e pulso do
símbolo (F-IA-2) na v1.x. Confirmar ou ajustar.

### N-07 🟢 O que existe hoje?
Isso é um projeto do zero, certo? Existe algo já feito (design, pesquisa, público, comunidade,
sócios)? Existe prazo ou evento-alvo (ex.: lançar em X meses)?

---

## T — Técnico (defaults propostos — vetar ou confirmar)

Para não travar o planejamento, proponho defaults. Se você não discordar, viram decisão:

### T-01 🟠 Versões e frameworks
**Default proposto**: Java 21 LTS + Spring Boot 3.x; React 18 + TypeScript + Vite.

### T-02 🟠 Arquitetura inicial
**Default proposto**: monólito modular (um app Spring Boot com módulos bem separados) + um serviço
de ingestão de cotações. Microserviços só quando doer. Banco único PostgreSQL + TimescaleDB + Redis.

### T-03 🟠 Biblioteca de gráficos
**Default proposto**: TradingView **Lightweight Charts** (open source) no MVP; solicitar em paralelo
a licença gratuita da Charting Library completa.

### T-04 🟠 Fonte de dados v1
**Default proposto** (depende de N-02): WebSocket público da Binance para cripto (tempo real, grátis).

### T-05 🟠 Hospedagem e orçamento de infra
Onde você pretende rodar (AWS, GCP, Hetzner, Railway, VPS...)? Qual orçamento mensal máximo
aceitável para o MVP? (Estimei USD 25–150/mês no doc técnico.) Isso poda decisões de arquitetura.

### T-06 🟢 Mobile
**Default proposto**: web responsivo primeiro; app mobile fora do escopo v1.

### T-07 🟢 Autenticação
**Default proposto**: e-mail/senha + login Google (OAuth2), JWT.

### T-08 🟠 Provedor de LLM e orçamento de API
Depende de N-08. Qual provedor de LLM para as features de IA (Anthropic/Claude, OpenAI,
Google/Gemini, modelos abertos) e qual teto de gasto mensal com API no MVP?
**Default proposto**: decidir o provedor na Fase 2 com PoC comparativa; arquitetura trata o
LLM como plugável; teto inicial sugerido: USD 50/mês (features baratas F-IA-1/F-IA-5 cabem).

---

## Registro de Decisões

Movido para [`../DECISIONS.md`](../DECISIONS.md) no formato ADR do padrão `hiria_pro` (ADR-008).
As referências D-001…D-007 deste documento correspondem a ADR-001…ADR-007.
