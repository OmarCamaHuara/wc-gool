# Documentação do Projeto — Plataforma de Análise e Rede Social para Traders

> Repositório de **documentação apenas**. Nenhum código de aplicação vive aqui.
> O objetivo é produzir regras de negócio e especificações tão detalhadas que
> qualquer LLM consiga executar cada micro-tarefa de implementação sem contexto adicional.
> Governança no padrão da guia [`hiria_pro`](https://github.com/OmarCamaHuara/hiria_pro) (ADR-008).

## Comece por aqui (ordem de leitura obrigatória para agentes)

1. [`CONSTITUTION.md`](CONSTITUTION.md) — regras imutáveis e governança
2. [`CONTEXT_GLOBAL.md`](CONTEXT_GLOBAL.md) — memória viva: estado atual, pendências, riscos
3. [`DECISIONS.md`](DECISIONS.md) — registro de decisões (ADRs, append-only)
4. O documento da tarefa em questão

## Estado atual

**Fase 1 — Regras de Negócio** (escritas, em validação pelo CEO)

## Estrutura

| Caminho | Conteúdo | Fase |
|---|---|---|
| [`CONSTITUTION.md`](CONSTITUTION.md) | Regras imutáveis, stack, método, convenções de US | — |
| [`CONTEXT_GLOBAL.md`](CONTEXT_GLOBAL.md) | Memória viva do projeto | — |
| [`DECISIONS.md`](DECISIONS.md) | ADRs | — |
| [`00-descoberta/`](00-descoberta/) | Pesquisa: TradingView, concorrentes, considerações técnicas | 0 ✅ |
| [`01-alinhamento/duvidas-e-decisoes.md`](01-alinhamento/duvidas-e-decisoes.md) | Dúvidas abertas (respondidas viram ADR) | contínuo |
| [`02-regras-de-negocio/`](02-regras-de-negocio/) | Escopo do MVP + regras dos módulos M1–M6 | 1 🔄 |
| `03-especificacao-tecnica/` | (a criar) arquitetura, modelo de dados, contratos de API | 2 ⏳ |
| [`../US_BySteps/`](../US_BySteps/) | Micro-tarefas por Etapa | 3 ⏳ |

### Regras de negócio (Fase 1)

1. [`02-regras-de-negocio/00-escopo-mvp.md`](02-regras-de-negocio/00-escopo-mvp.md) — o contrato de escopo
2. [`01-usuarios-e-perfis.md`](02-regras-de-negocio/01-usuarios-e-perfis.md) · [`02-dados-de-mercado.md`](02-regras-de-negocio/02-dados-de-mercado.md) · [`03-graficos.md`](02-regras-de-negocio/03-graficos.md) · [`04-ideias.md`](02-regras-de-negocio/04-ideias.md) · [`05-social-feed.md`](02-regras-de-negocio/05-social-feed.md) · [`06-watchlists.md`](02-regras-de-negocio/06-watchlists.md)

## Convenções

- **Idioma da documentação**: PT-BR (dúvida P-02 em aberto); UI do produto em inglês (ADR-006).
- Regras numeradas: `RT-XX` (transversais), `RN-M{n}-XX` (por módulo), `Q-M{n}-X` (pontos em aberto).
- Toda decisão vira ADR em `DECISIONS.md`; dúvidas vivem em `01-alinhamento/duvidas-e-decisoes.md`.
