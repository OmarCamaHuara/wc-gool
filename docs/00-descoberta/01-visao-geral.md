# Visão Geral do Projeto

**Status**: rascunho de descoberta — sujeito a mudança após respostas do documento de dúvidas.
**Data**: 2026-07-07

## 1. A ideia em uma frase

Criar uma plataforma web inspirada no [TradingView](https://es.tradingview.com/): uma combinação de
**ferramenta de análise de mercados financeiros** (gráficos, indicadores, screeners, alertas) com uma
**rede social de traders** (publicação de ideias/análises, follows, comentários, reputação).

## 2. O que o TradingView É — e o que ele NÃO é

Entender isso é essencial para definir nosso escopo:

| O TradingView É | O TradingView NÃO é |
|---|---|
| Plataforma de **gráficos e análise técnica** (o melhor do mercado) | Uma corretora — ele não custodia dinheiro nem executa ordens por conta própria |
| **Rede social de conteúdo** (ideias, minds, streams) | Uma plataforma de **copy trading** automático (isso é eToro/ZuluTrade) |
| **Hub de dados** de mercado (ações, cripto, forex, futuros, bonds) | Um robô de trading / plataforma de sinais pagos |
| Camada de **integração com corretoras** (você opera via broker parceiro dentro do gráfico) | Um portal de notícias (tem notícias, mas é secundário) |

Essa distinção importa muito por causa de **regulação**: enquanto a plataforma não executa ordens
nem movimenta dinheiro dos usuários, ela é "só software + mídia social" — sem necessidade de licença
de corretora (CVM/SEC/etc.). No momento em que entra execução ou copy trading com dinheiro real,
o projeto muda completamente de categoria legal.

## 3. Pilares funcionais de uma plataforma tipo TradingView

Qualquer recorte de MVP vai escolher um subconjunto destes pilares:

1. **Dados de mercado** — ingestão de cotações (tempo real ou com atraso) e histórico OHLCV
2. **Gráficos (charting)** — candlesticks, timeframes, desenhos, indicadores técnicos
3. **Social** — perfis, ideias publicadas (gráfico anotado + tese), follows, likes, comentários, feed
4. **Watchlists** — listas de ativos acompanhados pelo usuário
5. **Alertas** — regras de preço/indicador que disparam notificações
6. **Screeners** — filtros para descobrir ativos por critérios (preço, volume, indicadores)
7. **Scripts/indicadores customizados** — no TradingView, o Pine Script (pilar MUITO caro de replicar)
8. **Paper trading** — simulação de operações com dinheiro virtual
9. **Integração com corretoras** — execução real via parceiros (pilar regulatório/comercialmente pesado)
10. **Monetização** — planos de assinatura, ads, marketplace

Ver detalhamento de cada pilar em [`02-analise-tradingview.md`](02-analise-tradingview.md).

## 4. Restrições e definições já estabelecidas

- **Backend**: Java
- **Frontend**: React
- **Este repositório**: somente documentação. O código será escrito depois, seguindo milestones
  quebrados em micro-tarefas executáveis por LLM.
- **Metodologia de documentação**: seguir a guia do repositório `OmarCamaHuara/hiria_pro`
  (acesso pendente — dúvida P-01).

## 5. O que ainda NÃO está definido

Tudo o mais — em especial: mercados cobertos, público-alvo, escopo do MVP, modelo de negócio,
orçamento para dados de mercado e infraestrutura. Ver
[`../01-alinhamento/duvidas-e-decisoes.md`](../01-alinhamento/duvidas-e-decisoes.md).
