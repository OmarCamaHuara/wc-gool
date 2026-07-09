# Escopo do MVP

**Base**: decisões D-004 (pilar = gráficos + ideias), D-005 (só cripto), D-006 (global/inglês).
**Status**: proposta para validação do Omar. Vira contrato de escopo quando aprovada.

---

## 1. Definição do produto (v1)

> Uma plataforma web **em inglês** onde qualquer pessoa acompanha o mercado de **criptomoedas**
> em gráficos profissionais em **tempo real** e publica/consome **ideias de trade**
> (análises com gráfico anotado), construindo reputação pública pelo histórico de acertos.

O loop central do produto (o que faz o usuário voltar todo dia):

```
ver gráfico → montar análise → publicar ideia → receber boosts/comentários/seguidores
     ▲                                                        │
     └────────── acompanhar ideias de quem segue ◄────────────┘
```

## 2. Módulos do MVP (dentro do escopo)

| # | Módulo | Documento de regras | Resumo |
|---|---|---|---|
| M1 | Usuários e perfis | [`01-usuarios-e-perfis.md`](01-usuarios-e-perfis.md) | Cadastro, login, perfil público, configurações |
| M2 | Dados de mercado | [`02-dados-de-mercado.md`](02-dados-de-mercado.md) | Catálogo de símbolos cripto, ingestão de ticks, candles históricos |
| M3 | Gráficos | [`03-graficos.md`](03-graficos.md) | Chart de candles em tempo real, timeframes, indicadores básicos, desenhos |
| M4 | Ideias | [`04-ideias.md`](04-ideias.md) | Publicação de análises (snapshot + tese + direção), ciclo de vida, accountability |
| M5 | Social e feed | [`05-social-feed.md`](05-social-feed.md) | Follows, boosts, comentários, feed, notificações, moderação mínima |
| M6 | Watchlists | [`06-watchlists.md`](06-watchlists.md) | Listas de símbolos com cotação ao vivo |

## 3. Fora do escopo da v1 (explícito, para evitar scope creep)

| Funcionalidade | Quando entra | Motivo do corte |
|---|---|---|
| Alertas de preço | v1.1 (primeiro incremento pós-MVP) | Valioso, mas não é o loop central |
| Screener | v2 | Exige universo de métricas calculadas |
| Paper trading + ranking | v2 | Pilar próprio; MVP prova o loop de ideias primeiro |
| Scripts/indicadores customizados (tipo Pine) | sem previsão | Custo altíssimo (linguagem + sandbox) |
| Streams/vídeo, chat em tempo real | sem previsão | Custo de infra e moderação |
| Ações, forex, futuros, B3 | v2+ | D-005: cripto primeiro; delayed depois |
| Integração com corretoras / execução | sem previsão | Regulatório; ver análise de concorrentes |
| App mobile nativo | v2+ | Web responsivo primeiro (T-06) |
| Monetização/planos pagos | decidir em N-05 | MVP grátis; regras já preveem limites por usuário |
| i18n PT/ES | v1.x | D-006: inglês primeiro; textos centralizados desde o início para facilitar |

## 4. Personas de referência

1. **Alex, o analista** (produtor): faz análise técnica de cripto por hobby/semi-pro, hoje posta
   prints no X/Discord. Quer audiência e reputação verificável. Publica 3–5 ideias/semana.
2. **Sam, o seguidor** (consumidor): opera pouco, quer aprender e acompanhar analistas bons.
   Lê o feed diariamente, raramente publica. É a maioria dos usuários (~90%).
3. **Visitante anônimo** (SEO): chega do Google numa ideia ou página de símbolo. Precisa ver
   conteúdo sem login (aquisição), com chamadas para se cadastrar.

## 5. Regras transversais do produto

- **RT-01 — Leitura pública**: gráficos, páginas de símbolo, ideias e perfis são visíveis sem login.
  Criar/interagir (publicar, boost, comentar, seguir, watchlist) exige conta.
- **RT-02 — Accountability**: uma ideia publicada **nunca pode ser editada nem apagada
  silenciosamente** (regra detalhada em M4). É a base da reputação.
- **RT-03 — Idioma**: toda a UI e validações em inglês (EN-US). Conteúdo de usuário em qualquer idioma.
- **RT-04 — Tempo**: toda data/hora armazenada e trafegada em UTC; exibição no fuso do navegador.
- **RT-05 — Identificadores**: usuários têm `username` único e imutável após criação (regra em M1);
  símbolos usam o padrão `EXCHANGE:PAIR` (ex.: `BINANCE:BTCUSDT`) (regra em M2).
- **RT-06 — Limites free**: todo recurso criado por usuário tem limite explícito (ver módulo);
  os limites são as futuras alavancas de monetização.
- **RT-07 — Temas**: a UI oferece **tema claro e tema escuro desde a v1** (ADR-009); escuro é o
  padrão. Preferência persistida por usuário (localStorage para anônimos). Todo componente novo
  deve ser homologado nos dois temas.

## 6. Métricas de sucesso do MVP (proposta)

| Métrica | Meta inicial |
|---|---|
| Usuários registrados | validar aquisição — sem meta numérica; medir |
| Ideias publicadas/semana | ≥ 20 orgânicas após 1º mês de divulgação |
| Retenção D7 de produtores | ≥ 25% |
| Tempo até primeiro candle na tela (visitante) | < 2 s |
