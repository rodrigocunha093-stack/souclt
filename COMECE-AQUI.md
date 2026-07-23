# 🎮 COMECE AQUI — Continuando o Projeto

Bem-vindo! Você foi convidado a continuar o desenvolvimento do **Sou CLT** — jogo educativo sobre direitos do trabalho para o TRT.

---

## 📖 Leia Nessa Ordem

### 1. **Este arquivo** (você está aqui)
   Orientação de início

### 2. **README.md**
   Visão geral do projeto, como rodar, status

### 3. **docs/CONTEXT.md** (incluído no repositório)
   Resumo completo do que foi feito:
   - Por que foi rejeitado o formato visual-novel
   - Bugs encontrados e corrigidos
   - Testes realizados
   - Decisões tomadas

### 4. **docs/DESENVOLVIMENTO.md** (incluído no repositório)
   Guia prático: como adicionar conteúdo, testar, publicar
   - Como adicionar perguntas
   - Como validar

### 5. **docs/VALIDACAO-JURIDICA.md** (incluído no repositório)
   Matriz de cada pergunta com base legal CLT
   ⚠️ **CRÍTICO**: Antes de campanha pública, especialista TRT DEVE revisar

### 6. **docs/MEMORIA.md** (incluído no repositório)
   O que funcionou, o que não funcionou
   Erros que não devem ser repetidos

### 7. **docs/PARECER-TECNICO-PRE-VALIDACAO.md**
   Auditoria documental, riscos residuais e termo para aprovação formal do TRT

---

## 🚀 Comece Agora (5 min)

### 1. Clonar o repo
```bash
git clone https://github.com/rodrigocunha093-stack/souclt.git
cd souclt
```

### 2. Rodar o jogo
```bash
cd game
python -m http.server 8000
# Ou: npx http-server -p 8000
```
Abrir: http://localhost:8000/trilha-dos-direitos.html

### 3. Testar
- Clicar em "Jogar"
- Passar por uma fase completa (3 perguntas)
- Ver o resultado (estrelas, diploma)
- Recarregar → progresso salvo? ✅

---

## 📚 Documentação incluída

Os documentos de continuidade estão em `/docs/`:
- **CONTEXT.md** — histórico recuperado e lacunas identificadas
- **DESENVOLVIMENTO.md** — guia prático
- **VALIDACAO-JURIDICA.md** — matriz das 24 perguntas, pendente de revisão especializada
- **MEMORIA.md** — decisões, feedback disponível e cuidados para continuidade
- **PARECER-TECNICO-PRE-VALIDACAO.md** — pré-validação e formulário de aprovação institucional

Informações da conversa original que não puderam ser verificadas estão marcadas como **“A confirmar com o usuário”**.

---

## 💡 O Que É Este Projeto

Um **jogo de fases com quiz** onde crianças aprendem direitos CLT respondendo perguntas corretas e erradas, vendo a lei citada.

**8 fases** × **3 perguntas** = **24 perguntas** sobre:
1. Idade mínima para trabalhar
2. Lei da Aprendizagem (10.097)
3. Contrato e carteira
4. FGTS, 13º, férias
5. Trabalho vs Escola
6. Trabalho proibido <18 anos
7. Onde pedir ajuda
8. O que é trabalhar protegido e quando não trabalhar

**Mecânica**:
- Mascote coruja que reage 😊 / 😢
- Opções embaralhadas (não decora)
- Feedback com lei citada (aprendizado)
- ⭐ Estrelas por acurácia
- 🏆 Diploma ao final
- 💾 Progresso salvo

---

## ⚠️ Pontos Críticos

### 1. Validação Jurídica
Antes de QUALQUER campanha pública, **um especialista do TRT DEVE revisar**:
- Cada pergunta
- Cada resposta
- Cada citação CLT

Ver: `docs/VALIDACAO-JURIDICA.md`

### 2. Público-Alvo
Este jogo é para **crianças 10-18 anos**, não para adultos.
- Linguagem: simples, clara
- Estrutura: fases (não simulador)
- Ritmo: rápido (5-10 min/fase)

### 3. Versão Atual
**v1.0 é protótipo** — funcional, testado, SEM dependências externas.
Pronto para validação jurídica, mas **não** para campanha pública.

---

## 📝 Próximos Passos

1. [ ] Ler README.md
2. [ ] Rodar jogo localmente
3. [ ] Ler CONTEXT.md (histórico)
4. [ ] Ler DESENVOLVIMENTO.md (guia)
5. [ ] Revisar VALIDACAO-JURIDICA.md (legal)
6. [ ] Ler MEMORIA.md (não fazer novamente)
7. [ ] Fazer branch para sua mudança
8. [ ] Adicionar conteúdo/features
9. [ ] Testar
10. [ ] Commitar com mensagem descritiva
11. [ ] Push/PR

---

## 🔗 Repo

https://github.com/rodrigocunha093-stack/souclt

---

## 📞 Dúvidas?

O contexto recuperado está em `docs/CONTEXT.md`. Trechos históricos sem evidência no repositório foram marcados para confirmação.

---

**Sucesso!** 🚀
Bem-vindo ao time do Sou CLT!
