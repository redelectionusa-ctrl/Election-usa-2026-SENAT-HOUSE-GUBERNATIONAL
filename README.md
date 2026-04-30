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
      padding:20px; color: #fff;
    }
    .main-header {
      width:100%; max-width:1400px;
      background: rgba(5,10,20,0.6); backdrop-filter: blur(16px);
      padding: 1.8rem 2rem; text-align:center; margin-bottom: 30px;
      box-shadow: 0 15px 40px rgba(0,0,0,0.7); border-radius: 12px;
    }
    .main-title {
      font-size: clamp(2.2rem, 6vw, 4.5rem); font-weight: 900;
      letter-spacing: 0.25em; color: #fff; text-transform: uppercase;
      text-shadow: 0 0 30px rgba(255,215,150,0.4);
    }
    .main-subtitle {
      font-size: clamp(1rem, 2.5vw, 1.6rem); color: rgba(255,255,255,0.9);
      letter-spacing: 0.4em; text-transform: uppercase;
      border-top: 1.5px solid rgba(255,215,150,0.5);
      display: inline-block; padding-top: 0.7rem; margin-top: 0.6rem;
    }
    .main-content { width:100%; max-width:1400px; }
    .category-tabs { display:flex; gap:0.8rem; margin-bottom: 2rem; flex-wrap:wrap; }
    .cat-tab {
      background: rgba(0,0,0,0.5); backdrop-filter: blur(8px);
      border: 1px solid rgba(255,255,255,0.15); color: white;
      padding: 1rem 1.8rem; font-size: 1.1rem; font-weight: 700;
      text-transform: uppercase; letter-spacing: 0.15em; cursor: pointer;
      flex: 1; min-width: 140px; text-align: center;
      transition: all 0.3s ease; border-radius: 50px;
    }
    .cat-tab:hover { background: rgba(255,255,255,0.1); transform: translateY(-2px); }
    .cat-tab.active { background: rgba(255,255,255,0.15); border-color: rgba(255,215,150,0.8); box-shadow: 0 0 30px rgba(255,215,150,0.25); }
    .cat-panel { display:none; }
    .cat-panel.active { display:block; animation: fadeIn 0.4s ease; }
    @keyframes fadeIn { from { opacity:0; transform: translateY(10px); } to { opacity:1; transform: translateY(0); } }
    
    .race-list { display:flex; flex-direction:column; gap:0.6rem; margin-bottom: 2rem; }
    .race-item {
      background: rgba(0,0,0,0.4); backdrop-filter: blur(10px);
      border: 1px solid rgba(220,200,180,0.15); padding: 1rem 1.5rem;
      cursor: pointer; display: flex; justify-content: space-between;
      align-items: center; flex-wrap: wrap; gap: 0.8rem;
      border-radius: 10px; transition: all 0.3s ease;
    }
    .race-item:hover { background: rgba(255,255,255,0.08); transform: translateX(5px); }
    .race-item.active { background: rgba(255,255,255,0.12); border-color: rgba(255,215,150,0.8); box-shadow: 0 0 25px rgba(255,215,150,0.2); }
    .race-info h3 { color: #f0e6d2; font-size: 1rem; }
    .race-info p { color: rgba(255,255,255,0.5); font-size: 0.75rem; }
    
    .race-tag {
      padding: 0.25rem 0.9rem; font-weight: 700; text-transform: uppercase;
      font-size: 0.65rem; letter-spacing: 0.08em; border-radius: 20px;
    }
    .safe-r { background: #3e0000; color: #ff8a80; border: 1px solid #b71c1c; }
    .likely-r { background: #6a0a0a; color: #ff6b5e; border: 1px solid #d32f2f; }
    .lean-r { background: #7a1515; color: #ff9e8f; border: 1px solid #e53935; }
    .tilt-r { background: #8a2020; color: #ffab91; border: 1px solid #ff7043; }
    .tossup { background: #5a4a00; color: #ffe082; border: 1px solid #ffc107; }
    .tilt-d { background: #0a2f5a; color: #91caff; border: 1px solid #42a5f5; }
    .lean-d { background: #0a2f6a; color: #8fc1ff; border: 1px solid #1e88e5; }
    .likely-d { background: #0a2060; color: #64b5f6; border: 1px solid #1976d2; }
    .safe-d { background: #001a4d; color: #82b1ff; border: 1px solid #0d47a1; }
    
    .card {
      background: rgba(10,10,20,0.5); backdrop-filter: blur(16px);
      border: 1px solid rgba(220,200,180,0.15); padding: 1.8rem;
      margin-bottom: 1.2rem; border-radius: 16px;
    }
    .card-header { display: flex; justify-content: space-between; align-items: center; margin-bottom: 1.5rem; border-bottom: 1px solid rgba(255,255,255,0.1); padding-bottom: 1rem; flex-wrap: wrap; gap: 1rem; }
    .card-title { font-size: 1.3rem; font-weight: 700; color: #f0e6d2; text-transform: uppercase; letter-spacing: 0.08em; }
    
    .candidate-row { margin-bottom: 1.2rem; }
    .candidate-label { display: flex; justify-content: space-between; margin-bottom: 0.3rem; }
    .party-name { font-size: 1.1rem; font-weight: 700; }
    .party-pct { font-size: 1.4rem; font-weight: 800; }
    .rep { color: #ff9e8f; } .dem { color: #8fc1ff; }
    .bar-wrap { height: 32px; background: #121212; border-radius: 6px; overflow: hidden; }
    .bar-fill { height: 100%; display: flex; align-items: center; justify-content: flex-end; padding-right: 12px; font-weight: 700; color: white; font-size: 0.9rem; }
    .bar-r { background: linear-gradient(90deg, #a51c1c, #d32f2f); }
    .bar-d { background: linear-gradient(90deg, #0a3a7a, #1976d2); }
    
    .gauge-container { margin: 1.5rem 0; }
    .gauge-label { display: flex; justify-content: space-between; font-size: 0.65rem; color: rgba(255,255,255,0.5); margin-bottom: 0.4rem; }
    .gauge-bar { height: 12px; background: linear-gradient(to right, #3e0000, #6a0a0a, #7a1515, #8a2020, #5a4a00, #0a2f5a, #0a2f6a, #0a2060, #001a4d); border-radius: 20px; position: relative; margin-bottom: 0.6rem; }
    .gauge-arrow { position: absolute; top: -12px; transform: translateX(-50%); font-size: 1.6rem; }
    .gauge-pos { text-align: center; font-size: 0.85rem; color: rgba(255,255,255,0.8); }
    
    .chart-container { position: relative; width:100%; height: 250px; margin: 1rem 0; border-radius: 12px; overflow: hidden; box-shadow: 0 8px 25px rgba(0,0,0,0.4); }
    canvas { display: block; width:100%; height:100%; background: rgba(10,10,15,0.6); border: 1px solid rgba(255,255,255,0.15); cursor: crosshair; border-radius: 12px; }
    .chart-tooltip { position: absolute; background: rgba(20,20,30,0.95); color: white; padding: 8px 14px; border: 1px solid rgba(255,255,255,0.3); font-size: 11px; font-weight: 600; pointer-events: none; z-index: 100; text-align: center; line-height: 1.4; white-space: nowrap; border-radius: 8px; }
    .chart-legend { display: flex; justify-content: center; gap: 1.5rem; margin-top: 0.8rem; color: rgba(255,255,255,0.7); font-size: 0.85rem; }
    .legend-dot { width: 10px; height: 10px; display: inline-block; margin-right: 5px; border-radius: 50%; }
    .legend-dot.r { background: #e53935; } .legend-dot.d { background: #1e88e5; }
    
    .prim-tabs { display: flex; gap: 0.5rem; margin-bottom: 1rem; }
    .prim-tab { background: rgba(0,0,0,0.3); border: 1px solid rgba(255,255,255,0.2); color: white; padding: 0.5rem 1rem; font-size: 0.85rem; font-weight: 600; cursor: pointer; flex: 1; text-align: center; border-radius: 20px; }
    .prim-tab.active { background: rgba(255,255,255,0.2); border-color: rgba(255,215,150,0.6); }
    .prim-tab.ra { background: rgba(229,57,53,0.2); }
    .prim-tab.da { background: rgba(30,136,229,0.2); }
    .prim-panel { display: none; }
    .prim-panel.active { display: block; }
    .primary-grid { display: grid; grid-template-columns: repeat(auto-fit, minmax(160px, 1fr)); gap: 0.8rem; }
    .cand-card { background: rgba(0,0,0,0.3); border: 1px solid rgba(255,255,255,0.1); padding: 1rem; text-align: center; border-radius: 10px; }
    .cand-photo { width: 45px; height: 45px; border-radius: 50%; margin: 0 auto 0.5rem; display: flex; align-items: center; justify-content: center; font-weight: bold; font-size: 1.2rem; color: white; }
    .cand-photo.rr { background: #a51c1c; } .cand-photo.dd { background: #0a3a7a; }
    
    .polls-table { width: 100%; border-collapse: collapse; font-size: 0.75rem; margin: 1rem 0; }
    .polls-table th { text-align: left; padding: 0.5rem; background: rgba(0,0,0,0.3); color: rgba(255,255,255,0.6); font-weight: 600; border-bottom: 1px solid rgba(255,255,255,0.1); }
    .polls-table td { padding: 0.4rem 0.5rem; border-bottom: 1px solid rgba(255,255,255,0.05); }
    .polls-table .r-val { color: #ff9e8f; font-weight: 600; }
    .polls-table .d-val { color: #8fc1ff; font-weight: 600; }
    
    .sources-section { margin-top: 1.2rem; padding-top: 1rem; border-top: 1px solid rgba(255,255,255,0.1); }
    .sources-title { font-size: 0.75rem; color: rgba(255,255,255,0.5); text-transform: uppercase; margin-bottom: 0.6rem; }
    .source-links { display: flex; flex-wrap: wrap; gap: 0.6rem; }
    .source-link { background: rgba(255,255,255,0.08); border: 1px solid rgba(255,255,255,0.2); color: rgba(255,255,255,0.8); padding: 0.4rem 0.9rem; border-radius: 20px; font-size: 0.7rem; text-decoration: none; transition: all 0.2s; }
    .source-link:hover { background: rgba(255,215,150,0.15); border-color: rgba(255,215,150,0.5); color: #ffe082; }
    
    .no-data { text-align: center; color: rgba(255,255,255,0.4); padding: 2rem; font-style: italic; }
    
    @media (max-width: 750px) { .card-title { font-size: 1.1rem; } }
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
  const ratingPos = {'Safe R':5,'Likely R':16,'Lean R':27,'Tilt R':38,'Tossup':50,'Tilt D':62,'Lean D':73,'Likely D':84,'Safe D':95};
  const racesData = {};

  const houseRaces = [
    // AVEC SONDAGES
    {id:'house-wa3',state:'Washington',district:'3e District',rating:'Tossup',cls:'tossup',rep:'John Braun',repD:'Ancien chef de la minorité au Sénat d\'État',dem:'Marie Gluesenkamp Perez',demD:'Représentante sortante',repPct:47,demPct:48,proj:{rSafe:8,rLikely:12,rLean:15,rTilt:5,tossup:30,dTilt:5,dLean:18,dLikely:7},note:'Trump +0.4% en 2024',primaryDate:'5 août 2025',polls:[{date:'2024-06',rep:46,dem:47,src:'SurveyUSA'},{date:'2024-09',rep:45,dem:48,src:'Emerson'},{date:'2024-11',rep:47,dem:46,src:'NYT/Siena'},{date:'2025-02',rep:46,dem:47,src:'SurveyUSA'},{date:'2025-06',rep:45,dem:49,src:'Emerson'},{date:'2025-09',rep:47,dem:46,src:'PPP'},{date:'2025-12',rep:46,dem:48,src:'YouGov'},{date:'2026-02',rep:47,dem:47,src:'SurveyUSA'},{date:'2026-04',rep:47,dem:48,src:'Emerson'}],sources:{rcp:'https://www.realclearpolling.com/maps/house/2026/washington-3',bp:'https://ballotpedia.org/Washington%27s_3rd_Congressional_District_election,_2026'}},
    {id:'house-az6',state:'Arizona',district:'6e District',rating:'Tossup',cls:'tossup',rep:'Juan Ciscomani',repD:'Représentant sortant',dem:'JoAnna Mendoza',demD:'Candidate démocrate',repPct:48,demPct:49,proj:{rSafe:5,rLikely:8,rLean:12,rTilt:5,tossup:30,dTilt:10,dLean:18,dLikely:12},note:'Biden +0.1% en 2020',primaryDate:'5 août 2026',polls:[{date:'2024-06',rep:48,dem:47,src:'OH Predictive'},{date:'2024-09',rep:47,dem:48,src:'Emerson'},{date:'2024-11',rep:49,dem:46,src:'NYT/Siena'},{date:'2025-03',rep:47,dem:49,src:'PPP'},{date:'2025-07',rep:48,dem:47,src:'YouGov'},{date:'2025-10',rep:47,dem:48,src:'Emerson'},{date:'2026-01',rep:48,dem:48,src:'OH Predictive'},{date:'2026-04',rep:48,dem:49,src:'Emerson'}],sources:{rcp:'https://www.realclearpolling.com/maps/house/2026/arizona-6',bp:'https://ballotpedia.org/Arizona%27s_6th_Congressional_District_election,_2026'}},
    {id:'house-mi7',state:'Michigan',district:'7e District',rating:'Tossup',cls:'tossup',rep:'Tom Barrett',repD:'Représentant sortant',dem:'Bridget Brink',demD:'Candidate démocrate',repPct:47,demPct:49,proj:{rSafe:5,rLikely:8,rLean:12,rTilt:8,tossup:28,dTilt:8,dLean:18,dLikely:13},note:'Trump +2% en 2024',primaryDate:'5 août 2026',polls:[{date:'2024-08',rep:48,dem:46,src:'EPIC-MRA'},{date:'2024-11',rep:49,dem:47,src:'NYT/Siena'},{date:'2025-04',rep:47,dem:49,src:'PPP'},{date:'2025-08',rep:47,dem:48,src:'YouGov'},{date:'2026-01',rep:47,dem:49,src:'EPIC-MRA'},{date:'2026-04',rep:47,dem:49,src:'Emerson'}],sources:{rcp:'https://www.realclearpolling.com/maps/house/2026/michigan-7',bp:'https://ballotpedia.org/Michigan%27s_7th_Congressional_District_election,_2026'}},
    {id:'house-ia3',state:'Iowa',district:'3e District',rating:'Tossup',cls:'tossup',rep:'Zach Nunn',repD:'Représentant sortant',dem:'Sarah Trone Garriott',demD:'Sénatrice d\'État de l\'Iowa',repPct:48,demPct:48,proj:{rSafe:5,rLikely:10,rLean:15,rTilt:8,tossup:28,dTilt:8,dLean:15,dLikely:11},note:'Trump +0.5% en 2024',primaryDate:'2 juin 2026',polls:[{date:'2024-09',rep:49,dem:47,src:'Selzer'},{date:'2024-11',rep:49,dem:48,src:'NYT/Siena'},{date:'2025-05',rep:48,dem:48,src:'PPP'},{date:'2025-09',rep:48,dem:47,src:'Selzer'},{date:'2026-02',rep:48,dem:48,src:'YouGov'},{date:'2026-04',rep:48,dem:48,src:'Emerson'}],sources:{}},
    {id:'house-pa7',state:'Pennsylvanie',district:'7e District',rating:'Lean R',cls:'lean-r',rep:'Ryan Mackenzie',repD:'Représentant sortant',dem:'Bob Brooks',demD:'Candidat démocrate',repPct:49,demPct:47,proj:{rSafe:10,rLikely:18,rLean:22,rTilt:8,tossup:22,dTilt:8,dLean:8,dLikely:4},note:'Trump +1% en 2024',primaryDate:'19 mai 2026',polls:[{date:'2024-09',rep:50,dem:46,src:'Muhlenberg'},{date:'2024-11',rep:49,dem:47,src:'NYT/Siena'},{date:'2025-04',rep:49,dem:47,src:'PPP'},{date:'2025-09',rep:49,dem:47,src:'YouGov'},{date:'2026-03',rep:49,dem:47,src:'Muhlenberg'}],sources:{bp:'https://ballotpedia.org/Pennsylvania%27s_7th_Congressional_District_election,_2026'}},
    {id:'house-ny17',state:'New York',district:'17e District',rating:'Lean R',cls:'lean-r',rep:'Mike Lawler',repD:'Représentant sortant',dem:'Démocrate',demD:'Candidat à déterminer',repPct:49,demPct:48,proj:{rSafe:8,rLikely:18,rLean:24,rTilt:8,tossup:22,dTilt:8,dLean:8,dLikely:4},note:'Biden +10% en 2020, Trump +0.5% en 2024',primaryDate:'24 juin 2026',polls:[{date:'2024-09',rep:50,dem:47,src:'Siena'},{date:'2024-11',rep:49,dem:48,src:'NYT/Siena'},{date:'2025-05',rep:49,dem:47,src:'PPP'},{date:'2025-10',rep:49,dem:48,src:'Siena'},{date:'2026-03',rep:49,dem:48,src:'Emerson'}],sources:{poly:'https://polymarket.com/event/new-york-17th-district-2026',bp:'https://ballotpedia.org/New_York%27s_17th_Congressional_District_election,_2026'}},
    {id:'house-co8',state:'Colorado',district:'8e District',rating:'Tossup',cls:'tossup',rep:'Gabe Evans',repD:'Représentant sortant',dem:'Démocrate',demD:'Candidat à déterminer (Caraveo a abandonné)',repPct:47,demPct:48,proj:{rSafe:8,rLikely:10,rLean:12,rTilt:5,tossup:28,dTilt:8,dLean:18,dLikely:11},note:'Biden +4% en 2020. Caraveo a abandonné.',primaryDate:'24 juin 2026',polls:[{date:'2024-08',rep:46,dem:49,src:'Emerson'},{date:'2024-11',rep:48,dem:47,src:'NYT/Siena'},{date:'2025-05',rep:47,dem:48,src:'PPP'},{date:'2025-10',rep:47,dem:49,src:'YouGov'},{date:'2026-03',rep:47,dem:48,src:'Emerson'}],sources:{rcp:'https://www.realclearpolling.com/maps/house/2026/colorado-8'}},
    // SANS SONDAGES
    {id:'house-az1',state:'Arizona',district:'1er District',rating:'Lean R',cls:'lean-r',rep:'Joseph Chaplik',repD:'Candidat républicain',dem:'Amish Cha',demD:'Candidat démocrate',repPct:49,demPct:47,proj:{rSafe:10,rLikely:20,rLean:25,rTilt:5,tossup:25,dTilt:5,dLean:8,dLikely:2},note:'Trump +1.5% en 2024',primaryDate:'5 août 2026',polls:[],sources:{}},
    {id:'house-tx34',state:'Texas',district:'34e District',rating:'Lean D',cls:'lean-d',rep:'Mayra Flores',repD:'Ancienne représentante',dem:'Eric Flores',demD:'Candidat démocrate',repPct:47,demPct:50,proj:{rSafe:5,rLikely:8,rLean:10,rTilt:5,tossup:18,dTilt:8,dLean:25,dLikely:21},note:'District frontalier',primaryDate:'4 mars 2026',polls:[],sources:{}},
    {id:'house-ia1',state:'Iowa',district:'1er District',rating:'Lean R',cls:'lean-r',rep:'Mariannette Miller-Meeks',repD:'Représentante sortante',dem:'Christina Bohannan',demD:'Ancienne candidate',repPct:49,demPct:47,proj:{rSafe:12,rLikely:18,rLean:22,rTilt:8,tossup:22,dTilt:8,dLean:8,dLikely:2},note:'District compétitif',primaryDate:'2 juin 2026',polls:[],sources:{}},
    {id:'house-wi3',state:'Wisconsin',district:'3e District',rating:'Lean R',cls:'lean-r',rep:'Derrick Van Orden',repD:'Représentant sortant',dem:'Rebecca Cooke',demD:'Femme d\'affaires',repPct:49,demPct:47,proj:{rSafe:10,rLikely:20,rLean:22,rTilt:8,tossup:22,dTilt:8,dLean:8,dLikely:2},note:'District rural',primaryDate:'12 août 2026',polls:[],sources:{}},
    {id:'house-mi10',state:'Michigan',district:'10e District',rating:'Lean R',cls:'lean-r',rep:'Mike Bouchard',repD:'Candidat républicain',dem:'Démocrate',demD:'Candidat à déterminer',repPct:50,demPct:47,proj:{rSafe:12,rLikely:18,rLean:22,rTilt:8,tossup:20,dTilt:8,dLean:8,dLikely:4},note:'Détroit suburbain',primaryDate:'5 août 2026',polls:[],sources:{}},
    {id:'house-oh9',state:'Ohio',district:'9e District',rating:'Lean D',cls:'lean-d',rep:'Merek Derrin',repD:'Candidat républicain',dem:'Marcy Kaptur',demD:'Représentante sortante',repPct:46,demPct:51,proj:{rSafe:5,rLikely:8,rLean:10,rTilt:5,tossup:18,dTilt:8,dLean:25,dLikely:21},note:'District de Toledo',primaryDate:'5 mai 2026',polls:[],sources:{}},
    {id:'house-pa8',state:'Pennsylvanie',district:'8e District',rating:'Lean R',cls:'lean-r',rep:'Rob Bresnahan',repD:'Représentant sortant',dem:'Paige Cognetti',demD:'Candidate démocrate',repPct:49,demPct:48,proj:{rSafe:8,rLikely:18,rLean:24,rTilt:8,tossup:22,dTilt:8,dLean:8,dLikely:4},note:'Scranton/Wilkes-Barre',primaryDate:'19 mai 2026',polls:[],sources:{}},
    {id:'house-pa10',state:'Pennsylvanie',district:'10e District',rating:'Lean R',cls:'lean-r',rep:'Scott Perry',repD:'Représentant sortant',dem:'Janelle Stelson',demD:'Ancienne candidate',repPct:50,demPct:46,proj:{rSafe:14,rLikely:20,rLean:20,rTilt:8,tossup:20,dTilt:8,dLean:6,dLikely:4},note:'Harrisburg',primaryDate:'19 mai 2026',polls:[],sources:{}},
    {id:'house-nj7',state:'New Jersey',district:'7e District',rating:'Lean R',cls:'lean-r',rep:'Thomas Kean Jr.',repD:'Représentant sortant',dem:'Rebecca Bennett',demD:'Candidate démocrate',repPct:49,demPct:47,proj:{rSafe:10,rLikely:18,rLean:24,rTilt:8,tossup:20,dTilt:8,dLean:8,dLikely:4},note:'District suburbain',primaryDate:'2 juin 2026',polls:[],sources:{}},
    {id:'house-ca22',state:'Californie',district:'22e District',rating:'Lean D',cls:'lean-d',rep:'David Valadao',repD:'Représentant sortant',dem:'Jasmeet Bains',demD:'Médecin · Députée d\'État',repPct:46,demPct:50,proj:{rSafe:3,rLikely:8,rLean:12,rTilt:5,tossup:25,dTilt:8,dLean:28,dLikely:11},note:'Fourchette : +3D à +12R',primaryDate:'3 juin 2025',polls:[],sources:{}},
  ];

  const senateRaces = [
    {id:'senate-tx',state:'Texas',rating:'Lean R',cls:'lean-r',rep:'John Cornyn',repD:'Sénateur sortant',dem:'James Talarico',demD:'Représentant d\'État',repPct:48,demPct:46,proj:{rSafe:18,rLikely:25,rLean:17,rTilt:0,tossup:20,dTilt:0,dLean:12,dLikely:8},note:'Second tour GOP le 26 mai',primaryDate:'4 mars 2026',polls:[{date:'2024-06',rep:49,dem:42,src:'YouGov'},{date:'2024-09',rep:48,dem:43,src:'Emerson'},{date:'2024-11',rep:50,dem:41,src:'UT Tyler'},{date:'2025-01',rep:47,dem:44,src:'Quinnipiac'},{date:'2025-03',rep:46,dem:45,src:'Marist'},{date:'2025-06',rep:48,dem:43,src:'YouGov'},{date:'2025-09',rep:47,dem:44,src:'Emerson'},{date:'2025-12',rep:46,dem:46,src:'PPP'},{date:'2026-01',rep:48,dem:45,src:'Quinnipiac'},{date:'2026-02',rep:47,dem:46,src:'Marist'},{date:'2026-03',rep:48,dem:45,src:'YouGov'},{date:'2026-04',rep:48,dem:46,src:'Emerson'}],primCands:{rep:[{name:'Ken Paxton',init:'KP',desc:'Procureur général',score:'48.8%',cls:'rr',badge:'2d tour'},{name:'John Cornyn',init:'JC',desc:'Sénateur sortant',score:'41.3%',cls:'rr',badge:'2d tour'}],dem:[{name:'James Talarico',init:'JT',desc:'Représentant',score:'53.1%',cls:'dd',badge:'🏆 Vainqueur'},{name:'Jasmine Crockett',init:'JC',desc:'Représentante',score:'45.6%',cls:'dd',badge:'Battue'}]},sources:{rcp:'https://www.realclearpolling.com/maps/senate/2026/texas',poly:'https://polymarket.com/event/texas-senate-2026',bp:'https://ballotpedia.org/United_States_Senate_election_in_Texas,_2026'}},
    {id:'senate-ga',state:'Géorgie',rating:'Tossup',cls:'tossup',rep:'Mike Collins',repD:'Représentant (GA-10)',dem:'Jon Ossoff',demD:'Sénateur sortant',repPct:47,demPct:48,proj:{rSafe:8,rLikely:12,rLean:18,rTilt:6,tossup:30,dTilt:6,dLean:12,dLikely:6},note:'Ultra-compétitive',primaryDate:'19 mai 2026',polls:[{date:'2024-06',rep:44,dem:50,src:'Quinnipiac'},{date:'2024-10',rep:46,dem:48,src:'Emerson'},{date:'2025-02',rep:47,dem:48,src:'PPP'},{date:'2025-06',rep:48,dem:47,src:'YouGov'},{date:'2025-10',rep:47,dem:48,src:'Quinnipiac'},{date:'2026-02',rep:48,dem:48,src:'Emerson'},{date:'2026-04',rep:47,dem:48,src:'Marist'}],sources:{rcp:'https://www.realclearpolling.com/maps/senate/2026/georgia',poly:'https://polymarket.com/event/georgia-senate-2026',bp:'https://ballotpedia.org/United_States_Senate_election_in_Georgia,_2026'}},
    {id:'senate-mi',state:'Michigan',rating:'Tilt D',cls:'tilt-d',rep:'Mike Rogers',repD:'Ancien représentant',dem:'Mallory McMorrow',demD:'Sénatrice d\'État',repPct:46,demPct:50,proj:{rSafe:3,rLikely:6,rLean:12,rTilt:4,tossup:22,dTilt:10,dLean:25,dLikely:12},note:'Siège ouvert (Peters)',primaryDate:'5 août 2026',polls:[{date:'2024-09',rep:44,dem:52,src:'EPIC-MRA'},{date:'2025-03',rep:46,dem:50,src:'PPP'},{date:'2025-08',rep:45,dem:51,src:'YouGov'},{date:'2026-01',rep:46,dem:50,src:'EPIC-MRA'},{date:'2026-04',rep:46,dem:50,src:'Emerson'}],sources:{rcp:'https://www.realclearpolling.com/maps/senate/2026/michigan',bp:'https://ballotpedia.org/United_States_Senate_election_in_Michigan,_2026'}},
    {id:'senate-nc',state:'Caroline du Nord',rating:'Tossup',cls:'tossup',rep:'Michael Whatley',repD:'Ancien président RNC',dem:'Roy Cooper',demD:'Ancien gouverneur',repPct:46,demPct:50,proj:{rSafe:4,rLikely:8,rLean:12,rTilt:8,tossup:30,dTilt:9,dLean:18,dLikely:8},note:'Tillis retraité',primaryDate:'3 mars 2026',polls:[{date:'2024-10',rep:48,dem:48,src:'PPP'},{date:'2025-04',rep:47,dem:49,src:'YouGov'},{date:'2025-09',rep:46,dem:50,src:'Emerson'},{date:'2026-02',rep:46,dem:50,src:'Marist'},{date:'2026-04',rep:46,dem:50,src:'Quinnipiac'}],sources:{rcp:'https://www.realclearpolling.com/maps/senate/2026/north-carolina',bp:'https://ballotpedia.org/United_States_Senate_election_in_North_Carolina,_2026'}}
  ];

  function buildEntry(r, type) {
    const init = n => n.split(' ').map(w => w[0]).join('');
    const primCands = r.primCands || {};
    return {
      id: r.id, title: type === 'house' ? `House · ${r.state} ${r.district}` : `Sénat · ${r.state}`,
      rating: r.rating, ratingClass: r.cls,
      candidates: [{ name:r.rep, party:'R', initials:init(r.rep), pct:r.repPct, desc:r.repD },{ name:r.dem, party:'D', initials:init(r.dem), pct:r.demPct, desc:r.demD }],
      proj: r.proj, seats: r.note,
      polls: r.polls || [], sources: r.sources || {},
      primaryDate: r.primaryDate,
      primaries: {
        rep: { cands: primCands.rep || [{ name:r.rep, init:init(r.rep), desc:'Candidat', score:'100%', cls:'rr', badge:'Investiture' }] },
        dem: { cands: primCands.dem || [{ name:r.dem, init:init(r.dem), desc:'Candidat', score:'100%', cls:'dd', badge:'Investiture' }] }
      }
    };
  }

  houseRaces.forEach(r => { racesData[r.id] = buildEntry(r, 'house'); });
  senateRaces.forEach(r => { racesData[r.id] = buildEntry(r, 'senate'); });

  function populateList(listId, races) {
    document.getElementById(listId).innerHTML = races.map(r => {
      const d = racesData[r.id]; if (!d) return '';
      const title = r.district ? `${r.state} · ${r.district}` : r.state;
      return `<div class="race-item" data-race="${r.id}"><div class="race-info"><h3>${title}</h3><p>${r.rep} (R) vs ${r.dem} (D)</p></div><div class="race-tag ${r.cls}">${r.rating}</div></div>`;
    }).join('');
  }
  populateList('house-races', houseRaces);
  populateList('senate-races', senateRaces);

  function showDetail(id) {
    const d = racesData[id]; if (!d) return;
    const container = document.getElementById('detail-container');
    const arrowPos = ratingPos[d.rating] || 50;
    const total = Object.values(d.proj).reduce((a,b) => a+b, 0) || 100;
    const s = 100/total;
    const hasPolls = d.polls && d.polls.length > 0;
    const hasSources = hasPolls && Object.keys(d.sources).length > 0;
    
    container.innerHTML = `
      <div class="card">
        <div class="card-header"><div class="card-title">${d.title}</div><div class="race-tag ${d.ratingClass}">${d.rating}</div></div>
        ${d.candidates.map(c => `
          <div class="candidate-row">
            <div class="candidate-label"><span class="party-name ${c.party==='R'?'rep':'dem'}">${c.name} (${c.party})</span><span class="party-pct ${c.party==='R'?'rep':'dem'}">${c.pct}%</span></div>
            <div style="color:rgba(255,255,255,0.45);font-size:0.7rem;margin-bottom:0.3rem;">${c.desc}</div>
            <div class="bar-wrap"><div class="bar-fill ${c.party==='R'?'bar-r':'bar-d'}" style="width:${c.pct}%">${c.pct}%</div></div>
          </div>
        `).join('')}
        
        <div class="gauge-container">
          <div class="gauge-label">${['Safe R','Likely R','Lean R','Tilt R','Tossup','Tilt D','Lean D','Likely D','Safe D'].map(x => `<span>${x}</span>`).join('')}</div>
          <div class="gauge-bar"><div class="gauge-arrow" style="left:${arrowPos}%;">▼</div></div>
          <div class="gauge-pos">Position : <strong style="color:${d.ratingClass.includes('r')?'#ff9e8f':d.ratingClass.includes('d')?'#8fc1ff':'#ffe082'}">${d.rating}</strong></div>
        </div>
        <p style="color:rgba(255,255,255,0.5);font-size:0.8rem;text-align:center;margin:1rem 0;">${d.seats}</p>
        
        ${hasPolls ? `
        <div style="margin-top:1.2rem;">
          <h4 style="color:rgba(255,255,255,0.5);font-size:0.75rem;text-transform:uppercase;">📈 Graphique des sondages</h4>
          <div class="chart-container"><canvas id="detailChart" width="800" height="230"></canvas><div class="chart-tooltip" id="chartTooltip" style="opacity:0;"></div></div>
          <div class="chart-legend"><span><span class="legend-dot r"></span> ${d.candidates[0].name.split(' ').pop()} (R)</span><span><span class="legend-dot d"></span> ${d.candidates[1].name.split(' ').pop()} (D)</span></div>
          
          <h4 style="color:rgba(255,255,255,0.5);font-size:0.75rem;text-transform:uppercase;margin-top:1rem;">📊 Sondages</h4>
          <div style="max-height:250px;overflow-y:auto;">
            <table class="polls-table">
              <thead><tr><th>Date</th><th>Source</th><th>${d.candidates[0].name.split(' ').pop()} (R)</th><th>${d.candidates[1].name.split(' ').pop()} (D)</th></tr></thead>
              <tbody>${d.polls.map(p => `<tr><td>${p.date}</td><td style="color:rgba(255,255,255,0.5);">${p.src}</td><td class="r-val">${p.rep}%</td><td class="d-val">${p.dem}%</td></tr>`).join('')}</tbody>
            </table>
          </div>
        </div>` : '<p class="no-data">Aucun sondage disponible pour cette course</p>'}
        
        ${hasSources ? `
        <div class="sources-section">
          <div class="sources-title">🔗 Sources</div>
          <div class="source-links">
            ${d.sources.rcp ? `<a href="${d.sources.rcp}" target="_blank" class="source-link">📊 RealClearPolitics</a>` : ''}
            ${d.sources.poly ? `<a href="${d.sources.poly}" target="_blank" class="source-link">💰 Polymarket</a>` : ''}
            ${d.sources.bp ? `<a href="${d.sources.bp}" target="_blank" class="source-link">📋 Ballotpedia</a>` : ''}
          </div>
        </div>` : ''}
      </div>
      
      <div class="card">
        <div class="card-header"><div class="card-title">Primaires</div><div style="color:rgba(255,255,255,0.5);font-size:0.8rem;">📅 ${d.primaryDate}</div></div>
        <div class="prim-tabs"><div class="prim-tab ra active" data-prim="rep">Républicaine</div><div class="prim-tab da" data-prim="dem">Démocrate</div></div>
        <div class="prim-panel active" id="panel-rep"><div class="primary-grid">${d.primaries.rep.cands.map(c => `<div class="cand-card"><div class="cand-photo ${c.cls}">${c.init}</div><div style="font-weight:700;color:white;">${c.name}</div><div style="font-size:0.65rem;color:rgba(255,255,255,0.5);">${c.desc}</div><div style="font-size:1.4rem;font-weight:800;color:#ff9e8f;">${c.score}</div><div style="font-size:0.6rem;color:#ffd700;">${c.badge}</div></div>`).join('')}</div></div>
        <div class="prim-panel" id="panel-dem"><div class="primary-grid">${d.primaries.dem.cands.map(c => `<div class="cand-card"><div class="cand-photo ${c.cls}">${c.init}</div><div style="font-weight:700;color:white;">${c.name}</div><div style="font-size:0.65rem;color:rgba(255,255,255,0.5);">${c.desc}</div><div style="font-size:1.4rem;font-weight:800;color:#8fc1ff;">${c.score}</div><div style="font-size:0.6rem;color:#ffd700;">${c.badge}</div></div>`).join('')}</div></div>
      </div>
    `;
    
    setTimeout(() => {
      container.querySelectorAll('.prim-tab').forEach(t => {
        t.addEventListener('click', function() {
          const target = this.dataset.prim;
          this.parentElement.querySelectorAll('.prim-tab').forEach(x => x.classList.remove('active','ra','da'));
          this.classList.add('active'); this.classList.add(target==='rep'?'ra':'da');
          container.querySelector('#panel-rep').style.display = target==='rep'?'block':'none';
          container.querySelector('#panel-dem').style.display = target==='dem'?'block':'none';
        });
      });
      if (hasPolls) drawChart(d.polls, d.candidates);
    }, 100);
  }

  function drawChart(polls, cands) {
    const canvas = document.getElementById('detailChart'); if(!canvas) return;
    const ctx = canvas.getContext('2d');
    const tooltip = document.getElementById('chartTooltip');
    const repAvg=[], demAvg=[];
    for(let i=0;i<polls.length;i++){ let sR=0,sD=0,c=0; for(let j=Math.max(0,i-2);j<=i;j++){sR+=polls[j].rep;sD+=polls[j].dem;c++;} repAvg.push(Math.round(sR/c*10)/10); demAvg.push(Math.round(sD/c*10)/10); }
    const pad={top:20,right:25,bottom:30,left:36}, minY=Math.min(...polls.map(p=>Math.min(p.rep,p.dem)))-5, maxY=Math.max(...polls.map(p=>Math.max(p.rep,p.dem)))+5;
    let points=[];
    function draw(){
      const w=canvas.width,h=canvas.height,cW=w-pad.left-pad.right,cH=h-pad.top-pad.bottom;
      ctx.clearRect(0,0,w,h); ctx.fillStyle='rgba(10,10,18,0.5)'; ctx.fillRect(pad.left,pad.top,cW,cH);
      const gX=i=>pad.left+(i/(polls.length-1))*cW, gY=v=>pad.top+cH-((v-minY)/(maxY-minY))*cH;
      ctx.strokeStyle='rgba(255,255,255,0.06)';
      for(let i=Math.floor(minY/5)*5;i<=maxY;i+=5){const y=gY(i);ctx.beginPath();ctx.moveTo(pad.left,y);ctx.lineTo(pad.left+cW,y);ctx.stroke();}
      polls.forEach((p,i)=>{ctx.fillStyle='rgba(255,255,255,0.45)';ctx.font='9px Segoe UI';ctx.fillText(p.date.slice(-2),gX(i),pad.top+cH+10);});
      [{d:repAvg,c:'#ff8a7a'},{d:demAvg,c:'#8fc1ff'}].forEach(l=>{ctx.beginPath();ctx.moveTo(gX(0),gY(l.d[0]));for(let i=1;i<l.d.length;i++){const xc=gX(i),yc=gY(l.d[i]),xp=gX(i-1),yp=gY(l.d[i-1]);ctx.bezierCurveTo(xp+(xc-xp)*0.5,yp,xc-(xc-xp)*0.5,yc,xc,yc);}ctx.strokeStyle=l.c;ctx.lineWidth=2.2;ctx.stroke();});
      points=[];
      polls.forEach((p,i)=>{[{v:p.rep,t:'r',c:'rgba(180,40,40,0.5)'},{v:p.dem,t:'d',c:'rgba(30,80,180,0.5)'}].forEach(pt=>{const x=gX(i),y=gY(pt.v);points.push({x,y,type:pt.t,value:pt.v,date:p.date});ctx.beginPath();ctx.arc(x,y,5,0,2*Math.PI);ctx.fillStyle=pt.c;ctx.fill();});});
    }
    draw();
    canvas.onmousemove=e=>{
      const rect=canvas.getBoundingClientRect(),sX=canvas.width/rect.width,sY=canvas.height/rect.height;
      const mx=(e.clientX-rect.left)*sX,my=(e.clientY-rect.top)*sY;
      let cl=null,md=18; points.forEach(p=>{const d=Math.hypot(mx-p.x,my-p.y);if(d<md){md=d;cl=p;}});
      if(cl){tooltip.innerHTML=`<strong>${cl.type==='r'?cands[0].name:cands[1].name}</strong><br><span style="color:${cl.type==='r'?'#ff9e8f':'#8fc1ff'}">${cl.value}%</span><br>${cl.date}`;tooltip.style.left=Math.max(5,Math.min(cl.x/sX-45,rect.width-95))+'px';tooltip.style.top=Math.max(5,cl.y/sY-45)+'px';tooltip.style.opacity='1';}else{tooltip.style.opacity='0';}
    };
    canvas.onmouseleave=()=>tooltip.style.opacity='0';
  }

  document.querySelectorAll('.cat-tab').forEach(t=>t.addEventListener('click',function(){
    document.querySelectorAll('.cat-tab').forEach(x=>x.classList.remove('active'));this.classList.add('active');
    document.querySelectorAll('.cat-panel').forEach(x=>x.classList.remove('active'));
    document.getElementById('cat-'+this.dataset.cat).classList.add('active');
    (document.querySelector('#cat-'+this.dataset.cat+' .race-item')||{}).click?.();
  }));
  document.addEventListener('click',e=>{
    const item=e.target.closest('.race-item[data-race]');
    if(item){document.querySelectorAll('.race-item').forEach(i=>i.classList.remove('active'));item.classList.add('active');showDetail(item.dataset.race);}
  });
  (document.querySelector('#house-races .race-item')||{}).click?.();
})();
</script>
<div style="height:30px;"></div>
</body>
</html>
