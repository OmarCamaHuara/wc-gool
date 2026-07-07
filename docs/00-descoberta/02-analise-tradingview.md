# Anatomia do TradingView

**Objetivo**: mapear em detalhe o que o TradingView oferece, para que possamos decidir
conscientemente o que entra, o que fica de fora e o que é inviável no nosso produto.

**Fontes**: uso direto da plataforma, [tradingview.com](https://www.tradingview.com/),
[página da rede social](https://www.tradingview.com/social-network/), reviews de mercado
([StockBrokers.com](https://www.stockbrokers.com/review/tools/tradingview),
[strike.money](https://www.strike.money/reviews/tradingview)).

**Escala de referência** (2026): ~100 milhões de usuários registrados, plataforma de gráficos
mais usada do mundo por traders de varejo.

---

## 1. Módulo de Gráficos ("Supercharts")

O coração da plataforma. Tudo o mais orbita ao redor do gráfico.

### 1.1 Funcionalidades principais

- **Tipos de gráfico**: candlestick, barras, linha, área, Heikin Ashi, Renko, Kagi, Point & Figure, etc.
- **Timeframes**: de 1 segundo (planos pagos) até mensal; timeframes customizados.
- **Indicadores**: 400+ nativos (médias móveis, RSI, MACD, Bollinger, VWAP, volume profile...)
  + mais de 100.000 publicados pela comunidade via Pine Script.
- **Ferramentas de desenho**: linhas de tendência, Fibonacci, ondas de Elliott, retângulos,
  anotações de texto, posições long/short (com cálculo de risco/retorno).
- **Multi-chart layout**: até 16 gráficos sincronizados na mesma tela (por plano).
- **Comparação de símbolos**: sobrepor ativos diferentes no mesmo gráfico.
- **Replay de mercado**: "voltar no tempo" e reproduzir o candle a candle para treinar leitura.
- **Templates**: salvar combinações de indicadores/estilos.

### 1.2 O que isso implica para nós

Construir um motor de charting do zero é um projeto de anos. **A boa notícia**: o próprio
TradingView mantém a [Lightweight Charts](https://github.com/tradingview/lightweight-charts)
(open source, Apache 2.0) e licencia gratuitamente a **Charting Library** completa
(mediante aprovação de cadastro). Detalhes em
[`04-consideracoes-tecnicas.md`](04-consideracoes-tecnicas.md).

---

## 2. Pine Script (indicadores e estratégias customizadas)

- Linguagem de programação proprietária, simples, executada nos servidores do TradingView.
- Usuários criam indicadores e estratégias, publicam como código aberto, protegido ou invite-only.
- Existe um **marketplace informal**: autores de scripts invite-only vendem acesso por fora.
- É o maior gerador de efeito de rede da plataforma: os 100k+ scripts comunitários são conteúdo
  que nenhum concorrente consegue copiar.

**Implicação**: replicar Pine Script é inviável para um MVP (é literalmente criar uma linguagem +
sandbox de execução). Alternativas de longo prazo: permitir fórmulas simples, ou nada no MVP.

## 3. Dados de mercado

- Cobertura: ações (dezenas de bolsas globais, incluindo B3), cripto (todas as grandes exchanges),
  forex, futuros, índices, bonds, fundos.
- **Modelo de dados**: dados com atraso (delayed, 15 min) grátis; dados em tempo real de cada bolsa
  são **comprados à parte** pelo usuário (ex.: NYSE real-time custa X USD/mês) — porque as bolsas
  cobram royalties por usuário. Cripto e forex são tempo real de graça (exchanges não cobram).
- Notícias integradas (Reuters, Dow Jones, etc.) e **calendário econômico**.

**Implicação**: dados de mercado são O maior custo/complexidade de um clone. A rota barata é
começar por **cripto** (APIs públicas e gratuitas de exchanges como a Binance, com WebSocket
em tempo real e sem royalties).

## 4. Rede social

### 4.1 Ideias (Ideas)
- Publicação central da plataforma: um **snapshot do gráfico anotado** + texto com a tese
  (análise, previsão) + direção (long/short) + tags.
- A ideia fica ligada ao símbolo e ao timeframe; aparece no perfil do autor, na página do ativo
  e no feed dos seguidores.
- Interações: boost (like), comentários, compartilhar. As ideias não podem ser editadas depois
  de publicadas (accountability: previsão fica registrada).
- Depois que o tempo passa, qualquer um pode ver se a previsão acertou — isso cria **reputação**.

### 4.2 Minds
- Feed curto estilo Twitter **por símbolo**: posts rápidos de sentimento/notícia sobre um ativo.
  (Muito parecido com o StockTwits.)

### 4.3 Streams
- Transmissões ao vivo (vídeo) de traders analisando mercado.

### 4.4 Mecânicas sociais
- Perfis públicos com histórico de ideias/scripts, seguidores, reputação por pontos.
- Follows (usuários, símbolos e ideias), notificações.
- Moderação forte: regras rígidas contra spam/promessa de lucro/venda de sinais fora das regras.

## 5. Ferramentas de produtividade

- **Watchlists**: listas de símbolos com cotação em tempo real, organizáveis, com notas.
- **Alertas**: por preço, cruzamento de indicador, desenho no gráfico ou condição de script;
  entregues via push, e-mail, webhook (planos pagos), pop-up. Limite por plano.
- **Screeners**: ações, forex e cripto — filtros por dezenas de métricas técnicas e fundamentalistas.
- **Calendário econômico e de earnings.**
- **Paper trading**: conta de simulação com saldo virtual (USD 100.000) operada direto do gráfico.

## 6. Integração com corretoras (trading real)

- O usuário conecta a conta de uma corretora parceira (dezenas: OANDA, Interactive Brokers,
  FxPro, corretoras cripto...) e envia ordens **de dentro do gráfico**.
- O TradingView não toca no dinheiro: é uma interface; a execução/custódia é da corretora.
- Receita: acordos de revenue share/referral com as corretoras.

## 7. Modelo de negócio

| Fonte de receita | Descrição |
|---|---|
| **Assinaturas** (principal) | Planos Free → Essential → Plus → Premium → Ultimate (+ planos institucionais). Free tem ads, 1 indicador extra por gráfico, poucos alertas; pagos liberam mais gráficos por layout, mais alertas, timeframes menores, sem ads |
| **Venda de dados real-time** | Repasse das taxas das bolsas + margem |
| **Parcerias com corretoras** | Referral/revenue share por usuário que opera via plataforma |
| **Ads** | Somente no plano Free |
| **Marketplace/streams** | Monetização de criadores (mais recente) |

## 8. Resumo — por que o TradingView vence

1. **Melhor gráfico do mercado** — atrai o usuário.
2. **Efeito de rede do conteúdo** — 100k+ scripts e milhões de ideias publicadas o retêm.
3. **Freemium generoso** — o plano grátis é genuinamente útil; a conversão vem de limites.
4. **Neutralidade** — não é corretora, então TODAS as corretoras podem ser parceiras.
