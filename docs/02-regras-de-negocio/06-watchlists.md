# M6 — Watchlists

**Status**: proposta para validação.
**Depende de**: M1 (usuário), M2 (símbolos e cotações).

---

## 1. Conceito

Lista pessoal de símbolos que o usuário acompanha, com cotação ao vivo. É a "home privada"
do trader e a principal razão de retorno diário junto com o feed.

## 2. Regras

- **RN-M6-01**: todo usuário nasce com uma watchlist padrão ("My Watchlist"), não deletável,
  criada no primeiro login com 3 símbolos populares pré-carregados (ex.: BTC, ETH, SOL) —
  elimina tela vazia.
- **RN-M6-02 — limites** (RT-06): até **5 watchlists** por usuário, até **50 símbolos** por lista.
- **RN-M6-03**: watchlists têm nome (1–40 chars) e são **privadas** na v1 (compartilhável é v1.x).
- **RN-M6-04**: um símbolo pode estar em várias listas; adicionar duplicado na mesma lista é no-op.
- **RN-M6-05 — conteúdo da linha**: símbolo, logo, último preço (tempo real, RN-M2-06),
  variação 24 h (% com cor), volume 24 h e mini-sparkline (últimas 24 h). Clique → página do símbolo.
- **RN-M6-06 — ordenação**: manual (drag and drop, ordem persistida) por padrão; ordenação
  transitória por coluna (preço, variação, volume) sem sobrescrever a ordem manual.
- **RN-M6-07**: adicionar/remover símbolo disponível em: página da watchlist (busca RN-M2-04),
  página do símbolo (botão estrela) e gráfico (mesma estrela na topbar).
- **RN-M6-08**: exige conta `ACTIVE`? Não — `UNVERIFIED` **pode** usar watchlist (é privado,
  sem risco de spam; reduz fricção pré-verificação). Anônimo não pode (RT-01).
- **RN-M6-09**: símbolo `DELISTED` (RN-M2-03) permanece na lista com selo "delisted" e último
  preço congelado; usuário pode remover.
- **RN-M6-10**: renomear e deletar listas é livre (exceto a padrão, RN-M6-01); deletar pede
  confirmação e não tem lixeira.

## 3. Fora do escopo (v1)

Watchlists públicas/compartilhadas; colunas configuráveis; notas por símbolo; seções/headers
dentro da lista; importar/exportar; alertas a partir da watchlist (v1.1 junto com M-alertas).

## 4. Pontos em aberto

- **Q-M6-A**: a watchlist padrão pré-carregada com BTC/ETH/SOL confirma? (Alternativa: vazia com CTA.)
