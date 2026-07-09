# M3 — Gráficos

**Status**: proposta para validação.
**Depende de**: M2 (dados de mercado).
**É dependência de**: M4 (ideias — snapshot do gráfico).
**Base técnica presumida**: TradingView Lightweight Charts (T-03) — as regras abaixo respeitam
o que essa biblioteca oferece de fábrica, marcando o que exigiria implementação própria.

---

## 1. Princípio do módulo

O gráfico é a **home do produto** e o palco onde as ideias nascem. Na v1 ele deve ser
**rápido, fluido e confiável** — não completo. Profundidade de ferramenta (dezenas de indicadores,
desenhos avançados) vem depois do loop social validado.

## 2. Exibição básica

- **RN-M3-01 — tipos de série v1**: candlestick (padrão), linha e área. Nada mais.
- **RN-M3-02 — timeframes**: os do M2 (`1m, 5m, 15m, 1h, 4h, 1D, 1W`), trocáveis por toolbar;
  o timeframe escolhido persiste por usuário (e por sessão anônima via localStorage).
- **RN-M3-03 — tempo real**: o último candle atualiza a cada tick (RN-M2-12) sem re-render
  perceptível; preço atual destacado na escala com a cor de variação (verde/vermelho).
- **RN-M3-04 — navegação**: pan e zoom fluidos; **scroll infinito para o passado** — ao chegar
  perto da borda esquerda, carrega mais histórico (paginado) até o limite do RN-M2-11.
- **RN-M3-05 — crosshair + OHLCV legend**: ao passar o mouse, exibir OHLCV e variação do candle
  sob o cursor.
- **RN-M3-06 — volume**: histograma de volume opcional (ligado por padrão) no painel inferior.
- **RN-M3-07 — performance**: primeiro candle visível em < 2 s (métrica do MVP); interação
  (pan/zoom) a 60 fps com 5.000 candles carregados.

## 3. Indicadores técnicos (v1: conjunto mínimo)

- **RN-M3-08 — indicadores v1**: SMA, EMA, Bollinger Bands (overlay); RSI, MACD, Volume (painéis).
  **Seis, e só.** Cada um com parâmetros configuráveis (períodos, fonte) e valores padrão de mercado.
- **RN-M3-09**: máximo de **3 indicadores simultâneos** por gráfico na v1 (limite de UX e RT-06).
- **RN-M3-10**: os indicadores são calculados de forma consistente com as referências de mercado
  (validar resultados contra o TradingView na homologação).
- **RN-M3-11**: a configuração de indicadores do usuário persiste por símbolo+usuário.

## 4. Ferramentas de desenho (v1: conjunto mínimo)

> Atenção: Lightweight Charts **não traz desenhos prontos** — isto é implementação própria
> (custo alto). Por isso o conjunto é mínimo e negociável.

- **RN-M3-12 — desenhos v1**: linha de tendência, linha horizontal, retângulo e texto. Quatro, e só.
- **RN-M3-13**: desenhos são salvos automaticamente por **símbolo+usuário** e reaparecem quando o
  usuário reabre o símbolo (em qualquer timeframe, ancorados a tempo+preço).
- **RN-M3-14**: limite de 50 objetos de desenho por símbolo por usuário (RT-06).
- **RN-M3-15**: usuário anônimo pode desenhar (fica em localStorage), mas perde ao trocar de
  dispositivo — incentivo a criar conta ("Sign up to save your drawings").

## 5. Snapshot (ponte para o módulo de Ideias)

- **RN-M3-16**: o botão **"Publish idea"** no gráfico captura um **snapshot estático** (imagem)
  do estado atual: candles visíveis, indicadores e desenhos, com marca d'água do produto +
  símbolo + timeframe + timestamp UTC.
- **RN-M3-17**: o snapshot é gerado no cliente (canvas → imagem) e congelado — nunca re-renderizado
  com dados posteriores (RT-02: a ideia mostra o que o autor via no momento).

## 6. Fora do escopo deste módulo (v1)

Multi-chart layouts; comparação de símbolos; replay de mercado; templates de indicadores;
timeframes por segundos/custom; Heikin Ashi/Renko/etc.; customização de cores por elemento
do gráfico; exportar dados.

- **RN-M3-18 — temas**: o gráfico respeita o tema global claro/escuro da plataforma (RT-07),
  com paletas próprias para cada tema (candles, grid, escalas); escuro é o padrão.

## 7. Pontos em aberto

- **Q-M3-A ✅** (2026-07-09, ADR-009): **tema claro + escuro desde a v1** — ver RT-07 e RN-M3-18.
- **Q-M3-B ✅** (2026-07-09, ADR-009): **seguir com Lightweight Charts sem esperar** a resposta da
  licença da Charting Library; se aprovada depois, reavaliamos o M3 por ADR.
