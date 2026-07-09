# US_BySteps — Micro-tarefas por Etapa

Padrão herdado da guia [`hiria_pro`](https://github.com/OmarCamaHuara/hiria_pro): as tarefas de
implementação vivem em pastas `Etapa-XXX/`, escritas para serem executáveis por qualquer LLM
sem contexto além dos documentos referenciados.

**Status: vazio de propósito.** Esta pasta só será populada na **Fase 3** (ver
`docs/CONSTITUTION.md` §5), depois que as regras de negócio (Fase 1) e a especificação técnica
(Fase 2) forem aprovadas.

## Convenções (CONSTITUTION §6)

- Nomenclatura: `US-XXXX-B` (backend) · `US-XXXX-F` (frontend) · `US-XXXX-D` (docs/infra);
  numeração global zero-padded (`US-0001-B`, `US-0002-F`, ...).
- Organização: `Etapa-001/`, `Etapa-002/`, ... — cada Etapa é um milestone entregável.
- Uma US = um PR pequeno (alvo ≤ ~2 h de trabalho).

## Template de US (rascunho — fechar na Fase 3)

```markdown
# US-XXXX-Y — Título imperativo curto

## Objetivo
O que existe ao final que não existia antes (1–2 frases).

## Contexto obrigatório
Links para: regra de negócio (RN-*), ADRs e specs relevantes. Nada além disso é necessário.

## Critérios de aceitação
- [ ] Comportamento verificável 1
- [ ] Comportamento verificável 2

## Arquivos afetados (previsão)
- caminho/arquivo — o que muda

## Definição de pronto
- [ ] Testes escritos e passando
- [ ] Critérios de aceitação demonstrados
- [ ] Sem violação da CONSTITUTION
```
