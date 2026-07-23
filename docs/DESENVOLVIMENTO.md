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
8. Solicite revisão jurídica antes de tratar cm=ӛh��춻�q�^upetition.players.map(p=>`<button class="rank-row" data-player="${p.id}"><span class="rank-pos">${p.avatar}</span><span class="rank-person"><strong>${esc(p.name)}</strong></span><span class="rank-score"><b>${totalStarsFor(p)}/${MAX_STARS} ★</b>${p.points||0} pontos</span></button>`).join("")}
    </div>
    <button class="btn-3d ghost" id="back-title">Voltar</button>`;
  root.appendChild(s);
  $$('[data-player]',s).forEach(btn=>btn.onclick=()=>{setActivePlayer(btn.dataset.player);title();});
  $("#new-player",s).onclick=()=>playerSetup(true);
  $("#back-title",s).onclick=title;
}

function ranking(){
  root.innerHTML="";
  const players=sortedPlayers();
  const medals=["🥇","🥈","🥉"];
  const s=document.createElement("div"); s.className="screen ranking";
  s.innerHTML=`
    <div class="ranking-head"><div><div class="kicker">Recordes</div><h1>Ranking</h1></div><button class="btn-3d" id="rank-new">+ Jogador</button></div>
    <div class="ranking-card ranking-list">
      ${players.length?players.map((p,i)=>`<div class="rank-row ${p.id===competition.activePlayerId?'active':''}">
        <div class="rank-pos">${medals[i]||i+1}</div>
        <div class="rank-person"><span>${p.avatar}</span><strong>${esc(p.name)}</strong></div>
        <div class="rank-score"><b>${totalStarsFor(p)}/${MAX_STARS} ★ · ${p.points||0} pts</b>${completedPhases(p)}/${PHASES.length} fases · ${p.completedAt?formatTime(p.elapsedMs):'em jogo'}</div>
      </div>`).join(""):'<div class="empty-rank">O ranking aparecerá quando o primeiro jogador for criado.</div>'}
    </div>
    <button class="btn-3d ghost" id="rank-back">Voltar</button>`;
  root.appendChild(s);
  $("#rank-new",s).onclick=()=>playerSetup(true);
  $("#rank-back",s).onclick=title;
}

/* ---------- TITLE ---------- */
function title(){
  if(!save){playerSetup(false);return;}
  root.innerHTML="";
  const s=document.createElement("div"); s.className="screen title";
  s.innerHTML=`
    <div class="kicker">Direitos do Trabalho · para você</div>
    <h1>Trilha dos <span class="g">Direitos</span></h1>
    <p>Descubra o que é trabalhar com proteção — e quando estudar, brincar, descansar e crescer devem vir antes do trabalho.</p>
    <div class="player-card">
      <div class="player-id"><span class="player-avatar">${save.avatar}</span><div><strong>${esc(save.name)}</strong><small>${totalStarsFor(save)}/${MAX_STARS} estrelas · ${save.points||0} pontos</small></div></div>
      <button class="small-link" id="switch-player">trocar</button>
    </div>
    <div class="title-actions"><button class="btn-3d" id="go">▶ Jogar</button><button class="btn-3d sun" id="show-ranking">🏆 Ranking</button></div>
    ${save.unlocked>1||save.points>0?'<button class="small-link" id="reset">reiniciar progresso deste jogador</button>':''}`;
  root.appendChild(s);
  s.insertBefore(owl(), s.firstChild);
  $("#go").onclick=map;
  $("#show-ranking").onclick=ranking;
  $("#switch-player").onclick=choosePlayer;
  const rs=$("#reset"); if(rs)rs.onclick=()=>{
    if(confirm(`Reiniciar todo o progresso de ${save.name}?`)){
      Object.assign(save,freshProgress());persist();title();
    }
  };
}

/* ---------- MAP ---------- */
function totalStars(){return Object.values(save.stars).reduce((a,b)=>a+b,0);}
function map(){
  root.innerHTML="";
  const s=document.createElement("div"); s.className="screen";
  const firstLocked = PHASES.findIndex(p=>p.id>=save.unlocked);
  s.innerHTML=`
    <div class="map-head">
      <div class="player-badge"><span>${save.avatar}</span>${esc(save.name)}</div>
      <div class="scorepill" aria-label="${totalStars()} de ${PHASES.length*3} estrelas"><span class="star" aria-hidden="true">★</span> ${totalStars()}/${PHASES.length*3}</div>
    </div>
    <h2>Escolha a fase</h2>
    <div class="trail">
      <svg class="trail-line" width="120" viewBox="0 0 120 ${PHASES.length*100}" preserveAspectRatio="none">
        <path d="${trailPath()}" fill="none" stroke="#ffffff" stroke-width="8" stroke-linecap="round" stroke-dasharray="2 16" opacity=".8"/>
      </svg>
      <div class="nodes" id="nodes"></div>
    </div>`;
  root.appendChild(s);
  const nodes=$("#nodes");
  PHASES.forEach(p=>{
    const locked=p.id>=save.unlocked;
    const st=save.stars[p.id]||0;
    const isCurrent=p.id===save.unlocked-1 && st===0 || p.id===save.unlocked && !locked;
    const n=document.createElement("div");
    n.className="node"+(locked?" locked-node":"")+(p.id===firstUnlockedPlayable()?" current":"");
    n.setAttribute("role","button");
    n.tabIndex=0;
    n.setAttribute("aria-disabled",String(locked));
    n.setAttribute("aria-label",`Fase ${p.id+1}: ${p.name}. ${locked?'Bloqueada':`${st} de 3 estrelas`}`);
    n.innerHTML=`
      <div class="bubble ${locked?'locked':p.color}"><span>${p.icon}</span></div>
      <div class="meta">
        <div class="ph">Fase ${p.id+1}</div>
        <div class="nm">${p.name}</div>
        <div class="stars" aria-hidden="true">${[0,1,2].map(i=>`<span class="s ${i<st?'on':''}">★</span>`).join("")}</div>
      </div>`;
    const activate=()=>locked?wiggle(n):startPhase(p.id);
    n.onclick=activate;
    n.onkeydown=e=>{if(e.key==="Enter"||e.key===" "){e.preventDefault();activate();}};
    nodes.appendChild(n);
  });
}
function firstUnlockedPlayable(){
  for(const p of PHASES){ if(p.id<save.unlocked && (save.stars[p.id]||0)<3) return p.id; }
  return Math.min(save.unlocked, PHASES.length-1);
}
function trailPath(){
  let d=`M60 20`; for(let i=1;i<PHASES.length;i++){const y=i*100+20;const x=i%2?100:20;d+=` Q60 ${y-50} ${x} ${y}`;}
  return d;
}
function wiggle(n){n.animate([{transform:'translateX(0)'},{transform:'translateX(-6px)'},{transform:'translateX(6px)'},{transform:'translateX(0)'}],{duration:300});}

/* ---------- QUIZ ---------- */
function startPhase(id){
  cur={phase:id,qi:0,correct:0,answered:false,startedAt:Date.now()};
  quiz();
}
function quiz(){
  const p=PHASES[cur.phase]; const item=p.q[cur.qi];
  // shuffle options, remember correct
  const idx=item.o.map((_,i)=>i);
  for(let i=idx.length-1;i>0;i--){const j=Math.floor(Math.random()*(i+1));[idx[i],idx[j]]=[idx[j],idx[i]];}
  cur.order=idx; cur.answered=false;
  const prog=((cur.qi)/p.q.length)*100;
  root.innerHTML="";
  const s=document.createElement("div"); s.className="screen";
  s.innerHTML=`
    <div class="qtop">
      <button class="back" id="back" aria-label="Voltar ao mapa">‹</button>
      <div class="pbar" role="progressbar" aria-label="Progresso da fase" aria-valuemin="0" aria-valuemax="${p.q.length}" aria-valuenow="${cur.qi}"><i style="width:${prog}%"></i></div>
      <div class="hearts" id="hearts" aria-label="${cur.correct} acertos até agora"></div>
    </div>
    <div class="qbanner"><span class="ic">${p.icon}</span><div class="t">Fase ${p.id+1}<b>${p.name}</b></div><div class="player-badge" style="margin-left:auto"><span>${save.avatar}</span>${esc(save.name)}</div></div>
    <div class="qcard">
      <div class="qmascot" id="qm"></div>
      <div class="qnum">Pergunta ${cur.qi+1} de ${p.q.length}</div>
      <div class="qtext" id="question-text">${item.q}</div>
      <div class="opts" id="opts" role="group" aria-labelledby="question-text"></div>
      <div class="feedback" id="fb" role="status" aria-live="polite"></div>
      <div class="next-wrap hidden" id="nextwrap"><button class="btn-3d blue" id="next">Continuar ▸</button></div>
    </div>`;
  root.appendChild(s);
  $("#qm").appendChild(owl());
  const hearts=$("#hearts");
  for(let i=0;i<p.q.length;i++) hearts.innerHTML+=`<span>${i<cur.correct?'💚':(i<cur.qi?'🩶':'🤍')}</span>`;
  const opts=$("#opts"); const letters=["A","B","C","D"];
  cur.order.forEach((origIndex,pos)=>{
    const b=document.createElement("button");
    b.className="opt"; b.innerHTML=`<span class="kbd">${letters[pos]}</span><span>${item.o[origIndex]}</span>`;
    b.onclick=()=>answer(b,origIndex===item.a);
    opts.appendChild(b);
  });
  $("#back").onclick=map;
}
function answer(btn,isRight){
  if(cur.answered)return; cur.answered=true;
  const p=PHASES[cur.phase]; const item=p.q[cur.qi];
  $$(".opt").forEach(o=>o.disabled=true);
  const qm=$("#qm .owl");
  if(isRight){
    btn.classList.add("correct"); cur.correct++;
    if(qm){qm.classList.add("happy");}
    burst(6);
  }else{
    btn.classList.add("wrong");
    // reveal the correct one
    $$(".opt").forEach((o,pos)=>{ if(cur.order[pos]===item.a) o.classList.add("correct"); });
    if(qm){qm.classList.add("sad"); $$(".brow",qm).forEach(b=>b.classList.remove("hidden"));}
  }
  $$(".opt").forEach(o=>{ if(!o.classList.contains("correct")&&!o.classList.contains("wrong")) o.classList.add("dim"); });
  const fb=$("#fb");
  fb.className="feedback show "+(isRight?"ok":"no");
  fb.innerHTML=`<div class="fh">${isRight?"✅ Isso mesmo!":"💡 Quase! Veja só:"}</div>
    <div class="fx">${item.fx}</div>${item.law?`<span class="law">📌 ${item.law}</span>`:""}`;
  // update hearts
  const hearts=$("#hearts"); hearts.innerHTML="";
  for(let i=0;i<p.q.length;i++){ let ic = i<cur.correct?'💚' : (i<=cur.qi?'🩶':'🤍'); hearts.innerHTML+=`<span>${ic}</span>`; }
  $("#nextwrap").classList.remove("hidden");
  const last = cur.qi>=p.q.length-1;
  $("#next").textContent = last?"Ver resultado ▸":"Continuar ▸";
  $("#next").onclick=()=>{ if(last){phaseResult();} else {cur.qi++;quiz();} };
}

/* ---------- PHASE RESULT ---------- */
function phaseResult(){
  const p=PHASES[cur.phase];
  const total=p.q.length; const got=cur.correct;
  let stars = got===total?3 : got>=Math.ceil(total*0.6)?2 : got>=1?1:0;
  if(got===0)stars=0;
  if(!save.completedAt&&cur.startedAt) save.elapsedMs=(save.elapsedMs||0)+Math.max(0,Date.now()-cur.startedAt);
  const prev=save.stars[p.id]||0;
  if(stars>prev)save.stars[p.id]=stars;
  const prevCorrect=save.bestCorrects[p.id]||0;
  if(got>prevCorrect){save.bestCorrects[p.id]=got;save.points=(save.points||0)+(got-prevCorrect)*10;}
  // unlocked = how many phases are open (ids 0..unlocked-1). Clearing phase p.id
  // with at least 1 star opens the next one, so unlocked must reach p.id+2.
  if(stars>=1) save.unlocked=Math.min(PHASES.length, Math.max(save.unlocked, p.id+2));
  persist();
  if(stars>=2) bigConfetti();
  const allDone = PHASES.every(ph=>(save.stars[ph.id]||0)>=1);
  if(allDone&&!save.completedAt){save.completedAt=Date.now();persist();}
  root.innerHTML="";
  const s=document.createElement("div"); s.className="screen result";
  const msgs=["Continue tentando — cada erro ensina!","Muito bem! Já sabe bastante.","Excelente! Você mandou muito bem!","PERFEITO! Você é um expert nessa fase! 🌟"];
  s.innerHTML=`
    <h2>${stars>=2?"Fase concluída!":"Boa tentativa!"}</h2>
    <div class="big-stars">${[0,1,2].map(i=>`<span class="bs ${i<stars?'on':''}">★</span>`).join("")}</div>
    <div class="rscore">✅ ${got} de ${total} certas · recorde ${save.points}/${MAX_POINTS} pontos</div>
    <p class="msg">${msgs[stars]}</p>
    <div class="actions">
      <button class="btn-3d ghost" id="retry">↻ Refazer</button>
      ${allDone?'<button class="btn-3d sun" id="cert">🏆 Meu diploma</button>':`<button class="btn-3d" id="cont">${cur.phase<PHASES.length-1?'Próxima fase ▸':'Ver mapa ▸'}</button>`}
    </div>
    <button class="small-link" id="tomap">voltar ao mapa</button>`;
  root.appendChild(s);
  s.insertBefore(owl(stars>=2?"happy":""), s.firstChild);
  $("#retry").onclick=()=>startPhase(p.id);
  $("#tomap").onclick=map;
  const cont=$("#cont"); if(cont)cont.onclick=()=>{ if(cur.phase<PHASES.length-1 && (save.unlocked>cur.phase+1||stars>=1)){startPhase(cur.phase+1);} else {map();} };
  const cert=$("#cert"); if(cert)cert.onclick=finalCert;
}

/* ---------- FINAL ---------- */
function finalCert(){
  bigConfetti();
  root.innerHTML="";
  const s=document.createElement("div"); s.className="screen";
  s.innerHTML=`
    <div class="cert">
      <div class="seal">${save.avatar}</div>
      <h2>Diploma dos Direitos</h2>
      <p>Este certificado reconhece que</p>
      <div class="name">${esc(save.name)} concluiu a Trilha dos Direitos!</div>
      <p><strong>Recorde:</strong> ${totalStars()}/${MAX_STARS} estrelas · ${save.points}/${MAX_POINTS} pontos · ${formatTime(save.elapsedMs)}</p>
      <p>Agora você conhece os seus direitos no trabalho e na aprendizagem:</p>
      <ul>
        <li>Só se trabalha a partir dos 14 (aprendiz) ou 16 anos</li>
        <li>Carteira assinada e contrato protegem você</li>
        <li>13º, férias e FGTS são direitos seus</li>
        <li>Estudar sempre vem primeiro</li>
        <li>Trabalho noturno e perigoso é proibido pra menor de 18</li>
        <li>Disque 100 para denunciar e proteger</li>
      </ul>
      <div class="actions" style="display:flex;gap:10px;justify-content:center;margin-top:20px;flex-wrap:wrap">
        <button class="btn-3d ghost" id="tomap2">Voltar ao mapa</button>
        <button class="btn-3d sun" id="final-rank">🏆 Ver ranking</button>
        <button class="btn-3d" id="next-player">Próximo jogador</button>
      </div>
    </div>`;
  root.appendChild(s);
  $("#tomap2").onclick=map;
  $("#final-rank").onclick=ranking;
  $("#next-player").onclick=choosePlayer;
}

/* ---------- confetti ---------- */
function burst(n){
  const box=$("#confetti"); box.classList.remove("hidden");
  const cols=["#ffcb3d","#57b85f","#3d8bd4","#ff6b5e","#8a6cf0"];
  for(let i=0;i<n;i++){
    const p=document.createElement("i");
    p.style.left=(40+Math.random()*20)+"%"; p.style.background=cols[i%cols.length];
    p.style.animationDuration=(1+Math.random()*.8)+"s"; p.style.top="30%";
    box.appendChild(p); setTimeout(()=>p.remove(),1800);
  }
}
function bigConfetti(){
  const box=$("#confetti"); box.classList.remove("hidden");
  const cols=["#ffcb3d","#57b85f","#3d8bd4","#ff6b5e","#8a6cf0"];
  for(let i=0;i<60;i++){
    const p=document.createElement("i");
    p.style.left=Math.random()*100+"%"; p.style.background=cols[i%cols.length];
    p.style.animationDuration=(1.6+Math.random()*1.6)+"s"; p.style.animationDelay=(Math.random()*.4)+"s";
    box.appendChild(p); setTimeout(()=>p.remove(),3600);
  }
}

title();
</script>
</body>
</html>
