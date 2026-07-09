# M4 — Ideias (o coração social do produto)

**Status**: proposta para validação.
**Depende de**: M1 (autor), M2 (símbolo), M3 (snapshot).
**É dependência de**: M5 (feed, boosts, comentários).

---

## 1. Conceito

Uma **ideia** é uma análise publicada, composta de snapshot do gráfico + tese em texto +
metadados de previsão. É **imutável após publicada** — o histórico público de ideias é o
track record do autor e a moeda de reputação da plataforma (RT-02).

## 2. Composição de uma ideia

| Campo | Obrigatório | Regra |
|---|---|---|
| Autor | ✅ | conta `ACTIVE` (RN-M1-05) |
| Símbolo | ✅ | um único símbolo do catálogo (RN-M2-02) |
| Timeframe | ✅ | herdado do gráfico no momento do snapshot |
| Snapshot | ✅ | imagem congelada (RN-M3-16/17) |
| Título | ✅ | 10–120 caracteres |
| Tese (corpo) | ✅ | 50–10.000 caracteres; texto com formatação básica (negrito, itálico, listas, links `nofollow`) |
| Direção | ✅ | `LONG`, `SHORT` ou `NEUTRAL` (análise educacional sem viés) |
| Tags | opcional | 0–5, de vocabulário livre (lowercase, 2–30 chars) |

- **RN-M4-01**: só contas `ACTIVE` publicam (RN-M1-05).
- **RN-M4-02**: a publicação nasce da tela do gráfico (RN-M3-16) — não existe "criar ideia" sem gráfico.
- **RN-M4-03 — rate limit de publicação**: máximo **5 ideias por dia** e **1 por símbolo por hora**
  por usuário (anti-spam; RT-06).
- **RN-M4-04**: o preço do símbolo no momento da publicação é registrado no metadado da ideia
  (base para métricas futuras de acerto — ver seção 6).

## 3. Imutabilidade e ciclo de vida

```
DRAFT (opcional) → PUBLISHED → (UPDATED com anexos) → ARCHIVED_BY_MODERATION
```

- **RN-M4-05 — imutável**: após publicar, título, tese, snapshot, símbolo, direção e timeframe
  **não podem ser alterados**. Sem exceções.
- **RN-M4-06 — janela de arrependimento**: o autor pode **deletar** a própria ideia apenas nos
  **primeiros 15 minutos** após publicar e somente se ela ainda não tiver boost/comentário de
  terceiros. Depois disso, nunca mais (nem o autor, só moderação).
- **RN-M4-07 — updates**: o autor pode **anexar atualizações** à ideia (texto até 2.000 chars +
  snapshot novo opcional), em ordem cronológica, sem tocar no conteúdo original — padrão
  TradingView ("idea updates"). Máximo 20 updates por ideia.
- **RN-M4-08 — status da tese**: o autor pode marcar a ideia como `TARGET REACHED` ou
  `STOPPED/INVALIDATED` via update estruturado — alimenta o track record e sinaliza aos leitores.
- **RN-M4-09 — remoção por moderação**: ideia removida por violação fica `ARCHIVED_BY_MODERATION`:
  invisível ao público, contabilizada com aviso no perfil ("1 idea removed for guideline violation").
- **RN-M4-10 — rascunhos**: no máximo 5 por usuário; privados; expiram em 30 dias sem edição.

## 4. Exibição e distribuição

- **RN-M4-11 — página da ideia** (`/ideas/{id-slug}`): pública (RT-01); mostra snapshot (com link
  "open live chart" para o gráfico atual do símbolo), tese, direção com selo visual
  (verde LONG / vermelho SHORT / cinza NEUTRAL), autor, data UTC, preço na publicação, updates,
  boosts e comentários.
- **RN-M4-12 — onde a ideia aparece**: perfil do autor (RN-M1-18), página do símbolo (RN-M2-05),
  feed dos seguidores (M5) e listagem global "Latest ideas" (com filtro por símbolo e direção).
- **RN-M4-13 — SEO**: páginas de ideia são indexáveis, com metadados sociais (Open Graph — o
  snapshot é a imagem do card). São a principal porta de aquisição orgânica (persona Visitante).
- **RN-M4-14**: ideias de símbolo `DELISTED` permanecem acessíveis (RN-M2-03), com aviso.

## 5. Fora do escopo deste módulo (v1)

Minds (posts curtos por símbolo — StockTwits-like; candidato forte a v1.x); ideias em vídeo;
co-autoria; ideias privadas/pagas; tradução automática; agendamento de publicação.

## 6. Pontos em aberto

- **Q-M4-A — score de acerto automático**: com direção + preço de publicação registrados (RN-M4-04),
  dá para calcular objetivamente se a ideia "acertou" (ex.: variação após 7/30 dias) e montar um
  ranking de autores. É poderoso, mas sensível (falsa precisão, gaming). **Entra na v1, v1.x ou não entra?**
  *Default proposto: v1 apenas registra os dados (custo zero); exibição de score fica para v1.x com regra própria.*
- **Q-M4-B**: campos estruturados opcionais de trade (entry, target, stop-loss) na publicação?
  TradingView tem via desenho long/short. *Default proposto: v1.x, junto com o score.*
- **Q-M4-C**: idioma do conteúdo é livre (RT-03) — precisamos de filtro "ideas in my language" na
  listagem global? *Default proposto: não na v1.*
