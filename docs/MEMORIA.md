# Memória de decisões do Sou CLT

> Atualizado em 22 de julho de 2026. A conversa original não estava disponível; citações literais e datas sem evidência não foram inventadas.

## Decisões consolidadas

| Decisão | Estado | Evidência |
|---|---|---|
| Usar fases com quiz | Confirmada | Código e README. |
| Manter 7 temas e 21 perguntas na v1.0 | Confirmada | Constante `PHASES`. |
| Usar HTML, CSS e JavaScript sem dependências | Confirmada | Arquivo único do jogo. |
| Usar a coruja como mascote | Confirmada | SVG e reações no código. |
| Embaralhar opções a cada pergunta | Confirmada | Algoritmo Fisher–Yates em `quiz()`. |
| Exibir explicação e referência legal após responder | Confirmada | Campos `fx` e `law`. |
| Persistir progresso no navegador | Confirmada | `localStorage`. |
| Bloquear campanha pública antes da revisão TRT | Confirmada | README, COMECE-AQUI e instruções do usuário. |
| Rejeitar visual novel “O Primeiro Contrato” | ❓ A confirmar | Citada nas instruções, sem artefato ou citação original disponível. |

## Feedback do usuário disponível

Não há citação literal da conversa original no repositório. O único feedback verificável nesta continuidade é o pedido, em 22/07/2026, de completar a documentação e preservar incertezas sem inventar dados.

**❓ A confirmar com o usuário:** fala exata, data e contexto da rejeição da visual novel.

## O que funciona na versão atual

- fluxo de título, mapa, quiz, resultado e diploma;
- sete fases desbloqueadas progressivamente;
- três perguntas por fase;
- opções embaralhadas;
- feedback visual da coruja;
- estrelas e pontos;
- armazenamento local do progresso;
- reinício manual do progresso;
- diploma depois de obter ao menos uma estrela em todas as fases.

## O que não deve ser repetido

- não declarar conteúdo “aprovado pelo TRT” sem documento formal;
- não chamar o protótipo de pronto para campanha pública;
- não registrar como fato histórico algo que só foi mencionado sem evidência;
- não atribuir citações literais ao usuário sem a conversa original;
- não alterar perguntas jurídicas sem sincronizar a matriz de validação;
- não usar referências genéricas como “CLT” ou “ECA” quando um artigo específico puder ser revisado e indicado;
- não confundir ausência de contrato escrito com ausência automática de direitos;
- não supor que todos os aprendizes têm a mesma jornada ou situação escolar;
- não testar persistência apenas no fluxo normal: verificar também JSON inválido, armazenamento bloqueado e reinício.

## Problemas históricos mencionados

- charset/acento: ❓ detalhes a confirmar; a estrutura HTML ainda não declara charset;
- animação com `requestAnimationFrame`: ❓ detalhes a confirmar; não existe na versão atual;
- desbloqueio: correção visível em `phaseResult()`, mas causa e data originais não estão documentadas.

## Decisões pendentes

1. confirmar se 10–18 anos continuará sendo uma única faixa ou se haverá versões por idade;
2. decidir se a v2 manterá três perguntas por fase;
3. definir responsável e rito formal da validação jurídica;
4. escolher GitHub Pages, Vercel ou outra hospedagem;
5. definir requisitos de acessibilidade e privacidade;
6. decidir se o diploma será apenas visual ou exportável;
7. recuperar e anexar evidências dos testes já realizados.

## Checklist para continuidade

- [ ] Ler `README.md`, `COMECE-AQUI.md` e os quatro arquivos em `docs/`.
- [ ] Comparar toda mudança de conteúdo com `PHASES`.
- [ ] Manter cada pergunta com `q`, `o`, `a`, `fx` e `law`.
- [ ] Fazer playthrough correto e com erros.
- [ ] Testar desbloqueio, estrelas, diploma, recarga e reset.
- [ ] Registrar navegador, dispositivo, data e resultado dos testes.
- [ ] Atualizar a matriz jurídica e manter status pendente até confirmação formal.
- [ ] Revisar o diff antes do commit.

