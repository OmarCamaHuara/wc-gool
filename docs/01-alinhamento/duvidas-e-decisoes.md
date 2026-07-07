# Dúvidas de Alinhamento e Registro de Decisões

**Como usar este documento**: cada dúvida tem um ID. Responda no chat ou editando este arquivo.
Quando uma dúvida for respondida, a resposta vira uma **Decisão numerada** na seção final e a
dúvida é marcada como ✅. Nenhum documento de regra de negócio será escrito com dúvidas 🔴 abertas.

Legenda de prioridade: 🔴 bloqueia o planejamento · 🟠 importante, mas tem default razoável · 🟢 pode esperar

---

## P — Processo e documentação

### P-01 🔴 Acesso à guia `hiria_pro`
Tentei acessar `https://github.com/OmarCamaHuara/hiria_pro` e recebi 404 — o repositório é privado
e a ferramenta de adicioná-lo à sessão falhou repetidamente por instabilidade de conexão.
**Preciso de uma destas opções:**
- (a) você adiciona o repo `hiria_pro` a esta sessão / torna acessível; ou
- (b) você cola aqui a estrutura de pastas + um documento de exemplo dele; ou
- (c) me autoriza a propor uma estrutura própria (que depois adaptamos à guia).
*Enquanto isso segui com uma estrutura provisória (`00-descoberta/`, `01-alinhamento/`).*

### P-02 🟠 Idioma da documentação
Estou escrevendo em PT-BR. Confirma? (Alternativas: espanhol, inglês, ou PT para negócio +
inglês para specs técnicas — inglês costuma render melhor com LLMs na hora de codar.)

### P-03 🟠 Granularidade das micro-tarefas
Você pediu tarefas que "qualquer LLM possa fazer". Para calibrar: uma micro-tarefa ideal para você é
algo como **"criar endpoint `GET /api/watchlists/{id}` retornando X, com teste"** (1–2 h de trabalho,
um PR pequeno)? Ou ainda menor (ex.: "criar a entidade JPA `Watchlist` com os campos X, Y")?

### P-04 🟢 Ferramenta de gestão das tarefas
Os milestones/micro-tarefas viverão onde? (a) arquivos Markdown neste repo; (b) GitHub Issues +
Milestones deste repo; (c) GitHub Projects. Sugestão: (a) como fonte da verdade + (b) gerado a partir de (a).

---

## N — Negócio e produto

### N-01 🔴 Qual é o pilar central do produto?
O TradingView tem ~10 pilares (ver visão geral). Um MVP precisa escolher UM núcleo.
Qual destas frases descreve melhor o seu sonho?
- (a) "Um TradingView": **gráficos excelentes** + ideias sociais em volta.
- (b) "Um StockTwits": **rede social** de traders (posts por ativo, sentimento), gráficos simples.
- (c) "Um eToro sem dinheiro": **paper trading + ranking público** — competição de performance simulada.
- (d) Outra visão sua (descreva com suas palavras, sem se prender aos exemplos).

### N-02 🔴 Quais mercados/ativos na v1?
- (a) Só **cripto** (dados em tempo real gratuitos — caminho mais barato e rápido);
- (b) Cripto + ações US delayed;
- (c) Foco em **B3/Brasil** (nicho mal servido, mas dados mais difíceis);
- (d) Tudo (não recomendado para MVP).

### N-03 🔴 Público-alvo e idioma da plataforma
Quem é o usuário nº 1? Trader iniciante ou experiente? Brasil, América Latina (espanhol — você
mandou o link `es.tradingview.com`), ou global (inglês)? Isso define idioma da UI, dos conteúdos e o marketing.

### N-04 🟠 Copy trading / execução real está no horizonte?
Mesmo que não seja MVP: o plano de longo prazo inclui executar ordens ou copy trading com dinheiro
real? A resposta muda decisões de arquitetura e a estratégia regulatória desde já
(ver análise de concorrentes, seção 4.1). Minha recomendação: manter fora do horizonte v1–v2.

### N-05 🟠 Modelo de monetização pretendido
(a) Freemium com assinatura (padrão do setor); (b) grátis por enquanto, monetiza depois;
(c) ads; (d) marketplace/criadores. Precisa estar claro cedo porque limites de plano
(nº de alertas, watchlists etc.) entram nas regras de negócio.

### N-06 🟠 Nome do produto
"wc-gool" é o nome do repositório — é também o nome do produto? Tem marca/nome em mente?
(Impacta domínio, textos da documentação e identidade visual.)

### N-07 🟢 O que existe hoje?
Isso é um projeto do zero, certo? Existe algo já feito (design, pesquisa, público, comunidade,
sócios)? Existe prazo ou evento-alvo (ex.: lançar em X meses)?

---

## T — Técnico (defaults propostos — vetar ou confirmar)

Para não travar o planejamento, proponho defaults. Se você não discordar, viram decisão:

### T-01 🟠 Versões e frameworks
**Default proposto**: Java 21 LTS + Spring Boot 3.x; React 18 + TypeScript + Vite.

### T-02 🟠 Arquitetura inicial
**Default proposto**: monólito modular (um app Spring Boot com módulos bem separados) + um serviço
de ingestão de cotações. Microserviços só quando doer. Banco único PostgreSQL + TimescaleDB + Redis.

### T-03 🟠 Biblioteca de gráficos
**Default proposto**: TradingView **Lightweight Charts** (open source) no MVP; solicitar em paralelo
a licença gratuita da Charting Library completa.

### T-04 🟠 Fonte de dados v1
**Default proposto** (depende de N-02): WebSocket público da Binance para cripto (tempo real, grátis).

### T-05 🟠 Hospedagem e orçamento de infra
Onde você pretende rodar (AWS, GCP, Hetzner, Railway, VPS...)? Qual orçamento mensal máximo
aceitável para o MVP? (Estimei USD 25–150/mês no doc técnico.) Isso poda decisões de arquitetura.

### T-06 🟢 Mobile
**Default proposto**: web responsivo primeiro; app mobile fora do escopo v1.

### T-07 🟢 Autenticação
**Default proposto**: e-mail/senha + login Google (OAuth2), JWT.

---

## Registro de Decisões

| # | Data | Decisão | Origem |
|---|---|---|---|
| D-001 | 2026-07-07 | Stack: Java no backend, React no frontend | Definido pelo Omar no kickoff |
| D-002 | 2026-07-07 | Este repositório conterá somente documentação; código virá depois, guiado por micro-tarefas executáveis por LLM | Definido pelo Omar no kickoff |
| D-003 | 2026-07-07 | Método: primeiro recopilar informação → alinhar dúvidas → só então escrever regras de negócio sólidas | Definido pelo Omar no kickoff |
