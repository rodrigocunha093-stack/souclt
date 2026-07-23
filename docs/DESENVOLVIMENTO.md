# Guia de desenvolvimento

## Estrutura

```text
souclt/
├── game/
│   └── trilha-dos-direitos.html
├── docs/
│   ├── CONTEXT.md
│   ├── DESENVOLVIMENTO.md
│   ├── VALIDACAO-JURIDICA.md
│   └── MEMORIA.md
├── .gitignore
├── COMECE-AQUI.md
└── README.md
```

O jogo está concentrado em um arquivo:

1. `<title>` e `<style>`: aparência, animações e responsividade;
2. corpo visual: nuvens, contêiner `#root`, confetes e template SVG da coruja;
3. `<script>`: utilitários, conteúdo, persistência e telas.

**Limitação conhecida:** o arquivo atual não declara doctype, elementos `html/head/body` nem `<meta charset="utf-8">`. Essa correção deve ser feita e testada em mudança separada.

## Executar localmente

Com Python:

```bash
cd game
python -m http.server 8000
```

Com Node, sem instalar dependência no projeto:

```bash
cd game
npx http-server -p 8000
```

Abra `http://localhost:8000/trilha-dos-direitos.html`.

## Modelo de conteúdo

As fases ficam na constante `PHASES`. Cada fase tem:

```js
{
  id: 0,
  name: "Nome da fase",
  icon: "🎯",
  color: "b-green",
  q: [/* perguntas */]
}
```

Cada pergunta tem:

```js
{
  q: "Texto da pergunta",
  o: ["Resposta correta", "Distrator"],
  a: 0,
  fx: "Explicação exibida depois da resposta.",
  law: "Referência legal a revisar"
}
```

- `q`: pergunta;
- `o`: opções na ordem de autoria;
- `a`: índice da correta em `o`, começando por zero;
- `fx`: feedback educativo;
- `law`: rótulo curto de fonte. Não equivale a validação jurídica.

As opções são embaralhadas na apresentação, mas `cur.order` preserva o vínculo com o índice correto.

## Adicionar ou alterar uma pergunta

1. Localize a fase em `PHASES`.
2. Adicione o objeto de pergunta ao array `q`.
3. Confirme o índice `a`; ele deve apontar para a opção correta antes do embaralhamento.
4. Use linguagem compreensível para a faixa etária.
5. Evite afirmações absolutas quando a regra tiver exceções.
6. Inclua referência legal específica, mas mantenha o status pendente.
7. Atualize a entrada correspondente em `docs/VALIDACAO-JURIDICA.md`.
8. Solicite revisão jurídica antes de tratar a mudança como aprovada.

Exemplo técnico, não destinado à publicação sem revisão:

```js
{
  q: "Exemplo de pergunta?",
  o: ["Resposta correta", "Resposta incorreta"],
  a: 0,
  fx: "Explicação simples e precisa.",
  law: "Lei X, art. Y"
}
```

O total máximo de estrelas é calculado como `PHASES.length * 3`. Se uma fase passar a ter quantidade diferente de três perguntas, revise a interface e as regras de estrelas.

## Progressão e pontuação

- `save.unlocked` indica quantas fases estão abertas;
- `save.stars` guarda a melhor pontuação por fase;
- `save.points` soma dez pontos por acerto, inclusive em repetições;
- uma estrela já libera a fase seguinte;
- o diploma aparece quando todas as fases têm ao menos uma estrela.

Observação: repetir perguntas acumula pontos indefinidamente. Confirme se isso é desejado antes de usar pontos em ranking ou premiação.

## Testes manuais mínimos

### Fluxo completo

1. Apague o progresso.
2. Inicie a fase 1.
3. Responda uma alternativa errada e confira:
   - alternativa correta revelada;
   - feedback e referência legal visíveis;
   - botão de continuidade funcional.
4. Termine com zero acertos: a próxima fase deve continuar bloqueada.
5. Refaça e obtenha ao menos uma estrela: a próxima fase deve abrir.
6. Termine as sete fases e abra o diploma.

### Estrelas

- 3 acertos: 3 estrelas;
- 2 acertos: 2 estrelas;
- 1 acerto: 1 estrela;
- 0 acertos: 0 estrelas;
- repetir com resultado pior não deve reduzir o melhor resultado salvo.

### Persistência

No console do navegador:

```js
localStorage.getItem("trilha_direitos_save")
```

Recarregue e confira mapa, estrelas e pontos. Para limpar manualmente:

```js
localStorage.removeItem("trilha_direitos_save")
```

Teste também armazenamento indisponível: o jogo captura erros, mas o progresso não persistirá.

### Responsividade e acessibilidade

Teste ao menos 320, 375, 768 e 1280 px, orientação retrato/paisagem, teclado, zoom de 200% e preferência de movimento reduzido. Registre navegador, versão, sistema, data e resultado.

## Verificações antes do commit

- [ ] `git status --short` mostra apenas mudanças intencionais.
- [ ] `git diff --check` não aponta erros de espaços.
- [ ] As 21 entradas da matriz correspondem ao HTML.
- [ ] Nenhuma pergunta está marcada como validada sem documento do TRT.
- [ ] Fluxo com acertos e erros foi testado.
- [ ] Recarga preserva progresso.
- [ ] Reset apaga progresso.
- [ ] Links dos documentos funcionam.
- [ ] Informações históricas sem evidência estão marcadas.

## Publicação

### GitHub Pages

Como o jogo é estático, pode ser hospedado por Pages. Configure a origem de publicação no repositório e use uma página inicial ou link direto para `game/trilha-dos-direitos.html`.

### Vercel

Importe o repositório como site estático, sem comando de build. Confirme a raiz pública ou crie uma entrada adequada.

**Não publicar como campanha pública antes da validação jurídica e dos testes necessários.** Um preview privado para revisão técnica não representa aprovação.

## Problemas comuns

| Sintoma | Verificação |
|---|---|
| Acentos incorretos | Servir como UTF-8 e adicionar `<meta charset="utf-8">` após teste. |
| Fase não desbloqueia | Confirmar ao menos uma estrela e valor de `save.unlocked`. |
| Progresso estranho | Inspecionar a chave `trilha_direitos_save` e testar após limpá-la. |
| Resposta correta errada | Conferir se `a` aponta para o índice correto em `o`. |
| Matriz divergente | Extrair novamente os objetos de `PHASES` e atualizar a documentação. |
| Pontos crescem ao repetir | Comportamento atual; decidir regra de negócio antes de mudar. |

