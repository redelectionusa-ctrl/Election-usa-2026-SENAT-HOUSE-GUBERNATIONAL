<!DOCTYPE html>
<html lang="fr">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Election USA 2026 · House, Senate & Gubernatorial</title>
  <style>
    * { margin:0; padding:0; box-sizing:border-box; }
    body {
      min-height:100vh; width:100%;
      font-family:'Segoe UI', 'Roboto', system-ui, sans-serif;
      display:flex; flex-direction:column; align-items:center;
      background: radial-gradient(ellipse at 20% 50%, #0a1f3a 0%, #000 50%, #2a0a0a 100%);
      background-attachment:fixed;
      padding:20px;
      color: #fff;
      overflow-x: hidden;
    }
    body::before {
      content: '';
      position: fixed;
      top: 0; left: 0; right: 0; bottom: 0;
      background: url('data:image/svg+xml;utf8,<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 100 100" fill="none"><circle cx="20" cy="80" r="1" fill="white" opacity="0.3"/><circle cx="80" cy="30" r="1.5" fill="white" opacity="0.2"/><circle cx="50" cy="10" r="0.8" fill="white" opacity="0.4"/><circle cx="90" cy="70" r="1" fill="white" opacity="0.25"/></svg>');
      background-size: 200px 200px;
      opacity: 0.4;
      pointer-events: none;
      animation: drift 30s linear infinite;
    }
    @keyframes drift {
      0% { transform: translate(0, 0); }
      100% { transform: translate(-200px, -200px); }
    }
    .main-header {
      width:100%; max-width:1400px;
      background: rgba(5,10,20,0.6);
      backdrop-filter: blur(16px);
      -webkit-backdrop-filter: blur(16px);
      padding: 1.8rem 2rem;
      text-align:center;
      margin-bottom: 30px;
      box-shadow: 0 15px 40px rgba(0,0,0,0.7), 0 0 0 1px rgba(210,180,140,0.2) inset;
      border-bottom: 1px solid rgba(210,180,140,0.2);
      border-radius: 12px;
      position: relative;
      z-index: 10;
    }
    .main-title {
      font-size: clamp(2.2rem, 6vw, 4.5rem);
      font-weight: 900;
      letter-spacing: 0.25em;
      color: #fff;
      text-transform: uppercase;
      text-shadow: 0 0 30px rgba(255,215,150,0.4), 0 4px 20px rgba(0,0,0,0.8);
      animation: titleGlow 3s ease-in-out infinite alternate;
    }
    @keyframes titleGlow {
      from { text-shadow: 0 0 30px rgba(255,215,150,0.3), 0 4px 20px rgba(0,0,0,0.8); }
      to { text-shadow: 0 0 50px rgba(255,215,150,0.6), 0 4px 25px rgba(0,0,0,0.9); }
    }
    .main-subtitle {
      font-size: clamp(1rem, 2.5vw, 1.6rem);
      color: rgba(255,255,255,0.9);
      letter-spacing: 0.4em;
      text-transform: uppercase;
      border-top: 1.5px solid rgba(255,215,150,0.5);
      display: inline-block;
      padding-top: 0.7rem;
      margin-top: 0.6rem;
      font-weight: 300;
      text-shadow: 0 0 15px rgba(0,0,0,0.5);
    }
    .main-content { width:100%; max-width:1400px; position: relative; z-index: 5; }
    .category-tabs { display:flex; gap:0.8rem; margin-bottom: 2rem; flex-wrap:wrap; }
    .cat-tab {
      background: rgba(0,0,0,0.5);
      backdrop-filter: blur(8px);
      border: 1px solid rgba(255,255,255,0.15);
      color: white;
      padding: 1rem 1.8rem;
      font-size: 1.1rem;
      font-weight: 700;
      text-transform: uppercase;
      letter-spacing: 0.15em;
      cursor: pointer;
      flex: 1; min-width: 140px;
      text-align: center;
      transition: all 0.3s ease;
      border-radius: 50px;
      position: relative;
      overflow: hidden;
    }
    .cat-tab::before {
      content: '';
      position: absolute;
      top: 0; left: -100%;
      width: 100%; height: 100%;
      background: linear-gradient(90deg, transparent, rgba(255,215,150,0.2), transparent);
      transition: left 0.5s;
    }
    .cat-tab:hover::before { left: 100%; }
    .cat-tab:hover {
      background: rgba(255,255,255,0.1);
      border-color: rgba(255,215,150,0.4);
      transform: translateY(-2px);
      box-shadow: 0 8px 25px rgba(0,0,0,0.3);
    }
    .cat-tab.active {
      background: rgba(255,255,255,0.15);
      border-color: rgba(255,215,150,0.8);
      box-shadow: 0 0 30px rgba(255,215,150,0.25);
      font-weight: 800;
    }
    .cat-panel { display:none; }
    .cat-panel.active { display:block; animation: fadeInUp 0.4s ease; }
    @keyframes fadeInUp {
      from { opacity: 0; transform: translateY(20px); }
      to { opacity: 1; transform: translateY(0); }
    }
    .race-list { display:flex; flex-direction:column; gap:0.6rem; margin-bottom: 2rem; }
    .race-item {
      background: rgba(0,0,0,0.4);
      backdrop-filter: blur(10px);
      border: 1px solid rgba(220,200,180,0.15);
      padding: 1rem 1.8rem;
      cursor: pointer;
      display: flex;
      justify-content: space-between;
      align-items: center;
      flex-wrap: wrap;
      gap: 1rem;
      border-radius: 10px;
      transition: all 0.3s ease;
    }
    .race-item:hover {
      background: rgba(255,255,255,0.08);
      border-color: rgba(255,215,150,0.5);
      transform: translateX(5px);
      box-shadow: 0 10px 25px rgba(0,0,0,0.3);
    }
    .race-item.active {
      background: rgba(255,255,255,0.12);
      border-color: rgba(255,215,150,0.8);
      box-shadow: 0 0 35px rgba(255,215,150,0.2);
      transform: translateX(8px);
    }
    .race-info h3 { color: #f0e6d2; font-size: 1.1rem; margin-bottom: 0.2rem; font-weight: 600; }
    .race-info p { color: rgba(255,255,255,0.55); font-size: 0.8rem; }
    .race-tag {
      padding: 0.3rem 1rem;
      font-weight: 700;
      text-transform: uppercase;
      font-size: 0.7rem;
      letter-spacing: 0.1em;
      white-space: nowrap;
      border-radius: 20px;
      background: #222;
      border: 1px solid #444;
    }
    .safe-r { background: #3e0000; color: #ff8a80; border-color: #b71c1c; }
    .likely-r { background: #6a0a0a; color: #ff6b5e; border-color: #d32f2f; }
    .lean-r { background: #7a1515; color: #ff9e8f; border-color: #e53935; }
    .tilt-r { background: #8a2020; color: #ffab91; border-color: #ff7043; }
    .tossup { background: #5a4a00; color: #ffe082; border-color: #ffc107; }
    .tilt-d { background: #0a2f5a; color: #91caff; border-color: #42a5f5; }
    .lean-d { background: #0a2f6a; color: #8fc1ff; border-color: #1e88e5; }
    .likely-d { background: #0a2060; color: #64b5f6; border-color: #1976d2; }
    .safe-d { background: #001a4d; color: #82b1ff; border-color: #0d47a1; }
    .card {
      width: 100%;
      background: rgba(10,10,20,0.5);
      backdrop-filter: blur(16px);
      -webkit-backdrop-filter: blur(16px);
      border: 1px solid rgba(220,200,180,0.15);
      box-shadow: 0 25px 50px -10px rgba(0,0,0,0.8);
      padding: 2rem;
      margin-bottom: 1.5rem;
      border-radius: 20px;
      transition: transform 0.3s ease, box-shadow 0.3s ease;
    }
    .card:hover { box-shadow: 0 30px 60px -10px rgba(0,0,0,0.9), 0 0 0 1px rgba(255,215,150,0.2) inset; }
    .card-header {
      display: flex;
      align-items: center;
      justify-content: space-between;
      margin-bottom: 1.8rem;
      border-bottom: 2px solid rgba(255,255,255,0.12);
      padding-bottom: 1.4rem;
      flex-wrap: wrap;
      gap: 1rem;
    }
    .card-title {
      font-size: 1.5rem;
      font-weight: 600;
      letter-spacing: 0.1em;
      text-transform: uppercase;
      color: #f0e6d2;
      display: flex;
      align-items: center;
      gap: 1rem;
      text-shadow: 0 2px 10px rgba(0,0,0,0.5);
    }
    .rep { color: #ff9e8f; } .dem { color: #8fc1ff; }
    .candidate-row { margin-bottom: 1.6rem; }
    .candidate-label { display: flex; justify-content: space-between; margin-bottom: 0.4rem; flex-wrap: wrap; }
    .party-name { font-size: 1.2rem; font-weight: 700; letter-spacing: 0.06em; text-transform: uppercase; }
    .party-pct { font-size: 1.6rem; font-weight: 800; }
    .bar-wrap {
      width: 100%; height: 38px;
      background: rgba(18,18,18,0.9);
      border: 1px solid rgba(255,255,255,0.15);
      overflow: hidden;
      border-radius: 10px;
      box-shadow: inset 0 2px 8px rgba(0,0,0,0.5);
    }
    .bar-fill {
      height: 100%; display: flex; align-items: center; justify-content: flex-end;
      padding-right: 16px; font-weight: 700; color: white; font-size: 1rem;
      border-radius: 10px;
    }
    .bar-fill.rf { background: linear-gradient(90deg, #a51c1c, #d32f2f); box-shadow: 0 0 20px #e53935; }
    .bar-fill.df { background: linear-gradient(90deg, #0a3a7a, #1976d2); box-shadow: 0 0 20px #1e88e5; }
    .poll-footer {
      margin-top: 1.2rem;
      display: flex;
      justify-content: space-between;
      color: rgba(255,240,220,0.7);
      border-top: 1px solid rgba(255,255,240,0.08);
      padding-top: 1rem;
      font-size: 0.8rem;
    }
    .gauge-container { margin: 2rem 0 1.5rem; }
    .gauge-label {
      display: flex; justify-content: space-between;
      font-size: 0.7rem; color: rgba(255,255,255,0.5);
      margin-bottom: 0.5rem; text-transform: uppercase; letter-spacing: 0.05em;
    }
    .gauge-bar {
      height: 14px;
      background: linear-gradient(to right, #3e0000, #6a0a0a, #7a1515, #8a2020, #5a4a00, #0a2f5a, #0a2f6a, #0a2060, #001a4d);
      border-radius: 20px;
      position: relative;
      margin-bottom: 0.8rem;
      box-shadow: inset 0 2px 10px rgba(0,0,0,0.6), 0 0 20px rgba(255,255,255,0.1);
    }
    .gauge-arrow {
      position: absolute;
      top: -14px;
      transform: translateX(-50%);
      font-size: 2rem;
      filter: drop-shadow(0 4px 6px rgba(0,0,0,0.8));
      transition: left 0.6s cubic-bezier(0.25, 0.8, 0.25, 1.2);
      z-index: 2;
    }
    .gauge-pos-text {
      text-align: center;
      font-size: 0.9rem;
      color: rgba(255,255,255,0.8);
      font-weight: 600;
      text-shadow: 0 2px 8px rgba(0,0,0,0.5);
    }
    .projections-bar {
      display: flex; height: 10px; margin: 0.8rem 0; background: #121212;
      border-radius: 20px; overflow: hidden;
    }
    .p-safe-r { background:#3e0000; } .p-likely-r { background:#6a0a0a; } .p-lean-r { background:#7a1515; }
    .p-tilt-r { background:#8a2020; } .p-tossup { background:#5a4a00; } .p-tilt-d { background:#0a2f5a; }
    .p-lean-d { background:#0a2f6a; } .p-likely-d { background:#0a2060; } .p-safe-d { background:#001a4d; }
    .prim-tabs { display:flex; gap:0.8rem; margin-bottom:1.5rem; }
    .prim-tab {
      background: rgba(0,0,0,0.4);
      border: 1px solid rgba(255,255,255,0.2);
      color: white;
      padding: 0.7rem 1.2rem;
      font-size: 0.95rem; font-weight: 600;
      text-transform: uppercase; cursor: pointer;
      flex: 1; text-align: center;
      border-radius: 30px;
      transition: all 0.3s;
      letter-spacing: 0.05em;
    }
    .prim-tab:hover { background: rgba(255,255,255,0.1); border-color: rgba(255,215,150,0.4); }
    .prim-tab.active { background: rgba(255,255,255,0.2); border-color: rgba(255,215,150,0.7); box-shadow: 0 0 20px rgba(255,215,150,0.2); }
    .prim-tab.ra { background: rgba(229,57,53,0.25); border-color: #e53935; }
    .prim-tab.da { background: rgba(30,136,229,0.25); border-color: #1e88e5; }
    .prim-panel { display:none; }
    .prim-panel.active { display:block; animation: fadeIn 0.4s ease; }
    @keyframes fadeIn { from { opacity:0; } to { opacity:1; } }
    .primary-grid {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(180px, 1fr));
      gap: 1rem;
      margin-bottom: 1.5rem;
    }
    .candidate-card {
      background: rgba(0,0,0,0.3);
      border: 1px solid rgba(255,255,255,0.1);
      padding: 1.2rem;
      text-align: center;
      border-radius: 14px;
      transition: transform 0.2s, box-shadow 0.2s;
    }
    .candidate-card:hover { transform: translateY(-3px); box-shadow: 0 12px 25px rgba(0,0,0,0.4); border-color: rgba(255,215,150,0.3); }
    .cand-photo {
      width: 55px; height: 55px;
      border-radius: 50%;
      margin: 0 auto 0.8rem;
      display: flex; align-items: center; justify-content: center;
      font-weight: bold; font-size: 1.5rem;
      color: white;
      border: 2px solid rgba(255,255,255,0.3);
      box-shadow: 0 4px 12px rgba(0,0,0,0.5);
    }
    .cand-photo.rr { background: #a51c1c; }
    .cand-photo.dd { background: #0a3a7a; }
    .cand-name { font-size: 1rem; font-weight: 700; color: white; margin-top: 0.5rem; }
    .chart-container {
      position: relative; width:100%; height: 250px; margin: 1rem 0;
      border-radius: 12px; overflow: hidden;
      box-shadow: 0 8px 25px rgba(0,0,0,0.4);
    }
    canvas {
      display: block; width:100%; height:100%;
      background: rgba(10,10,15,0.6);
      border: 1px solid rgba(255,255,255,0.15);
      cursor: crosshair;
      border-radius: 12px;
    }
    .chart-tooltip {
      position: absolute;
      background: rgba(20,20,30,0.95);
      color: white;
      padding: 8px 14px;
      border: 1px solid rgba(255,255,255,0.3);
      font-size: 11px; font-weight: 600;
      pointer-events: none; z-index: 100;
      text-align: center; line-height: 1.4;
      white-space: nowrap;
      border-radius: 8px;
      backdrop-filter: blur(8px);
      box-shadow: 0 10px 25px rgba(0,0,0,0.7);
    }
    .chart-legend {
      display: flex; justify-content: center; gap: 1.5rem;
      margin-top: 0.8rem; color: rgba(255,255,255,0.7);
      font-size: 0.85rem;
    }
    .legend-dot {
      width: 10px; height: 10px; display: inline-block; margin-right: 5px; border-radius: 50%;
    }
    .legend-dot.r { background: #e53935; box-shadow: 0 0 10px #e53935; }
    .legend-dot.d { background: #1e88e5; box-shadow: 0 0 10px #1e88e5; }
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
  <div class="cat-panel active" id="cat-house"><div class="race-list" id="house-races"></div></div>
  <div class="cat-panel" id="cat-senate"><div class="race-list" id="senate-races"></div></div>
  <div class="cat-panel" id="cat-governor"><div class="race-list"><div class="race-item" style="opacity:0.5;cursor:default;"><div class="race-info"><h3>Courses à venir</h3><p>Données bientôt disponibles</p></div></div></div></div>
  <div id="detail-container"></div>
</div>

<script>
(function() {
  const ratingPositions = {'Safe R':5,'Likely R':16,'Lean R':27,'Tilt R':38,'Tossup':50,'Tilt D':62,'Lean D':73,'Likely D':84,'Safe D':95};
  const racesData = {};

  // NOUVEAUX DISTRICTS HOUSE (ajoutés à la liste)
  const houseRacesData = [
    // --- Districts existants ---
    {id:'house-wa3',state:'Washington',district:'3e District',rating:'Tossup',cls:'tossup',rep:'John Braun',repD:'Ancien chef de la minorité au Sénat d\'État',dem:'Marie Gluesenkamp Perez',demD:'Représentante sortante',repPct:47,demPct:48,proj:{rSafe:8,rLikely:12,rLean:15,rTilt:5,tossup:30,dTilt:5,dLean:18,dLikely:7},note:'Fourchette : +5D à +15R',primaryDate:'5 août 2025'},
    {id:'house-ca22',state:'Californie',district:'22e District',rating:'Lean D',cls:'lean-d',rep:'David Valadao',repD:'Représentant sortant',dem:'Jasmeet Bains',demD:'Médecin · Députée d\'État',repPct:46,demPct:50,proj:{rSafe:3,rLikely:8,rLean:12,rTilt:5,tossup:25,dTilt:8,dLean:28,dLikely:11},note:'Fourchette : +3D à +12R',primaryDate:'3 juin 2025'},
    
    // --- NOUVEAUX DISTRICTS ---
    // Arizona 1er et 6e
    {id:'house-az1',state:'Arizona',district:'1er District',rating:'Lean R',cls:'lean-r',rep:'David Schweikert',repD:'Représentant sortant',dem:'Conor O\'Callaghan',demD:'Ancien banquier',repPct:49,demPct:47,proj:{rSafe:10,rLikely:20,rLean:25,rTilt:5,tossup:25,dTilt:5,dLean:8,dLikely:2},note:'District compétitif (Trump +1.5%)',primaryDate:'5 août 2026'},
    {id:'house-az6',state:'Arizona',district:'6e District',rating:'Tossup',cls:'tossup',rep:'Juan Ciscomani',repD:'Représentant sortant',dem:'Kirsten Engel',demD:'Ancienne sénatrice d\'État',repPct:48,demPct:49,proj:{rSafe:5,rLikely:8,rLean:12,rTilt:5,tossup:30,dTilt:10,dLean:18,dLikely:12},note:'District ultra-compétitif (Biden +0.1%)',primaryDate:'5 août 2026'},
    
    // Colorado 8e
    {id:'house-co8',state:'Colorado',district:'8e District',rating:'Tossup',cls:'tossup',rep:'Gabe Evans',repD:'Représentant sortant',dem:'Yadira Caraveo',demD:'Ancienne représentante',repPct:47,demPct:48,proj:{rSafe:8,rLikely:10,rLean:12,rTilt:5,tossup:28,dTilt:8,dLean:18,dLikely:11},note:'District créé en 2022, très disputé',primaryDate:'24 juin 2026'},
    
    // Texas 34e
    {id:'house-tx34',state:'Texas',district:'34e District',rating:'Lean D',cls:'lean-d',rep:'Mayra Flores',repD:'Ancienne représentante',dem:'Vicente Gonzalez',demD:'Représentant sortant',repPct:47,demPct:50,proj:{rSafe:5,rLikely:8,rLean:10,rTilt:5,tossup:18,dTilt:8,dLean:25,dLikely:21},note:'District frontalier compétitif',primaryDate:'4 mars 2026'},
    
    // Iowa 1er et 3e
    {id:'house-ia1',state:'Iowa',district:'1er District',rating:'Lean R',cls:'lean-r',rep:'Mariannette Miller-Meeks',repD:'Représentante sortante',dem:'Christina Bohannan',demD:'Ancienne candidate',repPct:49,demPct:47,proj:{rSafe:12,rLikely:18,rLean:22,rTilt:8,tossup:22,dTilt:8,dLean:8,dLikely:2},note:'District compétitif du sud-est',primaryDate:'2 juin 2026'},
    {id:'house-ia3',state:'Iowa',district:'3e District',rating:'Tossup',cls:'tossup',rep:'Zach Nunn',repD:'Représentant sortant',dem:'Lanon Baccam',demD:'Ancien candidat',repPct:48,demPct:48,proj:{rSafe:5,rLikely:10,rLean:15,rTilt:8,tossup:28,dTilt:8,dLean:15,dLikely:11},note:'District de Des Moines très disputé',primaryDate:'2 juin 2026'},
    
    // Wisconsin 3e
    {id:'house-wi3',state:'Wisconsin',district:'3e District',rating:'Lean R',cls:'lean-r',rep:'Derrick Van Orden',repD:'Représentant sortant',dem:'Rebecca Cooke',demD:'Femme d\'affaires',repPct:49,demPct:47,proj:{rSafe:10,rLikely:20,rLean:22,rTilt:8,tossup:22,dTilt:8,dLean:8,dLikely:2},note:'District rural compétitif',primaryDate:'12 août 2026'},
    
    // Michigan 7e et 10e
    {id:'house-mi7',state:'Michigan',district:'7e District',rating:'Tossup',cls:'tossup',rep:'Tom Barrett',repD:'Représentant sortant',dem:'Curtis Hertel',demD:'Ancien sénateur d\'État',repPct:47,demPct:49,proj:{rSafe:5,rLikely:8,rLean:12,rTilt:8,tossup:28,dTilt:8,dLean:18,dLikely:13},note:'District de Lansing très disputé',primaryDate:'5 août 2026'},
    {id:'house-mi10',state:'Michigan',district:'10e District',rating:'Lean R',cls:'lean-r',rep:'John James',repD:'Représentant sortant',dem:'Carl Marlinga',demD:'Ancien candidat',repPct:50,demPct:47,proj:{rSafe:12,rLikely:18,rLean:22,rTilt:8,tossup:20,dTilt:8,dLean:8,dLikely:4},note:'District de Détroit suburbain',primaryDate:'5 août 2026'},
    
    // Ohio 9e
    {id:'house-oh9',state:'Ohio',district:'9e District',rating:'Lean D',cls:'lean-d',rep:'J.R. Majewski',repD:'Ancien candidat',dem:'Marcy Kaptur',demD:'Représentante sortante',repPct:46,demPct:51,proj:{rSafe:5,rLikely:8,rLean:10,rTilt:5,tossup:18,dTilt:8,dLean:25,dLikely:21},note:'District de Toledo, Kaptur bien implantée',primaryDate:'5 mai 2026'},
    
    // Pennsylvanie 7e, 8e, 10e
    {id:'house-pa7',state:'Pennsylvanie',district:'7e District',rating:'Lean R',cls:'lean-r',rep:'Ryan Mackenzie',repD:'Représentant sortant',dem:'Susan Wild',demD:'Ancienne représentante',repPct:49,demPct:47,proj:{rSafe:10,rLikely:18,rLean:22,rTilt:8,tossup:22,dTilt:8,dLean:8,dLikely:4},note:'District de Lehigh Valley',primaryDate:'19 mai 2026'},
    {id:'house-pa8',state:'Pennsylvanie',district:'8e District',rating:'Lean R',cls:'lean-r',rep:'Rob Bresnahan',repD:'Représentant sortant',dem:'Matt Cartwright',demD:'Ancien représentant',repPct:49,demPct:48,proj:{rSafe:8,rLikely:18,rLean:24,rTilt:8,tossup:22,dTilt:8,dLean:8,dLikely:4},note:'District de Scranton/Wilkes-Barre',primaryDate:'19 mai 2026'},
    {id:'house-pa10',state:'Pennsylvanie',district:'10e District',rating:'Lean R',cls:'lean-r',rep:'Scott Perry',repD:'Représentant sortant',dem:'Janelle Stelson',demD:'Ancienne candidate',repPct:50,demPct:46,proj:{rSafe:14,rLikely:20,rLean:20,rTilt:8,tossup:20,dTilt:8,dLean:6,dLikely:4},note:'District de Harrisburg',primaryDate:'19 mai 2026'},
    
    // New Jersey 7e
    {id:'house-nj7',state:'New Jersey',district:'7e District',rating:'Lean R',cls:'lean-r',rep:'Thomas Kean Jr.',repD:'Représentant sortant',dem:'Sue Altman',demD:'Militante progressiste',repPct:49,demPct:47,proj:{rSafe:10,rLikely:18,rLean:24,rTilt:8,tossup:20,dTilt:8,dLean:8,dLikely:4},note:'District suburbain compétitif',primaryDate:'2 juin 2026'},
    
    // New York 17e
    {id:'house-ny17',state:'New York',district:'17e District',rating:'Lean R',cls:'lean-r',rep:'Mike Lawler',repD:'Représentant sortant',dem:'Mondaire Jones',demD:'Ancien représentant',repPct:49,demPct:48,proj:{rSafe:8,rLikely:18,rLean:24,rTilt:8,tossup:22,dTilt:8,dLean:8,dLikely:4},note:'District de Hudson Valley, très disputé',primaryDate:'24 juin 2026'}
  ];

  // Course Sénat (inchangées, mais on garde la liste pour l'onglet Senate)
  const senateRaces = [
    {id:'senate-wy',state:'Wyoming',rating:'Safe R',cls:'safe-r',rep:'Cynthia Lummis',repD:'Sénatrice sortante (retraite)',dem:'Sam Mead',demD:'Rancher · Ancien maire',repPct:64,demPct:34,proj:{rSafe:92,rLikely:6,rLean:2,rTilt:0,tossup:0,dTilt:0,dLean:0,dLikely:0},note:'Siège républicain très sûr',primaryDate:'18 août 2026'},
    {id:'senate-id',state:'Idaho',rating:'Safe R',cls:'safe-r',rep:'Jim Risch',repD:'Sénateur sortant',dem:'David Roth',demD:'Candidat démocrate',repPct:63,demPct:35,proj:{rSafe:90,rLikely:8,rLean:2,rTilt:0,tossup:0,dTilt:0,dLean:0,dLikely:0},note:'Siège républicain très sûr',primaryDate:'19 mai 2026'},
    {id:'senate-ok',state:'Oklahoma',rating:'Safe R',cls:'safe-r',rep:'Kevin Hern',repD:'Représentant (OK-1)',dem:'Jason Hart',demD:'Ancien procureur fédéral',repPct:62,demPct:36,proj:{rSafe:88,rLikely:10,rLean:2,rTilt:0,tossup:0,dTilt:0,dLean:0,dLikely:0},note:'Siège républicain très sûr',primaryDate:'16 mai 2026'},
    {id:'senate-sd',state:'South Dakota',rating:'Safe R',cls:'safe-r',rep:'Mike Rounds',repD:'Sénateur sortant',dem:'Julian Beaudion',demD:'Ancien trooper',repPct:64,demPct:34,proj:{rSafe:92,rLikely:6,rLean:2,rTilt:0,tossup:0,dTilt:0,dLean:0,dLikely:0},note:'Siège républicain très sûr',primaryDate:'2 juin 2026'},
    {id:'senate-ne',state:'Nebraska',rating:'Safe R',cls:'safe-r',rep:'Pete Ricketts',repD:'Sénateur nommé',dem:'Dan Osborn',demD:'Indépendant (soutenu Dém)',repPct:57,demPct:41,proj:{rSafe:84,rLikely:12,rLean:4,rTilt:0,tossup:0,dTilt:0,dLean:0,dLikely:0},note:'Siège républicain très sûr',primaryDate:'12 mai 2026'},
    {id:'senate-ks',state:'Kansas',rating:'Safe R',cls:'safe-r',rep:'Roger Marshall',repD:'Sénateur sortant',dem:'Anne Parelkar',demD:'Candidat démocrate',repPct:60,demPct:38,proj:{rSafe:86,rLikely:10,rLean:4,rTilt:0,tossup:0,dTilt:0,dLean:0,dLikely:0},note:'Siège républicain très sûr',primaryDate:'4 août 2026'},
    {id:'senate-ar',state:'Arkansas',rating:'Safe R',cls:'safe-r',rep:'Tom Cotton',repD:'Sénateur sortant',dem:'Hallie Shoffner',demD:'Agricultrice',repPct:62,demPct:36,proj:{rSafe:88,rLikely:10,rLean:2,rTilt:0,tossup:0,dTilt:0,dLean:0,dLikely:0},note:'Siège républicain très sûr',primaryDate:'3 mars 2026'},
    {id:'senate-al',state:'Alabama',rating:'Safe R',cls:'safe-r',rep:'Barry Moore',repD:'Représentant (AL-2)',dem:'Dakarai Larriett',demD:'Candidat démocrate',repPct:62,demPct:36,proj:{rSafe:88,rLikely:10,rLean:2,rTilt:0,tossup:0,dTilt:0,dLean:0,dLikely:0},note:'Siège ouvert (Tuberville candidat gouverneur)',primaryDate:'19 mai 2026'},
    {id:'senate-ms',state:'Mississippi',rating:'Safe R',cls:'safe-r',rep:'Cindy Hyde-Smith',repD:'Sénatrice sortante',dem:'Scott Colom',demD:'Procureur de district',repPct:60,demPct:38,proj:{rSafe:88,rLikely:10,rLean:2,rTilt:0,tossup:0,dTilt:0,dLean:0,dLikely:0},note:'Siège républicain très sûr',primaryDate:'10 mars 2026'},
    {id:'senate-tn',state:'Tennessee',rating:'Safe R',cls:'safe-r',rep:'Bill Hagerty',repD:'Sénateur sortant',dem:'David Miller',demD:'Éducateur retraité',repPct:62,demPct:36,proj:{rSafe:88,rLikely:10,rLean:2,rTilt:0,tossup:0,dTilt:0,dLean:0,dLikely:0},note:'Siège républicain très sûr',primaryDate:'6 août 2026'},
    {id:'senate-ky',state:'Kentucky',rating:'Safe R',cls:'safe-r',rep:'Nate Morris',repD:'Homme d\'affaires',dem:'Pamela Stevenson',demD:'Représentante d\'État',repPct:58,demPct:40,proj:{rSafe:85,rLikely:12,rLean:3,rTilt:0,tossup:0,dTilt:0,dLean:0,dLikely:0},note:'Siège ouvert (McConnell retraité)',primaryDate:'19 mai 2026',primCands:{rep:[{name:'Nate Morris',init:'NM',desc:'Homme d\'affaires',score:'38%',cls:'rr',badge:'En tête'},{name:'Daniel Cameron',init:'DC',desc:'Ancien procureur général',score:'32%',cls:'rr',badge:'Compétitif'},{name:'Mike Harmon',init:'MH',desc:'Auditeur d\'État',score:'18%',cls:'rr',badge:'En lice'}],dem:[{name:'Pamela Stevenson',init:'PS',desc:'Représentante d\'État',score:'42%',cls:'dd',badge:'En tête'},{name:'Logan Forsythe',init:'LF',desc:'Avocat',score:'28%',cls:'dd',badge:''}]}},
    {id:'senate-sc',state:'Caroline du Sud',rating:'Safe R',cls:'safe-r',rep:'Lindsey Graham',repD:'Sénateur sortant',dem:'Annie Andrews',demD:'Pédiatre',repPct:57,demPct:41,proj:{rSafe:82,rLikely:14,rLean:4,rTilt:0,tossup:0,dTilt:0,dLean:0,dLikely:0},note:'Siège républicain très sûr',primaryDate:'9 juin 2026'},
    {id:'senate-wv',state:'Virginie-Occidentale',rating:'Safe R',cls:'safe-r',rep:'Shelley Moore Capito',repD:'Sénatrice sortante',dem:'Rio Phillips',demD:'Entrepreneur média',repPct:63,demPct:35,proj:{rSafe:90,rLikely:8,rLean:2,rTilt:0,tossup:0,dTilt:0,dLean:0,dLikely:0},note:'Siège républicain très sûr',primaryDate:'12 mai 2026'},
    {id:'senate-la',state:'Louisiane',rating:'Likely R',cls:'likely-r',rep:'Julia Letlow',repD:'Représentante (LA-5)',dem:'Jabarie Walker',demD:'Militant démocrate',repPct:54,demPct:44,proj:{rSafe:55,rLikely:30,rLean:10,rTilt:0,tossup:5,dTilt:0,dLean:0,dLikely:0},note:'Primaire compétitive (Cassidy vs Letlow)',primaryDate:'16 mai 2026',primCands:{rep:[{name:'Julia Letlow',init:'JL',desc:'Représentante',score:'34%',cls:'rr',badge:'En tête'},{name:'Bill Cassidy',init:'BC',desc:'Sénateur sortant',score:'30%',cls:'rr',badge:'Compétitif'}],dem:[{name:'Jabarie Walker',init:'JW',desc:'Militant',score:'100%',cls:'dd',badge:'Candidat'}]}},
    {id:'senate-mt',state:'Montana',rating:'Likely R',cls:'likely-r',rep:'Kurt Alme',repD:'Ancien procureur fédéral',dem:'Reilly Neill',demD:'Femme d\'affaires',repPct:53,demPct:45,proj:{rSafe:48,rLikely:32,rLean:12,rTilt:0,tossup:8,dTilt:0,dLean:0,dLikely:0},note:'Siège ouvert (Daines retraité)',primaryDate:'2 juin 2026'},
    {id:'senate-fl',state:'Floride (spéciale)',rating:'Likely R',cls:'likely-r',rep:'Ashley Moody',repD:'Sénatrice nommée',dem:'Alexander Vindman',demD:'Ancien colonel',repPct:52,demPct:45,proj:{rSafe:42,rLikely:35,rLean:15,rTilt:0,tossup:8,dTilt:0,dLean:0,dLikely:0},note:'Spéciale (siège Rubio)',primaryDate:'18 août 2026',primCands:{rep:[{name:'Ashley Moody',init:'AM',desc:'Sénatrice nommée',score:'52%',cls:'rr',badge:'En tête'}],dem:[{name:'Alexander Vindman',init:'AV',desc:'Ancien colonel',score:'48%',cls:'dd',badge:'En tête'},{name:'Angie Nixon',init:'AN',desc:'Représentante',score:'38%',cls:'dd',badge:''}]}},
    {id:'senate-ak',state:'Alaska',rating:'Lean R',cls:'lean-r',rep:'Dan Sullivan',repD:'Sénateur sortant',dem:'Mary Peltola',demD:'Ancienne représentante',repPct:49,demPct:48,proj:{rSafe:18,rLikely:25,rLean:25,rTilt:0,tossup:22,dTilt:0,dLean:10,dLikely:0},note:'Course compétitive',primaryDate:'19 août 2026'},
    {id:'senate-tx',state:'Texas',rating:'Lean R',cls:'lean-r',rep:'John Cornyn',repD:'Sénateur sortant',dem:'James Talarico',demD:'Représentant d\'État',repPct:48,demPct:46,proj:{rSafe:18,rLikely:25,rLean:17,rTilt:0,tossup:20,dTilt:0,dLean:12,dLikely:8},note:'Course compétitive (second tour GOP)',primaryDate:'4 mars 2026',primCands:{rep:[{name:'Ken Paxton',init:'KP',desc:'Procureur général',score:'48.8%',cls:'rr',badge:'2d tour'},{name:'John Cornyn',init:'JC',desc:'Sénateur sortant',score:'41.3%',cls:'rr',badge:'2d tour'}],dem:[{name:'James Talarico',init:'JT',desc:'Représentant',score:'53.1%',cls:'dd',badge:'🏆 Vainqueur'},{name:'Jasmine Crockett',init:'JC',desc:'Représentante',score:'45.6%',cls:'dd',badge:'Battue'}]}},
    {id:'senate-ia',state:'Iowa',rating:'Lean R',cls:'lean-r',rep:'Joni Ernst',repD:'Sénatrice sortante',dem:'Nathan Sage',demD:'Candidat démocrate',repPct:50,demPct:46,proj:{rSafe:25,rLikely:30,rLean:20,rTilt:0,tossup:15,dTilt:0,dLean:10,dLikely:0},note:'Siège républicain compétitif',primaryDate:'2 juin 2026'},
    {id:'senate-oh',state:'Ohio (spéciale)',rating:'Tilt R',cls:'tilt-r',rep:'Jon Husted',repD:'Sénateur nommé',dem:'Sherrod Brown',demD:'Ancien sénateur',repPct:48,demPct:47,proj:{rSafe:8,rLikely:18,rLean:25,rTilt:8,tossup:25,dTilt:5,dLean:10,dLikely:1},note:'Spéciale (siège JD Vance)',primaryDate:'5 mai 2026',primCands:{rep:[{name:'Jon Husted',init:'JH',desc:'Sénateur nommé',score:'68%',cls:'rr',badge:'En tête'}],dem:[{name:'Sherrod Brown',init:'SB',desc:'Ancien sénateur',score:'72%',cls:'dd',badge:'En tête'}]}},
    {id:'senate-ga',state:'Géorgie',rating:'Tossup',cls:'tossup',rep:'Mike Collins',repD:'Représentant (GA-10)',dem:'Jon Ossoff',demD:'Sénateur sortant',repPct:47,demPct:48,proj:{rSafe:8,rLikely:12,rLean:18,rTilt:6,tossup:30,dTilt:6,dLean:12,dLikely:6},note:'Ultra-compétitive',primaryDate:'19 mai 2026',primCands:{rep:[{name:'Mike Collins',init:'MC',desc:'Représentant',score:'38%',cls:'rr',badge:'En tête'},{name:'Buddy Carter',init:'BC',desc:'Représentant',score:'30%',cls:'rr',badge:'Compétitif'}],dem:[{name:'Jon Ossoff',init:'JO',desc:'Sénateur sortant',score:'100%',cls:'dd',badge:'Sans opposition'}]}},
    {id:'senate-nc',state:'Caroline du Nord',rating:'Tossup',cls:'tossup',rep:'Michael Whatley',repD:'Ancien président RNC',dem:'Roy Cooper',demD:'Ancien gouverneur',repPct:46,demPct:50,proj:{rSafe:4,rLikely:8,rLean:12,rTilt:8,tossup:30,dTilt:9,dLean:18,dLikely:8},note:'Tillis retraité',primaryDate:'3 mars 2026'},
    {id:'senate-mi',state:'Michigan',rating:'Tilt D',cls:'tilt-d',rep:'Mike Rogers',repD:'Ancien représentant',dem:'Mallory McMorrow',demD:'Sénatrice d\'État',repPct:46,demPct:50,proj:{rSafe:3,rLikely:6,rLean:12,rTilt:4,tossup:22,dTilt:10,dLean:25,dLikely:12},note:'Siège ouvert (Peters)',primaryDate:'5 août 2026'},
    {id:'senate-mn',state:'Minnesota',rating:'Lean D',cls:'lean-d',rep:'Michele Tafoya',repD:'Ancienne reporter NFL',dem:'Peggy Flanagan',demD:'Lieutenante-gouverneure',repPct:44,demPct:52,proj:{rSafe:0,rLikely:3,rLean:8,rTilt:3,tossup:18,dTilt:8,dLean:30,dLikely:20},note:'Siège ouvert (Smith)',primaryDate:'11 août 2026'},
    {id:'senate-nh',state:'New Hampshire',rating:'Lean D',cls:'lean-d',rep:'Scott Brown',repD:'Ancien sénateur (MA)',dem:'Chris Pappas',demD:'Représentant (NH-1)',repPct:45,demPct:52,proj:{rSafe:0,rLikely:3,rLean:10,rTilt:3,tossup:22,dTilt:8,dLean:30,dLikely:16},note:'Siège ouvert (Shaheen)',primaryDate:'8 septembre 2026'},
    {id:'senate-va',state:'Virginie',rating:'Lean D',cls:'lean-d',rep:'Bryce Reeves',repD:'Sénateur d\'État',dem:'Mark Warner',demD:'Sénateur sortant',repPct:45,demPct:52,proj:{rSafe:0,rLikely:3,rLean:8,rTilt:3,tossup:18,dTilt:8,dLean:30,dLikely:22},note:'Siège démocrate compétitif',primaryDate:'16 juin 2026'},
    {id:'senate-co',state:'Colorado',rating:'Likely D',cls:'likely-d',rep:'Clinton Dale',repD:'Candidat républicain',dem:'John Hickenlooper',demD:'Sénateur sortant',repPct:42,demPct:56,proj:{rSafe:0,rLikely:0,rLean:3,rTilt:2,tossup:8,dTilt:5,dLean:28,dLikely:34},note:'Siège démocrate favorable',primaryDate:'30 juin 2026'},
    {id:'senate-nj',state:'New Jersey',rating:'Likely D',cls:'likely-d',rep:'Alex Zdan',repD:'Ancien journaliste',dem:'Cory Booker',demD:'Sénateur sortant',repPct:41,demPct:57,proj:{rSafe:0,rLikely:0,rLean:2,rTilt:2,tossup:6,dTilt:5,dLean:25,dLikely:35},note:'Siège démocrate favorable',primaryDate:'2 juin 2026'},
    {id:'senate-il',state:'Illinois',rating:'Safe D',cls:'safe-d',rep:'Don Tracy',repD:'Ancien président GOP Illinois',dem:'Juliana Stratton',demD:'Lieutenante-gouverneure',repPct:38,demPct:60,proj:{rSafe:0,rLikely:0,rLean:0,rTilt:0,tossup:3,dTilt:3,dLean:8,dLikely:18},note:'Siège démocrate très sûr (Durbin retraité)',primaryDate:'17 mars 2026'},
    {id:'senate-de',state:'Delaware',rating:'Safe D',cls:'safe-d',rep:'Mike Katz',repD:'Ancien sénateur d\'État',dem:'Chris Coons',demD:'Sénateur sortant',repPct:37,demPct:61,proj:{rSafe:0,rLikely:0,rLean:0,rTilt:0,tossup:3,dTilt:3,dLean:8,dLikely:18},note:'Siège démocrate très sûr',primaryDate:'15 septembre 2026'},
    {id:'senate-ma',state:'Massachusetts',rating:'Safe D',cls:'safe-d',rep:'John Deaton',repD:'Avocat',dem:'Ed Markey',demD:'Sénateur sortant',repPct:36,demPct:62,proj:{rSafe:0,rLikely:0,rLean:0,rTilt:0,tossup:3,dTilt:3,dLean:8,dLikely:18},note:'Siège démocrate très sûr',primaryDate:'15 septembre 2026'},
    {id:'senate-ri',state:'Rhode Island',rating:'Safe D',cls:'safe-d',rep:'Connor Burbridge',repD:'Candidat républicain',dem:'Jack Reed',demD:'Sénateur sortant',repPct:35,demPct:63,proj:{rSafe:0,rLikely:0,rLean:0,rTilt:0,tossup:3,dTilt:3,dLean:8,dLikely:18},note:'Siège démocrate très sûr',primaryDate:'8 septembre 2026'},
    {id:'senate-or',state:'Oregon',rating:'Safe D',cls:'safe-d',rep:'David Brock Smith',repD:'Sénateur d\'État',dem:'Jeff Merkley',demD:'Sénateur sortant',repPct:38,demPct:60,proj:{rSafe:0,rLikely:0,rLean:0,rTilt:0,tossup:3,dTilt:3,dLean:8,dLikely:18},note:'Siège démocrate très sûr',primaryDate:'19 mai 2026'},
    {id:'senate-nm',state:'Nouveau-Mexique',rating:'Safe D',cls:'safe-d',rep:'(aucun)',repD:'Pas de républicain qualifié',dem:'Ben Ray Luján',demD:'Sénateur sortant',repPct:0,demPct:98,proj:{rSafe:0,rLikely:0,rLean:0,rTilt:0,tossup:0,dTilt:0,dLean:2,dLikely:8},note:'Aucun républicain qualifié',primaryDate:'2 juin 2026'}
  ];

  function buildRaceEntry(r) {
    const initials = (n) => n.split(' ').map(w => w[0]).join('');
    const polls = [];
    for (let m = 1; m <= 9; m++) {
      polls.push({ date: ['Jan','Fév','Mar','Avr','Mai','Jun','Jul','Aoû','Sep'][m-1], rep: r.repPct + Math.round(Math.random()*4-2), dem: r.demPct + Math.round(Math.random()*4-2) });
    }
    polls.push({ date: 'Sep', rep: r.repPct, dem: r.demPct });
    const primCands = r.primCands || {};
    return {
      id: r.id, title: `House · ${r.state} ${r.district}`, rating: r.rating, ratingClass: r.cls,
      stateName: r.state, districtName: r.district,
      candidates: [{ name:r.rep, party:'R', initials:initials(r.rep), pct:r.repPct, desc:r.repD },{ name:r.dem, party:'D', initials:initials(r.dem), pct:r.demPct, desc:r.demD }],
      proj: r.proj, seats: r.note, moe:'±3.5%', sample:'1 200 LV', dates:'Sep 2026', polls,
      primaryDate: r.primaryDate,
      primaries: {
        rep: { note:'Source : Ballotpedia.', cands: primCands.rep || [{ name:r.rep, init:initials(r.rep), desc:'Candidat présumé', score:'100%', cls:'rr', badge:'Investiture' }] },
        dem: { note:'Source : Ballotpedia.', cands: primCands.dem || [{ name:r.dem, init:initials(r.dem), desc:'Candidat présumé', score:'100%', cls:'dd', badge:'Investiture' }] }
      }
    };
  }

  senateRaces.forEach(r => { racesData[r.id] = buildRaceEntry(r); });
  houseRacesData.forEach(r => { racesData[r.id] = buildRaceEntry(r); });

  // Trier les districts House par ordre alphabétique d'État puis par numéro de district
  houseRacesData.sort((a, b) => {
    if (a.state !== b.state) return a.state.localeCompare(b.state);
    const numA = parseInt(a.district) || 0;
    const numB = parseInt(b.district) || 0;
    return numA - numB;
  });

  function populateList(listId, ids) {
    document.getElementById(listId).innerHTML = ids.map(id => {
      const r = racesData[id]; if(!r) return '';
      const displayTitle = r.districtName ? `${r.stateName} · ${r.districtName}` : r.stateName;
      return `<div class="race-item" data-race="${id}"><div class="race-info"><h3>${displayTitle}</h3><p>${r.candidates[0].name} (R) vs ${r.candidates[1].name} (D)</p></div><div class="race-tag ${r.ratingClass}">${r.rating}</div></div>`;
    }).join('');
  }
  populateList('senate-races', senateRaces.map(r=>r.id));
  populateList('house-races', houseRacesData.map(r=>r.id));

  function showRaceDetail(id) {
    const d = racesData[id]; if(!d) return;
    const container = document.getElementById('detail-container');
    const arrowPos = ratingPositions[d.rating] || 50;
    const total = (d.proj.rSafe||0)+(d.proj.rLikely||0)+(d.proj.rLean||0)+(d.proj.rTilt||0)+(d.proj.tossup||0)+(d.proj.dTilt||0)+(d.proj.dLean||0)+(d.proj.dLikely||0)+(d.proj.dSafe||0) || 100;
    const s = 100/total;
    
    container.innerHTML = `
      <div class="card">
        <div class="card-header"><div class="card-title">${d.title}</div><div class="race-tag ${d.ratingClass}">${d.rating}</div></div>
        ${d.candidates.map(c=>`<div class="candidate-row"><div class="candidate-label"><span class="party-name ${c.party==='R'?'rep':'dem'}">${c.name} (${c.party})</span><span class="party-pct ${c.party==='R'?'rep':'dem'}">${c.pct}%</span></div><div style="color:rgba(255,255,255,0.45);font-size:0.7rem;margin-bottom:0.3rem;">${c.desc}</div><div class="bar-wrap"><div class="bar-fill ${c.party==='R'?'rf':'df'}" style="width:${c.pct}%">${c.pct}%</div></div></div>`).join('')}
        <div class="poll-footer"><span>📊 Marge ${d.moe}</span><span>👥 ${d.sample} · ${d.dates}</span></div>
        <div class="gauge-container">
          <div class="gauge-label" style="display:flex;justify-content:space-between;">${['Safe R','Likely R','Lean R','Tilt R','Tossup','Tilt D','Lean D','Likely D','Safe D'].map(x=>`<span>${x}</span>`).join('')}</div>
          <div class="gauge-bar"><div class="gauge-arrow" style="left:${arrowPos}%;">▼</div></div>
          <div class="gauge-pos-text">Position actuelle : <strong style="color:${d.ratingClass.includes('r')?'#ff9e8f':d.ratingClass.includes('d')?'#8fc1ff':'#ffe082'}">${d.rating}</strong></div>
        </div>
        <div style="margin-top:1rem;"><h4 style="color:rgba(255,255,255,0.5);font-size:0.7rem;">Projections détaillées</h4>
          <div class="projections-bar">
            <div class="p-safe-r" style="width:${(d.proj.rSafe||0)*s}%"></div><div class="p-likely-r" style="width:${(d.proj.rLikely||0)*s}%"></div><div class="p-lean-r" style="width:${(d.proj.rLean||0)*s}%"></div><div class="p-tilt-r" style="width:${(d.proj.rTilt||0)*s}%"></div><div class="p-tossup" style="width:${(d.proj.tossup||0)*s}%"></div><div class="p-tilt-d" style="width:${(d.proj.dTilt||0)*s}%"></div><div class="p-lean-d" style="width:${(d.proj.dLean||0)*s}%"></div><div class="p-likely-d" style="width:${(d.proj.dLikely||0)*s}%"></div><div class="p-safe-d" style="width:${(d.proj.dSafe||0)*s}%"></div>
          </div>
        </div>
        <div style="margin-top:1rem;color:rgba(255,255,255,0.5);font-size:0.75rem;text-align:center;">${d.seats}</div>
        <div style="margin-top:1.2rem;"><h4 style="color:rgba(255,255,255,0.5);font-size:0.7rem;">📈 Sondages</h4>
          <div class="chart-container"><canvas id="detailChart" width="800" height="230"></canvas><div class="chart-tooltip" id="chartTooltip" style="opacity:0;"></div></div>
          <div class="chart-legend"><span><span class="legend-dot r"></span> ${d.candidates[0].name.split(' ').pop()} (R)</span><span><span class="legend-dot d"></span> ${d.candidates[1].name.split(' ').pop()} (D)</span></div>
        </div>
      </div>
      <div class="card">
        <div class="card-header"><div class="card-title">Primaires</div><div style="color:rgba(255,255,255,0.5);">📅 ${d.primaryDate}</div></div>
        <div class="prim-tabs"><div class="prim-tab ra active" data-prim="rep">Républicaine</div><div class="prim-tab da" data-prim="dem">Démocrate</div></div>
        <div class="prim-panel active" id="panel-rep"><div class="primary-grid">${d.primaries.rep.cands.map(c=>`<div class="candidate-card"><div class="cand-photo ${c.cls}">${c.init}</div><div class="cand-name">${c.name}</div><div style="font-size:0.65rem;">${c.desc}</div><div style="font-size:1.4rem;font-weight:800;color:#ff9e8f;">${c.score}</div><div style="font-size:0.6rem;color:#ffd700;">${c.badge}</div></div>`).join('')}</div><div style="color:rgba(255,255,255,0.5);font-size:0.7rem;text-align:center;">${d.primaries.rep.note}</div></div>
        <div class="prim-panel" id="panel-dem"><div class="primary-grid">${d.primaries.dem.cands.map(c=>`<div class="candidate-card"><div class="cand-photo ${c.cls}">${c.init}</div><div class="cand-name">${c.name}</div><div style="font-size:0.65rem;">${c.desc}</div><div style="font-size:1.4rem;font-weight:800;color:#8fc1ff;">${c.score}</div><div style="font-size:0.6rem;color:#ffd700;">${c.badge}</div></div>`).join('')}</div><div style="color:rgba(255,255,255,0.5);font-size:0.7rem;text-align:center;">${d.primaries.dem.note}</div></div>
      </div>
    `;
    setTimeout(() => {
      document.querySelectorAll('.prim-tab').forEach(t => t.addEventListener('click', function(){
        const target = this.dataset.prim;
        this.parentElement.querySelectorAll('.prim-tab').forEach(x=>x.classList.remove('active','ra','da'));
        this.classList.add('active'); this.classList.add(target==='rep'?'ra':'da');
        document.getElementById('panel-rep').style.display = target==='rep'?'block':'none';
        document.getElementById('panel-dem').style.display = target==='dem'?'block':'none';
      }));
      drawChart(d.polls, d.candidates);
    }, 100);
  }

  function drawChart(polls, cands) {
    const canvas = document.getElementById('detailChart'); if(!canvas) return;
    const ctx = canvas.getContext('2d');
    const tooltip = document.getElementById('chartTooltip');
    const repAvg=[], demAvg=[];
    for(let i=0;i<polls.length;i++){ let sR=0,sD=0,c=0; for(let j=Math.max(0,i-2);j<=i;j++){sR+=polls[j].rep;sD+=polls[j].dem;c++;} repAvg.push(Math.round(sR/c*10)/10); demAvg.push(Math.round(sD/c*10)/10); }
    const pad={top:20,right:25,bottom:30,left:36}, minY=30, maxY=65;
    let points=[];
    function draw(){
      const w=canvas.width,h=canvas.height,cW=w-pad.left-pad.right,cH=h-pad.top-pad.bottom;
      ctx.clearRect(0,0,w,h); ctx.fillStyle='rgba(10,10,18,0.5)'; ctx.fillRect(pad.left,pad.top,cW,cH);
      const gX=i=>pad.left+(i/(polls.length-1))*cW, gY=v=>pad.top+cH-((v-minY)/(maxY-minY))*cH;
      ctx.strokeStyle='rgba(255,255,255,0.06)';
      for(let i=minY;i<=maxY;i+=5){const y=gY(i);ctx.beginPath();ctx.moveTo(pad.left,y);ctx.lineTo(pad.left+cW,y);ctx.stroke();}
      polls.forEach((p,i)=>{ctx.fillStyle='rgba(255,255,255,0.45)';ctx.font='9px Segoe UI';ctx.fillText(p.date,gX(i),pad.top+cH+10);});
      [{d:repAvg,c:'#ff8a7a'},{d:demAvg,c:'#8fc1ff'}].forEach(l=>{ctx.beginPath();ctx.moveTo(gX(0),gY(l.d[0]));for(let i=1;i<l.d.length;i++){const xc=gX(i),yc=gY(l.d[i]),xp=gX(i-1),yp=gY(l.d[i-1]);ctx.bezierCurveTo(xp+(xc-xp)*0.5,yp,xc-(xc-xp)*0.5,yc,xc,yc);}ctx.strokeStyle=l.c;ctx.lineWidth=2.2;ctx.stroke();});
      points=[];
      polls.forEach((p,i)=>{[{v:p.rep,t:'r',c:'rgba(180,40,40,0.5)'},{v:p.dem,t:'d',c:'rgba(30,80,180,0.5)'}].forEach(pt=>{const x=gX(i),y=gY(pt.v);points.push({x,y,type:pt.t,value:pt.v,date:p.date});ctx.beginPath();ctx.arc(x,y,5,0,2*Math.PI);ctx.fillStyle=pt.c;ctx.fill();});});
    }
    draw();
    canvas.onmousemove=e=>{
      const rect=canvas.getBoundingClientRect(),sX=canvas.width/rect.width,sY=canvas.height/rect.height;
      const mx=(e.clientX-rect.left)*sX,my=(e.clientY-rect.top)*sY;
      let cl=null,md=18; points.forEach(p=>{const d=Math.hypot(mx-p.x,my-p.y);if(d<md){md=d;cl=p;}});
      if(cl){tooltip.innerHTML=`<strong>${cl.type==='r'?cands[0].name:cands[1].name}</strong><br><span style="color:${cl.type==='r'?'#ff9e8f':'#8fc1ff'}">${cl.value}%</span><br>${cl.date} 2026`;tooltip.style.left=Math.max(5,Math.min(cl.x/sX-45,rect.width-95))+'px';tooltip.style.top=Math.max(5,cl.y/sY-45)+'px';tooltip.style.opacity='1';}else{tooltip.style.opacity='0';}
    };
    canvas.onmouseleave=()=>tooltip.style.opacity='0';
  }

  document.querySelectorAll('.cat-tab').forEach(t=>t.addEventListener('click', function(){
    document.querySelectorAll('.cat-tab').forEach(x=>x.classList.remove('active')); this.classList.add('active');
    document.querySelectorAll('.cat-panel').forEach(x=>x.classList.remove('active'));
    document.getElementById('cat-'+this.dataset.cat).classList.add('active');
    (document.querySelector('#cat-'+this.dataset.cat+' .race-item')||{}).click?.();
  }));
  document.addEventListener('click',e=>{
    const item = e.target.closest('.race-item[data-race]');
    if(item){ document.querySelectorAll('.race-item').forEach(i=>i.classList.remove('active')); item.classList.add('active'); showRaceDetail(item.dataset.race); }
  });
  // Afficher le premier district House par défaut
  (document.querySelector('#house-races .race-item')||{}).click?.();
})();
</script>
<div style="height:30px;"></div>
</body>
</html>
