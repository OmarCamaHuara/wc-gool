# M1 — Usuários e Perfis

**Status**: proposta para validação.
**Depende de**: — (módulo base).
**É dependência de**: todos os outros módulos.

---

## 1. Conceitos

| Conceito | Definição |
|---|---|
| **Conta** | Credenciais + estado de acesso de uma pessoa (e-mail, senha, status) |
| **Perfil** | A face pública da conta (username, nome de exibição, bio, avatar, estatísticas) |
| **Sessão** | Login ativo de uma conta em um dispositivo |

## 2. Cadastro

- **RN-M1-01**: cadastro por **e-mail + senha** ou **Google OAuth** (T-07). Nenhum outro método na v1.
- **RN-M1-02**: campos obrigatórios no cadastro: e-mail, senha (ou vínculo Google), `username`.
  Nada mais — fricção mínima.
- **RN-M1-03 — username**: 3–30 caracteres, apenas `a-z`, `0-9` e `_`, começando por letra;
  único (case-insensitive); **imutável** após a criação (RT-05). Lista de reservados
  (`admin`, `api`, `settings`, `ideas`, `symbol`, etc.) mantida em documento próprio na fase de specs.
- **RN-M1-04 — senha**: mínimo 8 caracteres; validar contra lista de senhas vazadas comuns;
  sem regras arbitrárias de composição (maiúscula/símbolo não obrigatórios).
- **RN-M1-05 — verificação de e-mail**: conta nasce `UNVERIFIED`; pode navegar logada, mas
  **não pode publicar ideias, comentar, dar boost nem seguir** até verificar o e-mail
  (link com token, validade 24 h, reenvio permitido com rate limit de 1/min).
- **RN-M1-06**: cadastro via Google entra já `ACTIVE` (e-mail verificado pelo provedor).

## 3. Autenticação e sessão

- **RN-M1-07**: login por e-mail (não por username) + senha, ou Google.
- **RN-M1-08**: 5 tentativas falhas de login no mesmo e-mail em 15 min → bloqueio temporário de
  15 min (com mensagem genérica, sem revelar se o e-mail existe).
- **RN-M1-09 — recuperação de senha**: link por e-mail com token de uso único, validade 1 h.
  Resposta idêntica exista ou não o e-mail (não vazar existência de conta).
- **RN-M1-10**: sessões longas ("lembrar de mim" é o padrão) com renovação; logout invalida a sessão.
- **RN-M1-11**: trocar a senha invalida todas as outras sessões ativas.

## 4. Estados da conta

```
UNVERIFIED → ACTIVE → (SUSPENDED ⇄ ACTIVE) → DELETED
```

| Estado | Pode ler | Pode interagir | Perfil visível | Como entra |
|---|---|---|---|---|
| `UNVERIFIED` | ✅ | ❌ (RN-M1-05) | ✅ | cadastro por e-mail |
| `ACTIVE` | ✅ | ✅ | ✅ | verificação / Google |
| `SUSPENDED` | ✅ (deslogado) | ❌ | ✅ com aviso "suspended" | ação de moderação (M5) |
| `DELETED` | — | — | ❌ (ver RN-M1-15) | pedido do usuário |

- **RN-M1-12**: suspensão é ação administrativa (M5); usuário suspenso é deslogado e vê o motivo.
- **RN-M1-13 — exclusão de conta**: auto-serviço nas configurações, com confirmação de senha.
- **RN-M1-14**: exclusão é **soft delete** com carência de 30 dias (login dentro do prazo reativa);
  após 30 dias, dados pessoais são anonimizados definitivamente.
- **RN-M1-15 — conteúdo do usuário excluído**: ideias e comentários **permanecem** (RT-02,
  accountability), reatribuídos a um autor anonimizado `[deleted]` sem link de perfil.

## 5. Perfil público (`/u/{username}` ou `/{username}` — decidir na spec)

- **RN-M1-16 — campos do perfil**: nome de exibição (até 50 chars), bio (até 300 chars),
  avatar (upload, quadrado, máx. 2 MB, formatos jpg/png/webp), link externo (1 URL, com `rel=nofollow`),
  país (opcional, lista ISO). Todos editáveis a qualquer momento.
- **RN-M1-17 — estatísticas exibidas** (calculadas, não editáveis): nº de ideias publicadas,
  nº de seguidores, nº de seguindo, data de cadastro ("Member since"), nº total de boosts recebidos.
- **RN-M1-18 — abas do perfil**: Ideas (padrão, ordenadas da mais recente), Following, Followers.
- **RN-M1-19**: perfil é público sem login (RT-01), incluindo para contas `UNVERIFIED` e `SUSPENDED`
  (esta última com selo). Perfis `DELETED` retornam 404.
- **RN-M1-20 — avatar padrão**: gerado deterministicamente a partir do username (sem foto genérica única).

## 6. Configurações da conta

- **RN-M1-21**: seções da página de configurações: Profile (RN-M1-16), Account (e-mail, senha,
  exclusão), Notifications (preferências — regras em M5).
- **RN-M1-22**: troca de e-mail exige confirmação no e-mail novo (token 24 h); o antigo recebe aviso.

## 7. Fora do escopo deste módulo (v1)

Perfis privados; bloquear usuário; verificação "selo azul"; 2FA (desejável, v1.x);
múltiplos links sociais; banner de perfil; API pública.

## 8. Pontos em aberto

- **Q-M1-A**: rota do perfil: `/{username}` (curta, estilo TradingView) ou `/u/{username}`
  (evita colisão com rotas do app)? *Default proposto: `/u/{username}`.*
- **Q-M1-B**: cadastro exige idade mínima/termos de uso? (Texto legal ainda não existe — precisa
  de ToS e Privacy Policy antes do lançamento público; quem redige?)
