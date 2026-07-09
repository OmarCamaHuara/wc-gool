# M2 — Dados de Mercado (Cripto)

**Status**: proposta para validação.
**Depende de**: — (módulo base de dados).
**É dependência de**: M3 (gráficos), M4 (ideias), M6 (watchlists).
**Base**: D-005 (só cripto na v1), T-04 (Binance como fonte primária).

---

## 1. Conceitos

| Conceito | Definição |
|---|---|
| **Símbolo** | Um par negociável identificado como `EXCHANGE:PAIR` (ex.: `BINANCE:BTCUSDT`) |
| **Tick** | Última negociação/preço de um símbolo (preço, quantidade, timestamp) |
| **Candle (OHLCV)** | Agregação de ticks num intervalo: open, high, low, close, volume |
| **Timeframe** | Duração do candle: `1m, 5m, 15m, 1h, 4h, 1D, 1W` (conjunto da v1) |
| **Ticker 24h** | Resumo do símbolo: último preço, variação 24 h (abs e %), máx/mín 24 h, volume 24 h |

## 2. Catálogo de símbolos

- **RN-M2-01 — universo v1**: pares **spot da Binance com quote USDT**, filtrados pelos
  **top ~200 por volume**, revisados periodicamente. Começar controlado; ampliar é fácil,
  encolher (quebrando ideias/watchlists) é traumático.
- **RN-M2-02**: cada símbolo tem: código (`BINANCE:BTCUSDT`), base asset (`BTC`), quote (`USDT`),
  nome de exibição (`Bitcoin / TetherUS`), logo do ativo, precisão de preço (casas decimais),
  status (`ACTIVE`/`DELISTED`).
- **RN-M2-03 — delistagem**: símbolo removido da exchange vira `DELISTED`: sai de buscas e do
  screener futuro, **mas permanece resolvível** — ideias e watchlists antigas continuam
  renderizando o histórico congelado (RT-02).
- **RN-M2-04 — busca de símbolos**: por código, base asset ou nome (`btc`, `bitcoin`);
  ordenação por volume 24 h; usada na topbar e em "add to watchlist".
- **RN-M2-05 — página do símbolo** (`/symbol/BINANCE:BTCUSDT`): pública (RT-01); mostra ticker 24 h,
  gráfico (M3) e as ideias publicadas para o símbolo (M4).

## 3. Dados em tempo real

- **RN-M2-06**: o preço exibido é **tempo real** (sem delay) — é o diferencial de cripto e do produto.
- **RN-M2-07 — freshness**: um tick deve chegar ao navegador em **< 2 s** da sua ocorrência na
  exchange (p95). Acima disso, degradação visível (ver RN-M2-08).
- **RN-M2-08 — indicador de conexão**: a UI sempre expõe o estado do stream: `LIVE` (verde),
  `RECONNECTING` (amarelo, dados possivelmente atrasados), `OFFLINE` (vermelho, último preço com
  timestamp "as of HH:MM:SS"). Nunca mostrar preço congelado como se fosse ao vivo.
- **RN-M2-09**: a plataforma assina na fonte **apenas os símbolos que algum cliente conectado
  está observando** + os do catálogo top N necessários para tickers agregados (otimização de rate limit).

## 4. Dados históricos (candles)

- **RN-M2-10 — timeframes v1**: `1m, 5m, 15m, 1h, 4h, 1D, 1W`. Todos derivados/backfillados
  a partir da fonte; timeframes maiores agregados a partir do `1m`.
- **RN-M2-11 — profundidade de histórico**: mínimo de **2 anos** de candles (ou desde a listagem
  do par, o que for menor) para timeframes ≥ 1h; **90 dias** para `1m/5m/15m`.
- **RN-M2-12 — candle em formação**: o candle do intervalo corrente atualiza em tempo real a cada
  tick e "fecha" na virada do intervalo; após fechar, é imutável.
- **RN-M2-13 — lacunas (gaps)**: se a ingestão cair, o sistema faz **backfill automático** dos
  candles perdidos ao reconectar (via REST da fonte). Consistência histórica > tempo real.
- **RN-M2-14 — auditoria de qualidade**: job periódico compara amostras de candles locais com a
  fonte; divergência > 0,1% em close/volume gera correção + log interno.

## 5. Fonte de dados e resiliência

- **RN-M2-15**: fonte primária v1: **Binance** (WebSocket para ticks/klines; REST para backfill).
  A arquitetura deve tratar "fonte" como plugável (v2 adiciona outras exchanges/classes — D-005).
- **RN-M2-16**: respeitar os termos de uso e rate limits da fonte; validar (risco técnico nº 1 do
  doc de considerações) que o plano gratuito sustenta o catálogo v1 ANTES de fechar a spec técnica.
- **RN-M2-17**: indisponibilidade da fonte não pode derrubar a plataforma: gráficos servem o
  histórico já armazenado + estado `OFFLINE` (RN-M2-08).

## 6. Fora do escopo deste módulo (v1)

Order book / depth; trades tape detalhado; múltiplas exchanges; pares não-USDT; dados
fundamentalistas de cripto (market cap, supply — avaliar CoinGecko na v1.x para enriquecer a
página do símbolo); notícias; calendário.

## 7. Pontos em aberto

- **Q-M2-A ✅** (2026-07-09, ADR-009): confirmado **top ~200 por volume**.
- **Q-M2-B ✅** (2026-07-09, ADR-009): confirmado **tudo em USDT na v1**, sem conversão de moeda
  (conversão de preferência do usuário fica para v1.x).
