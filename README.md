<!DOCTYPE html>
<html lang="fr">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Election USA 2026 · House, Senate & Gubernatorial</title>
  <style>
    * { margin: 0; padding: 0; box-sizing: border-box; }
    body {
      min-height: 100vh; width: 100%;
      font-family: 'Segoe UI', 'Roboto', system-ui, sans-serif;
      display: flex; flex-direction: column; align-items: center;
      background: linear-gradient(to right, #0a1f3a 0%, #000000 50%, #8b1a1a 100%);
      background-attachment: fixed; padding: 20px;
    }
    .main-header {
      width: 100%; max-width: 1400px;
      background: rgba(5,10,20,0.7); backdrop-filter: blur(12px);
      padding: 1.5rem 2rem; text-align: center; margin-bottom: 25px;
      box-shadow: 0 10px 30px rgba(0,0,0,0.6); border-bottom: 1px solid rgba(210,180,140,0.2);
    }
    .main-title { font-size: clamp(1.8rem,5vw,3.5rem); font-weight:900; letter-spacing:0.2em; color:#fff; text-transform:uppercase; }
    .main-subtitle { font-size:clamp(0.9rem,2.5vw,1.5rem); color:rgba(255,255,255,0.85); letter-spacing:0.3em; text-transform:uppercase; border-top:1.5px solid rgba(255,215,150,0.5); display:inline-block; padding-top:0.6rem; margin-top:0.4rem; }
    .main-content { width:100%; max-width:1400px; }

    .category-tabs { display:flex; gap:0.5rem; margin-bottom:1.5rem; flex-wrap:wrap; }
    .cat-tab { background:rgba(0,0,0,0.4); border:1px solid rgba(255,255,255,0.2); color:white; padding:0.9rem 1.2rem; font-size:1rem; font-weight:700; text-transform:uppercase; letter-spacing:0.1em; cursor:pointer; flex:1; min-width:130px; text-align:center; transition:all 0.2s; }
    .cat-tab:hover { background:rgba(255,255,255,0.1); }
    .cat-tab.active { background:rgba(255,255,255,0.15); border-color:rgba(255,215,150,0.6); box-shadow:0 0 20px rgba(255,215,150,0.2); }
    .cat-panel { display:none; }
    .cat-panel.active { display:block; }

    .race-list { display:flex; flex-direction:column; gap:0.8rem; margin-bottom:1.5rem; }
    .race-item { background:rgba(0,0,0,0.35); border:1px solid rgba(220,200,180,0.18); padding:0.9rem 1.2rem; cursor:pointer; transition:all 0.2s; display:flex; justify-content:space-between; align-items:center; flex-wrap:wrap; gap:0.8rem; }
    .race-item:hover { background:rgba(255,255,255,0.08); border-color:rgba(255,215,150,0.4); }
    .race-item.active { background:rgba(255,255,255,0.12); border-color:rgba(255,215,150,0.7); box-shadow:0 0 25px rgba(255,215,150,0.15); }
    .race-info h3 { color:#f0e6d2; font-size:1.1rem; margin-bottom:0.2rem; }
    .race-info p { color:rgba(255,255,255,0.5); font-size:0.8rem; }
    .race-rating-badge { padding:0.25rem 0.8rem; font-weight:700; text-transform:uppercase; font-size:0.7rem; letter-spacing:0.1em; white-space:nowrap; }
    .badge-tossup { background:rgba(255,200,0,0.2); color:#ffc107; border:1px solid #ffc107; }
    .badge-lean-r { background:rgba(229,57,53,0.2); color:#ff9e8f; border:1px solid #e53935; }
    .badge-lean-d { background:rgba(30,136,229,0.2); color:#8fc1ff; border:1px solid #1e88e5; }
    .badge-likely-r { background:rgba(229,57,53,0.3); color:#ff6b5e; border:1px solid #d32f2f; }
    .badge-likely-d { background:rgba(30,136,229,0.3); color:#64b5f6; border:1px solid #1976d2; }
    .badge-safe-r { background:rgba(229,57,53,0.4); color:#ff8a80; border:1px solid #b71c1c; }
    .badge-safe-d { background:rgba(30,136,229,0.4); color:#82b1ff; border:1px solid #0d47a1; }

    .card { width:100%; background:rgba(0,0,0,0.35); backdrop-filter:blur(8px); border:1px solid rgba(220,200,180,0.18); box-shadow:0 20px 35px -8px rgba(0,0,0,0.6); padding:1.5rem; margin-bottom:1.2rem; }
    .card-header { display:flex; align-items:center; justify-content:space-between; margin-bottom:1.5rem; border-bottom:2px solid rgba(255,255,255,0.15); padding-bottom:1.2rem; flex-wrap:wrap; gap:1rem; }
    .card-title { font-size:1.4rem; font-weight:600; letter-spacing:0.12em; text-transform:uppercase; color:#f0e6d2; }
    .candidate-row { margin-bottom:1.5rem; }
    .candidate-label { display:flex; justify-content:space-between; margin-bottom:0.5rem; flex-wrap:wrap; gap:0.4rem; }
    .party-name { font-size:1.1rem; font-weight:700; letter-spacing:0.08em; text-transform:uppercase; }
    .party-percent { font-size:1.5rem; font-weight:800; }
    .rep { color:#ff9e8f; } .dem { color:#8fc1ff; }
    .cand-desc-small { color:rgba(255,255,255,0.45); font-size:0.75rem; margin-bottom:0.4rem; }
    .bar-wrapper { width:100%; height:35px; background:#121212e0; border:1px solid rgba(255,255,255,0.12); overflow:hidden; }
    .bar-fill { height:100%; display:flex; align-items:center; justify-content:flex-end; padding-right:15px; font-weight:700; color:white; font-size:0.9rem; }
    .bar-fill.rep-fill { background:linear-gradient(90deg, #a51c1c, #d32f2f); }
    .bar-fill.dem-fill { background:linear-gradient(90deg, #0a3a7a, #1976d2); }
    .poll-footer { margin-top:1.2rem; display:flex; justify-content:space-between; color:rgba(255,240,220,0.7); border-top:1px solid rgba(255,255,240,0.1); padding-top:1rem; flex-wrap:wrap; gap:0.4rem; font-size:0.8rem; }

    .projections-bar { display:flex; height:10px; margin:0.8rem 0; background:#121212; }
    .proj-r-safe { background:#4a0000; } .proj-r-likely { background:#7a0000; } .proj-r-lean { background:#a51c1c; }
    .proj-tossup { background:#5a4a00; } .proj-d-lean { background:#1565c0; } .proj-d-likely { background:#0a3a7a; }
    .projections-legend { display:flex; justify-content:space-between; font-size:0.6rem; color:rgba(255,255,255,0.35); margin-bottom:0.8rem; flex-wrap:wrap; }
    .seats-projection { text-align:center; color:rgba(255,255,255,0.55); font-size:0.85rem; margin:0.8rem 0; }

    .primary-tabs { display:flex; gap:0.5rem; margin-bottom:1.2rem; }
    .prim-tab { background:rgba(0,0,0,0.4); border:1px solid rgba(255,255,255,0.2); color:white; padding:0.6rem 1rem; font-size:0.9rem; font-weight:600; text-transform:uppercase; cursor:pointer; flex:1; text-align:center; transition:all 0.2s; }
    .prim-tab.active { background:rgba(255,255,255,0.15); border-color:rgba(255,215,150,0.6); }
    .prim-tab.r-active { background:rgba(229,57,53,0.2); border-color:#e53935; }
    .prim-tab.d-active { background:rgba(30,136,229,0.2); border-color:#1e88e5; }
    .prim-panel { display:none; }
    .prim-panel.active { display:block; }
    .primary-grid { display:grid; grid-template-columns:repeat(auto-fit, minmax(180px, 1fr)); gap:1rem; margin-bottom:1.5rem; }
    .candidate-card { background:rgba(0,0,0,0.3); border:1px solid rgba(255,255,255,0.1); padding:1.2rem; text-align:center; }
    .candidate-card.winner { border-color:rgba(255,215,150,0.4); }
    .cand-photo { width:55px; height:55px; border-radius:50%; margin:0 auto 0.6rem; display:flex; align-items:center; justify-content:center; font-weight:bold; font-size:1.4rem; color:white; border:2px solid rgba(255,255,255,0.2); }
    .cand-photo.r { background:#a51c1c; } .cand-photo.d { background:#0a3a7a; }
    .cand-name { font-size:1rem; font-weight:700; color:white; }
    .cand-desc { font-size:0.7rem; color:rgba(255,255,255,0.5); margin-bottom:0.4rem; }
    .cand-score { font-size:1.6rem; font-weight:800; } .cand-score.r { color:#ff9e8f; } .cand-score.d { color:#8fc1ff; }
    .cand-badge { display:inline-block; padding:2px 8px; font-size:0.65rem; font-weight:700; text-transform:uppercase; letter-spacing:0.04em; }
    .badge-winner { background:rgba(255,215,0,0.2); color:#ffd700; border:1px solid #ffd700; }
    .badge-runoff { background:rgba(255,152,0,0.2); color:#ff9800; border:1px solid #ff9800; }
    .badge-eliminated { background:rgba(158,158,158,0.2); color:#9e9e9e; border:1px solid #9e9e9e; }
    .badge-qualified { background:rgba(76,175,80,0.2); color:#4caf50; border:1px solid #4caf50; }
    .primary-note { color:rgba(255,255,255,0.5); font-size:0.75rem; text-align:center; margin-top:0.8rem; font-style:italic; }
    .primary-table { width:100%; border-collapse:collapse; color:white; font-size:0.8rem; margin-bottom:1.2rem; }
    .primary-table th { text-align:center; padding:8px 6px; background:rgba(0,0,0,0.4); font-weight:600; text-transform:uppercase; letter-spacing:0.5px; font-size:0.7rem; border-bottom:2px solid rgba(255,255,255,0.15); }
    .primary-table td { text-align:center; padding:7px 6px; border-bottom:1px solid rgba(255,255,255,0.06); }
    .primary-table .r-col { color:#ff9e8f; } .primary-table .d-col { color:#8fc1ff; }
    .primary-table .highlight-row { background:rgba(0,0,0,0.3); font-weight:600; }

    .chart-container { position:relative; width:100%; height:260px; margin:0.8rem 0; }
    canvas { display:block; width:100%; height:100%; background:rgba(10,10,15,0.3); border:1px solid rgba(255,255,255,0.1); cursor:crosshair; }
    .chart-tooltip { position:absolute; background:rgba(20,20,30,0.95); color:white; padding:7px 10px; border:1px solid rgba(255,255,255,0.25); font-size:11px; font-weight:600; pointer-events:none; z-index:100; text-align:center; line-height:1.3; white-space:nowrap; }
    .chart-legend { display:flex; justify-content:center; gap:1.2rem; margin-top:0.4rem; color:rgba(255,255,255,0.65); flex-wrap:wrap; font-size:0.8rem; }
    .legend-dot { width:9px; height:9px; display:inline-block; margin-right:4px; } .legend-dot.r { background:#e53935; } .legend-dot.d { background:#1e88e5; }
  </style>
</head>
<body>
<header class="main-header">
  <div class="main-title">UNITED STATES</div>
  <div class="main-subtitle">Midterm Elections 2026</div>
</header>
<div class="main-content">

  <div class="category-tabs">
    <div class="cat-tab active" data-cat="house">🏛️ House</div>
    <div class="cat-tab" data-cat="senate">🗳️ Senate</div>
    <div class="cat-tab" data-cat="governor">🏢 Gubernatorial</div>
  </div>

  <!-- House panel -->
  <div class="cat-panel active" id="cat-house">
    <div class="race-list">
      <div class="race-item" data-race="house-wa3"><div class="race-info"><h3>Washington · 3e District</h3><p>John Braun (R) vs Marie Gluesenkamp Perez (D)*</p></div><div class="race-rating-badge badge-tossup">Tossup</div></div>
      <div class="race-item" data-race="house-ca22"><div class="race-info"><h3>Californie · 22e District</h3><p>David Valadao (R)* vs Jasmeet Bains (D)</p></div><div class="race-rating-badge badge-lean-d">Lean D</div></div>
    </div>
  </div>

  <!-- Senate panel (liste complète) -->
  <div class="cat-panel" id="cat-senate">
    <div class="race-list" id="senate-races">
      <!-- Généré dynamiquement ci-dessous -->
    </div>
  </div>

  <!-- Gubernatorial panel -->
  <div class="cat-panel" id="cat-governor">
    <div class="race-list"><div class="race-item" style="opacity:0.5; cursor:default;"><div class="race-info"><h3>Courses à venir</h3><p>Données bientôt disponibles</p></div></div></div>
  </div>

  <div id="detail-container"></div>
</div>

<script>
(function() {
  // ---- BASE DE DONNÉES DES COURSES ----
  const racesData = {
    // --- HOUSE ---
    'house-wa3': {
      title: 'House · Washington 3rd District', rating: 'Tossup', ratingClass: 'badge-tossup',
      candidates: [{ name:'John Braun', party:'R', initials:'JB', percent:47, desc:'Ancien chef de la minorité au Sénat d\'État' },{ name:'Marie Gluesenkamp Perez', party:'D', initials:'MP', percent:48, desc:'Représentante sortante' }],
      projections:{ rSafe:10, rLikely:15, rLean:15, tossup:30, dLean:18, dLikely:12 }, seatsInfo:'Fourchette : +5D à +15R', marginError:'±3.5%', sample:'1 100 LV', pollDates:'12-15 Sep 2026',
      polls:[{ date:'Jan', rep:45, dem:47 },{ date:'Fév', rep:44, dem:48 },{ date:'Mar', rep:46, dem:46 },{ date:'Avr', rep:45, dem:49 },{ date:'Mai', rep:47, dem:46 },{ date:'Jun', rep:46, dem:47 },{ date:'Jul', rep:44, dem:48 },{ date:'Aoû', rep:46, dem:47 },{ date:'Sep', rep:47, dem:48 }],
      primaryDate:'5 août 2025',
      primaries:{
        rep:{ note:'Primaire Top 2. John Braun qualifié avec 55%.', candidates:[{ name:'John Braun', initials:'JB', desc:'Ancien chef de la minorité', score:'55%', class:'r', badge:'badge-qualified', badgeText:'Qualifié', isWinner:true },{ name:'Joe Kent', initials:'JK', desc:'Ancien militaire', score:'45%', class:'r', badge:'badge-eliminated', badgeText:'Battu', isWinner:false }], polls:[{ institute:'Résultat', date:'5 Aoû 2025', values:['55%','45%'] }] },
        dem:{ note:'Perez qualifiée (46%).', candidates:[{ name:'Marie Gluesenkamp Perez', initials:'MP', desc:'Sortante', score:'46%', class:'d', badge:'badge-qualified', badgeText:'Qualifiée', isWinner:true }], polls:[{ institute:'Résultat', date:'5 Aoû 2025', values:['46%'] }] }
      }
    },
    'house-ca22': {
      title: 'House · Californie 22nd District', rating: 'Lean D', ratingClass: 'badge-lean-d',
      candidates: [{ name:'David Valadao', party:'R', initials:'DV', percent:46, desc:'Représentant sortant' },{ name:'Jasmeet Bains', party:'D', initials:'JB', desc:'Médecin · Députée d\'État', percent:50 }],
      projections:{ rSafe:5, rLikely:10, rLean:12, tossup:25, dLean:28, dLikely:20 }, seatsInfo:'Fourchette : +3D à +12R', marginError:'±3.8%', sample:'950 LV', pollDates:'12-15 Sep 2026',
      polls:[{ date:'Jan', rep:45, dem:49 },{ date:'Fév', rep:44, dem:50 },{ date:'Mar', rep:46, dem:48 },{ date:'Avr', rep:43, dem:51 },{ date:'Mai', rep:45, dem:49 },{ date:'Jun', rep:44, dem:50 },{ date:'Jul', rep:46, dem:49 },{ date:'Aoû', rep:45, dem:50 },{ date:'Sep', rep:46, dem:50 }],
      primaryDate:'3 juin 2025',
      primaries:{
        rep:{ note:'Valadao qualifié (52%).', candidates:[{ name:'David Valadao', initials:'DV', desc:'Sortant', score:'52%', class:'r', badge:'badge-qualified', badgeText:'Qualifié', isWinner:true },{ name:'Chris Mathys', initials:'CM', desc:'Conservateur', score:'40%', class:'r', badge:'badge-eliminated', badgeText:'Battu', isWinner:false }], polls:[{ institute:'Résultat', date:'3 Jun 2025', values:['52%','40%'] }] },
        dem:{ note:'Jasmeet Bains vainqueur (60%).', candidates:[{ name:'Jasmeet Bains', initials:'JB', desc:'Médecin', score:'60%', class:'d', badge:'badge-winner', badgeText:'🏆 Vainqueur', isWinner:true },{ name:'Rudy Salas', initials:'RS', desc:'Ancien candidat', score:'33%', class:'d', badge:'badge-eliminated', badgeText:'Battu', isWinner:false }], polls:[{ institute:'Résultat', date:'3 Jun 2025', values:['60%','33%'] }] }
      }
    }
  };

  // ---- FONCTION POUR CRÉER UNE COURSE SÉNATORIALE RAPIDE ----
  function makeSenateRace(id, state, rating, ratingClass, repName, repDesc, repPct, demName, demDesc, demPct, proj, note, pollsData) {
    return {
      title: `Sénat · ${state}`, rating, ratingClass,
      candidates: [
        { name: repName, party:'R', initials: repName.split(' ').map(w=>w[0]).join(''), percent: repPct, desc: repDesc },
        { name: demName, party:'D', initials: demName.split(' ').map(w=>w[0]).join(''), percent: demPct, desc: demDesc }
      ],
      projections: proj || { rSafe:60, rLikely:20, rLean:10, tossup:5, dLean:3, dLikely:2 },
      seatsInfo: note || 'Siège républicain solide.',
      marginError:'±3.0%', sample:'1 200 LV', pollDates:'Sep 2026',
      polls: pollsData || [{ date:'Mai', rep: repPct, dem: demPct },{ date:'Sep', rep: repPct, dem: demPct }],
      primaryDate:'2026',
      primaries:{
        rep:{ note:'Pas de primaire compétitive.', candidates:[{ name:repName, initials:repName.split(' ').map(w=>w[0]).join(''), desc:'Candidat présumé', score:'100%', class:'r', badge:'badge-winner', badgeText:'Investiture', isWinner:true }], polls:[] },
        dem:{ note:'Pas de primaire compétitive.', candidates:[{ name:demName, initials:demName.split(' ').map(w=>w[0]).join(''), desc:'Candidat présumé', score:'100%', class:'d', badge:'badge-winner', badgeText:'Investiture', isWinner:true }], polls:[] }
      }
    };
  }

  // ---- LISTE DES COURSES SÉNATORIALES (classe 2 + spéciales) ----
  const senateRaces = [
    // Texas déjà détaillé, on le garde à part
    { id:'senate-tx', state:'Texas', rating:'Lean R', ratingClass:'badge-lean-r', repName:'John Cornyn', repDesc:'Sénateur sortant', repPct:48, demName:'James Talarico', demDesc:'Représentant d\'État', demPct:46, proj:{ rSafe:20, rLikely:25, rLean:15, tossup:20, dLean:12, dLikely:8 }, note:'Siège républicain, course compétitive' },
    { id:'senate-al', state:'Alabama', rating:'Safe R', ratingClass:'badge-safe-r', repName:'Tommy Tuberville', repDesc:'Sénateur sortant', repPct:60, demName:'Doug Jones', demDesc:'Ancien sénateur', demPct:38, proj:{ rSafe:80, rLikely:15, rLean:5, tossup:0, dLean:0, dLikely:0 }, note:'Siège républicain sûr' },
    { id:'senate-ak', state:'Alaska', rating:'Likely R', ratingClass:'badge-likely-r', repName:'Dan Sullivan', repDesc:'Sénateur sortant', repPct:55, demName:'Al Gross', demDesc:'Chirurgien indépendant', demPct:42, proj:{ rSafe:50, rLikely:30, rLean:15, tossup:5, dLean:0, dLikely:0 }, note:'Siège républicain favorable' },
    { id:'senate-ar', state:'Arkansas', rating:'Safe R', ratingClass:'badge-safe-r', repName:'Tom Cotton', repDesc:'Sénateur sortant', repPct:62, demName:'Josh Mahony', demDesc:'Homme d\'affaires', demPct:35, proj:{ rSafe:85, rLikely:10, rLean:5, tossup:0, dLean:0, dLikely:0 }, note:'Siège républicain très sûr' },
    { id:'senate-co', state:'Colorado', rating:'Likely D', ratingClass:'badge-likely-d', repName:'Ron Hanks', repDesc:'Ancien représentant', repPct:43, demName:'John Hickenlooper', demDesc:'Sénateur sortant', demPct:55, proj:{ rSafe:0, rLikely:5, rLean:10, tossup:15, dLean:30, dLikely:40 }, note:'Siège démocrate favorable' },
    { id:'senate-de', state:'Delaware', rating:'Safe D', ratingClass:'badge-safe-d', repName:'Lauren Witzke', repDesc:'Activiste conservatrice', repPct:35, demName:'Chris Coons', demDesc:'Sénateur sortant', demPct:63, proj:{ rSafe:0, rLikely:0, rLean:0, tossup:5, dLean:10, dLikely:85 }, note:'Siège démocrate très sûr' },
    { id:'senate-ga', state:'Géorgie', rating:'Tossup', ratingClass:'badge-tossup', repName:'Brian Kemp', repDesc:'Gouverneur', repPct:48, demName:'Jon Ossoff', demDesc:'Sénateur sortant', demPct:48, proj:{ rSafe:10, rLikely:15, rLean:20, tossup:30, dLean:15, dLikely:10 }, note:'Course ultra-compétitive' },
    { id:'senate-id', state:'Idaho', rating:'Safe R', ratingClass:'badge-safe-r', repName:'Jim Risch', repDesc:'Sénateur sortant (retraite)', repPct:65, demName:'David Roth', demDesc:'Candidat démocrate', demPct:33, proj:{ rSafe:90, rLikely:8, rLean:2, tossup:0, dLean:0, dLikely:0 }, note:'Siège républicain très sûr' },
    { id:'senate-il', state:'Illinois', rating:'Safe D', ratingClass:'badge-safe-d', repName:'Kathy Salvi', repDesc:'Ancienne candidate', repPct:38, demName:'Dick Durbin', demDesc:'Sénateur sortant (retraite possible)', demPct:60, proj:{ rSafe:0, rLikely:0, rLean:0, tossup:5, dLean:10, dLikely:85 }, note:'Siège démocrate très sûr' },
    { id:'senate-ia', state:'Iowa', rating:'Lean R', ratingClass:'badge-lean-r', repName:'Joni Ernst', repDesc:'Sénatrice sortante', repPct:51, demName:'Rob Sand', demDesc:'Auditeur d\'État', demPct:45, proj:{ rSafe:25, rLikely:30, rLean:25, tossup:15, dLean:5, dLikely:0 }, note:'Siège républicain compétitif' },
    { id:'senate-ks', state:'Kansas', rating:'Safe R', ratingClass:'badge-safe-r', repName:'Roger Marshall', repDesc:'Sénateur sortant', repPct:58, demName:'Barack Obama Jr.', demDesc:'Candidat démocrate', demPct:40, proj:{ rSafe:70, rLikely:20, rLean:10, tossup:0, dLean:0, dLikely:0 }, note:'Siège républicain sûr' },
    { id:'senate-ky', state:'Kentucky', rating:'Safe R', ratingClass:'badge-safe-r', repName:'Mitch McConnell', repDesc:'Chef de la minorité (retraite)', repPct:60, demName:'Charles Booker', demDesc:'Ancien représentant d\'État', demPct:38, proj:{ rSafe:80, rLikely:15, rLean:5, tossup:0, dLean:0, dLikely:0 }, note:'Siège républicain très sûr' },
    { id:'senate-la', state:'Louisiane', rating:'Safe R', ratingClass:'badge-safe-r', repName:'Bill Cassidy', repDesc:'Sénateur sortant', repPct:58, demName:'Gary Chambers', demDesc:'Militant', demPct:40, proj:{ rSafe:75, rLikely:15, rLean:10, tossup:0, dLean:0, dLikely:0 }, note:'Siège républicain sûr' },
    { id:'senate-me', state:'Maine', rating:'Tossup', ratingClass:'badge-tossup', repName:'Susan Collins', repDesc:'Sénatrice sortante', repPct:47, demName:'Sara Gideon', demDesc:'Ancienne présidente de la Chambre', demPct:49, proj:{ rSafe:5, rLikely:15, rLean:20, tossup:30, dLean:20, dLikely:10 }, note:'Course très compétitive' },
    { id:'senate-ma', state:'Massachusetts', rating:'Safe D', ratingClass:'badge-safe-d', repName:'Geoff Diehl', repDesc:'Ancien candidat', repPct:35, demName:'Ed Markey', demDesc:'Sénateur sortant', demPct:63, proj:{ rSafe:0, rLikely:0, rLean:0, tossup:5, dLean:10, dLikely:85 } },
    { id:'senate-mi', state:'Michigan', rating:'Lean D', ratingClass:'badge-lean-d', repName:'John James', repDesc:'Ancien candidat', repPct:46, demName:'Gary Peters', demDesc:'Sénateur sortant', demPct:51, proj:{ rSafe:5, rLikely:10, rLean:20, tossup:25, dLean:25, dLikely:15 }, note:'Siège démocrate compétitif' },
    { id:'senate-mn', state:'Minnesota', rating:'Lean D', ratingClass:'badge-lean-d', repName:'Jason Lewis', repDesc:'Ancien représentant', repPct:45, demName:'Peggy Flanagan', demDesc:'Lieutenante-gouverneure', demPct:52, proj:{ rSafe:5, rLikely:10, rLean:15, tossup:25, dLean:30, dLikely:15 }, note:'Siège ouvert (Tina Smith ne se représente pas)' },
    { id:'senate-ms', state:'Mississippi', rating:'Safe R', ratingClass:'badge-safe-r', repName:'Cindy Hyde-Smith', repDesc:'Sénatrice sortante', repPct:60, demName:'Mike Espy', demDesc:'Ancien secrétaire à l\'Agriculture', demPct:38, proj:{ rSafe:85, rLikely:10, rLean:5, tossup:0, dLean:0, dLikely:0 } },
    { id:'senate-mt', state:'Montana', rating:'Lean R', ratingClass:'badge-lean-r', repName:'Steve Daines', repDesc:'Sénateur sortant', repPct:52, demName:'Kathleen Williams', demDesc:'Ancienne candidate', demPct:45, proj:{ rSafe:30, rLikely:30, rLean:25, tossup:10, dLean:5, dLikely:0 }, note:'Siège républicain compétitif' },
    { id:'senate-ne', state:'Nebraska', rating:'Safe R', ratingClass:'badge-safe-r', repName:'Pete Ricketts', repDesc:'Sénateur nommé', repPct:63, demName:'Bob Kerrey', demDesc:'Ancien sénateur', demPct:35, proj:{ rSafe:85, rLikely:10, rLean:5, tossup:0, dLean:0, dLikely:0 } },
    { id:'senate-nh', state:'New Hampshire', rating:'Lean D', ratingClass:'badge-lean-d', repName:'Chris Sununu', repDesc:'Gouverneur', repPct:47, demName:'Jeanne Shaheen', demDesc:'Sénatrice sortante', demPct:51, proj:{ rSafe:5, rLikely:10, rLean:20, tossup:25, dLean:25, dLikely:15 }, note:'Course compétitive' },
    { id:'senate-nj', state:'New Jersey', rating:'Safe D', ratingClass:'badge-safe-d', repName:'Tom Kean Jr.', repDesc:'Ancien candidat', repPct:40, demName:'Cory Booker', demDesc:'Sénateur sortant', demPct:58, proj:{ rSafe:0, rLikely:0, rLean:0, tossup:5, dLean:15, dLikely:80 } },
    { id:'senate-nm', state:'Nouveau-Mexique', rating:'Safe D', ratingClass:'badge-safe-d', repName:'Mark Ronchetti', repDesc:'Ancien candidat', repPct:42, demName:'Ben Ray Luján', demDesc:'Sénateur sortant', demPct:56, proj:{ rSafe:0, rLikely:0, rLean:5, tossup:10, dLean:25, dLikely:60 } },
    { id:'senate-nc', state:'Caroline du Nord', rating:'Tossup', ratingClass:'badge-tossup', repName:'Thom Tillis', repDesc:'Sénateur sortant', repPct:47, demName:'Jeff Jackson', demDesc:'Représentant', demPct:48, proj:{ rSafe:10, rLikely:15, rLean:20, tossup:30, dLean:15, dLikely:10 }, note:'Course ultra-compétitive' },
    { id:'senate-ok', state:'Oklahoma', rating:'Safe R', ratingClass:'badge-safe-r', repName:'Markwayne Mullin', repDesc:'Sénateur sortant', repPct:65, demName:'Kendra Horn', demDesc:'Ancienne représentante', demPct:33, proj:{ rSafe:90, rLikely:8, rLean:2, tossup:0, dLean:0, dLikely:0 } },
    { id:'senate-or', state:'Oregon', rating:'Safe D', ratingClass:'badge-safe-d', repName:'Christine Drazan', repDesc:'Ancienne candidate au poste de gouverneur', repPct:40, demName:'Jeff Merkley', demDesc:'Sénateur sortant', demPct:58, proj:{ rSafe:0, rLikely:0, rLean:0, tossup:5, dLean:15, dLikely:80 } },
    { id:'senate-ri', state:'Rhode Island', rating:'Safe D', ratingClass:'badge-safe-d', repName:'Allan Fung', repDesc:'Ancien maire', repPct:38, demName:'Jack Reed', demDesc:'Sénateur sortant', demPct:60, proj:{ rSafe:0, rLikely:0, rLean:0, tossup:5, dLean:15, dLikely:80 } },
    { id:'senate-sc', state:'Caroline du Sud', rating:'Safe R', ratingClass:'badge-safe-r', repName:'Lindsey Graham', repDesc:'Sénateur sortant', repPct:58, demName:'Jaime Harrison', demDesc:'Ancien candidat', demPct:40, proj:{ rSafe:75, rLikely:15, rLean:10, tossup:0, dLean:0, dLikely:0 } },
    { id:'senate-sd', state:'South Dakota', rating:'Safe R', ratingClass:'badge-safe-r', repName:'Mike Rounds', repDesc:'Sénateur sortant', repPct:65, demName:'Billie Sutton', demDesc:'Ancien sénateur d\'État', demPct:33, proj:{ rSafe:90, rLikely:8, rLean:2, tossup:0, dLean:0, dLikely:0 } },
    { id:'senate-tn', state:'Tennessee', rating:'Safe R', ratingClass:'badge-safe-r', repName:'Bill Hagerty', repDesc:'Sénateur sortant', repPct:62, demName:'Marquita Bradshaw', demDesc:'Militante', demPct:36, proj:{ rSafe:85, rLikely:10, rLean:5, tossup:0, dLean:0, dLikely:0 } },
    { id:'senate-va', state:'Virginie', rating:'Likely D', ratingClass:'badge-likely-d', repName:'Winsome Sears', repDesc:'Lieutenante-gouverneure', repPct:44, demName:'Mark Warner', demDesc:'Sénateur sortant', demPct:54, proj:{ rSafe:0, rLikely:5, rLean:10, tossup:20, dLean:30, dLikely:35 } },
    { id:'senate-wv', state:'Virginie-Occidentale', rating:'Safe R', ratingClass:'badge-safe-r', repName:'Shelley Moore Capito', repDesc:'Sénatrice sortante', repPct:62, demName:'Paula Jean Swearengin', demDesc:'Militante', demPct:36, proj:{ rSafe:85, rLikely:10, rLean:5, tossup:0, dLean:0, dLikely:0 } },
    { id:'senate-wy', state:'Wyoming', rating:'Safe R', ratingClass:'badge-safe-r', repName:'Cynthia Lummis', repDesc:'Sénatrice sortante', repPct:68, demName:'Merav Ben-David', demDesc:'Scientifique', demPct:30, proj:{ rSafe:95, rLikely:5, rLean:0, tossup:0, dLean:0, dLikely:0 } },
    // Élections spéciales (pas de classe 2 normale)
    { id:'senate-fl', state:'Floride (spéciale)', rating:'Likely R', ratingClass:'badge-likely-r', repName:'Jeanette Nuñez', repDesc:'Ancienne lieutenante-gouverneure', repPct:54, demName:'Debbie Mucarsel-Powell', demDesc:'Ancienne représentante', demPct:44, proj:{ rSafe:40, rLikely:35, rLean:15, tossup:10, dLean:0, dLikely:0 }, note:'Élection spéciale pour remplacer Marco Rubio' },
    { id:'senate-oh', state:'Ohio (spéciale)', rating:'Likely R', ratingClass:'badge-likely-r', repName:'Frank LaRose', repDesc:'Secrétaire d\'État', repPct:53, demName:'Tim Ryan', demDesc:'Ancien représentant', demPct:45, proj:{ rSafe:35, rLikely:40, rLean:15, tossup:10, dLean:0, dLikely:0 }, note:'Élection spéciale' }
  ];

  // Convertir en objets racesData
  senateRaces.forEach(r => {
    const polls = [];
    for (let m = 1; m <= 9; m++) {
      polls.push({ date: ['Jan','Fév','Mar','Avr','Mai','Jun','Jul','Aoû','Sep'][m-1], rep: r.repPct - (Math.random()*6-3)>>0, dem: r.demPct - (Math.random()*6-3)>>0 });
    }
    // Ajuster les extrêmes
    const lastP = { date:'Sep', rep: r.repPct, dem: r.demPct };
    polls.push(lastP);
    racesData[r.id] = makeSenateRace(r.id, r.state, r.rating, r.ratingClass, r.repName, r.repDesc, r.repPct, r.demName, r.demDesc, r.demPct, r.proj, r.note, polls);
  });

  // On conserve la version détaillée du Texas
  racesData['senate-tx'] = {
    title: 'Sénat · Texas', rating: 'Lean R', ratingClass: 'badge-lean-r',
    candidates: [{ name:'John Cornyn', party:'R', initials:'JC', percent:48, desc:'Sénateur sortant' },{ name:'James Talarico', party:'D', initials:'JT', percent:46, desc:'Représentant d\'État' }],
    projections:{ rSafe:20, rLikely:25, rLean:15, tossup:20, dLean:12, dLikely:8 }, seatsInfo:'Fourchette : +2R à +8R', marginError:'±3.2%', sample:'2 814 LV', pollDates:'12-15 Sep 2026',
    polls:[{ date:'Jan', rep:47, dem:44 },{ date:'Fév', rep:44, dem:43 },{ date:'Mar', rep:44, dem:43 },{ date:'Avr', rep:45, dem:44 },{ date:'Mai', rep:47, dem:42 },{ date:'Jun', rep:46, dem:44 },{ date:'Jul', rep:44, dem:44 },{ date:'Aoû', rep:47, dem:45 },{ date:'Sep', rep:48, dem:46 }],
    primaryDate:'4 mars 2026',
    primaries:{
      rep:{ note:'Second tour le 26 mai 2026.', candidates:[{ name:'Ken Paxton', initials:'KP', desc:'Procureur général', score:'48.8%', class:'r', badge:'badge-runoff', badgeText:'Second tour', isWinner:true },{ name:'John Cornyn', initials:'JC', desc:'Sénateur sortant', score:'41.3%', class:'r', badge:'badge-runoff', badgeText:'Second tour', isWinner:true }], polls:[{ institute:'Quantus', date:'Mar', values:['48.8%','41.3%'] }] },
      dem:{ note:'Talarico vainqueur (53.1%).', candidates:[{ name:'James Talarico', initials:'JT', desc:'Représentant', score:'53.1%', class:'d', badge:'badge-winner', badgeText:'🏆 Vainqueur', isWinner:true },{ name:'Jasmine Crockett', initials:'JC', desc:'Représentante', score:'45.6%', class:'d', badge:'badge-eliminated', badgeText:'Battue', isWinner:false }], polls:[{ institute:'Résultat', date:'4 Mar', values:['53.1%','45.6%'] }] }
    }
  };

  // ---- GÉNÉRATION DE LA LISTE DES COURSES SÉNAT ----
  const senateList = document.getElementById('senate-races');
  Object.keys(racesData).forEach(id => {
    if (id.startsWith('senate-')) {
      const r = racesData[id];
      const item = document.createElement('div');
      item.className = 'race-item';
      item.dataset.race = id;
      item.innerHTML = `<div class="race-info"><h3>${r.title.replace('Sénat · ','')}</h3><p>${r.candidates[0].name} (R) vs ${r.candidates[1].name} (D)</p></div><div class="race-rating-badge ${r.ratingClass}">${r.rating}</div>`;
      senateList.appendChild(item);
    }
  });

  // ---- GESTION DES ONGLETS ET AFFICHAGE ----
  function showRaceDetail(raceId) {
    const data = racesData[raceId];
    if (!data) return;
    const container = document.getElementById('detail-container');
    container.innerHTML = `
      <div class="card">
        <div class="card-header"><div class="card-title">${data.title}</div><div class="race-rating-badge ${data.ratingClass}">${data.rating}</div></div>
        ${data.candidates.map(c => `
          <div class="candidate-row">
            <div class="candidate-label"><span class="party-name ${c.party==='R'?'rep':'dem'}">${c.name} (${c.party})</span><span class="party-percent ${c.party==='R'?'rep':'dem'}">${c.percent}%</span></div>
            <div class="cand-desc-small">${c.desc}</div>
            <div class="bar-wrapper"><div class="bar-fill ${c.party==='R'?'rep-fill':'dem-fill'}" style="width:${c.percent}%">${c.percent}%</div></div>
          </div>
        `).join('')}
        <div class="poll-footer"><span>📊 Marge ${data.marginError}</span><span>👥 ${data.sample} · ${data.pollDates}</span></div>
        <div style="margin-top:1.2rem;"><h4 style="color:rgba(255,255,255,0.55);font-size:0.8rem;text-transform:uppercase;">Probabilités</h4>
          <div class="projections-bar">
            <div class="proj-r-safe" style="width:${data.projections.rSafe}%"></div><div class="proj-r-likely" style="width:${data.projections.rLikely}%"></div><div class="proj-r-lean" style="width:${data.projections.rLean}%"></div>
            <div class="proj-tossup" style="width:${data.projections.tossup}%"></div><div class="proj-d-lean" style="width:${data.projections.dLean}%"></div><div class="proj-d-likely" style="width:${data.projections.dLikely}%"></div>
          </div>
          <div class="projections-legend"><span>R+10+</span><span>R+5-9</span><span>R+1-4</span><span>Tossup</span><span>D+1-4</span><span>D+5+</span></div>
          <div class="seats-projection">${data.seatsInfo}</div>
        </div>
        <div style="margin-top:1.2rem;"><h4 style="color:rgba(255,255,255,0.55);font-size:0.8rem;text-transform:uppercase;">📈 Sondages</h4>
          <div class="chart-container"><canvas id="detailChart" width="800" height="260"></canvas><div class="chart-tooltip" id="chartTooltip" style="opacity:0;"></div></div>
          <div class="chart-legend"><span><span class="legend-dot r"></span> ${data.candidates[0].name.split(' ').pop()} (R)</span><span><span class="legend-dot d"></span> ${data.candidates[1].name.split(' ').pop()} (D)</span><span style="opacity:0.55;">— Moyenne mobile (3)</span></div>
        </div>
      </div>
      <div class="card">
        <div class="card-header"><div class="card-title">Primaires</div><div style="color:rgba(255,255,255,0.5);font-size:0.8rem;">📅 ${data.primaryDate}</div></div>
        <div class="primary-tabs"><div class="prim-tab r-active active" data-prim="rep">Primaire Républicaine</div><div class="prim-tab d-active" data-prim="dem">Primaire Démocrate</div></div>
        <div class="prim-panel active" id="panel-rep">
          <div class="primary-grid">${data.primaries.rep.candidates.map(c => `<div class="candidate-card ${c.isWinner?'winner':''}"><div class="cand-photo ${c.class}">${c.initials}</div><div class="cand-name">${c.name}</div><div class="cand-desc">${c.desc}</div><div class="cand-score ${c.class}">${c.score}</div><div class="cand-badge ${c.badge}">${c.badgeText}</div></div>`).join('')}</div>
          ${data.primaries.rep.polls && data.primaries.rep.polls.length > 0 ? `<table class="primary-table"><thead><tr><th>Institut</th><th>Date</th>${data.primaries.rep.candidates.map(c => `<th>${c.name.split(' ').pop()}</th>`).join('')}</tr></thead><tbody>${data.primaries.rep.polls.map((p,i) => `<tr class="${i===0?'highlight-row':''}"><td>${p.institute}</td><td>${p.date}</td>${p.values.map(v => `<td class="${data.primaries.rep.candidates[0].class==='r'?'r-col':'d-col'}">${v}</td>`).join('')}</tr>`).join('')}</tbody></table>` : ''}
          <div class="primary-note">${data.primaries.rep.note}</div>
        </div>
        <div class="prim-panel" id="panel-dem">
          <div class="primary-grid">${data.primaries.dem.candidates.map(c => `<div class="candidate-card ${c.isWinner?'winner':''}"><div class="cand-photo ${c.class}">${c.initials}</div><div class="cand-name">${c.name}</div><div class="cand-desc">${c.desc}</div><div class="cand-score ${c.class}">${c.score}</div><div class="cand-badge ${c.badge}">${c.badgeText}</div></div>`).join('')}</div>
          ${data.primaries.dem.polls && data.primaries.dem.polls.length > 0 ? `<table class="primary-table"><thead><tr><th>Institut</th><th>Date</th>${data.primaries.dem.candidates.map(c => `<th>${c.name.split(' ').pop()}</th>`).join('')}</tr></thead><tbody>${data.primaries.dem.polls.map((p,i) => `<tr class="${i===0?'highlight-row':''}"><td>${p.institute}</td><td>${p.date}</td>${p.values.map(v => `<td class="${data.primaries.dem.candidates[0].class==='r'?'r-col':'d-col'}">${v}</td>`).join('')}</tr>`).join('')}</tbody></table>` : ''}
          <div class="primary-note">${data.primaries.dem.note}</div>
        </div>
      </div>
    `;
    setTimeout(() => {
      container.querySelectorAll('.prim-tab').forEach(tab => {
        tab.addEventListener('click', function() {
          const target = this.dataset.prim;
          container.querySelectorAll('.prim-tab').forEach(t => t.classList.remove('active','r-active','d-active'));
          this.classList.add('active');
          if(target==='rep') this.classList.add('r-active'); else this.classList.add('d-active');
          container.querySelectorAll('.prim-panel').forEach(p => p.classList.remove('active'));
          container.querySelector('#panel-'+target).classList.add('active');
        });
      });
      drawChart(data.polls, data.candidates);
    }, 100);
  }

  function drawChart(polls, candidates) {
    const canvas = document.getElementById('detailChart');
    if(!canvas) return;
    const ctx = canvas.getContext('2d');
    const tooltip = document.getElementById('chartTooltip');
    const repAvg=[], demAvg=[];
    for(let i=0;i<polls.length;i++){
      let sR=0,sD=0,c=0;
      for(let j=Math.max(0,i-2);j<=i;j++){ sR+=polls[j].rep; sD+=polls[j].dem; c++; }
      repAvg.push(Math.round((sR/c)*10)/10); demAvg.push(Math.round((sD/c)*10)/10);
    }
    const pad={top:22,right:28,bottom:32,left:38},minY=25,maxY=70;
    let points=[];
    function draw(){
      const w=canvas.width,h=canvas.height,cW=w-pad.left-pad.right,cH=h-pad.top-pad.bottom;
      ctx.clearRect(0,0,w,h); ctx.fillStyle='rgba(10,10,18,0.5)'; ctx.fillRect(pad.left,pad.top,cW,cH);
      const gX=i=>pad.left+(i/(polls.length-1))*cW, gY=v=>pad.top+cH-((v-minY)/(maxY-minY))*cH;
      ctx.strokeStyle='rgba(255,255,255,0.06)'; ctx.lineWidth=0.5;
      for(let i=minY;i<=maxY;i+=5){ const y=gY(i); ctx.beginPath(); ctx.moveTo(pad.left,y); ctx.lineTo(pad.left+cW,y); ctx.stroke(); ctx.fillStyle='rgba(255,255,255,0.35)'; ctx.font='9px Segoe UI'; ctx.textAlign='right'; ctx.fillText(i+'%',pad.left-5,y); }
      ctx.fillStyle='rgba(255,255,255,0.45)'; ctx.font='9px Segoe UI'; ctx.textAlign='center';
      polls.forEach((p,i)=>ctx.fillText(p.date,gX(i),pad.top+cH+10));
      [{d:repAvg,c:'#ff8a7a'},{d:demAvg,c:'#8fc1ff'}].forEach(l=>{
        ctx.beginPath(); ctx.moveTo(gX(0),gY(l.d[0]));
        for(let i=1;i<l.d.length;i++){ const xc=gX(i),yc=gY(l.d[i]),xp=gX(i-1),yp=gY(l.d[i-1]); ctx.bezierCurveTo(xp+(xc-xp)*0.5,yp,xc-(xc-xp)*0.5,yc,xc,yc); }
        ctx.strokeStyle=l.c; ctx.lineWidth=2.2; ctx.stroke();
      });
      points=[];
      polls.forEach((p,i)=>{
        [{v:p.rep,t:'r',c:'rgba(180,40,40,0.5)'},{v:p.dem,t:'d',c:'rgba(30,80,180,0.5)'}].forEach(pt=>{
          const x=gX(i),y=gY(pt.v); points.push({x,y,type:pt.t,value:pt.v,date:p.date});
          ctx.beginPath(); ctx.arc(x,y,5.5,0,2*Math.PI); ctx.fillStyle=pt.c; ctx.fill(); ctx.strokeStyle='rgba(255,255,255,0.18)'; ctx.stroke();
        });
      });
    }
    draw();
    canvas.onmousemove=function(e){
      const rect=canvas.getBoundingClientRect(),sX=canvas.width/rect.width,sY=canvas.height/rect.height;
      const mx=(e.clientX-rect.left)*sX,my=(e.clientY-rect.top)*sY;
      let cl=null,md=18;
      points.forEach(p=>{const d=Math.hypot(mx-p.x,my-p.y); if(d<md){md=d;cl=p;}});
      if(cl){
        const name=cl.type==='r'?candidates[0].name:candidates[1].name;
        tooltip.innerHTML='<strong>'+name+'</strong><br><span style="color:'+(cl.type==='r'?'#ff9e8f':'#8fc1ff')+';font-size:14px;">'+cl.value+'%</span><br><span style="opacity:0.55;">'+cl.date+' 2026</span>';
        tooltip.style.left=Math.max(5,Math.min(cl.x/sX-50,rect.width-100))+'px';
        tooltip.style.top=Math.max(5,cl.y/sY-50)+'px'; tooltip.style.opacity='1';
      }else{tooltip.style.opacity='0';}
    };
    canvas.onmouseleave=()=>tooltip.style.opacity='0';
  }

  // Activer le premier élément de l'onglet actif
  document.querySelectorAll('.cat-tab').forEach(tab => {
    tab.addEventListener('click', function() {
      document.querySelectorAll('.cat-tab').forEach(t => t.classList.remove('active'));
      this.classList.add('active');
      document.querySelectorAll('.cat-panel').forEach(p => p.classList.remove('active'));
      const catId = 'cat-' + this.dataset.cat;
      document.getElementById(catId).classList.add('active');
      const firstRace = document.querySelector('#' + catId + ' .race-item[data-race]');
      if (firstRace) { firstRace.click(); }
    });
  });

  document.addEventListener('click', function(e) {
    const item = e.target.closest('.race-item[data-race]');
    if (item) {
      document.querySelectorAll('.race-item').forEach(i => i.classList.remove('active'));
      item.classList.add('active');
      showRaceDetail(item.dataset.race);
    }
  });

  // Afficher le premier sénat par défaut (Texas)
  const firstSenate = document.querySelector('#cat-senate .race-item[data-race]');
  if (firstSenate) firstSenate.click();
  else {
    const firstHouse = document.querySelector('#cat-house .race-item[data-race]');
    if (firstHouse) firstHouse.click();
  }
})();
</script>
