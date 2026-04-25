<!DOCTYPE html>
<html lang="fr">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Election USA 2026 · House, Senate & Gubernatorial</title>
  <style>
    * { margin:0; padding:0; box-sizing:border-box; }
    body { min-height:100vh; width:100%; font-family:'Segoe UI','Roboto',system-ui,sans-serif; display:flex; flex-direction:column; align-items:center; background:linear-gradient(to right,#0a1f3a 0%,#000 50%,#8b1a1a 100%); background-attachment:fixed; padding:20px; }
    .main-header { width:100%; max-width:1400px; background:rgba(5,10,20,0.7); backdrop-filter:blur(12px); padding:1.5rem 2rem; text-align:center; margin-bottom:25px; box-shadow:0 10px 30px rgba(0,0,0,0.6); border-bottom:1px solid rgba(210,180,140,0.2); }
    .main-title { font-size:clamp(1.8rem,5vw,3.5rem); font-weight:900; letter-spacing:0.2em; color:#fff; text-transform:uppercase; }
    .main-subtitle { font-size:clamp(0.9rem,2.5vw,1.5rem); color:rgba(255,255,255,0.85); letter-spacing:0.3em; text-transform:uppercase; border-top:1.5px solid rgba(255,215,150,0.5); display:inline-block; padding-top:0.6rem; margin-top:0.4rem; }
    .main-content { width:100%; max-width:1400px; }
    .category-tabs { display:flex; gap:0.5rem; margin-bottom:1.5rem; flex-wrap:wrap; }
    .cat-tab { background:rgba(0,0,0,0.4); border:1px solid rgba(255,255,255,0.2); color:white; padding:0.9rem 1.2rem; font-size:1rem; font-weight:700; text-transform:uppercase; letter-spacing:0.1em; cursor:pointer; flex:1; min-width:130px; text-align:center; }
    .cat-tab.active { background:rgba(255,255,255,0.15); border-color:rgba(255,215,150,0.6); box-shadow:0 0 20px rgba(255,215,150,0.2); }
    .cat-panel { display:none; } .cat-panel.active { display:block; }
    .race-list { display:flex; flex-direction:column; gap:0.8rem; margin-bottom:1.5rem; }
    .race-item { background:rgba(0,0,0,0.35); border:1px solid rgba(220,200,180,0.18); padding:0.9rem 1.2rem; cursor:pointer; display:flex; justify-content:space-between; align-items:center; flex-wrap:wrap; gap:0.8rem; }
    .race-item.active { background:rgba(255,255,255,0.12); border-color:rgba(255,215,150,0.7); box-shadow:0 0 25px rgba(255,215,150,0.15); }
    .race-info h3 { color:#f0e6d2; font-size:1.1rem; margin-bottom:0.2rem; }
    .race-info p { color:rgba(255,255,255,0.5); font-size:0.8rem; }
    .race-tag { padding:0.25rem 0.8rem; font-weight:700; text-transform:uppercase; font-size:0.7rem; letter-spacing:0.1em; white-space:nowrap; }
    .tossup { background:rgba(255,200,0,0.2); color:#ffc107; border:1px solid #ffc107; }
    .lean-r { background:rgba(229,57,53,0.2); color:#ff9e8f; border:1px solid #e53935; }
    .lean-d { background:rgba(30,136,229,0.2); color:#8fc1ff; border:1px solid #1e88e5; }
    .likely-r { background:rgba(229,57,53,0.3); color:#ff6b5e; border:1px solid #d32f2f; }
    .likely-d { background:rgba(30,136,229,0.3); color:#64b5f6; border:1px solid #1976d2; }
    .safe-r { background:rgba(229,57,53,0.4); color:#ff8a80; border:1px solid #b71c1c; }
    .safe-d { background:rgba(30,136,229,0.4); color:#82b1ff; border:1px solid #0d47a1; }
    .tilt-r { background:rgba(229,57,53,0.2); color:#ffab91; border:1px solid #ff7043; }
    .tilt-d { background:rgba(30,136,229,0.2); color:#91caff; border:1px solid #42a5f5; }
    .card { width:100%; background:rgba(0,0,0,0.35); backdrop-filter:blur(8px); border:1px solid rgba(220,200,180,0.18); box-shadow:0 20px 35px -8px rgba(0,0,0,0.6); padding:1.5rem; margin-bottom:1.2rem; }
    .card-header { display:flex; align-items:center; justify-content:space-between; margin-bottom:1.5rem; border-bottom:2px solid rgba(255,255,255,0.15); padding-bottom:1.2rem; flex-wrap:wrap; gap:1rem; }
    .card-title { font-size:1.4rem; font-weight:600; letter-spacing:0.12em; text-transform:uppercase; color:#f0e6d2; }
    .rep { color:#ff9e8f; } .dem { color:#8fc1ff; }
    .candidate-row { margin-bottom:1.5rem; }
    .candidate-label { display:flex; justify-content:space-between; margin-bottom:0.5rem; flex-wrap:wrap; }
    .party-name { font-size:1.1rem; font-weight:700; letter-spacing:0.08em; text-transform:uppercase; }
    .party-pct { font-size:1.5rem; font-weight:800; }
    .bar-wrap { width:100%; height:35px; background:#121212e0; border:1px solid rgba(255,255,255,0.12); overflow:hidden; }
    .bar-fill { height:100%; display:flex; align-items:center; justify-content:flex-end; padding-right:15px; font-weight:700; color:white; font-size:0.9rem; }
    .bar-fill.rf { background:linear-gradient(90deg,#a51c1c,#d32f2f); }
    .bar-fill.df { background:linear-gradient(90deg,#0a3a7a,#1976d2); }
    .poll-footer { margin-top:1.2rem; display:flex; justify-content:space-between; color:rgba(255,240,220,0.7); border-top:1px solid rgba(255,255,240,0.1); padding-top:1rem; flex-wrap:wrap; gap:0.4rem; font-size:0.8rem; }
    .projections-bar { display:flex; height:10px; margin:0.8rem 0; background:#121212; }
    .p-safe-r { background:#4a0000; } .p-likely-r { background:#7a0000; } .p-lean-r { background:#a51c1c; }
    .p-tossup { background:#5a4a00; } .p-lean-d { background:#1565c0; } .p-likely-d { background:#0a3a7a; }
    .prim-tabs { display:flex; gap:0.5rem; margin-bottom:1.2rem; }
    .prim-tab { background:rgba(0,0,0,0.4); border:1px solid rgba(255,255,255,0.2); color:white; padding:0.6rem 1rem; font-size:0.9rem; font-weight:600; text-transform:uppercase; cursor:pointer; flex:1; text-align:center; }
    .prim-tab.active { background:rgba(255,255,255,0.15); border-color:rgba(255,215,150,0.6); }
    .prim-tab.ra { background:rgba(229,57,53,0.2); border-color:#e53935; }
    .prim-tab.da { background:rgba(30,136,229,0.2); border-color:#1e88e5; }
    .prim-panel { display:none; } .prim-panel.active { display:block; }
    .primary-grid { display:grid; grid-template-columns:repeat(auto-fit,minmax(180px,1fr)); gap:1rem; margin-bottom:1.5rem; }
    .candidate-card { background:rgba(0,0,0,0.3); border:1px solid rgba(255,255,255,0.1); padding:1.2rem; text-align:center; }
    .cand-photo { width:55px; height:55px; border-radius:50%; margin:0 auto 0.6rem; display:flex; align-items:center; justify-content:center; font-weight:bold; font-size:1.4rem; color:white; border:2px solid rgba(255,255,255,0.2); }
    .cand-photo.rr { background:#a51c1c; } .cand-photo.dd { background:#0a3a7a; }
    .cand-name { font-size:1rem; font-weight:700; color:white; }
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

  <!-- House -->
  <div class="cat-panel active" id="cat-house">
    <div class="race-list">
      <div class="race-item" data-race="house-wa3"><div class="race-info"><h3>Washington · 3e District</h3><p>John Braun (R) vs Marie Gluesenkamp Perez (D)*</p></div><div class="race-tag tossup">Tossup</div></div>
      <div class="race-item" data-race="house-ca22"><div class="race-info"><h3>Californie · 22e District</h3><p>David Valadao (R)* vs Jasmeet Bains (D)</p></div><div class="race-tag lean-d">Lean D</div></div>
    </div>
  </div>

  <!-- Senate -->
  <div class="cat-panel" id="cat-senate">
    <div class="race-list" id="senate-races"></div>
  </div>

  <!-- Gubernatorial -->
  <div class="cat-panel" id="cat-governor">
    <div class="race-list"><div class="race-item" style="opacity:0.5;cursor:default;"><div class="race-info"><h3>Courses à venir</h3><p>Données bientôt disponibles</p></div></div></div>
  </div>

  <div id="detail-container"></div>
</div>

<script>
(function() {
  // ---- BASE DE DONNÉES ----
  const racesData = {
    'house-wa3': {
      title:'House · Washington 3rd',rating:'Tossup',ratingClass:'tossup',
      candidates:[{name:'John Braun',party:'R',initials:'JB',pct:47,desc:'Ancien chef de la minorité au Sénat d\'État'},{name:'Marie Gluesenkamp Perez',party:'D',initials:'MP',pct:48,desc:'Représentante sortante'}],
      proj:{rSafe:10,rLikely:15,rLean:15,tossup:30,dLean:18,dLikely:12},seats:'Fourchette : +5D à +15R',moe:'±3.5%',sample:'1 100 LV',dates:'12-15 Sep 2026',
      polls:[{date:'Jan',rep:45,dem:47},{date:'Fév',rep:44,dem:48},{date:'Mar',rep:46,dem:46},{date:'Avr',rep:45,dem:49},{date:'Mai',rep:47,dem:46},{date:'Jun',rep:46,dem:47},{date:'Jul',rep:44,dem:48},{date:'Aoû',rep:46,dem:47},{date:'Sep',rep:47,dem:48}],
      primaryDate:'5 août 2025',
      primaries:{
        rep:{note:'Primaire Top 2. John Braun qualifié avec 55%.',cands:[{name:'John Braun',init:'JB',desc:'Ancien chef de la minorité',score:'55%',cls:'rr',badge:'Qualifié'},{name:'Joe Kent',init:'JK',desc:'Ancien militaire',score:'45%',cls:'rr',badge:'Battu'}],polls:[{inst:'Résultat',date:'5 Aoû 2025',vals:['55%','45%']}]},
        dem:{note:'Perez qualifiée (46%).',cands:[{name:'Marie Gluesenkamp Perez',init:'MP',desc:'Sortante',score:'46%',cls:'dd',badge:'Qualifiée'}],polls:[{inst:'Résultat',date:'5 Aoû 2025',vals:['46%']}]}
      }
    },
    'house-ca22': {
      title:'House · Californie 22nd',rating:'Lean D',ratingClass:'lean-d',
      candidates:[{name:'David Valadao',party:'R',initials:'DV',pct:46,desc:'Représentant sortant'},{name:'Jasmeet Bains',party:'D',initials:'JB',pct:50,desc:'Médecin · Députée d\'État'}],
      proj:{rSafe:5,rLikely:10,rLean:12,tossup:25,dLean:28,dLikely:20},seats:'Fourchette : +3D à +12R',moe:'±3.8%',sample:'950 LV',dates:'12-15 Sep 2026',
      polls:[{date:'Jan',rep:45,dem:49},{date:'Fév',rep:44,dem:50},{date:'Mar',rep:46,dem:48},{date:'Avr',rep:43,dem:51},{date:'Mai',rep:45,dem:49},{date:'Jun',rep:44,dem:50},{date:'Jul',rep:46,dem:49},{date:'Aoû',rep:45,dem:50},{date:'Sep',rep:46,dem:50}],
      primaryDate:'3 juin 2025',
      primaries:{
        rep:{note:'Valadao qualifié (52%).',cands:[{name:'David Valadao',init:'DV',desc:'Sortant',score:'52%',cls:'rr',badge:'Qualifié'},{name:'Chris Mathys',init:'CM',desc:'Conservateur',score:'40%',cls:'rr',badge:'Battu'}],polls:[{inst:'Résultat',date:'3 Jun 2025',vals:['52%','40%']}]},
        dem:{note:'Jasmeet Bains vainqueur (60%).',cands:[{name:'Jasmeet Bains',init:'JB',desc:'Médecin',score:'60%',cls:'dd',badge:'🏆 Vainqueur'},{name:'Rudy Salas',init:'RS',desc:'Ancien candidat',score:'33%',cls:'dd',badge:'Battu'}],polls:[{inst:'Résultat',date:'3 Jun 2025',vals:['60%','33%']}]}
      }
    }
  };

  // ---- LISTE SÉNAT TRIÉE PAR RATING ----
  const senateRaces = [
    // SAFE R
    {id:'senate-wy',state:'Wyoming',rating:'Safe R',cls:'safe-r',rep:'Cynthia Lummis',repD:'Sénatrice sortante (retraite)',dem:'Sam Mead',demD:'Rancher · Ancien maire',repPct:65,demPct:33,proj:{rSafe:90,rLikely:8,rLean:2,tossup:0,dLean:0,dLikely:0},note:'Siège républicain très sûr',primaryDate:'18 août 2026'},
    {id:'senate-id',state:'Idaho',rating:'Safe R',cls:'safe-r',rep:'Jim Risch',repD:'Sénateur sortant',dem:'David Roth',demD:'Candidat démocrate',repPct:64,demPct:34,proj:{rSafe:90,rLikely:8,rLean:2,tossup:0,dLean:0,dLikely:0},note:'Siège républicain très sûr',primaryDate:'19 mai 2026'},
    {id:'senate-ok',state:'Oklahoma',rating:'Safe R',cls:'safe-r',rep:'Kevin Hern',repD:'Représentant (OK-1)',dem:'Jason Hart',demD:'Ancien procureur fédéral',repPct:62,demPct:36,proj:{rSafe:88,rLikely:10,rLean:2,tossup:0,dLean:0,dLikely:0},note:'Siège républicain très sûr (Mullin parti au DHS)',primaryDate:'16 mai 2026'},
    {id:'senate-sd',state:'South Dakota',rating:'Safe R',cls:'safe-r',rep:'Mike Rounds',repD:'Sénateur sortant',dem:'Julian Beaudion',demD:'Ancien trooper d\'État',repPct:64,demPct:34,proj:{rSafe:92,rLikely:6,rLean:2,tossup:0,dLean:0,dLikely:0},note:'Siège républicain très sûr',primaryDate:'2 juin 2026'},
    {id:'senate-ne',state:'Nebraska',rating:'Safe R',cls:'safe-r',rep:'Pete Ricketts',repD:'Sénateur nommé',dem:'Dan Osborn',demD:'Indépendant (soutenu par les Démocrates)',repPct:58,demPct:40,proj:{rSafe:85,rLikely:10,rLean:5,tossup:0,dLean:0,dLikely:0},note:'Siège républicain très sûr',primaryDate:'12 mai 2026'},
    {id:'senate-ks',state:'Kansas',rating:'Safe R',cls:'safe-r',rep:'Roger Marshall',repD:'Sénateur sortant',dem:'Anne Parelkar',demD:'Candidat démocrate',repPct:60,demPct:38,proj:{rSafe:85,rLikely:10,rLean:5,tossup:0,dLean:0,dLikely:0},note:'Siège républicain très sûr',primaryDate:'4 août 2026'},
    {id:'senate-ar',state:'Arkansas',rating:'Safe R',cls:'safe-r',rep:'Tom Cotton',repD:'Sénateur sortant',dem:'Hallie Shoffner',demD:'Agricultrice',repPct:62,demPct:36,proj:{rSafe:88,rLikely:10,rLean:2,tossup:0,dLean:0,dLikely:0},note:'Siège républicain très sûr',primaryDate:'3 mars 2026'},
    {id:'senate-al',state:'Alabama',rating:'Safe R',cls:'safe-r',rep:'Barry Moore',repD:'Représentant (AL-2)',dem:'Dakarai Larriett',demD:'Candidat démocrate',repPct:62,demPct:36,proj:{rSafe:88,rLikely:10,rLean:2,tossup:0,dLean:0,dLikely:0},note:'Siège ouvert (Tuberville candidat au poste de gouverneur)',primaryDate:'19 mai 2026'},
    {id:'senate-ms',state:'Mississippi',rating:'Safe R',cls:'safe-r',rep:'Cindy Hyde-Smith',repD:'Sénatrice sortante',dem:'Scott Colom',demD:'Procureur de district',repPct:60,demPct:38,proj:{rSafe:88,rLikely:10,rLean:2,tossup:0,dLean:0,dLikely:0},note:'Siège républicain très sûr',primaryDate:'10 mars 2026'},
    {id:'senate-tn',state:'Tennessee',rating:'Safe R',cls:'safe-r',rep:'Bill Hagerty',repD:'Sénateur sortant',dem:'David Miller',demD:'Éducateur retraité',repPct:62,demPct:36,proj:{rSafe:88,rLikely:10,rLean:2,tossup:0,dLean:0,dLikely:0},note:'Siège républicain très sûr',primaryDate:'6 août 2026'},
    {id:'senate-ky',state:'Kentucky',rating:'Safe R',cls:'safe-r',rep:'Daniel Cameron',repD:'Ancien procureur général',dem:'Amy McGrath',demD:'Ancienne pilote de chasse',repPct:58,demPct:40,proj:{rSafe:85,rLikely:12,rLean:3,tossup:0,dLean:0,dLikely:0},note:'Siège ouvert (McConnell retraité)',primaryDate:'19 mai 2026'},
    {id:'senate-sc',state:'Caroline du Sud',rating:'Safe R',cls:'safe-r',rep:'Lindsey Graham',repD:'Sénateur sortant',dem:'Annie Andrews',demD:'Pédiatre',repPct:57,demPct:41,proj:{rSafe:82,rLikely:13,rLean:5,tossup:0,dLean:0,dLikely:0},note:'Siège républicain très sûr',primaryDate:'9 juin 2026'},
    {id:'senate-wv',state:'Virginie-Occidentale',rating:'Safe R',cls:'safe-r',rep:'Shelley Moore Capito',repD:'Sénatrice sortante',dem:'Rio Phillips',demD:'Entrepreneur média',repPct:63,demPct:35,proj:{rSafe:90,rLikely:8,rLean:2,tossup:0,dLean:0,dLikely:0},note:'Siège républicain très sûr',primaryDate:'12 mai 2026'},
    // LIKELY R
    {id:'senate-la',state:'Louisiane',rating:'Likely R',cls:'likely-r',rep:'Julia Letlow',repD:'Représentante (LA-5)',dem:'Gary Chambers',demD:'Militant',repPct:54,demPct:44,proj:{rSafe:55,rLikely:30,rLean:10,tossup:5,dLean:0,dLikely:0},note:'Primaire compétitive (Cassidy vs Letlow)',primaryDate:'16 mai 2026'},
    {id:'senate-mt',state:'Montana',rating:'Likely R',cls:'likely-r',rep:'Kurt Alme',repD:'Ancien procureur fédéral',dem:'Reilly Neill',demD:'Femme d\'affaires',repPct:53,demPct:45,proj:{rSafe:50,rLikely:30,rLean:12,tossup:8,dLean:0,dLikely:0},note:'Siège ouvert (Daines retraité)',primaryDate:'2 juin 2026'},
    // LEAN R
    {id:'senate-ak',state:'Alaska',rating:'Lean R',cls:'lean-r',rep:'Dan Sullivan',repD:'Sénateur sortant',dem:'Mary Peltola',demD:'Ancienne représentante',repPct:49,demPct:48,proj:{rSafe:20,rLikely:25,rLean:25,tossup:20,dLean:10,dLikely:0},note:'Course compétitive (Peltola bonne candidate)',primaryDate:'19 août 2026'},
    {id:'senate-tx',state:'Texas',rating:'Lean R',cls:'lean-r',rep:'John Cornyn',repD:'Sénateur sortant',dem:'James Talarico',demD:'Représentant d\'État',repPct:48,demPct:46,proj:{rSafe:20,rLikely:25,rLean:15,tossup:20,dLean:12,dLikely:8},note:'Course compétitive (second tour GOP)',primaryDate:'4 mars 2026'},
    {id:'senate-ia',state:'Iowa',rating:'Lean R',cls:'lean-r',rep:'Ashley Hinson',repD:'Représentante (IA-2)',dem:'Josh Turek',demD:'Représentant d\'État',repPct:50,demPct:46,proj:{rSafe:25,rLikely:30,rLean:20,tossup:15,dLean:10,dLikely:0},note:'Siège ouvert (Ernst ne se représente pas)',primaryDate:'2 juin 2026'},
    // TILT R
    {id:'senate-oh',state:'Ohio (spéciale)',rating:'Tilt R',cls:'tilt-r',rep:'Jon Husted',repD:'Sénateur nommé',dem:'Sherrod Brown',demD:'Ancien sénateur',repPct:48,demPct:47,proj:{rSafe:10,rLikely:20,rLean:25,tossup:25,dLean:15,dLikely:5},note:'Élection spéciale (siège de JD Vance)',primaryDate:'5 mai 2026'},
    // TOSSUP
    {id:'senate-ga',state:'Géorgie',rating:'Tossup',cls:'tossup',rep:'Mike Collins',repD:'Représentant (GA-10)',dem:'Jon Ossoff',demD:'Sénateur sortant',repPct:47,demPct:48,proj:{rSafe:10,rLikely:15,rLean:20,tossup:30,dLean:15,dLikely:10},note:'Course ultra-compétitive',primaryDate:'19 mai 2026'},
    {id:'senate-nc',state:'Caroline du Nord',rating:'Tossup',cls:'tossup',rep:'Michael Whatley',repD:'Ancien président du RNC',dem:'Roy Cooper',demD:'Ancien gouverneur',repPct:46,demPct:50,proj:{rSafe:5,rLikely:10,rLean:15,tossup:30,dLean:25,dLikely:15},note:'Course compétitive (Tillis retraité)',primaryDate:'3 mars 2026'},
    {id:'senate-me',state:'Maine',rating:'Tossup',cls:'tossup',rep:'Susan Collins',repD:'Sénatrice sortante',dem:'Graham Platner',demD:'Ostréiculteur',repPct:47,demPct:49,proj:{rSafe:5,rLikely:15,rLean:20,tossup:30,dLean:20,dLikely:10},note:'Course très compétitive',primaryDate:'9 juin 2026'},
    // TILT D
    {id:'senate-mi',state:'Michigan',rating:'Tilt D',cls:'tilt-d',rep:'Mike Rogers',repD:'Ancien représentant',dem:'Mallory McMorrow',demD:'Sénatrice d\'État',repPct:46,demPct:50,proj:{rSafe:5,rLikely:10,rLean:15,tossup:25,dLean:25,dLikely:20},note:'Siège ouvert (Peters ne se représente pas)',primaryDate:'5 août 2026'},
    // LEAN D
    {id:'senate-mn',state:'Minnesota',rating:'Lean D',cls:'lean-d',rep:'Michele Tafoya',repD:'Ancienne reporter NFL',dem:'Peggy Flanagan',demD:'Lieutenante-gouverneure',repPct:44,demPct:52,proj:{rSafe:0,rLikely:5,rLean:10,tossup:20,dLean:30,dLikely:35},note:'Siège ouvert (Smith retraitée)',primaryDate:'11 août 2026'},
    {id:'senate-nh',state:'New Hampshire',rating:'Lean D',cls:'lean-d',rep:'John E. Sununu',repD:'Ancien sénateur',dem:'Chris Pappas',demD:'Représentant (NH-1)',repPct:46,demPct:51,proj:{rSafe:0,rLikely:5,rLean:15,tossup:25,dLean:30,dLikely:25},note:'Siège ouvert (Shaheen retraitée)',primaryDate:'8 septembre 2026'},
    {id:'senate-va',state:'Virginie',rating:'Lean D',cls:'lean-d',rep:'Bryce Reeves',repD:'Sénateur d\'État',dem:'Mark Warner',demD:'Sénateur sortant',repPct:45,demPct:52,proj:{rSafe:0,rLikely:5,rLean:10,tossup:20,dLean:30,dLikely:35},note:'Siège démocrate compétitif',primaryDate:'16 juin 2026'},
    // LIKELY D
    {id:'senate-co',state:'Colorado',rating:'Likely D',cls:'likely-d',rep:'Janak Joshi',repD:'Médecin',dem:'John Hickenlooper',demD:'Sénateur sortant',repPct:42,demPct:56,proj:{rSafe:0,rLikely:0,rLean:5,tossup:10,dLean:30,dLikely:55},note:'Siège démocrate favorable',primaryDate:'30 juin 2026'},
    {id:'senate-nj',state:'New Jersey',rating:'Likely D',cls:'likely-d',rep:'Alex Zdan',repD:'Ancien journaliste',dem:'Cory Booker',demD:'Sénateur sortant',repPct:41,demPct:57,proj:{rSafe:0,rLikely:0,rLean:5,tossup:10,dLean:25,dLikely:60},note:'Siège démocrate favorable',primaryDate:'2 juin 2026'},
    // SAFE D
    {id:'senate-il',state:'Illinois',rating:'Safe D',cls:'safe-d',rep:'Don Tracy',repD:'Ancien président du GOP d\'État',dem:'Juliana Stratton',demD:'Lieutenante-gouverneure',repPct:38,demPct:60,proj:{rSafe:0,rLikely:0,rLean:0,tossup:5,dLean:10,dLikely:85},note:'Siège démocrate très sûr (Durbin retraité)',primaryDate:'17 mars 2026'},
    {id:'senate-de',state:'Delaware',rating:'Safe D',cls:'safe-d',rep:'Mike Katz',repD:'Ancien sénateur d\'État',dem:'Chris Coons',demD:'Sénateur sortant',repPct:37,demPct:61,proj:{rSafe:0,rLikely:0,rLean:0,tossup:5,dLean:10,dLikely:85},note:'Siège démocrate très sûr',primaryDate:'15 septembre 2026'},
    {id:'senate-ma',state:'Massachusetts',rating:'Safe D',cls:'safe-d',rep:'John Deaton',repD:'Avocat',dem:'Ed Markey',demD:'Sénateur sortant',repPct:36,demPct:62,proj:{rSafe:0,rLikely:0,rLean:0,tossup:5,dLean:10,dLikely:85},note:'Siège démocrate très sûr',primaryDate:'15 septembre 2026'},
    {id:'senate-ri',state:'Rhode Island',rating:'Safe D',cls:'safe-d',rep:'Connor Burbridge',repD:'Candidat républicain',dem:'Jack Reed',demD:'Sénateur sortant',repPct:35,demPct:63,proj:{rSafe:0,rLikely:0,rLean:0,tossup:5,dLean:10,dLikely:85},note:'Siège démocrate très sûr',primaryDate:'8 septembre 2026'},
    {id:'senate-or',state:'Oregon',rating:'Safe D',cls:'safe-d',rep:'David Brock Smith',repD:'Sénateur d\'État',dem:'Jeff Merkley',demD:'Sénateur sortant',repPct:38,demPct:60,proj:{rSafe:0,rLikely:0,rLean:0,tossup:5,dLean:10,dLikely:85},note:'Siège démocrate très sûr',primaryDate:'19 mai 2026'},
    {id:'senate-nm',state:'Nouveau-Mexique',rating:'Safe D',cls:'safe-d',rep:'(aucun qualifié)',repD:'Pas de républicain sur le bulletin',dem:'Ben Ray Luján',demD:'Sénateur sortant',repPct:0,demPct:98,proj:{rSafe:0,rLikely:0,rLean:0,tossup:0,dLean:5,dLikely:95},note:'Aucun républicain qualifié',primaryDate:'2 juin 2026'},
    // Floride spéciale (pas classe 2)
    {id:'senate-fl',state:'Floride (spéciale)',rating:'Likely R',cls:'likely-r',rep:'Jeanette Nuñez',repD:'Ancienne lieutenante-gouverneure',dem:'Debbie Mucarsel-Powell',demD:'Ancienne représentante',repPct:53,demPct:44,proj:{rSafe:45,rLikely:35,rLean:12,tossup:8,dLean:0,dLikely:0},note:'Élection spéciale (siège de Marco Rubio)',primaryDate:'18 août 2026'}
  ];

  // Générer les entrées de course pour chaque sénateur
  senateRaces.forEach(r => {
    if (!racesData[r.id]) {
      const initials = (n) => n.split(' ').map(w => w[0]).join('');
      const polls = [];
      for (let m = 1; m <= 9; m++) {
        const vR = r.repPct + Math.round(Math.random() * 6 - 3);
        const vD = r.demPct + Math.round(Math.random() * 6 - 3);
        polls.push({ date: ['Jan','Fév','Mar','Avr','Mai','Jun','Jul','Aoû','Sep'][m-1], rep: vR, dem: vD });
      }
      polls.push({ date: 'Sep', rep: r.repPct, dem: r.demPct });

      racesData[r.id] = {
        title: `Sénat · ${r.state}`,
        rating: r.rating,
        ratingClass: r.cls,
        candidates: [
          { name: r.rep, party: 'R', initials: initials(r.rep), pct: r.repPct, desc: r.repD },
          { name: r.dem, party: 'D', initials: initials(r.dem), pct: r.demPct, desc: r.demD }
        ],
        proj: r.proj,
        seats: r.note,
        moe: '±3.5%',
        sample: '1 200 LV',
        dates: 'Sep 2026',
        polls: polls,
        primaryDate: r.primaryDate,
        primaries: {
          rep: { note: 'Pas de primaire compétitive.', cands: [{ name: r.rep, init: initials(r.rep), desc: 'Candidat présumé', score: '100%', cls: 'rr', badge: 'Investiture' }], polls: [] },
          dem: { note: 'Pas de primaire compétitive.', cands: [{ name: r.dem, init: initials(r.dem), desc: 'Candidat présumé', score: '100%', cls: 'dd', badge: 'Investiture' }], polls: [] }
        }
      };
    }
  });

  // Remplir la liste Sénat
  const senateList = document.getElementById('senate-races');
  senateRaces.forEach(r => {
    const item = document.createElement('div');
    item.className = 'race-item';
    item.dataset.race = r.id;
    item.innerHTML = `<div class="race-info"><h3>${r.state}</h3><p>${r.rep} (R) vs ${r.dem} (D)</p></div><div class="race-tag ${r.cls}">${r.rating}</div>`;
    senateList.appendChild(item);
  });

  // ---- AFFICHAGE DES DÉTAILS ----
  function showRaceDetail(raceId) {
    const data = racesData[raceId];
    if (!data) return;
    const container = document.getElementById('detail-container');
    container.innerHTML = `
      <div class="card">
        <div class="card-header"><div class="card-title">${data.title}</div><div class="race-tag ${data.ratingClass}">${data.rating}</div></div>
        ${data.candidates.map(c => `
          <div class="candidate-row">
            <div class="candidate-label"><span class="party-name ${c.party==='R'?'rep':'dem'}">${c.name} (${c.party})</span><span class="party-pct ${c.party==='R'?'rep':'dem'}">${c.pct}%</span></div>
            <div style="color:rgba(255,255,255,0.45);font-size:0.75rem;margin-bottom:0.4rem;">${c.desc}</div>
            <div class="bar-wrap"><div class="bar-fill ${c.party==='R'?'rf':'df'}" style="width:${c.pct}%">${c.pct}%</div></div>
          </div>
        `).join('')}
        <div class="poll-footer"><span>📊 Marge ${data.moe}</span><span>👥 ${data.sample} · ${data.dates}</span></div>
        <div style="margin-top:1.2rem;"><h4 style="color:rgba(255,255,255,0.55);font-size:0.8rem;text-transform:uppercase;">Probabilités</h4>
          <div class="projections-bar">
            <div class="p-safe-r" style="width:${data.proj.rSafe}%"></div><div class="p-likely-r" style="width:${data.proj.rLikely}%"></div><div class="p-lean-r" style="width:${data.proj.rLean}%"></div>
            <div class="p-tossup" style="width:${data.proj.tossup}%"></div><div class="p-lean-d" style="width:${data.proj.dLean}%"></div><div class="p-likely-d" style="width:${data.proj.dLikely}%"></div>
          </div>
          <div style="display:flex;justify-content:space-between;font-size:0.6rem;color:rgba(255,255,255,0.35);">${['R+10+','R+5-9','R+1-4','Tossup','D+1-4','D+5+'].map(s=>'<span>'+s+'</span>').join('')}</div>
          <div style="text-align:center;color:rgba(255,255,255,0.55);font-size:0.85rem;margin:0.8rem 0;">${data.seats}</div>
        </div>
        <div style="margin-top:1.2rem;"><h4 style="color:rgba(255,255,255,0.55);font-size:0.8rem;text-transform:uppercase;">📈 Sondages</h4>
          <div class="chart-container"><canvas id="detailChart" width="800" height="260"></canvas><div class="chart-tooltip" id="chartTooltip" style="opacity:0;"></div></div>
          <div class="chart-legend"><span><span class="legend-dot r"></span> ${data.candidates[0].name.split(' ').pop()} (R)</span><span><span class="legend-dot d"></span> ${data.candidates[1].name.split(' ').pop()} (D)</span><span style="opacity:0.55;">— Moyenne mobile (3)</span></div>
        </div>
      </div>
      <div class="card">
        <div class="card-header"><div class="card-title">Primaires</div><div style="color:rgba(255,255,255,0.5);font-size:0.8rem;">📅 ${data.primaryDate}</div></div>
        <div class="prim-tabs"><div class="prim-tab ra active" data-prim="rep">Primaire Républicaine</div><div class="prim-tab da" data-prim="dem">Primaire Démocrate</div></div>
        <div class="prim-panel active" id="panel-rep">
          <div class="primary-grid">${data.primaries.rep.cands.map(c => `<div class="candidate-card"><div class="cand-photo ${c.cls}">${c.init}</div><div class="cand-name">${c.name}</div><div style="font-size:0.7rem;color:rgba(255,255,255,0.5);">${c.desc}</div><div style="font-size:1.6rem;font-weight:800;color:${c.cls==='rr'?'#ff9e8f':'#8fc1ff'};">${c.score}</div><div style="font-size:0.65rem;font-weight:700;color:#ffd700;">${c.badge}</div></div>`).join('')}</div>
          ${data.primaries.rep.polls && data.primaries.rep.polls.length > 0 ? `<table style="width:100%;border-collapse:collapse;color:white;font-size:0.8rem;"><thead><tr style="background:rgba(0,0,0,0.4);"><th>Institut</th><th>Date</th>${data.primaries.rep.cands.map(c=>`<th>${c.name.split(' ').pop()}</th>`).join('')}</tr></thead><tbody>${data.primaries.rep.polls.map((p,i)=>`<tr style="${i===0?'background:rgba(0,0,0,0.3);font-weight:600;':''}"><td>${p.inst}</td><td>${p.date}</td>${p.vals.map(v=>`<td style="color:#ff9e8f;">${v}</td>`).join('')}</tr>`).join('')}</tbody></table>`:''}
          <div style="color:rgba(255,255,255,0.5);font-size:0.75rem;text-align:center;margin-top:0.8rem;">${data.primaries.rep.note}</div>
        </div>
        <div class="prim-panel" id="panel-dem">
          <div class="primary-grid">${data.primaries.dem.cands.map(c => `<div class="candidate-card"><div class="cand-photo ${c.cls}">${c.init}</div><div class="cand-name">${c.name}</div><div style="font-size:0.7rem;color:rgba(255,255,255,0.5);">${c.desc}</div><div style="font-size:1.6rem;font-weight:800;color:${c.cls==='rr'?'#ff9e8f':'#8fc1ff'};">${c.score}</div><div style="font-size:0.65rem;font-weight:700;color:#ffd700;">${c.badge}</div></div>`).join('')}</div>
          ${data.primaries.dem.polls && data.primaries.dem.polls.length > 0 ? `<table style="width:100%;border-collapse:collapse;color:white;font-size:0.8rem;"><thead><tr style="background:rgba(0,0,0,0.4);"><th>Institut</th><th>Date</th>${data.primaries.dem.cands.map(c=>`<th>${c.name.split(' ').pop()}</th>`).join('')}</tr></thead><tbody>${data.primaries.dem.polls.map((p,i)=>`<tr style="${i===0?'background:rgba(0,0,0,0.3);font-weight:600;':''}"><td>${p.inst}</td><td>${p.date}</td>${p.vals.map(v=>`<td style="color:#8fc1ff;">${v}</td>`).join('')}</tr>`).join('')}</tbody></table>`:''}
          <div style="color:rgba(255,255,255,0.5);font-size:0.75rem;text-align:center;margin-top:0.8rem;">${data.primaries.dem.note}</div>
        </div>
      </div>
    `;
    setTimeout(() => {
      container.querySelectorAll('.prim-tab').forEach(tab => {
        tab.addEventListener('click', function() {
          const target = this.dataset.prim;
          container.querySelectorAll('.prim-tab').forEach(t => t.classList.remove('active','ra','da'));
          this.classList.add('active');
          this.classList.add(target==='rep'?'ra':'da');
          container.querySelectorAll('.prim-panel').forEach(p => p.classList.remove('active'));
          container.querySelector('#panel-'+target).classList.add('active');
        });
      });
      drawChart(data.polls, data.candidates);
    }, 100);
  }

  function drawChart(polls, candidates) {
    const canvas = document.getElementById('detailChart');
    if (!canvas) return;
    const ctx = canvas.getContext('2d');
    const tooltip = document.getElementById('chartTooltip');
    const repAvg = [], demAvg = [];
    for (let i = 0; i < polls.length; i++) {
      let sR = 0, sD = 0, c = 0;
      for (let j = Math.max(0, i - 2); j <= i; j++) { sR += polls[j].rep; sD += polls[j].dem; c++; }
      repAvg.push(Math.round((sR / c) * 10) / 10);
      demAvg.push(Math.round((sD / c) * 10) / 10);
    }
    const pad = { top: 22, right: 28, bottom: 32, left: 38 }, minY = 25, maxY = 70;
    let points = [];
    function draw() {
      const w = canvas.width, h = canvas.height, cW = w - pad.left - pad.right, cH = h - pad.top - pad.bottom;
      ctx.clearRect(0, 0, w, h);
      ctx.fillStyle = 'rgba(10,10,18,0.5)';
      ctx.fillRect(pad.left, pad.top, cW, cH);
      const gX = i => pad.left + (i / (polls.length - 1)) * cW, gY = v => pad.top + cH - ((v - minY) / (maxY - minY)) * cH;
      ctx.strokeStyle = 'rgba(255,255,255,0.06)'; ctx.lineWidth = 0.5;
      for (let i = minY; i <= maxY; i += 5) { const y = gY(i); ctx.beginPath(); ctx.moveTo(pad.left, y); ctx.lineTo(pad.left + cW, y); ctx.stroke(); }
      ctx.fillStyle = 'rgba(255,255,255,0.45)'; ctx.font = '9px Segoe UI'; ctx.textAlign = 'center';
      polls.forEach((p, i) => ctx.fillText(p.date, gX(i), pad.top + cH + 10));
      [{ d: repAvg, c: '#ff8a7a' }, { d: demAvg, c: '#8fc1ff' }].forEach(l => {
        ctx.beginPath(); ctx.moveTo(gX(0), gY(l.d[0]));
        for (let i = 1; i < l.d.length; i++) { const xc = gX(i), yc = gY(l.d[i]), xp = gX(i - 1), yp = gY(l.d[i - 1]); ctx.bezierCurveTo(xp + (xc - xp) * 0.5, yp, xc - (xc - xp) * 0.5, yc, xc, yc); }
        ctx.strokeStyle = l.c; ctx.lineWidth = 2.2; ctx.stroke();
      });
      points = [];
      polls.forEach((p, i) => {
        [{ v: p.rep, t: 'r', c: 'rgba(180,40,40,0.5)' }, { v: p.dem, t: 'd', c: 'rgba(30,80,180,0.5)' }].forEach(pt => {
          const x = gX(i), y = gY(pt.v); points.push({ x, y, type: pt.t, value: pt.v, date: p.date });
          ctx.beginPath(); ctx.arc(x, y, 5.5, 0, 2 * Math.PI); ctx.fillStyle = pt.c; ctx.fill(); ctx.strokeStyle = 'rgba(255,255,255,0.18)'; ctx.stroke();
        });
      });
    }
    draw();
    canvas.onmousemove = function(e) {
      const rect = canvas.getBoundingClientRect(), sX = canvas.width / rect.width, sY = canvas.height / rect.height;
      const mx = (e.clientX - rect.left) * sX, my = (e.clientY - rect.top) * sY;
      let cl = null, md = 18;
      points.forEach(p => { const d = Math.hypot(mx - p.x, my - p.y); if (d < md) { md = d; cl = p; } });
      if (cl) {
        const name = cl.type === 'r' ? candidates[0].name : candidates[1].name;
        tooltip.innerHTML = '<strong>' + name + '</strong><br><span style="color:' + (cl.type === 'r' ? '#ff9e8f' : '#8fc1ff') + ';font-size:14px;">' + cl.value + '%</span><br><span style="opacity:0.55;">' + cl.date + ' 2026</span>';
        tooltip.style.left = Math.max(5, Math.min(cl.x / sX - 50, rect.width - 100)) + 'px';
        tooltip.style.top = Math.max(5, cl.y / sY - 50) + 'px'; tooltip.style.opacity = '1';
      } else { tooltip.style.opacity = '0'; }
    };
    canvas.onmouseleave = () => tooltip.style.opacity = '0';
  }

  // Gestion des onglets
  document.querySelectorAll('.cat-tab').forEach(tab => {
    tab.addEventListener('click', function() {
      document.querySelectorAll('.cat-tab').forEach(t => t.classList.remove('active'));
      this.classList.add('active');
      document.querySelectorAll('.cat-panel').forEach(p => p.classList.remove('active'));
      const catId = 'cat-' + this.dataset.cat;
      document.getElementById(catId).classList.add('active');
      const firstRace = document.querySelector('#' + catId + ' .race-item[data-race]');
      if (firstRace) firstRace.click();
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

  // Afficher le premier Sénat par défaut
  const firstSenate = document.querySelector('#cat-senate .race-item[data-race]');
  if (firstSenate) firstSenate.click();
})();
</script>
<div style="height:20px;"></div>
</body>
</html>
