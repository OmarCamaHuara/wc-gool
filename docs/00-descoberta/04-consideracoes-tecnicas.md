# Considerações Técnicas — Java + React no Domínio de Trading

**Objetivo**: mapear os desafios técnicos ANTES de decidir escopo, para que as decisões de
produto sejam tomadas sabendo o custo de cada pilar. Nada aqui é decisão final de arquitetura —
isso virá na Fase 2, depois do alinhamento.

**Stack fixada pelo Omar**: Java (backend) + React (frontend).

---

## 1. Os quatro problemas difíceis do domínio

Numa plataforma tipo TradingView, 80% da complexidade está em quatro lugares:

| # | Problema | Por que é difícil | Grau |
|---|---|---|---|
| 1 | **Obter dados de mercado** | Custo, licenciamento, rate limits, cobertura | 🔴 crítico |
| 2 | **Distribuir cotações em tempo real** | Milhares de conexões WebSocket, fan-out por símbolo | 🟠 alto |
| 3 | **Armazenar/servir séries temporais** | Bilhões de candles, agregações por timeframe, queries rápidas | 🟠 alto |
| 4 | **Renderizar gráficos profissionais** | Anos de trabalho se feito do zero | 🔴 crítico (mas resolvível com biblioteca pronta) |

O resto (perfis, feed, comentários, watchlists, autenticação) é desenvolvimento web convencional.

## 2. Dados de mercado — opções e custos

### 2.1 Por classe de ativo

| Classe | Fontes | Tempo real? | Custo | Observação |
|---|---|---|---|---|
| **Cripto** | APIs públicas de exchanges (Binance, Coinbase, Kraken); agregadores (CoinGecko) | ✅ WebSocket grátis | **Grátis** | Sem royalties de bolsa. Melhor porta de entrada |
| **Ações US** | Polygon.io, Finnhub, Twelve Data, Alpha Vantage, Alpaca | Delayed grátis/barato; real-time pago | USD 0–200+/mês por provedor (uso pessoal); exibição pública real-time exige licença de bolsa (caro) | Delayed 15 min é o padrão viável |
| **Ações B3 (Brasil)** | B3 UP2DATA, Cedro, MetaTrader brokers, brapi.dev | Real-time é licenciado | brapi tem plano grátis (delayed) | Cobertura BR é nicho mal servido — possível diferencial |
| **Forex** | Twelve Data, Polygon, OANDA API | ✅ geralmente incluído | Baixo | Sem bolsa central, sem royalties |

### 2.2 Regra de ouro do licenciamento

Bolsas (NYSE, Nasdaq, B3...) cobram **royalties por usuário final** para exibição de dados em
tempo real. Por isso o TradingView vende real-time por bolsa separadamente. Um MVP deve usar:
**cripto real-time (grátis) + demais mercados delayed (grátis/barato)** — exatamente o modelo
free do TradingView.

## 3. Gráficos no frontend (React)

| Opção | Licença | Prós | Contras |
|---|---|---|---|
| **TradingView Lightweight Charts** | Apache 2.0 (open source) | Qualidade TradingView, 45KB, candles/linhas/áreas, séries em tempo real | Sem desenhos prontos (trendlines etc. teríamos que implementar por cima), sem indicadores embutidos |
| **TradingView Charting Library** | Grátis mediante aprovação de cadastro; código fechado | O gráfico COMPLETO do TradingView (desenhos, indicadores, UI) | Aprovação necessária; exige backend de dados no formato UDF/Datafeed deles; termos de uso restritos |
| Highcharts Stock | Comercial (paga) | Maduro, suporte | Custo de licença, visual menos "trading" |
| Apache ECharts | Apache 2.0 | Grátis, flexível | Muito trabalho para chegar em UX de trading |

**Leitura preliminar**: Lightweight Charts para MVP; tentar aprovação da Charting Library em paralelo.
Os indicadores técnicos (SMA, RSI, MACD...) seriam calculados por nós — backend (Java, com a lib
`ta4j`) ou frontend — decisão da Fase 2.

