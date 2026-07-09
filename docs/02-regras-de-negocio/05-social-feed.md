# M5 — Social: Follows, Boosts, Comentários, Feed, Notificações e Moderação

**Status**: proposta para validação.
**Depende de**: M1 (usuários), M4 (ideias).

---

## 1. Follows

- **RN-M5-01**: usuário `ACTIVE` pode seguir **usuários** e **símbolos**. Seguir é unilateral
  (modelo Twitter, não Facebook); sem aprovação.
- **RN-M5-02**: não pode seguir a si mesmo; deixar de seguir é livre e silencioso (não notifica).
- **RN-M5-03 — limites** (RT-06): até 2.000 usuários e 200 símbolos seguidos por conta.
- **RN-M5-04**: listas de seguidores/seguindo são públicas no perfil (RN-M1-18).

## 2. Boosts (o "like")

- **RN-M5-05**: boost é aplicável a **ideias** (não a comentários na v1); 1 por usuário por ideia;
  reversível (des-boost).
- **RN-M5-06**: contagem pública na ideia; soma total no perfil do autor (RN-M1-17).
- **RN-M5-07**: o autor não pode dar boost na própria ideia.

## 3. Comentários

- **RN-M5-08**: comentários em ideias; texto simples com links (`nofollow`), 1–2.000 caracteres.
- **RN-M5-09 — aninhamento**: 1 nível de resposta apenas (comentário → respostas; sem árvores infinitas).
- **RN-M5-10**: autor do comentário pode **editar por 5 minutos** (marcado "edited") e **apagar a
  qualquer momento** → placeholder "[comment deleted]" se tiver respostas; some se não tiver.
  (Comentário não é previsão — a imutabilidade de RT-02 não se aplica aqui.)
- **RN-M5-11 — rate limit**: máx. 30 comentários/hora por usuário; mínimo 10 s entre comentários.
- **RN-M5-12**: o autor da ideia pode **fixar** 1 comentário e **ocultar** comentários na própria
  ideia (ocultos ficam atrás de "show hidden comments" — transparência contra censura silenciosa).

## 4. Feed

- **RN-M5-13 — feed do usuário logado** (home): ideias de **usuários seguidos** + ideias novas de
  **símbolos seguidos**, em ordem **cronológica inversa** simples. Sem algoritmo de relevância na v1
  (previsibilidade > engajamento, e custo menor).
- **RN-M5-14 — feed vazio (cold start)**: usuário novo sem follows vê "Latest ideas" global +
  sugestão de autores/símbolos populares (top por boosts/volume nos últimos 7 dias).
- **RN-M5-15 — visitante anônimo**: home pública mostra "Latest ideas" + tickers dos top símbolos
  (aquisição, RT-01).
- **RN-M5-16**: paginação infinita; itens novos entram por "new ideas" pill (sem reordenar a tela
  sob o usuário).

## 5. Notificações

- **RN-M5-17 — eventos que notificam** (v1): novo seguidor; boost na sua ideia (agregado:
  "X and 12 others boosted..."); comentário na sua ideia; resposta ao seu comentário; nova ideia
  de usuário que você segue.
- **RN-M5-18 — canais**: central de notificações in-app (sino) + e-mail. Cada evento tem toggle
  de e-mail nas configurações (RN-M1-21); in-app não é desligável.
- **RN-M5-19 — digest**: e-mails de boost/comentário são agregados (máx. 1 e-mail/h por tipo);
  "nova ideia de quem sigo" é digest diário opcional, nunca imediato.
- **RN-M5-20**: notificações expiram/param de ser exibidas após 90 dias.

## 6. Moderação e denúncias (mínimo viável)

- **RN-M5-21 — report**: qualquer usuário logado denuncia ideia, comentário ou perfil, escolhendo
  motivo: `SPAM`, `SCAM/FRAUD`, `HARASSMENT`, `OTHER` (+texto). Máx. 20 reports/dia por usuário.
- **RN-M5-22 — fila de moderação**: reports caem numa fila para revisão manual por admin
  (ferramenta interna mínima: listar, ver contexto, agir).
- **RN-M5-23 — ações de moderação**: remover conteúdo (RN-M4-09 / apagar comentário),
  suspender conta (RN-M1-12), banir definitivamente. Toda ação registra motivo + moderador (audit log).
- **RN-M5-24 — regras de conteúdo (Community Guidelines, resumo v1)**: proibido: venda de sinais
  ou promessas de lucro; links de referral/afiliados; esquemas (pump groups); assédio; spam;
  conteúdo sem relação com mercados. Documento público completo a redigir antes do lançamento.
- **RN-M5-25 — automações mínimas anti-spam**: bloquear links repetidos + conta recém-criada
  postando links em série → flag automático para a fila.
- **RN-M5-26 — moderação assistida por IA (ADR-010)**: todo report (RN-M5-21) e todo conteúdo
  flagrado por heurística (RN-M5-25) é pré-classificado por IA (categoria provável + confiança)
  para **priorizar a fila** do admin. Conteúdo com alta confiança de scam/spam pode ser
  **ocultado preventivamente** ("under review"), mas **nenhuma remoção ou suspensão definitiva é
  automática** — a decisão final é sempre humana na v1. Classificações da IA ficam registradas
  no audit log (RN-M5-23) junto com a decisão humana, para calibração futura.

## 7. Fora do escopo deste módulo (v1)

DMs/chat; menções `@user` com autocomplete (v1.x — fácil e valioso); repost/share interno;
notificações push (browser/mobile); mute; blocklists pessoais; algoritmo de relevância no feed;
moderação por reputação/comunidade.

## 8. Pontos em aberto

- **Q-M5-A ✅** (2026-07-09, ADR-009): **Omar como único admin** no dia 1; ferramenta interna
  mínima (fila de reports + ações) entra nos milestones. Papel de moderador multi-conta fica para v1.x.
- **Q-M5-B**: e-mail transacional exige provedor (Resend/SES/Postmark...) — decidir na spec técnica;
  há restrição de custo? (ligado a T-05).
