<!DOCTYPE html>
<html lang="fr">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>SENATE · Texas · 2026</title>
  <style>
    * { margin: 0; padding: 0; box-sizing: border-box; }
    body {
      min-height: 100vh; width: 100%;
      font-family: 'Segoe UI', 'Roboto', system-ui, sans-serif;
      display: flex; flex-direction: column; align-items: center;
      background: linear-gradient(to right, #0a1f3a 0%, #000000 50%, #8b1a1a 100%);
      background-attachment: fixed; padding: 20px;
    }
    .back-link { color: rgba(255,255,255,0.6); text-decoration: none; margin-bottom: 15px; display: block; }
    .back-link:hover { color: white; }
    .senate-header {
      width: 100%; max-width: 1200px;
      background: rgba(5,10,20,0.65); backdrop-filter: blur(12px); -webkit-backdrop-filter: blur(12px);
      padding: 1.6rem 2rem; text-align: center;
      box-shadow: 0 10px 30px rgba(0,0,0,0.6); border-bottom: 1px solid rgba(210,180,140,0.2); margin-bottom: 30px;
    }
    .senate-main { font-size: clamp(3rem,10vw,6rem); font-weight:900; letter-spacing:0.28em; text-transform:uppercase; color:#fff; text-shadow:0 4px 20px rgba(0,0,0,0.8); }
    .senate-sub { font-size:clamp(1.5rem,5vw,2.8rem); font-weight:400; letter-spacing:0.5em; text-transform:uppercase; color:rgba(255,255,255,0.95); border-top:1.5px solid rgba(255,215,150,0.5); display:inline-block; padding-top:0.7rem; margin-top:0.2rem; }
    .main-content { width:100%; max-width:1200px; display:flex; flex-direction:column; gap:2rem; }
    .card { width:100%; background:rgba(0,0,0,0.35); backdrop-filter:blur(8px); border:1px solid rgba(220,200,180,0.18); box-shadow:0 25px 40px -10px rgba(0,0,0,0.7); padding:2rem; }
    .card-header { display:flex; align-items:center; justify-content:space-between; margin-bottom:2rem; border-bottom:2px solid rgba(255,255,255,0.15); padding-bottom:1.5rem; }
    .card-title { font-size:1.8rem; font-weight:600; letter-spacing:0.2em; text-transform:uppercase; color:#f0e6d2; }
    .texas-shape { width:130px; filter:drop-shadow(0 8px 14px rgba(0,0,0,0.6)); }
    .candidate-row { margin-bottom:2rem; }
    .candidate-label { display:flex; justify-content:space-between; margin-bottom:0.7rem; }
    .party-name { font-size:1.5rem; font-weight:700; letter-spacing:0.15em; text-transform:uppercase; }
    .party-percent { font-size:2rem; font-weight:800; }
    .republican .party-name { color:#ff9e8f; } .republican .party-percent { color:#ff6b5e; }
    .democrat .party-name { color:#8fc1ff; } .democrat .party-percent { color:#5a9cff; }
    .bar-wrapper { width:100%; height:45px; background:#121212e0; border:1px solid rgba(255,255,255,0.12); overflow:hidden; }
    .bar-fill { height:100%; display:flex; align-items:center; justify-content:flex-end; padding-right:20px; font-weight:700; color:white; }
    .bar-fill.rep-fill { background:linear-gradient(90deg,#a51c1c,#d32f2f); width:48%; }
    .bar-fill.dem-fill { background:linear-gradient(90deg,#0a3a7a,#1976d2); width:46%; }
    .poll-footer { margin-top:2rem; display:flex; justify-content:space-between; color:rgba(255,240,220,0.7); border-top:1px solid rgba(255,255,240,0.1); padding-top:1.4rem; }
    .toggle-section { display:flex; gap:1rem; margin-bottom:1.5rem; }
    .toggle-btn { background:rgba(0,0,0,0.4); border:1px solid rgba(255,255,255,0.2); color:white; padding:0.8rem 2rem; font-size:1rem; font-weight:600; text-transform:uppercase; cursor:pointer; flex:1; text-align:center; }
    .toggle-btn.active { background:rgba(255,255,255,0.15); border-color:rgba(255,215,150,0.6); }
    .section-panel { display:none; }
    .section-panel.active { display:block; }
    .primary-tabs { display:flex; gap:1rem; margin-bottom:1.5rem; }
    .tab-btn { background:rgba(0,0,0,0.4); border:1px solid rgba(255,255,255,0.2); color:white; padding:0.8rem 2rem; font-size:1.2rem; font-weight:600; text-transform:uppercase; cursor:pointer; flex:1; text-align:center; }
    .tab-btn.active { background:rgba(255,255,255,0.15); border-color:rgba(255,215,150,0.6); }
    .tab-btn.rep-tab.active { background:rgba(229,57,53,0.2); border-color:#e53935; }
    .tab-btn.dem-tab.active { background:rgba(30,136,229,0.2); border-color:#1e88e5; }
    .primary-panel { display:none; }
    .primary-panel.active { display:block; }
    .primary-grid { display:grid; grid-template-columns:repeat(auto-fit,minmax(200px,1fr)); gap:1.5rem; margin-bottom:1.5rem; }
    .candidate-card { background:rgba(0,0,0,0.3); border:1px solid rgba(255,255,255,0.1); padding:1.2rem; text-align:center; }
    .candidate-photo { width:70px; height:70px; border-radius:50%; margin:0 auto 0.8rem; background:#a51c1c; display:flex; align-items:center; justify-content:center; font-weight:bold; font-size:1.8rem; color:white; border:2px solid rgba(255,255,255,0.2); }
    .candidate-name { font-size:1.2rem; font-weight:700; color:white; }
    .candidate-desc { font-size:0.8rem; color:rgba(255,255,255,0.6); margin-bottom:0.5rem; }
    .candidate-score { font-size:2rem; font-weight:800; }
    .primary-rep .candidate-score { color:#ff9e8f; } .primary-dem .candidate-score { color:#8fc1ff; }
    .trend-badge { display:inline-block; padding:2px 8px; font-size:0.7rem; font-weight:600; text-transform:uppercase; }
    .trend-up { color:#4caf50; } .trend-down { color:#f44336; } .trend-stable { color:#ffc107; }
    .polls-table { width:100%; border-collapse:collapse; color:white; font-size:0.9rem; }
    .polls-table th { text-align:center; padding:10px 6px; background:rgba(0,0,0,0.4); font-weight:600; text-transform:uppercase; letter-spacing:1px; font-size:0.8rem; border-bottom:2px solid rgba(255,255,255,0.2); }
    .polls-table td { text-align:center; padding:8px 6px; border-bottom:1px solid rgba(255,255,255,0.08); }
    .polls-table .rep-value { color:#ff9e8f; font-weight:600; } .polls-table .dem-value { color:#8fc1ff; font-weight:600; }
    .polls-table .avg-row { background:rgba(0,0,0,0.3); font-weight:700; }
    .chart-container { position:relative; width:100%; height:300px; margin:1.5rem 0; }
    canvas { display:block; width:100%; height:100%; background:rgba(10,10,15,0.3); border:1px solid rgba(255,255,255,0.1); cursor:crosshair; }
    .chart-tooltip { position:absolute; background:rgba(20,20,30,0.95); color:white; padding:8px 12px; border:1px solid rgba(255,255,255,0.25); font-size:13px; font-weight:600; pointer-events:none; box-shadow:0 6px 20px rgba(0,0,0,0.6); z-index:100; text-align:center; line-height:1.4; white-space:nowrap; }
    .chart-legend { display:flex; justify-content:center; gap:2rem; margin-top:0.5rem; color:rgba(255,255,255,0.8); flex-wrap:wrap; }
    .legend-item { display:flex; align-items:center; gap:0.5rem; }
    .legend-dot { width:12px; height:12px; background:#e53935; opacity:0.7; } .legend-dot.dem { background:#1e88e5; }
    .legend-line { width:20px; height:3px; background:white; opacity:0.7; }
    @media (max-width:750px) { .senate-header { padding:1rem; } .card-header { flex-direction:column; } .texas-shape { width:100px; align-self:flex-end; } .chart-container { height:250px; } }
  </style>
</head>
<body>

<a href="index.html" class="back-link">← Retour à l'accueil</a>

<header class="senate-header">
  <div class="senate-main">SENATE</div>
  <div class="senate-sub">Texas</div>
</header>

<div class="main-content">

  <div class="toggle-section">
    <div class="toggle-btn active" data-section="general">Élection Générale</div>
    <div class="toggle-btn" data-section="primaries">Primaires</div>
  </div>

  <div class="section-panel active" id="section-general">
    <div class="card">
      <div class="card-header">
        <div class="card-title">Sénat 2026 · Texas</div>
        <div class="texas-shape">
          <svg viewBox="0 0 700 700" fill="none">
            <defs><linearGradient id="txGrad" x1="0%" y1="0%" x2="100%" y2="100%"><stop offset="0%" stop-color="#0a1f3a" stop-opacity="0.9"/><stop offset="50%" stop-color="#2a1a3a" stop-opacity="0.8"/><stop offset="100%" stop-color="#8b1a1a" stop-opacity="0.9"/></linearGradient></defs>
            <path d="m 573.98015,536.93549 -4.65902,-17.56842 0,3.30015 4.65902,14.26827 z m -1.06769,-30.86607 -3.30015,6.21204 -0.38825,2.03833 3.6884,-8.25037 z m 2.6207,-4.56196 3.10602,-4.07666 -2.23245,1.35889 -0.87357,2.71777 z m 10.96814,-9.90044 -7.27974,3.78546 2.03833,-0.38825 5.24141,-3.39721 z m 0.97063,-1.35889 2.03832,-1.65007 -0.7765,0.19413 -1.26182,1.45594 z m -115.11686,-162.87191 -0.67944,-0.0971 -3.30015,91.0452 -19.2185,-0.87357 -30.76901,-1.74713 -12.32701,-0.87357 2.42658,4.75609 0.0971,0.0971 10.48282,10.48281 6.01791,7.08561 7.95917,5.92085 5.62967,10.28869 2.13538,10.77401 4.56197,3.00895 3.59134,3.97959 5.14434,1.8442 7.47386,4.75609 3.39721,1.26183 4.65903,-4.65903 1.45595,-4.95022 2.42658,-4.7561 7.57092,-3.00895 2.91189,1.45594 8.44449,0.67945 7.66799,4.75609 5.24141,0.97063 -1.45595,2.71777 3.00896,1.94126 2.81483,3.39721 0.58238,3.59133 1.8442,2.42658 4.27077,10.28869 4.27078,3.59134 3.30015,5.43553 4.17371,4.27078 1.8442,0.58238 1.55301,11.06519 4.56197,2.52365 0.19412,3.49427 1.16476,-0.29119 7.95918,9.70631 3.97959,0.87357 5.04728,3.00896 7.76505,0 5.62966,3.10601 6.69735,-1.45594 -3.00895,-2.81483 -2.71777,-8.1533 -1.06769,-7.08561 -1.55301,-2.32952 0.67944,-4.75609 -2.03833,-0.19413 -2.71777,-4.4649 3.10602,3.30015 3.59134,-1.26182 1.94126,-5.14435 -3.88252,-5.24141 5.82378,0.67944 2.71777,-4.17371 -0.38825,-1.45595 2.42658,-3.20308 -0.58238,2.81483 2.71777,-2.13539 -1.0677,-3.78546 3.49427,1.8442 4.46491,-2.52364 -4.36784,-4.56197 2.71776,1.0677 5.04729,0.29119 6.60029,-1.45595 7.3768,-4.95022 4.4649,-3.6884 0.67944,-2.71777 2.71777,-2.81483 -1.45595,-4.65903 0.29119,-2.91189 4.85316,-2.13539 -0.38826,5.14435 2.9119,0 -3.20308,2.71776 12.90939,-6.79441 2.13539,-0.0971 1.35888,-6.21204 0.38826,0 1.45594,-3.59133 0.67944,-11.0652 0.87357,-4.4649 -2.52364,-7.95918 -3.10602,-5.43553 -0.0971,-2.62071 -3.20309,-4.4649 -1.94126,-18.73318 -0.0971,-2.32952 -0.19413,-2.42658 -0.58238,-8.54155 -5.82378,0.19413 -1.45595,-1.55301 -0.29119,-0.0971 -0.0971,0 -3.78546,-0.67944 -4.36784,-2.81483 -4.85316,-2.03832 -9.12393,2.6207 -2.42658,-0.58238 -3.00896,1.16476 -3.6884,3.00895 -9.90044,-4.65902 -3.10601,4.27077 -4.56197,-1.65007 -4.85316,-3.10602 -2.6207,2.23245 -2.52364,0.0971 0,-1.84419 -6.79442,-3.20309 -2.71777,1.26182 -1.35888,-1.55301 -7.47386,-0.7765 -5.72673,-5.24141 -0.87356,1.74714 -4.17372,-0.19413 -3.88252,-3.6884 -1.74714,-5.82379 -0.29119,-33.19558 -24.84816,-0.29119 -23.48927,-0.58238 -0.58238,0 z" fill="url(#txGrad)" stroke="rgba(255,235,200,0.7)" stroke-width="3"/>
          </svg>
        </div>
      </div>
      <div class="candidate-row republican">
        <div class="candidate-label"><span class="party-name">John Cornyn (R)</span><span class="party-percent" id="repFinal">48%</span></div>
        <div class="bar-wrapper"><div class="bar-fill rep-fill" id="repBar">48%</div></div>
      </div>
      <div class="candidate-row democrat">
        <div class="candidate-label"><span class="party-name">James Talarico (D)</span><span class="party-percent" id="demFinal">46%</span></div>
        <div class="bar-wrapper"><div class="bar-fill dem-fill" id="demBar">46%</div></div>
      </div>
      <div class="poll-footer">
        <span>Marge d'erreur ±3.2%</span>
        <span>2 814 LV · 12-15 Sep 2026</span>
      </div>
    </div>

    <div class="card">
      <div class="card-header"><div class="card-title">📈 Évolution des sondages</div></div>
      <div class="chart-container">
        <canvas id="pollChart" width="800" height="300"></canvas>
        <div class="chart-tooltip" id="chartTooltip" style="opacity:0;"></div>
      </div>
      <div class="chart-legend">
        <div class="legend-item"><span class="legend-dot"></span> Cornyn (R)</div>
        <div class="legend-item"><span class="legend-dot dem"></span> Talarico (D)</div>
        <div class="legend-item"><span class="legend-line" style="background:#ff8a7a;"></span> Moyenne R</div>
        <div class="legend-item"><span class="legend-line" style="background:#8fc1ff;"></span> Moyenne D</div>
      </div>
    </div>
  </div>

  <div class="section-panel" id="section-primaries">
    <div class="card">
      <div class="card-header"><div class="card-title">Primaires · 4 mars 2026</div></div>
      <div class="primary-tabs">
        <div class="tab-btn rep-tab active" data-tab="rep">Primaire Républicaine</div>
        <div class="tab-btn dem-tab" data-tab="dem">Primaire Démocrate</div>
      </div>
      <div class="primary-panel active" id="panel-rep">
        <div class="primary-grid">
          <div class="candidate-card"><div class="candidate-photo">JC</div><div class="candidate-name">John Cornyn</div><div class="candidate-desc">Sénateur sortant</div><div class="candidate-score">40%</div><span class="trend-badge trend-down">▼ Second tour</span></div>
          <div class="candidate-card"><div class="candidate-photo" style="background:#8b1a1a;">KP</div><div class="candidate-name">Ken Paxton</div><div class="candidate-desc">Procureur général</div><div class="candidate-score">48.8%</div><span class="trend-badge trend-up">▲ Second tour</span></div>
        </div>
        <p style="color:rgba(255,255,255,0.5);font-size:0.85rem;text-align:center;">Second tour républicain : 26 mai 2026</p>
      </div>
      <div class="primary-panel" id="panel-dem">
        <div class="primary-grid">
          <div class="candidate-card"><div class="candidate-photo" style="background:#0a3a7a;">JT</div><div class="candidate-name">James Talarico</div><div class="candidate-desc">Représentant d'État</div><div class="candidate-score">53.1%</div><span class="trend-badge trend-up">🏆 Vainqueur</span></div>
          <div class="candidate-card"><div class="candidate-photo" style="background:#1a5a9a;">JC</div><div class="candidate-name">Jasmine Crockett</div><div class="candidate-desc">Représentante (TX-30)</div><div class="candidate-score">45.6%</div><span class="trend-badge trend-down">Battue</span></div>
        </div>
        <p style="color:rgba(255,255,255,0.5);font-size:0.85rem;text-align:center;">James Talarico est le candidat démocrate pour novembre 2026</p>
      </div>
    </div>
  </div>

</div>

<script>
  (function() {
    document.querySelectorAll('.toggle-btn').forEach(btn => {
      btn.addEventListener('click', function() {
        const target = this.dataset.section;
        document.querySelectorAll('.toggle-btn').forEach(b => b.classList.remove('active'));
        this.classList.add('active');
        document.getElementById('section-general').classList.toggle('active', target==='general');
        document.getElementById('section-primaries').classList.toggle('active', target==='primaries');
      });
    });
    document.querySelectorAll('.tab-btn').forEach(tab => {
      tab.addEventListener('click', function() {
        const target = this.dataset.tab;
        document.querySelectorAll('.tab-btn').forEach(t => t.classList.remove('active'));
        this.classList.add('active');
        document.getElementById('panel-rep').classList.toggle('active', target==='rep');
        document.getElementById('panel-dem').classList.toggle('active', target==='dem');
      });
    });
    // Graphique (comme avant)
    const canvas = document.getElementById('pollChart');
    if(!canvas) return;
    const ctx = canvas.getContext('2d');
    const tooltip = document.getElementById('chartTooltip');
    const polls = [
      { date: 'Jan', rep: 47, dem: 44 }, { date: 'Fév', rep: 44, dem: 43 },
      { date: 'Mar', rep: 44, dem: 43 }, { date: 'Avr', rep: 45, dem: 44 },
      { date: 'Mai', rep: 47, dem: 42 }, { date: 'Jun', rep: 46, dem: 44 },
      { date: 'Jul', rep: 44, dem: 44 }, { date: 'Aoû', rep: 47, dem: 45 },
      { date: 'Sep', rep: 48, dem: 46 }
    ];
    const repAvg = [], demAvg = [];
    for(let i=0;i<polls.length;i++) {
      let sR=0,sD=0,c=0;
      for(let j=Math.max(0,i-2);j<=i;j++) { sR+=polls[j].rep; sD+=polls[j].dem; c++; }
      repAvg.push(Math.round((sR/c)*10)/10); demAvg.push(Math.round((sD/c)*10)/10);
    }
    const last = polls[polls.length-1];
    document.getElementById('repFinal').textContent = last.rep+'%';
    document.getElementById('demFinal').textContent = last.dem+'%';
    document.getElementById('repBar').style.width = last.rep+'%';
    document.getElementById('repBar').textContent = last.rep+'%';
    document.getElementById('demBar').style.width = last.dem+'%';
    document.getElementById('demBar').textContent = last.dem+'%';
    const pad={top:30,right:40,bottom:40,left:45}, minY=35, maxY=55;
    let points=[];
    function draw() {
      const w=canvas.width,h=canvas.height, cW=w-pad.left-pad.right, cH=h-pad.top-pad.bottom;
      ctx.clearRect(0,0,w,h);
      ctx.fillStyle='rgba(10,10,18,0.5)'; ctx.fillRect(pad.left,pad.top,cW,cH);
      const gX=i=>pad.left+(i/(polls.length-1))*cW, gY=v=>pad.top+cH-((v-minY)/(maxY-minY))*cH;
      ctx.strokeStyle='rgba(255,255,255,0.08)'; ctx.lineWidth=0.8;
      for(let i=minY;i<=maxY;i+=5){const y=gY(i);ctx.beginPath();ctx.moveTo(pad.left,y);ctx.lineTo(pad.left+cW,y);ctx.stroke();ctx.fillStyle='rgba(255,255,255,0.5)';ctx.font='11px Segoe UI';ctx.textAlign='right';ctx.fillText(i+'%',pad.left-8,y);}
      polls.forEach((p,i)=>ctx.fillText(p.date,gX(i),pad.top+cH+8));
      [{d:repAvg,c:'#ff8a7a'},{d:demAvg,c:'#8fc1ff'}].forEach(l=>{ctx.beginPath();ctx.moveTo(gX(0),gY(l.d[0]));for(let i=1;i<l.d.length;i++){const xc=gX(i),yc=gY(l.d[i]),xp=gX(i-1),yp=gY(l.d[i-1]);ctx.bezierCurveTo(xp+(xc-xp)*0.5,yp,xc-(xc-xp)*0.5,yc,xc,yc);}ctx.strokeStyle=l.c;ctx.lineWidth=3;ctx.stroke();});
      points=[];
      polls.forEach((p,i)=>{const x=gX(i),y=gY(p.rep);points.push({x,y,type:'rep',value:p.rep,date:p.date});ctx.beginPath();ctx.arc(x,y,7,0,2*Math.PI);ctx.fillStyle='rgba(180,40,40,0.4)';ctx.fill();ctx.strokeStyle='rgba(255,255,255,0.25)';ctx.stroke();});
      polls.forEach((p,i)=>{const x=gX(i),y=gY(p.dem);points.push({x,y,type:'dem',value:p.dem,date:p.date});ctx.beginPath();ctx.arc(x,y,7,0,2*Math.PI);ctx.fillStyle='rgba(30,80,180,0.4)';ctx.fill();ctx.strokeStyle='rgba(255,255,255,0.25)';ctx.stroke();});
    }
    draw();
    canvas.addEventListener('mousemove', function(e) {
      const rect=canvas.getBoundingClientRect(), sX=canvas.width/rect.width, sY=canvas.height/rect.height;
      const mx=(e.clientX-rect.left)*sX, my=(e.clientY-rect.top)*sY;
      let cl=null,md=25;
      points.forEach(p=>{const d=Math.hypot(mx-p.x,my-p.y);if(d<md){md=d;cl=p;}});
      if(cl){tooltip.innerHTML='<strong>'+(cl.type==='rep'?'John Cornyn (R)':'James Talarico (D)')+'</strong><br><span style="color:'+(cl.type==='rep'?'#ff9e8f':'#8fc1ff')+';font-size:16px;">'+cl.value+'%</span><br><span style="opacity:0.7;">'+cl.date+' 2026</span>';tooltip.style.left=Math.max(5,Math.min(cl.x/sX-60,rect.width-120))+'px';tooltip.style.top=Math.max(5,cl.y/sY-60)+'px';tooltip.style.opacity='1';}
      else { tooltip.style.opacity='0'; }
    });
    canvas.addEventListener('mouseleave',()=>tooltip.style.opacity='0');
  })();
</script>

<div style="height:20px;"></div>
</body>
</html>