## 4. Backend Java — mapa preliminar de tecnologias

Nada disso é decisão fechada; é o cardápio natural do ecossistema:

- **Framework**: Spring Boot 3.x (Java 21 LTS). Para os fluxos de tempo real, WebFlux (reativo)
  ou WebSocket clássico com STOMP.
- **Ingestão de cotações**: serviço conectado aos WebSockets dos provedores → normaliza →
  publica em um barramento interno (Redis Pub/Sub no início; Kafka se escalar).
- **Distribuição**: gateway WebSocket com assinatura por símbolo (usuário assina `BTCUSDT`,
  recebe só os ticks daquele símbolo).
- **Séries temporais**: PostgreSQL + **TimescaleDB** (candles OHLCV por timeframe, com
  agregação contínua) — mantém tudo num Postgres só, que também serve os dados sociais.
  Alternativas: QuestDB, InfluxDB.
- **Dados sociais/relacionais**: PostgreSQL puro (usuários, ideias, comentários, follows, watchlists).
- **Cache/tempo real auxiliar**: Redis (último preço por símbolo, sessões, rate limiting).
- **Alertas**: motor que avalia regras contra o stream de ticks (job dedicado consumindo o barramento).
- **Indicadores técnicos**: biblioteca `ta4j` (open source, Java) cobre as dezenas de indicadores clássicos.
- **Autenticação**: Spring Security + JWT; OAuth2 social login (Google etc.).

## 5. Frontend React — mapa preliminar

- React 18+ + TypeScript + Vite.
- Gráficos: Lightweight Charts (wrapper React).
- Estado/HTTP: TanStack Query + WebSocket client para cotações/notificações.
- UI: a decidir (Tailwind, MUI...) — decisão da Fase 2.
- Editor das ideias: editor rich-text (ex.: TipTap) + snapshot do gráfico como imagem.

## 6. Custos de infraestrutura (ordem de grandeza, MVP)

| Item | Estimativa/mês |
|---|---|
| VPS/cloud (app + banco, começo) | USD 20–80 |
| Dados de mercado (só cripto) | USD 0 |
| Dados ações delayed (opcional) | USD 0–50 |
| E-mail transacional, domínio, CDN | USD 5–20 |
| **Total MVP cripto-first** | **~USD 25–150/mês** |

## 7. Complexidade relativa dos pilares (para calibrar o MVP)

Estimativa qualitativa de esforço para versão mínima digna de cada pilar:

| Pilar | Esforço | Dependências |
|---|---|---|
| Autenticação + perfis | 🟢 baixo | — |
| Watchlists | 🟢 baixo | dados de mercado |
| Ideias + feed + comentários + follows | 🟡 médio | perfis, snapshot de gráfico |
| Gráfico com dados em tempo real (cripto) | 🟡 médio | ingestão + Lightweight Charts |
| Candles históricos multi-timeframe | 🟡 médio | TimescaleDB + backfill |
| Alertas de preço | 🟡 médio | stream de ticks + notificações |
| Screener | 🟠 alto | universo de ativos + métricas calculadas |
| Paper trading + ranking | 🟠 alto | stream de preços, matching virtual |
| Indicadores customizados (tipo Pine) | 🔴 muito alto | linguagem + sandbox |
| Integração com corretoras | 🔴 muito alto | parcerias, APIs de broker, compliance |
| Copy trading real | ⛔ fora de alcance de MVP | licença regulatória |

## 8. Riscos técnicos a validar cedo

1. **Rate limits dos provedores gratuitos** — quantos símbolos conseguimos assinar de graça na prática.
2. **Aprovação da Charting Library** do TradingView (se quisermos desenhos/indicadores prontos).
3. **Custo de manter histórico OHLCV** — backfill de anos de candles de centenas de símbolos.
4. **Snapshot de gráfico para as ideias** — gerar imagem do estado do gráfico (client-side canvas export resolve).
