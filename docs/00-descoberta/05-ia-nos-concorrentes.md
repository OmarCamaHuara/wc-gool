# IA nos Concorrentes — Como o Setor Usa IA na Experiência do Usuário

**Objetivo**: mapear como as plataformas de trading/social trading usam IA (2025–2026) para
melhorar a experiência do usuário, e derivar o que faz sentido para o nosso produto.
**Data da pesquisa**: 2026-07-09.
**Contexto**: 2025–2026 marcou a virada "AI-first" no setor — todos os grandes players lançaram
assistentes de IA como feature central, não acessório.

**Fontes principais**: [TradingView AI Copilot (Lune)](https://lunefi.com/blog/tradingview-assistant),
[eToro press release](https://www.etoro.com/news-and-analysis/press-releases/etoro-launches-new-app-ai-first-smart-and-social/),
[Robinhood newsroom](https://robinhood.com/us/en/newsroom/introducing-strategies-banking-and-cortex/),
[Public.com Alpha](https://public.com/alpha), [Investing.com WarrenAI](https://www.investing.com/warrenai),
[StockTwits/Thematic](https://stocktwits.com/news-articles/business/others/stocktwits-acquires-ai-startup-thematic/ch8KVxsR5pd).

---

## 1. Fichas por concorrente

### 1.1 TradingView — AI Chart Copilot (beta público, 2026)

- Painel lateral no navegador que **lê o gráfico ativo** e gera em linguagem natural:
  padrões técnicos identificados, suportes/resistências, força de tendência e possíveis setups.
- Configura **alertas por comando de texto** e **resume notícias** explicando movimentos de preço.
- Plano free: limitado a ~15 requisições/dia (IA como alavanca de conversão para planos pagos).
- **Não** gera Pine Script nativamente nem envia ordens — mantém a neutralidade da plataforma.
- Em volta: ecossistema de terceiros (extensões, geradores de Pine Script por IA como Pineify),
  e o Q1/2026 expandiu a "camada de IA" da plataforma.

### 1.2 eToro — Tori, o app "AI-first" (julho/2026)

- Reconstruiu o app inteiro em torno da assistente **Tori**: updates de portfólio, sinais de
  mercado, explicação de movimentos de preço em linguagem natural.
- **Agentes de IA que operam**: o usuário cria ou **copia agentes** que negociam 24/7, cada um
  numa sub-conta isolada — é o copy trading aplicado a robôs de IA.
- Tori integrada a canais externos (WhatsApp, Apple Watch) e com dados em tempo real do X
  (parceria Grok) para "inteligência social".
- Lição: o eToro transformou IA no **novo objeto social copiável** (antes copiava-se gente,
  agora copiam-se agentes).

### 1.3 Robinhood — Cortex (2025–2026)

- **Cortex Digests**: resumos diários personalizados — o que mexeu NO SEU portfólio e por quê,
  conectando notícias, movimentos e análises aos holdings do usuário.
- Comandos em linguagem natural: comprar/vender, pesquisar, ajustar configurações da conta.
- **Indicadores e scans customizados gerados por IA** (rollout 2026, exclusivo do plano Gold).
- Lição: IA como **benefício de assinatura premium** e motor de personalização do feed.

### 1.4 Public.com — Alpha (pioneiro, 2023; agentes em 2025–2026)

- **Alpha**: copiloto de pesquisa (GPT-4 desde 2023) — perguntas em linguagem natural sobre
  qualquer ativo, com dados fundamentais e contexto.
- Evoluiu para **agentes de investimento no-code** que automatizam estratégias.
- "Better Watchlist": watchlist com camada de IA (resumos e razões de movimento por item).

### 1.5 StockTwits — sentimento e curadoria por IA

- Historicamente: **índice de sentimento** bullish/bearish por ativo, agregado dos posts
  (dado tão valioso que é vendido a fundos via parceiros de analytics).
- 2025: **adquiriu a Thematic** (IA de research) para contextualizar 17 anos de dados de
  sentimento e comportamento — IA que resume o que a comunidade está dizendo e por quê.
- IA para *surfacing*: trending tickers, mudanças de sentimento, "key takeaways" da conversa.
- Lição: **o conteúdo da comunidade é matéria-prima de IA** — resumo e sentimento agregado
  transformam milhares de posts em um dado consumível em 5 segundos.

### 1.6 Investing.com — WarrenAI + ProPicks

- **WarrenAI**: assistente de pesquisa conversacional sobre 72.000+ ativos (screening e
  comparações em linguagem natural).
- **ProPicks AI**: carteiras mensais escolhidas por IA, com track record público divulgado
  agressivamente como marketing (~160–180% desde o lançamento vs ~60% do S&P 500, segundo eles).
- Lição: IA como **produto de assinatura** (InvestingPro) e como narrativa de marketing.

### 1.7 Especialistas (referência, conhecimento geral — validar antes de citar em specs)

- **TrendSpider**: detecção automática de linhas de tendência, padrões e níveis no gráfico.
- **Trade Ideas (Holly)**: scanner de sinais por IA que roda estratégias e sugere trades desde ~2016.
- **Danelfin**: score de ações por IA (probabilidade de bater o mercado, 1–10) — "rating objetivo".

## 2. Taxonomia — os 7 usos de IA no setor

| # | Uso | Quem faz | Valor para o usuário | Risco/custo |
|---|---|---|---|---|
| 1 | **Copiloto de gráfico** (padrões, S/R, setups em linguagem natural) | TradingView, TrendSpider | Democratiza análise técnica para iniciantes | Custo por análise; risco de "conselho financeiro" |
| 2 | **Assistente conversacional de pesquisa** | Public Alpha, WarrenAI, Tori, Cortex | Tira dúvidas sem sair da tela | Custo LLM contínuo; alucinação com números |
| 3 | **Digest personalizado** ("o que mexeu com o que você segue e por quê") | Robinhood Cortex | Retenção diária; e-mail/push com propósito | Precisa de notícias/dados + LLM barato |
| 4 | **Sentimento agregado da comunidade** | StockTwits | Transforma posts em indicador | Precisa de volume de conteúdo (efeito de rede) |
| 5 | **Resumo/curadoria de conteúdo da comunidade** | StockTwits (Thematic) | Consumir 1.000 posts em 5 s | Barato (batch); depende de conteúdo existir |
| 6 | **Geração de código/indicadores** | ecossistema Pine Script, Robinhood scans | Cria ferramenta sem programar | Só faz sentido com motor de scripts (não temos) |
| 7 | **Agentes que operam / picks de IA** | eToro Tori agents, ProPicks | "Faça por mim" | ⛔ Envolve execução/recomendação — regulatório pesado |

## 3. Padrões transversais observados

1. **IA é alavanca de monetização**: em todos os casos, o uso pleno é pago (Copilot com limite
   free de 15/dia; Cortex só no Gold; WarrenAI no InvestingPro). O free tem "degustação".
2. **Linguagem natural virou a nova UI**: configurar alerta, fazer screening e pesquisar ativo
   por texto livre em vez de formulários.
3. **Todos guardam o disclaimer**: a IA "explica" e "informa", nunca "recomenda" formalmente
   (exceto quem é corretora regulada e assume esse ônus).
4. **A IA mais defensável usa dados proprietários**: o sentimento do StockTwits e os digests do
   Robinhood só funcionam porque a plataforma tem dados que ninguém mais tem (comunidade,
   portfólio). LLM genérico qualquer um compra; o dado é o fosso.

## 4. Implicações para o nosso produto

### 4.1 Oportunidades alinhadas ao nosso pilar (gráficos + ideias, cripto)

Ordenadas por relação valor/custo, considerando que **nosso dado proprietário são as ideias**:

| Candidata | Descrição | Análogo | Fase sugerida |
|---|---|---|---|
| **F-IA-1: TL;DR de ideia** | Resumo de 2 linhas gerado por IA no topo de cada ideia longa + tradução sob demanda (produto global, conteúdo multilíngue) | StockTwits/Thematic | v1 (barato: 1 chamada por ideia publicada, cacheada) |
| **F-IA-2: Pulso do símbolo** | Na página do símbolo: "o que a comunidade está dizendo" — resumo + sentimento agregado das ideias/direções recentes | StockTwits | v1.x (precisa de volume de ideias) |
| **F-IA-3: Copiloto de gráfico** | Botão "Explain this chart": IA lê OHLCV + indicadores ativos e descreve tendência, S/R e padrões em linguagem simples | TradingView Copilot | v1.x (diferencial forte; custo por uso → limite free) |
| **F-IA-4: Digest do feed** | E-mail/notificação diária: "o que aconteceu com os símbolos e autores que você segue" | Robinhood Cortex | v1.x (junto do digest RN-M5-19) |
| **F-IA-5: Moderação assistida** | IA pré-classifica reports e detecta spam/scam/sinais pagos antes da fila humana | prática de mercado | v1 (barato e protege o único admin — Q-M5-A) |
| **F-IA-6: Alertas em linguagem natural** | "me avisa se BTC cair 5% no dia" → cria a regra de alerta | TradingView | v2 (junto do módulo de alertas) |
| ⛔ Agentes que operam, picks de IA | — | eToro, ProPicks | Nunca (viola CONSTITUTION §2.2, sem dinheiro real) |

### 4.2 Princípios propostos para IA no produto (a validar → virarão regras)

1. **IA explica, não recomenda**: nenhuma feature de IA emite recomendação de compra/venda;
   disclaimers padrão do setor em toda resposta de IA.
2. **IA não publica**: conteúdo gerado por IA nunca se passa por conteúdo de usuário;
   ideias são 100% humanas (protege a moeda da plataforma — reputação).
3. **Dado proprietário primeiro**: priorizar features que usam nossas ideias/comunidade
   (F-IA-1/2/5) sobre as que qualquer concorrente replica com uma chave de API.
4. **Custo controlado**: toda feature de IA nasce com limite por usuário/dia (RT-06) e cache;
   uso pleno é alavanca dos futuros planos pagos.

## 5. Dúvidas geradas por esta investigação

Registradas em [`../01-alinhamento/duvidas-e-decisoes.md`](../01-alinhamento/duvidas-e-decisoes.md):
**N-08** (quais features de IA entram na v1), **T-08** (provedor de LLM e orçamento mensal de API).
