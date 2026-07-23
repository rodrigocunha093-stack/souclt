# Contexto do projeto Sou CLT

> Documento reconstruído em 22 de julho de 2026 a partir do repositório e das instruções fornecidas pelo usuário. A conversa original completa não estava disponível. O que não pôde ser comprovado está explicitamente marcado.

## Objetivo e público

O **Sou CLT — Trilha dos Direitos** é um protótipo de jogo educativo sobre direitos do trabalho e prevenção ao trabalho infantil. A documentação existente indica uso futuro em iniciativas ligadas ao Tribunal Regional do Trabalho (TRT) e público de 10 a 18 anos.

Restrições de produto já registradas:

- linguagem simples, clara e adequada a crianças e adolescentes;
- sessões curtas, estruturadas em fases;
- conteúdo jurídico sujeito a revisão de especialista;
- nenhuma campanha pública antes da validação jurídica formal e de testes com o público-alvo.

## Linha do tempo confirmada

| Data | Evidência | Evento |
|---|---|---|
| 22/07/2026 | commit `8f34d84` | Inclusão do protótipo funcional `game/trilha-dos-direitos.html`. |
| 22/07/2026 | commit `eb0d374` | Inclusão de `README.md` e `COMECE-AQUI.md`. |
| 22/07/2026 | README e instruções do usuário | Estado declarado como protótipo v1.0, com 7 fases, 21 perguntas e playthrough 21/21 concluído sem erros. |
| 22/07/2026 | Solicitação da cliente e evolução local | Inclusão do eixo “trabalho protegido”, nova fase sobre quando não trabalhar e expansão para 8 fases e 24 perguntas. |

## Abordagens e decisões

### Jogo de fases com quiz

**Confirmado pelo código e pelo README.** A versão atual usa oito fases progressivas, três perguntas por fase, respostas embaralhadas, feedback educativo, estrelas, diploma, perfis competitivos e persistência no `localStorage`.

### Visual novel “O Primeiro Contrato”

**❓ A confirmar com o usuário.** As instruções recebidas informam que uma visual novel chamada “O Primeiro Contrato” foi rejeitada por ser inadequada para crianças. Não há código, commit, data ou citação literal do feedback no repositório. Até a conversa original ser disponibilizada, não é possível apresentar a fala exata nem reconstruir os critérios completos da rejeição.

## Arquitetura atual

O protótipo é um único arquivo HTML, sem dependências externas. CSS, marcação, template SVG da coruja, conteúdo das fases e lógica JavaScript estão reunidos em `game/trilha-dos-direitos.html`.

Desde a evolução competitiva, o estado persistido usa a chave `trilha_direitos_competicao_v2` e separa os dados por jogador:

```js
{
  activePlayerId: "p_...",
  players: [{
    name: "Ana",
    avatar: "🐼",
    unlocked: 1,
    stars: {},
    bestCorrects: {},
    points: 0,
    elapsedMs: 0
  }]
}
```

## Bugs históricos

As instruções fornecidas mencionam três bugs. O repositório contém apenas a versão final e dois commits, portanto não há diff ou registro técnico que comprove data, sintoma e causa de todos eles.

### Charset UTF-8 / acentuação

- **Status:** ❓ A confirmar com o usuário.
- **Evidência atual:** o arquivo está codificado em UTF-8, mas não contém `<!doctype html>`, `<html>`, `<head>` ou `<meta charset="utf-8">`.
- **Risco atual:** a interpretação de caracteres pode depender do cabeçalho HTTP ou da heurística do navegador.
- **Solução histórica:** ❌ Não confirmada.
- **Recomendação:** incluir estrutura HTML válida e `<meta charset="utf-8">` em uma mudança própria, seguida de teste visual.

### `requestAnimationFrame` congelado

- **Status:** ❓ A confirmar com o usuário.
- **Evidência atual:** não há chamada a `requestAnimationFrame` no protótipo atual.
- **Sintoma, causa, data e correção histórica:** ❌ Não confirmados.

### Desbloqueio de fases travado

- **Status:** correção presente no código; histórico detalhado não confirmado.
- **Evidência atual:** `phaseResult()` eleva `save.unlocked` para até `p.id + 2` quando a fase recebe ao menos uma estrela.
- **Comentário no código:** explica que concluir a fase deve abrir a próxima.
- **Sintoma, causa original e data da correção:** ❓ A confirmar com o usuário.

## Testes registrados

| Teste | Estado | Evidência |
|---|---|---|
| Playthrough original 21/21 | ✅ Declarado como concluído | README e relato do usuário sobre a versão de 7 fases. |
| Playthrough atual 24/24 | ✅ Automatizado | Suíte Playwright local cobre as 8 fases, diploma e persistência. |
| Persistência via `localStorage` | ✅ Implementada | Funções de leitura e `persist()` presentes no código. |
| Responsividade | ⏳ Pendente de evidência | Há CSS responsivo, mas não existe relatório com dispositivos, resoluções ou navegadores. |
| Acessibilidade | ⏳ Pendente | Não há auditoria registrada. |
| Testes com crianças/adolescentes | ⏳ Pendente | Próxima fase indicada pelo usuário. |
| Validação jurídica TRT | ⏳ Pendente | Condição obrigatória antes de campanha pública. |

## Estado atual

O projeto é um **protótipo v1.0 funcional, pronto para validação especializada**, não um produto aprovado para campanha pública.

Pendências prioritárias:

1. revisão das 24 perguntas por especialista do TRT;
2. correção das formulações apontadas em `VALIDACAO-JURIDICA.md`;
3. recuperação da conversa original para completar datas e feedback literal;
4. testes de usabilidade com participantes de 10 a 18 anos, com desenho ético e consentimentos adequados;
5. teste de navegadores, responsividade e acessibilidade;
6. decisão e configuração de deploy após as validações.
