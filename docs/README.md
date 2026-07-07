# Documentação do Projeto — Plataforma de Análise e Rede Social para Traders

> Repositório de **documentação apenas**. Nenhum código de aplicação vive aqui.
> O objetivo é produzir regras de negócio e especificações tão detalhadas que
> qualquer LLM consiga executar cada micro-tarefa de implementação sem contexto adicional.

## Estado atual

**Fase 0 — Descoberta e Alinhamento** (em andamento)

Nesta fase ainda NÃO definimos escopo, arquitetura ou milestones. Estamos:
1. ✅ Recopilando informação sobre o domínio (TradingView e concorrentes)
2. 🔄 Levantando dúvidas para alinhar a visão de produto
3. ⏳ Aguardando respostas para consolidar as regras de negócio

## Estrutura

| Pasta | Conteúdo |
|---|---|
| `00-descoberta/` | Pesquisa de domínio: análise do TradingView, concorrentes e considerações técnicas |
| `01-alinhamento/` | Dúvidas abertas e registro de decisões (fonte da verdade das escolhas do produto) |

### Documentos da Fase 0

1. [`00-descoberta/01-visao-geral.md`](00-descoberta/01-visao-geral.md) — O que estamos construindo e por quê
2. [`00-descoberta/02-analise-tradingview.md`](00-descoberta/02-analise-tradingview.md) — Anatomia completa do TradingView (funcionalidades, modelo de negócio)
3. [`00-descoberta/03-analise-concorrentes.md`](00-descoberta/03-analise-concorrentes.md) — Plataformas com dinâmica similar e o diferencial de cada uma
4. [`00-descoberta/04-consideracoes-tecnicas.md`](00-descoberta/04-consideracoes-tecnicas.md) — Desafios técnicos do domínio com a stack Java + React
5. [`01-alinhamento/duvidas-e-decisoes.md`](01-alinhamento/duvidas-e-decisoes.md) — **Dúvidas que precisam de resposta antes do planejamento**

## Convenções

- **Stack definida**: Java (backend) + React (frontend). Detalhes de versão/frameworks ainda em aberto (ver dúvidas).
- **Idioma**: documentação em português (PT-BR).
- **Guia de estrutura**: seguirá o padrão do repositório `OmarCamaHuara/hiria_pro` (pendente de acesso — ver dúvida P-01).
- Cada decisão tomada sai do documento de dúvidas e vira uma entrada numerada no registro de decisões.

## Próximas fases (após alinhamento)

1. **Fase 1 — Regras de Negócio**: especificação funcional de cada módulo do MVP
2. **Fase 2 — Especificação Técnica**: arquitetura, modelo de dados, contratos de API
3. **Fase 3 — Milestones e Micro-tarefas**: quebra em tarefas atômicas executáveis por LLM
