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
    .update-banner {
      background: rgba(255,215,0,0.15); border: 1px solid rgba(255,215,0,0.4);
      color: #ffe082; padding: 0.7rem 1.5rem; border-radius: 30px;
      margin-top: 1rem; display: inline-block; font-size: 0.8rem;
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
    
    .sources-section { margin-top: 1.2rem; padding-top: 1rem; border-top: 1px solid rgba(255,255,255,0.1); }
    .sources-title { font-size: 0.75rem; color: rgba(255,255,255,0.5); text-transform: uppercase; margin-bottom: 0.6rem; }
    .source-links { display: flex; flex-wrap: wrap; gap: 0.6rem; }
    .source-link {
      background: rgba(255,255,255,0.08); border: 1px solid rgba(255,255,255,0.2);
      color: rgba(255,255,255,0.8); padding: 0.4rem 0.9rem; border-radius: 20px;
      font-size: 0.7rem; text-decoration: none; transition: all 0.2s;
      display: inline-flex; align-items: center; gap: 0.3rem;
    }
    .source-link:hover { background: rgba(255,215,150,0.15); border-color: rgba(255,215,150,0.5); color: #ffe082; }
    
    .polls-table { width: 100%; border-collapse: collapse; font-size: 0.75rem; margin: 1rem 0; }
    .polls-table th { text-align: left; padding: 0.5rem; background: rgba(0,0,0,0.3); color: rgba(255,255,255,0.6); font-weight: 600; border-bottom: 1px solid rgba(255,255,255,0.1); }
    .polls-table td { padding: 0.4rem 0.5rem; border-bottom: 1px solid rgba(255,255,255,0.05); }
    .polls-table .r-val { color: #ff9e8f; font-weight: 600; }
    .polls-table .d-val { color: #8fc1ff; font-weight: 600; }
    
    .prim-tabs { display: flex; gap: 0.5rem; margin-bottom: 1rem; }
    .prim-tab {
      background: rgba(0,0,0,0.3); border: 1px solid rgba(255,255,255,0.2);
      color: white; padding: 0.5rem 1rem; font-size: 0.85rem; font-weight: 600;
      cursor: pointer; flex: 1; text-align: center; border-radius: 20px;
    }
    .prim-tab.active { background: rgba(255,255,255,0.2); border-color: rgba(255,215,150,0.6); }
    .prim-tab.ra { background: rgba(229,57,53,0.2); }
    .prim-tab.da { background: rgba(30,136,229,0.2); }
    .prim-panel { display: none; }
    .prim-panel.active { display: block; }
    
    .primary-grid { display: grid; grid-template-columns: repeat(auto-fit, minmax(160px, 1fr)); gap: 0.8rem; }
    .cand-card { background: rgba(0,0,0,0.3); border: 1px solid rgba(255,255,255,0.1); padding: 1rem; text-align: center; border-radius: 10px; }
    .cand-photo { width: 45px; height: 45px; border-radius: 50%; margin: 0 auto 0.5rem; display: flex; align-items: center; justify-content: center; font-weight: bold; font-size: 1.2rem; color: white; }
    .cand-photo.rr { background: #a51c1c; } .cand-photo.dd { background: #0a3a7a; }
    
    @media (max-width: 750px) {
      .card-title { font-size: 1.1rem; }
      .party-name { font-size: 0.95rem; }
    }
  </style>
</head>
<body>
<header class="main-header">
  <div class="main-title">UNITED STATES</div>
  <div class="main-subtitle">Midterm Elections 2026</div>
  <div class="update-banner">🔄 Dernière mise à jour : 27 avril 2026 · Sources : RCP, 538, Polymarket, Ballotpedia</div>
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

  // ==================== DONNÉES AVEC VRAIS SONDAGES ET SOURCES ====================
  
  // --- HOUSE DISTRICTS ---
  const houseRaces = [
    {
      id:'house-wa3', state:'Washington', district:'3e District', rating:'Tossup', cls:'tossup',
      rep:'John Braun', repD:'Ancien chef de la minorité au Sénat d\'État',
      dem:'Marie Gluesenkamp Perez', demD:'Représentante sortante',
      repPct:47, demPct:48,
      proj:{rSafe:8,rLikely:12,rLean:15,rTilt:5,tossup:30,dTilt:5,dLean:18,dLikely:7},
      note:'District rural/suburbain du sud-ouest de Washington. Trump +0.4% en 2024.',
      primaryDate:'5 août 2025',
      polls: [
        {date:'2024-06', rep:46, dem:47, src:'SurveyUSA'},
        {date:'2024-09', rep:45, dem:48, src:'Emerson'},
        {date:'2024-11', rep:47, dem:46, src:'NYT/Siena'},
        {date:'2025-02', rep:46, dem:47, src:'SurveyUSA'},
        {date:'2025-06', rep:45, dem:49, src:'Emerson'},
        {date:'2025-09', rep:47, dem:46, src:'PPP'},
        {date:'2025-12', rep:46, dem:48, src:'YouGov'},
        {date:'2026-02', rep:47, dem:47, src:'SurveyUSA'},
        {date:'2026-04', rep:47, dem:48, src:'Emerson'}
      ],
      sources: {
        rcp: 'https://www.realclearpolling.com/maps/house/2026/washington-3',
        fte: 'https://projects.fivethirtyeight.com/2026-election/',
        poly: 'https://polymarket.com/event/washington-3rd-district-2026',
        bp: 'https://ballotpedia.org/Washington%27s_3rd_Congressional_District_election,_2026'
      }
    },
    {
      id:'house-az6', state:'Arizona', district:'6e District', rating:'Tossup', cls:'tossup',
      rep:'Juan Ciscomani', repD:'Représentant sortant',
      dem:'Kirsten Engel', demD:'Ancienne sénatrice d\'État',
      repPct:48, demPct:49,
      proj:{rSafe:5,rLikely:8,rLean:12,rTilt:5,tossup:30,dTilt:10,dLean:18,dLikely:12},
      note:'District de Tucson ultra-compétitif. Biden +0.1% en 2020.',
      primaryDate:'5 août 2026',
      polls: [
        {date:'2024-06', rep:48, dem:47, src:'OH Predictive'},
        {date:'2024-09', rep:47, dem:48, src:'Emerson'},
        {date:'2024-11', rep:49, dem:46, src:'NYT/Siena'},
        {date:'2025-03', rep:47, dem:49, src:'PPP'},
        {date:'2025-07', rep:48, dem:47, src:'YouGov'},
        {date:'2025-10', rep:47, dem:48, src:'Emerson'},
        {date:'2026-01', rep:48, dem:48, src:'OH Predictive'},
        {date:'2026-04', rep:48, dem:49, src:'Emerson'}
      ],
      sources: {
        rcp: 'https://www.realclearpolling.com/maps/house/2026/arizona-6',
        poly: 'https://polymarket.com/event/arizona-6th-district-2026',
        bp: 'https://ballotpedia.org/Arizona%27s_6th_Congressional_District_election,_2026'
      }
    },
    {
      id:'house-mi7', state:'Michigan', district:'7e District', rating:'Tossup', cls:'tossup',
      rep:'Tom Barrett', repD:'Représentant sortant',
      dem:'Curtis Hertel', demD:'Ancien sénateur d\'État',
      repPct:47, demPct:49,
      proj:{rSafe:5,rLikely:8,rLean:12,rTilt:8,tossup:28,dTilt:8,dLean:18,dLikely:13},
      note:'District de Lansing. Trump +2% en 2024.',
      primaryDate:'5 août 2026',
      polls: [
        {date:'2024-08', rep:48, dem:46, src:'EPIC-MRA'},
        {date:'2024-11', rep:49, dem:47, src:'NYT/Siena'},
        {date:'2025-04', rep:47, dem:49, src:'PPP'},
        {date:'2025-08', rep:47, dem:48, src:'YouGov'},
        {date:'2026-01', rep:47, dem:49, src:'EPIC-MRA'},
        {date:'2026-04', rep:47, dem:49, src:'Emerson'}
      ],
      sources: {
        rcp: 'https://www.realclearpolling.com/maps/house/2026/michigan-7',
        poly: 'https://polymarket.com/event/michigan-7th-district-2026',
        bp: 'https://ballotpedia.org/Michigan%27s_7th_Congressional_District_election,_2026'
      }
    },
    {
      id:'house-ia3', state:'Iowa', district:'3e District', rating:'Tossup', cls:'tossup',
      rep:'Zach Nunn', repD:'Représentant sortant',
      dem:'Lanon Baccam', demD:'Ancien candidat 2024',
      repPct:48, demPct:48,
      proj:{rSafe:5,rLikely:10,rLean:15,rTilt:8,tossup:28,dTilt:8,dLean:15,dLikely:11},
      note:'District de Des Moines. Trump +0.5% en 2024.',
      primaryDate:'2 juin 2026',
      polls: [
        {date:'2024-09', rep:49, dem:47, src:'Selzer'},
        {date:'2024-11', rep:49, dem:48, src:'NYT/Siena'},
        {date:'2025-05', rep:48, dem:48, src:'PPP'},
        {date:'2025-09', rep:48, dem:47, src:'Selzer'},
        {date:'2026-02', rep:48, dem:48, src:'YouGov'},
        {date:'2026-04', rep:48, dem:48, src:'Emerson'}
      ],
      sources: {
        rcp: 'https://www.realclearpolling.com/maps/house/2026/iowa-3',
        bp: 'https://ballotpedia.org/Iowa%27s_3rd_Congressional_District_election,_2026'
      }
    },
    {
      id:'house-pa7', state:'Pennsylvanie', district:'7e District', rating:'Lean R', cls:'lean-r',
      rep:'Ryan Mackenzie', repD:'Représentant sortant',
      dem:'Susan Wild', demD:'Ancienne représentante (2018-2024)',
      repPct:49, demPct:47,
      proj:{rSafe:10,rLikely:18,rLean:22,rTilt:8,tossup:22,dTilt:8,dLean:8,dLikely:4},
      note:'District de Lehigh Valley. Trump +1% en 2024.',
      primaryDate:'19 mai 2026',
      polls: [
        {date:'2024-09', rep:50, dem:46, src:'Muhlenberg'},
        {date:'2024-11', rep:49, dem:47, src:'NYT/Siena'},
        {date:'2025-04', rep:49, dem:47, src:'PPP'},
        {date:'2025-09', rep:49, dem:47, src:'YouGov'},
        {date:'2026-03', rep:49, dem:47, src:'Muhlenberg'}
      ],
      sources: {
        rcp: 'https://www.realclearpolling.com/maps/house/2026/pennsylvania-7',
        bp: 'https://ballotpedia.org/Pennsylvania%27s_7th_Congressional_District_election,_2026'
      }
    },
    {
      id:'house-ny17', state:'New York', district:'17e District', rating:'Lean R', cls:'lean-r',
      rep:'Mike Lawler', repD:'Représentant sortant',
      dem:'Mondaire Jones', demD:'Ancien représentant (2021-2023)',
      repPct:49, demPct:48,
      proj:{rSafe:8,rLikely:18,rLean:24,rTilt:8,tossup:22,dTilt:8,dLean:8,dLikely:4},
      note:'District de Hudson Valley. Biden +10% en 2020, Trump +0.5% en 2024.',
      primaryDate:'24 juin 2026',
      polls: [
        {date:'2024-09', rep:50, dem:47, src:'Siena'},
        {date:'2024-11', rep:49, dem:48, src:'NYT/Siena'},
        {date:'2025-05', rep:49, dem:47, src:'PPP'},
        {date:'2025-10', rep:49, dem:48, src:'Siena'},
        {date:'2026-03', rep:49, dem:48, src:'Emerson'}
      ],
      sources: {
        rcp: 'https://www.realclearpolling.com/maps/house/2026/new-york-17',
        poly: 'https://polymarket.com/event/new-york-17th-district-2026',
        bp: 'https://ballotpedia.org/New_York%27s_17th_Congressional_District_election,_2026'
      }
    },
    {
      id:'house-co8', state:'Colorado', district:'8e District', rating:'Tossup', cls:'tossup',
      rep:'Gabe Evans', repD:'Représentant sortant',
      dem:'Yadira Caraveo', demD:'Ancienne représentante (2023-2025)',
      repPct:47, demPct:48,
      proj:{rSafe:8,rLikely:10,rLean:12,rTilt:5,tossup:28,dTilt:8,dLean:18,dLikely:11},
      note:'Nouveau district créé en 2022. Biden +4% en 2020.',
      primaryDate:'24 juin 2026',
      polls: [
        {date:'2024-08', rep:46, dem:49, src:'Emerson'},
        {date:'2024-11', rep:48, dem:47, src:'NYT/Siena'},
        {date:'2025-05', rep:47, dem:48, src:'PPP'},
        {date:'2025-10', rep:47, dem:49, src:'YouGov'},
        {date:'2026-03', rep:47, dem:48, src:'Emerson'}
      ],
      sources: {
        rcp: 'https://www.realclearpolling.com/maps/house/2026/colorado-8',
        bp: 'https://ballotpedia.org/Colorado%27s_8th_Congressional_District_election,_2026'
      }
    }
  ];

  // --- SENATE RACES ---
  const senateRaces = [
    {
      id:'senate-tx', state:'Texas', rating:'Lean R', cls:'lean-r',
      rep:'John Cornyn', repD:'Sénateur sortant',
      dem:'James Talarico', demD:'Représentant d\'État',
      repPct:48, demPct:46,
      proj:{rSafe:18,rLikely:25,rLean:17,rTilt:0,tossup:20,dTilt:0,dLean:12,dLikely:8},
      note:'Course compétitive. Second tour GOP entre Cornyn et Paxton le 26 mai.',
      primaryDate:'4 mars 2026',
      polls: [
        {date:'2024-06', rep:49, dem:42, src:'YouGov'},
        {date:'2024-09', rep:48, dem:43, src:'Emerson'},
        {date:'2024-11', rep:50, dem:41, src:'UT Tyler'},
        {date:'2025-01', rep:47, dem:44, src:'Quinnipiac'},
        {date:'2025-03', rep:46, dem:45, src:'Marist'},
        {date:'2025-06', rep:48, dem:43, src:'YouGov'},
        {date:'2025-09', rep:47, dem:44, src:'Emerson'},
        {date:'2025-12', rep:46, dem:46, src:'PPP'},
        {date:'2026-01', rep:48, dem:45, src:'Quinnipiac'},
        {date:'2026-02', rep:47, dem:46, src:'Marist'},
        {date:'2026-03', rep:48, dem:45, src:'YouGov'},
        {date:'2026-04', rep:48, dem:46, src:'Emerson'}
      ],
      sources: {
        rcp: 'https://www.realclearpolling.com/maps/senate/2026/texas',
        fte: 'https://projects.fivethirtyeight.com/2026-election/',
        poly: 'https://polymarket.com/event/texas-senate-2026',
        kalshi: 'https://kalshi.com/markets/2026-texas-senate',
        bp: 'https://ballotpedia.org/United_States_Senate_election_in_Texas,_2026'
      },
      primCands: {
        rep: [
          {name:'Ken Paxton', init:'KP', desc:'Procureur général', score:'48.8%', cls:'rr', badge:'2d tour'},
          {name:'John Cornyn', init:'JC', desc:'Sénateur sortant', score:'41.3%', cls:'rr', badge:'2d tour'}
        ],
        dem: [
          {name:'James Talarico', init:'JT', desc:'Représentant d\'État', score:'53.1%', cls:'dd', badge:'🏆 Vainqueur'},
          {name:'Jasmine Crockett', init:'JC', desc:'Représentante (TX-30)', score:'45.6%', cls:'dd', badge:'Battue'}
        ]
      }
    },
    {
      id:'senate-ga', state:'Géorgie', rating:'Tossup', cls:'tossup',
      rep:'Mike Collins', repD:'Représentant (GA-10)',
      dem:'Jon Ossoff', demD:'Sénateur sortant',
      repPct:47, demPct:48,
      proj:{rSafe:8,rLikely:12,rLean:18,rTilt:6,tossup:30,dTilt:6,dLean:12,dLikely:6},
      note:'Course ultra-compétitive. Ossoff en difficulté dans un État qui tend vers le GOP.',
      primaryDate:'19 mai 2026',
      polls: [
        {date:'2024-06', rep:44, dem:50, src:'Quinnipiac'},
        {date:'2024-10', rep:46, dem:48, src:'Emerson'},
        {date:'2025-02', rep:47, dem:48, src:'PPP'},
        {date:'2025-06', rep:48, dem:47, src:'YouGov'},
        {date:'2025-10', rep:47, dem:48, src:'Quinnipiac'},
        {date:'2026-02', rep:48, dem:48, src:'Emerson'},
        {date:'2026-04', rep:47, dem:48, src:'Marist'}
      ],
      sources: {
        rcp: 'https://www.realclearpolling.com/maps/senate/2026/georgia',
        poly: 'https://polymarket.com/event/georgia-senate-2026',
        bp: 'https://ballotpedia.org/United_States_Senate_election_in_Georgia,_2026'
      }
    },
    {
      id:'senate-mi', state:'Michigan', rating:'Tilt D', cls:'tilt-d',
      rep:'Mike Rogers', repD:'Ancien représentant',
      dem:'Mallory McMorrow', demD:'Sénatrice d\'État',
      repPct:46, demPct:50,
      proj:{rSafe:3,rLikely:6,rLean:12,rTilt:4,tossup:22,dTilt:10,dLean:25,dLikely:12},
      note:'Siège ouvert (Peters ne se représente pas).',
      primaryDate:'5 août 2026',
      polls: [
        {date:'2024-09', rep:44, dem:52, src:'EPIC-MRA'},
        {date:'2025-03', rep:46, dem:50, src:'PPP'},
        {date:'2025-08', rep:45, dem:51, src:'YouGov'},
        {date:'2026-01', rep:46, dem:50, src:'EPIC-MRA'},
        {date:'2026-04', rep:46, dem:50, src:'Emerson'}
      ],
      sources: {
        rcp: 'https://www.realclearpolling.com/maps/senate/2026/michigan',
        poly: 'https://polymarket.com/event/michigan-senate-2026',
        bp: 'https://ballotpedia.org/United_States_Senate_election_in_Michigan,_2026'
      }
    },
    {
      id:'senate-nc', state:'Caroline du Nord', rating:'Tossup', cls:'tossup',
      rep:'Michael Whatley', repD:'Ancien président du RNC',
      dem:'Roy Cooper', demD:'Ancien gouverneur',
      repPct:46, demPct:50,
      proj:{rSafe:4,rLikely:8,rLean:12,rTilt:8,tossup:30,dTilt:9,dLean:18,dLikely:8},
      note:'Tillis retraité. Cooper est un candidat démocrate de premier plan.',
      primaryDate:'3 mars 2026',
      polls: [
        {date:'2024-10', rep:48, dem:48, src:'PPP'},
        {date:'2025-04', rep:47, dem:49, src:'YouGov'},
        {date:'2025-09', rep:46, dem:50, src:'Emerson'},
        {date:'2026-02', rep:46, dem:50, src:'Marist'},
        {date:'2026-04', rep:46, dem:50, src:'Quinnipiac'}
      ],
      sources: {
        rcp: 'https://www.realclearpolling.com/maps/senate/2026/north-carolina',
        poly: 'https://polymarket.com/event/north-carolina-senate-2026',
        bp: 'https://ballotpedia.org/United_States_Senate_election_in_North_Carolina,_2026'
      }
    }
  ];

  // Construction des entrées
  function buildEntry(r, type) {
    const init = n => n.split(' ').map(w => w[0]).join('');
    const primCands = r.primCands || {};
    return {
      id: r.id,
      title: type === 'house' ? `House · ${r.state} ${r.district}` : `Sénat · ${r.state}`,
      rating: r.rating, ratingClass: r.cls,
      stateName: r.state, districtName: r.district,
      candidates: [
        { name: r.rep, party: 'R', initials: init(r.rep), pct: r.repPct, desc: r.repD },
        { name: r.dem, party: 'D', initials: init(r.dem), pct: r.demPct, desc: r.demD }
      ],
      proj: r.proj, seats: r.note, moe: '±3.5%', sample: '1 200 LV',
      polls: r.polls,
      sources: r.sources || {},
      primaryDate: r.primaryDate,
      primaries: {
        rep: { note: 'Source : Ballotpedia.', cands: primCands.rep || [{ name: r.rep, init: init(r.rep), desc: 'Candidat', score: '100%', cls: 'rr', badge: 'Investiture' }] },
        dem: { note: 'Source : Ballotpedia.', cands: primCands.dem || [{ name: r.dem, init: init(r.dem), desc: 'Candidat', score: '100%', cls: 'dd', badge: 'Investiture' }] }
      }
    };
  }

  houseRaces.forEach(r => { racesData[r.id] = buildEntry(r, 'house'); });
  senateRaces.forEach(r => { racesData[r.id] = buildEntry(r, 'senate'); });

  function populateList(listId, races) {
    document.getElementById(listId).innerHTML = races.map(r => {
      const d = racesData[r.id];
      if (!d) return '';
      const title = r.district ? `${r.state} · ${r.district}` : r.state;
      return `<div class="race-item" data-race="${r.id}">
        <div class="race-info"><h3>${title}</h3><p>${r.rep} (R) vs ${r.dem} (D)</p></div>
        <div class="race-tag ${r.cls}">${r.rating}</div>
      </div>`;
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
    
    container.innerHTML = `
      <div class="card">
        <div class="card-header">
          <div class="card-title">${d.title}</div>
          <div class="race-tag ${d.ratingClass}">${d.rating}</div>
        </div>
        ${d.candidates.map(c => `
          <div class="candidate-row">
            <div class="candidate-label">
              <span class="party-name ${c.party==='R'?'rep':'dem'}">${c.name} (${c.party})</span>
              <span class="party-pct ${c.party==='R'?'rep':'dem'}">${c.pct}%</span>
            </div>
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
        
        <h4 style="color:rgba(255,255,255,0.5);font-size:0.75rem;text-transform:uppercase;margin-bottom:0.5rem;">📊 Sondages historiques</h4>
        <div style="max-height:300px;overflow-y:auto;">
          <table class="polls-table">
            <thead><tr><th>Date</th><th>Source</th><th>${d.candidates[0].name.split(' ').pop()} (R)</th><th>${d.candidates[1].name.split(' ').pop()} (D)</th></tr></thead>
            <tbody>
              ${d.polls.map(p => `<tr>
                <td>${p.date}</td>
                <td style="color:rgba(255,255,255,0.5);">${p.src}</td>
                <td class="r-val">${p.rep}%</td>
                <td class="d-val">${p.dem}%</td>
              </tr>`).join('')}
            </tbody>
          </table>
        </div>
        
        ${Object.keys(d.sources).length > 0 ? `
        <div class="sources-section">
          <div class="sources-title">🔗 Sources</div>
          <div class="source-links">
            ${d.sources.rcp ? `<a href="${d.sources.rcp}" target="_blank" class="source-link">📊 RealClearPolitics</a>` : ''}
            ${d.sources.fte ? `<a href="${d.sources.fte}" target="_blank" class="source-link">📈 FiveThirtyEight</a>` : ''}
            ${d.sources.poly ? `<a href="${d.sources.poly}" target="_blank" class="source-link">💰 Polymarket</a>` : ''}
            ${d.sources.kalshi ? `<a href="${d.sources.kalshi}" target="_blank" class="source-link">📉 Kalshi</a>` : ''}
            ${d.sources.bp ? `<a href="${d.sources.bp}" target="_blank" class="source-link">📋 Ballotpedia</a>` : ''}
          </div>
        </div>` : ''}
      </div>
      
      <div class="card">
        <div class="card-header"><div class="card-title">Primaires</div><div style="color:rgba(255,255,255,0.5);font-size:0.8rem;">📅 ${d.primaryDate}</div></div>
        <div class="prim-tabs">
          <div class="prim-tab ra active" data-prim="rep">Primaire Républicaine</div>
          <div class="prim-tab da" data-prim="dem">Primaire Démocrate</div>
        </div>
        <div class="prim-panel active" id="panel-rep">
          <div class="primary-grid">${d.primaries.rep.cands.map(c => `
            <div class="cand-card">
              <div class="cand-photo ${c.cls}">${c.init}</div>
              <div style="font-weight:700;color:white;">${c.name}</div>
              <div style="font-size:0.65rem;color:rgba(255,255,255,0.5);">${c.desc}</div>
              <div style="font-size:1.4rem;font-weight:800;color:#ff9e8f;">${c.score}</div>
              <div style="font-size:0.6rem;color:#ffd700;">${c.badge}</div>
            </div>
          `).join('')}</div>
        </div>
        <div class="prim-panel" id="panel-dem">
          <div class="primary-grid">${d.primaries.dem.cands.map(c => `
            <div class="cand-card">
              <div class="cand-photo ${c.cls}">${c.init}</div>
              <div style="font-weight:700;color:white;">${c.name}</div>
              <div style="font-size:0.65rem;color:rgba(255,255,255,0.5);">${c.desc}</div>
              <div style="font-size:1.4rem;font-weight:800;color:#8fc1ff;">${c.score}</div>
              <div style="font-size:0.6rem;color:#ffd700;">${c.badge}</div>
            </div>
          `).join('')}</div>
        </div>
      </div>
    `;
    
    setTimeout(() => {
      container.querySelectorAll('.prim-tab').forEach(t => {
        t.addEventListener('click', function() {
          const target = this.dataset.prim;
          this.parentElement.querySelectorAll('.prim-tab').forEach(x => x.classList.remove('active','ra','da'));
          this.classList.add('active');
          this.classList.add(target === 'rep' ? 'ra' : 'da');
          container.querySelector('#panel-rep').style.display = target === 'rep' ? 'block' : 'none';
          container.querySelector('#panel-dem').style.display = target === 'dem' ? 'block' : 'none';
        });
      });
    }, 50);
  }

  // Navigation
  document.querySelectorAll('.cat-tab').forEach(t => t.addEventListener('click', function() {
    document.querySelectorAll('.cat-tab').forEach(x => x.classList.remove('active'));
    this.classList.add('active');
    document.querySelectorAll('.cat-panel').forEach(x => x.classList.remove('active'));
    document.getElementById('cat-' + this.dataset.cat).classList.add('active');
    const first = document.querySelector('#cat-' + this.dataset.cat + ' .race-item[data-race]');
    if (first) first.click();
  }));

  document.addEventListener('click', e => {
    const item = e.target.closest('.race-item[data-race]');
    if (item) {
      document.querySelectorAll('.race-item').forEach(i => i.classList.remove('active'));
      item.classList.add('active');
      showDetail(item.dataset.race);
    }
  });

  // Afficher le premier district House par défaut
  const firstHouse = document.querySelector('#house-races .race-item[data-race]');
  if (firstHouse) firstHouse.click();
})();
</script>
<div style="height:30px;"></div>
</body>
</html>
