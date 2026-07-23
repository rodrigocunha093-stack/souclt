# Sou CLT — Jogo Educativo sobre Direitos do Trabalho

**Projeto**: Jogo educativo para campanhas do TRT (Tribunal Regional do Trabalho) contra trabalho infantil.
**Público**: Crianças e adolescentes de 10-18 anos.
**Status**: Protótipo v1 em desenvolvimento — fases com quiz funcionais, 7 temas sobre CLT.

---

## 🎮 O Jogo

**"Trilha dos Direitos"** é um jogo de **fases + quiz** onde o jogador percorre uma trilha de 7 temas sobre direitos trabalhistas:

1. **Que idade pode trabalhar?** — 14 (aprendiz) / 16 (comum) / proibição
2. **O que é ser Aprendiz** — Lei 10.097, contrato, escola
3. **Carteira e Contrato** — Por que protegem
4. **O dinheiro dos direitos** — 13º, férias, FGTS
5. **Trabalho e Escola** — Prioridade, jornada reduzida
6. **Trabalho Proibido** — Noturno, perigoso, peso (<18)
7. **Pedir Ajuda** — Disque 100, MPT, TRT

---

## ✅ O que Funciona

- ✅ Trilha de 7 fases com trava/desbloqueio
- ✅ Quiz com opções embaralhadas, feedback + lei
- ✅ Mascote coruja que reage
- ✅ Sistema de estrelas (máx 21)
- ✅ Progresso persistente (localStorage)
- ✅ Diploma final
- ✅ HTML5 puro (zero dependências)
- ✅ Testado: playthrough completo 21/21 ⭐

---

## 📂 Estrutura

```
souclt/
├── game/trilha-dos-direitos.html       # Protótipo funcional
├── docs/
│   ├── CONTEXT.md                      # Histórico confirmado e lacunas
│   ├── DESENVOLVIMENTO.md              # Guia de continuidade
│   ├── VALIDACAO-JURIDICA.md           # Matriz pendente de revisão TRT
│   └── MEMORIA.md                      # Decisões e feedback disponíveis
└── README.md                           # Este arquivo
```

---

## 🚀 Para Rodar

```bash
cd game
python -m http.server 8000
# Abrir http://localhost:8000/trilha-dos-direitos.html
```

---

## ⚠️ Importante

**Todas as perguntas devem passar por revisão de especialista TRT antes de campanha pública.**
Veja `/docs/VALIDACAO-JURIDICA.md` para matriz de validação.

---

**Versão**: 1.0 Protótipo | **Data**: 22 de julho de 2026
