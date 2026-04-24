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
      padding: 2rem; text-align: center; margin-bottom: 30px;
      box-shadow: 0 10px 30px rgba(0,0,0,0.6); border-bottom: 1px solid rgba(210,180,140,0.2);
    }
    .main-title { font-size: clamp(2rem, 6vw, 4rem); font-weight: 900; letter-spacing: 0.2em; color: #fff; text-transform: uppercase; }
    .main-subtitle { font-size: clamp(1rem, 3vw, 1.8rem); color: rgba(255,255,255,0.85); letter-spacing: 0.3em; text-transform: uppercase; border-top: 1.5px solid rgba(255,215,150,0.5); display: inline-block; padding-top: 0.7rem; margin-top: 0.5rem; }
    .main-content { width: 100%; max-width: 1400px; }

    /* ONGLETS CATÉGORIE */
    .category-tabs { display: flex; gap: 0.5rem; margin-bottom: 1.5rem; flex-wrap: wrap; }
    .cat-tab { background: rgba(0,0,0,0.4); border: 1px solid rgba(255,255,255,0.2); color: white; padding: 1rem 1.5rem; font-size: 1.1rem; font-weight: 700; text-transform: uppercase; letter-spacing: 0.1em; cursor: pointer; flex: 1; min-width: 150px; text-align: center; transition: all 0.2s; }
    .cat-tab:hover { background: rgba(255,255,255,0.1); }
    .cat-tab.active { background: rgba(255,255,255,0.15); border-color: rgba(255,215,150,0.6); box-shadow: 0 0 20px rgba(255,215,150,0.2); }
    .cat-panel { display: none; }
    .cat-panel.active { display: block; }

    /* LISTE DES COURSES */
    .race-list { display: flex; flex-direction: column; gap: 1rem; margin-bottom: 2rem; }
    .race-item { background: rgba(0,0,0,0.35); border: 1px solid rgba(220,200,180,0.18); padding: 1rem 1.5rem; cursor: pointer; transition: all 0.2s; display: flex; justify-content: space-between; align-items: center; flex-wrap: wrap; gap: 1rem; }
    .race-item:hover { background: rgba(255,255,255,0.08); border-color: rgba(255,215,150,0.4); }
    .race-item.active { background: rgba(255,255,255,0.12); border-color: rgba(255,215,150,0.7); box-shadow: 0 0 25px rgba(255,215,150,0.15); }
    .race-info h3 { color: #f0e6d2; font-size: 1.2rem; margin-bottom: 0.3rem; }
    .race-info p { color: rgba(255,255,255,0.5); font-size: 0.85rem; }
    .race-rating-badge { padding: 0.3rem 1rem; font-weight: 700; text-transform: uppercase; font-size: 0.75rem; letter-spacing: 0.1em; white-space: nowrap; }
    .badge-tossup { background: rgba(255,200,0,0.2); color: #ffc107; border: 1px solid #ffc107; }
    .badge-lean-r { background: rgba(229,57,53,0.2); color: #ff9e8f; border: 1px solid #e53935; }
    .badge-lean-d { background: rgba(30,136,229,0.2); color: #8fc1ff; border: 1px solid #1e88e5; }
    .badge-likely-r { background: rgba(229,57,53,0.3); color: #ff6b5e; border: 1px solid #d32f2f; }

    /* PANNEAU DE DÉTAILS */
    .detail-panel { display: none; }
    .detail-panel.active { display: block; }
    .card { width: 100%; background: rgba(0,0,0,0.35); backdrop-filter: blur(8px); border: 1px solid rgba(220,200,180,0.18); box-shadow: 0 25px 40px -10px rgba(0,0,0,0.7); padding: 2rem; margin-bottom: 1.5rem; }
    .card-header { display: flex; align-items: center; justify-content: space-between; margin-bottom: 2rem; border-bottom: 2px solid rgba(255,255,255,0.15); padding-bottom: 1.5rem; flex-wrap: wrap; gap: 1rem; }
    .card-title { font-size: 1.6rem; font-weight: 600; letter-spacing: 0.15em; text-transform: uppercase; color: #f0e6d2; }
    .candidate-row { margin-bottom: 1.8rem; }
    .candidate-label { display: flex; justify-content: space-between; margin-bottom: 0.7rem; flex-wrap: wrap; gap: 0.5rem; }
    .party-name { font-size: 1.3rem; font-weight: 700; letter-spacing: 0.1em; text-transform: uppercase; }
    .party-percent { font-size: 1.8rem; font-weight: 800; }
    .rep { color: #ff9e8f; } .dem { color: #8fc1ff; }
    .bar-wrapper { width: 100%; height: 40px; background: #121212e0; border: 1px solid rgba(255,255,255,0.12); overflow: hidden; }
    .bar-fill { height: 100%; display: flex; align-items: center; justify-content: flex-end; padding-right: 20px; font-weight: 700; color: white; font-size: 1rem; }
    .bar-fill.rep-fill { background: linear-gradient(90deg, #a51c1c, #d32f2f); }
    .bar-fill.dem-fill { background: linear-gradient(90deg, #0a3a7a, #1976d2); }
    .poll-footer { margin-top: 1.5rem; display: flex; justify-content: space-between; color: rgba(255,240,220,0.7); border-top: 1px solid rgba(255,255,240,0.1); padding-top: 1.2rem; flex-wrap: wrap; gap: 0.5rem; font-size: 0.85rem; }

    /* PROJECTIONS */
    .projections-bar { display: flex; height: 12px; margin: 1rem 0; background: #121212; }
    .proj-r-safe { background: #5a0000; } .proj-r-likely { background: #8b0000; } .proj-r-lean { background: #b71c1c; }
    .proj-tossup { background: #6b5a00; } .proj-d-lean { background: #1565c0; } .proj-d-likely { background: #0d47a1; }
    .projections-legend { display: flex; justify-content: space-between; font-size: 0.65rem; color: rgba(255,255,255,0.4); margin-bottom: 1rem; flex-wrap: wrap; }
    .seats-projection { text-align: center; color: rgba(255,255,255,0.6); font-size: 0.9rem; margin: 1rem 0; }

    /* PRIMAIRES AMÉLIORÉES */
    .primary-section { margin-top: 1rem; }
    .primary-header { display: flex; justify-content: space-between; align-items: center; margin-bottom: 1.5rem; flex-wrap: wrap; gap: 1rem; }
    .primary-date { color: rgba(255,255,255,0.6); font-size: 0.9rem; }
    .primary-tabs { display: flex; gap: 0.5rem; margin-bottom: 1.5rem; }
    .prim-tab { background: rgba(0,0,0,0.4); border: 1px solid rgba(255,255,255,0.2); color: white; padding: 0.7rem 1.2rem; font-size: 1rem; font-weight: 600; text-transform: uppercase; cursor: pointer; flex: 1; text-align: center; transition: all 0.2s; }
    .prim-tab:hover { background: rgba(255,255,255,0.08); }
    .prim-tab.active { background: rgba(255,255,255,0.15); border-color: rgba(255,215,150,0.6); }
    .prim-tab.r-active { background: rgba(229,57,53,0.2); border-color: #e53935; }
    .prim-tab.d-active { background: rgba(30,136,229,0.2); border-color: #1e88e5; }
    .prim-panel { display: none; }
    .prim-panel.active { display: block; }

    .primary-grid { display: grid; grid-template-columns: repeat(auto-fit, minmax(200px, 1fr)); gap: 1.5rem; margin-bottom: 2rem; }
    .candidate-card { background: rgba(0,0,0,0.3); border: 1px solid rgba(255,255,255,0.1); padding: 1.5rem; text-align: center; }
    .candidate-card.winner { border-color: rgba(255,215,150,0.4); box-shadow: 0 0 20px rgba(255,215,150,0.1); }
    .cand-photo { width: 65px; height: 65px; border-radius: 50%; margin: 0 auto 0.8rem; display: flex; align-items: center; justify-content: center; font-weight: bold; font-size: 1.6rem; color: white; border: 2px solid rgba(255,255,255,0.2); }
    .cand-photo.r { background: #a51c1c; } .cand-photo.d { background: #0a3a7a; }
    .cand-photo.winner-photo { border-color: rgba(255,215,150,0.8); box-shadow: 0 0 15px rgba(255,215,150,0.3); }
    .cand-name { font-size: 1.1rem; font-weight: 700; color: white; margin-bottom: 0.3rem; }
    .cand-desc { font-size: 0.75rem; color: rgba(255,255,255,0.5); margin-bottom: 0.6rem; line-height: 1.3; }
    .cand-score { font-size: 2rem; font-weight: 800; margin-bottom: 0.3rem; } .cand-score.r { color: #ff9e8f; } .cand-score.d { color: #8fc1ff; }
    .cand-badge { display: inline-block; padding: 3px 10px; font-size: 0.7rem; font-weight: 700; text-transform: uppercase; letter-spacing: 0.05em; }
    .badge-winner { background: rgba(255,215,0,0.2); color: #ffd700; border: 1px solid #ffd700; }
    .badge-runoff { background: rgba(255,152,0,0.2); color: #ff9800; border: 1px solid #ff9800; }
    .badge-eliminated { background: rgba(158,158,158,0.2); color: #9e9e9e; border: 1px solid #9e9e9e; }
    .badge-qualified { background: rgba(76,175,80,0.2); color: #4caf50; border: 1px solid #4caf50; }

    /* TABLEAUX PRIMAIRES */
    .primary-table { width: 100%; border-collapse: collapse; color: white; font-size: 0.85rem; margin-bottom: 1.5rem; }
    .primary-table th { text-align: center; padding: 10px 8px; background: rgba(0,0,0,0.4); font-weight: 600; text-transform: uppercase; letter-spacing: 0.5px; font-size: 0.75rem; border-bottom: 2px solid rgba(255,255,255,0.15); }
    .primary-table td { text-align: center; padding: 8px; border-bottom: 1px solid rgba(255,255,255,0.06); }
    .primary-table .winner-col { font-weight: 700; }
    .primary-table .r-col { color: #ff9e8f; } .primary-table .d-col { color: #8fc1ff; }
    .primary-table .highlight-row { background: rgba(0,0,0,0.3); font-weight: 600; }
    .primary-note { color: rgba(255,255,255,0.5); font-size: 0.8rem; text-align: center; margin-top: 1rem; font-style: italic; }

    /* GRAPHIQUE */
    .chart-container { position: relative; width: 100%; height: 280px; margin: 1rem 0; }
    canvas { display: block; width: 100%; height: 100%; background: rgba(10,10,15,0.3); border: 1px solid rgba(255,255,255,0.1); cursor: crosshair; }
    .chart-tooltip { position: absolute; background: rgba(20,20,30,0.95); color: white; padding: 8px 12px; border: 1px solid rgba(255,255,255,0.25); font-size: 12px; font-weight: 600; pointer-events: none; box-shadow: 0 6px 20px rgba(0,0,0,0.6); z-index: 100; text-align: center; line-height: 1.4; white-space: nowrap; }
    .chart-legend { display: flex; justify-content: center; gap: 1.5rem; margin-top: 0.5rem; color: rgba(255,255,255,0.7); flex-wrap: wrap; font-size: 0.85rem; }
    .legend-dot { width: 10px; height: 10px; display: inline-block; margin-right: 5px; } .legend-dot.r { background: #e53935; } .legend-dot.d { background: #1e88e5; }

    .no-data { text-align: center; color: rgba(255,255,255,0.4); padding: 3rem; font-style: italic; }

    @media (max-width: 750px) { 
      .main-header { padding: 1rem; } 
      .card-title { font-size: 1.3rem; } 
      .primary-grid { grid-template-columns: 1fr; }
    }
  </style>
</head>
<body>

<header class="main-header">
  <div class="main-title">UNITED STATES</div>
  <div class="main-subtitle">Midterm Elections 2026</div>
</header>

<div class="main-content">

  <!-- ONGLETS CATÉGORIE -->
  <div class="category-tabs">
    <div class="cat-tab" data-cat="house">🏛️ House</div>
    <div class="cat-tab active" data-cat="senate">🗳️ Senate</div>
    <div class="cat-tab" data-cat="governor">🏢 Gubernatorial</div>
  </div>

  <!-- ==================== HOUSE ==================== -->
  <div class="cat-panel" id="cat-house">
    <div class="race-list" id="house-races">
      <div class="race-item" data-race="house-wa3">
        <div class="race-info"><h3>Washington · 3e District</h3><p>Leslie Lewallen (R) vs Marie Gluesenkamp Perez (D) *</p></div>
        <div class="race-rating-badge badge-tossup">Tossup</div>
      </div>
    </div>
  </div>

  <!-- ==================== SENATE ==================== -->
  <div class="cat-panel active" id="cat-senate">
    <div class="race-list" id="senate-races">
      <div class="race-item active" data-race="senate-tx">
        <div class="race-info"><h3>Texas · Sénat</h3><p>John Cornyn (R) * vs James Talarico (D)</p></div>
        <div class="race-rating-badge badge-lean-r">Lean R</div>
      </div>
    </div>
  </div>

  <!-- ==================== GUBERNATORIAL ==================== -->
  <div class="cat-panel" id="cat-governor">
    <div class="race-list" id="governor-races">
      <div class="race-item" style="cursor:default; opacity:0.5;">
        <div class="race-info"><h3>Courses à venir</h3><p>Données bientôt disponibles</p></div>
      </div>
    </div>
  </div>

  <!-- ==================== PANNEAUX DE DÉTAILS ==================== -->
  <div id="detail-container"></div>

</div>

<script>
  (function() {
    // Données des courses (enrichies)
    const racesData = {
      'senate-tx': {
        title: 'Sénat · Texas',
        rating: 'Lean R',
        ratingClass: 'badge-lean-r',
        state: 'Texas',
        candidates: [
          { name: 'John Cornyn', party: 'R', initials: 'JC', percent: 48, desc: 'Sénateur sortant · Élu depuis 2002' },
          { name: 'James Talarico', party: 'D', initials: 'JT', percent: 46, desc: 'Représentant d\'État · Ancien enseignant' }
        ],
        projections: { rSafe: 20, rLikely: 25, rLean: 15, tossup: 20, dLean: 12, dLikely: 8 },
        seatsInfo: 'Sièges projetés : 51 R - 47 D · Fourchette : +2R à +8R',
        marginError: '±3.2%',
        sample: '2 814 LV',
        pollDates: '12-15 Sep 2026',
        polls: [
          { date: 'Jan', rep: 47, dem: 44 }, { date: 'Fév', rep: 44, dem: 43 },
          { date: 'Mar', rep: 44, dem: 43 }, { date: 'Avr', rep: 45, dem: 44 },
          { date: 'Mai', rep: 47, dem: 42 }, { date: 'Jun', rep: 46, dem: 44 },
          { date: 'Jul', rep: 44, dem: 44 }, { date: 'Aoû', rep: 47, dem: 45 },
          { date: 'Sep', rep: 48, dem: 46 }
        ],
        primaryDate: '4 mars 2026',
        primaries: {
          rep: {
            title: 'Primaire Républicaine',
            note: 'Second tour républicain prévu le 26 mai 2026 entre John Cornyn et Ken Paxton. Le vainqueur affrontera James Talarico (D) en novembre.',
            candidates: [
              { name: 'Ken Paxton', initials: 'KP', desc: 'Procureur général du Texas · Soutenu par Trump', score: '48.8%', class: 'r', badge: 'badge-runoff', badgeText: 'Second tour', isWinner: true },
              { name: 'John Cornyn', initials: 'JC', desc: 'Sénateur sortant · Élu depuis 2002', score: '41.3%', class: 'r', badge: 'badge-runoff', badgeText: 'Second tour', isWinner: true },
              { name: 'Wesley Hunt', initials: 'WH', desc: 'Représentant (TX-38) · Vétéran', score: '~10%', class: 'r', badge: 'badge-eliminated', badgeText: 'Éliminé', isWinner: false }
            ],
            polls: [
              { institute: 'Quantus Insights', date: 'Mar 2026', values: ['48.8%', '41.3%', '~10%'] },
              { institute: 'Emerson College', date: 'Fév 2026', values: ['46%', '42%', '12%'] },
              { institute: 'YouGov/Texas', date: 'Jan 2026', values: ['44%', '43%', '13%'] }
            ]
          },
          dem: {
            title: 'Primaire Démocrate',
            note: 'James Talarico a remporté l\'investiture démocrate avec 53.1% des voix. Il affrontera le vainqueur de la primaire républicaine en novembre 2026.',
            candidates: [
              { name: 'James Talarico', initials: 'JT', desc: 'Représentant d\'État · Ancien enseignant', score: '53.1%', class: 'd', badge: 'badge-winner', badgeText: '🏆 Vainqueur', isWinner: true },
              { name: 'Jasmine Crockett', initials: 'JC', desc: 'Représentante (TX-30) · Ancienne avocate', score: '45.6%', class: 'd', badge: 'badge-eliminated', badgeText: 'Battue', isWinner: false },
              { name: 'Ahmad Hassan', initials: 'AH', desc: 'Avocat · Militant communautaire', score: '1.3%', class: 'd', badge: 'badge-eliminated', badgeText: 'Battu', isWinner: false }
            ],
            polls: [
              { institute: 'Résultat final', date: '4 Mar 2026', values: ['53.1%', '45.6%', '1.3%'] },
              { institute: 'Emerson College', date: 'Fév 2026', values: ['52%', '47%', '1%'] },
              { institute: 'YouGov/Texas', date: 'Jan 2026', values: ['50%', '46%', '4%'] }
            ]
          }
        }
      },
      'house-wa3': {
        title: 'House · Washington 3rd District',
        rating: 'Tossup',
        ratingClass: 'badge-tossup',
        state: 'Washington',
        candidates: [
          { name: 'Leslie Lewallen', party: 'R', initials: 'LL', percent: 48, desc: 'Ancienne procureure · Soutenue par NRCC' },
          { name: 'Marie Gluesenkamp Perez', party: 'D', initials: 'MP', percent: 46, desc: 'Représentante sortante · Élue en 2022' }
        ],
        projections: { rSafe: 10, rLikely: 15, rLean: 18, tossup: 30, dLean: 17, dLikely: 10 },
        seatsInfo: 'Sièges projetés : 218 R - 217 D · Fourchette : +5D à +15R',
        marginError: '±3.5%',
        sample: '1 100 LV',
        pollDates: '12-15 Sep 2026',
        polls: [
          { date: 'Jan', rep: 47, dem: 45 }, { date: 'Fév', rep: 46, dem: 44 },
          { date: 'Mar', rep: 45, dem: 46 }, { date: 'Avr', rep: 44, dem: 47 },
          { date: 'Mai', rep: 48, dem: 44 }, { date: 'Jun', rep: 47, dem: 45 },
          { date: 'Jul', rep: 45, dem: 47 }, { date: 'Aoû', rep: 48, dem: 45 },
          { date: 'Sep', rep: 48, dem: 46 }
        ],
        primaryDate: '5 août 2025',
        primaries: {
          rep: {
            title: 'Primaire Républicaine (Top 2)',
            note: 'Washington utilise un système de primaire unique ("Top 2"). Les deux candidats ayant reçu le plus de voix, tous partis confondus, s\'affrontent en novembre. Leslie Lewallen est arrivée en tête avec 52%.',
            candidates: [
              { name: 'Leslie Lewallen', initials: 'LL', desc: 'Ancienne procureure · Soutenue par NRCC', score: '52%', class: 'r', badge: 'badge-qualified', badgeText: 'Qualifiée', isWinner: true },
              { name: 'Joe Kent', initials: 'JK', desc: 'Ancien militaire · Candidat en 2022', score: '48%', class: 'r', badge: 'badge-eliminated', badgeText: 'Battu', isWinner: false }
            ],
            polls: [
              { institute: 'Résultat primaire', date: '5 Aoû 2025', values: ['52%', '48%'] },
              { institute: 'SurveyUSA', date: 'Juil 2025', values: ['50%', '46%'] },
              { institute: 'Public Policy', date: 'Jun 2025', values: ['48%', '47%'] }
            ]
          },
          dem: {
            title: 'Primaire Démocrate (Top 2)',
            note: 'Marie Gluesenkamp Perez s\'est qualifiée pour l\'élection générale avec 46% des voix. Elle est la seule démocrate à avoir franchi le seuil des 5%.',
            candidates: [
              { name: 'Marie Gluesenkamp Perez', initials: 'MP', desc: 'Représentante sortante · Élue en 2022', score: '46%', class: 'd', badge: 'badge-qualified', badgeText: 'Qualifiée', isWinner: true }
            ],
            polls: [
              { institute: 'Résultat primaire', date: '5 Aoû 2025', values: ['46%'] },
              { institute: 'SurveyUSA', date: 'Juil 2025', values: ['48%'] },
              { institute: 'Public Policy', date: 'Jun 2025', values: ['50%'] }
            ]
          }
        }
      }
    };

    // Gestion des onglets de catégorie
    document.querySelectorAll('.cat-tab').forEach(tab => {
      tab.addEventListener('click', function() {
        document.querySelectorAll('.cat-tab').forEach(t => t.classList.remove('active'));
        this.classList.add('active');
        document.querySelectorAll('.cat-panel').forEach(p => p.classList.remove('active'));
        const catId = 'cat-' + this.dataset.cat;
        document.getElementById(catId).classList.add('active');
        
        // Activer la première course de la catégorie
        const firstRace = document.querySelector('#' + catId + ' .race-item[data-race]');
        if (firstRace) {
          document.querySelectorAll('.race-item').forEach(i => i.classList.remove('active'));
          firstRace.classList.add('active');
          showRaceDetail(firstRace.dataset.race);
        } else {
          document.getElementById('detail-container').innerHTML = '<div class="no-data">Sélectionnez une course pour voir les détails</div>';
        }
      });
    });

    // Gestion du clic sur une course
    document.querySelectorAll('.race-item[data-race]').forEach(item => {
      item.addEventListener('click', function() {
        document.querySelectorAll('.race-item').forEach(i => i.classList.remove('active'));
        this.classList.add('active');
        showRaceDetail(this.dataset.race);
      });
    });

    function showRaceDetail(raceId) {
      const data = racesData[raceId];
      if (!data) return;
      
      const container = document.getElementById('detail-container');
      const lastP = data.polls[data.polls.length-1];
      
      container.innerHTML = `
        <!-- CARTE ÉLECTION GÉNÉRALE -->
        <div class="card">
          <div class="card-header">
            <div class="card-title">${data.title}</div>
            <div class="race-rating-badge ${data.ratingClass}">${data.rating}</div>
          </div>
          
          ${data.candidates.map(c => `
            <div class="candidate-row">
              <div class="candidate-label">
                <span class="party-name ${c.party==='R'?'rep':'dem'}">${c.name} (${c.party})</span>
                <span class="party-percent ${c.party==='R'?'rep':'dem'}">${c.percent}%</span>
              </div>
              <div style="color:rgba(255,255,255,0.45); font-size:0.8rem; margin-bottom:0.4rem;">${c.desc}</div>
              <div class="bar-wrapper">
                <div class="bar-fill ${c.party==='R'?'rep-fill':'dem-fill'}" style="width:${c.percent}%">${c.percent}%</div>
              </div>
            </div>
          `).join('')}
          
          <div class="poll-footer">
            <span>📊 Marge d'erreur ${data.marginError}</span>
            <span>👥 ${data.sample} · ${data.pollDates}</span>
          </div>
          
          <!-- Projections -->
          <div style="margin-top:1.5rem;">
            <h4 style="color:rgba(255,255,255,0.6); font-size:0.9rem; text-transform:uppercase; letter-spacing:0.1em;">Probabilités de victoire</h4>
            <div class="projections-bar">
              <div class="proj-r-safe" style="width:${data.projections.rSafe}%"></div>
              <div class="proj-r-likely" style="width:${data.projections.rLikely}%"></div>
              <div class="proj-r-lean" style="width:${data.projections.rLean}%"></div>
              <div class="proj-tossup" style="width:${data.projections.tossup}%"></div>
              <div class="proj-d-lean" style="width:${data.projections.dLean}%"></div>
              <div class="proj-d-likely" style="width:${data.projections.dLikely}%"></div>
            </div>
            <div class="projections-legend">
              <span>R+10+</span><span>R+5-9</span><span>R+1-4</span><span>Tossup</span><span>D+1-4</span><span>D+5+</span>
            </div>
            <div class="seats-projection">${data.seatsInfo}</div>
          </div>
          
          <!-- Graphique -->
          <div style="margin-top:1.5rem;">
            <h4 style="color:rgba(255,255,255,0.6); font-size:0.9rem; text-transform:uppercase; letter-spacing:0.1em;">📈 Évolution des sondages</h4>
            <div class="chart-container">
              <canvas id="detailChart" width="800" height="280"></canvas>
              <div class="chart-tooltip" id="chartTooltip" style="opacity:0;"></div>
            </div>
            <div class="chart-legend">
              <span><span class="legend-dot r"></span> ${data.candidates[0].name.split(' ').pop()} (R)</span>
              <span><span class="legend-dot d"></span> ${data.candidates[1].name.split(' ').pop()} (D)</span>
              <span style="opacity:0.6;">— Moyenne mobile (3 sondages)</span>
            </div>
          </div>
        </div>
        
        <!-- CARTE PRIMAIRES -->
        <div class="card">
          <div class="card-header">
            <div class="card-title">Primaires</div>
            <div class="primary-date">📅 ${data.primaryDate}</div>
          </div>
          
          <div class="primary-tabs">
            <div class="prim-tab r-active active" data-prim="rep">Primaire Républicaine</div>
            <div class="prim-tab d-active" data-prim="dem">Primaire Démocrate</div>
          </div>
          
          <!-- Panel Républicain -->
          <div class="prim-panel active" id="panel-rep">
            <div class="primary-grid">
              ${data.primaries.rep.candidates.map(c => `
                <div class="candidate-card ${c.isWinner ? 'winner' : ''}">
                  <div class="cand-photo ${c.class} ${c.isWinner ? 'winner-photo' : ''}">${c.initials}</div>
                  <div class="cand-name">${c.name}</div>
                  <div class="cand-desc">${c.desc}</div>
                  <div class="cand-score ${c.class}">${c.score}</div>
                  <div class="cand-badge ${c.badge}">${c.badgeText}</div>
                </div>
              `).join('')}
            </div>
            
            ${data.primaries.rep.polls ? `
            <table class="primary-table">
              <thead>
                <tr>
                  <th>Institut</th>
                  <th>Date</th>
                  ${data.primaries.rep.candidates.map(c => `<th>${c.name.split(' ').pop()}</th>`).join('')}
                </tr>
              </thead>
              <tbody>
                ${data.primaries.rep.polls.map((p, i) => `
                  <tr class="${i === 0 ? 'highlight-row' : ''}">
                    <td>${p.institute}</td>
                    <td>${p.date}</td>
                    ${p.values.map(v => `<td class="${data.primaries.rep.candidates[0].class === 'r' ? 'r-col' : 'd-col'}">${v}</td>`).join('')}
                  </tr>
                `).join('')}
              </tbody>
            </table>
            ` : ''}
            
            <div class="primary-note">${data.primaries.rep.note}</div>
          </div>
          
          <!-- Panel Démocrate -->
          <div class="prim-panel" id="panel-dem">
            <div class="primary-grid">
              ${data.primaries.dem.candidates.map(c => `
                <div class="candidate-card ${c.isWinner ? 'winner' : ''}">
                  <div class="cand-photo ${c.class} ${c.isWinner ? 'winner-photo' : ''}">${c.initials}</div>
                  <div class="cand-name">${c.name}</div>
                  <div class="cand-desc">${c.desc}</div>
                  <div class="cand-score ${c.class}">${c.score}</div>
                  <div class="cand-badge ${c.badge}">${c.badgeText}</div>
                </div>
              `).join('')}
            </div>
            
            ${data.primaries.dem.polls ? `
            <table class="primary-table">
              <thead>
                <tr>
                  <th>Institut</th>
                  <th>Date</th>
                  ${data.primaries.dem.candidates.map(c => `<th>${c.name.split(' ').pop()}</th>`).join('')}
                </tr>
              </thead>
              <tbody>
                ${data.primaries.dem.polls.map((p, i) => `
                  <tr class="${i === 0 ? 'highlight-row' : ''}">
                    <td>${p.institute}</td>
                    <td>${p.date}</td>
                    ${p.values.map(v => `<td class="${data.primaries.dem.candidates[0].class === 'r' ? 'r-col' : 'd-col'}">${v}</td>`).join('')}
                  </tr>
                `).join('')}
              </tbody>
            </table>
            ` : ''}
            
            <div class="primary-note">${data.primaries.dem.note}</div>
          </div>
        </div>
      `;
      
      // Gestion des onglets primaires
      setTimeout(() => {
        container.querySelectorAll('.prim-tab').forEach(tab => {
          tab.addEventListener('click', function() {
            const target = this.dataset.prim;
            container.querySelectorAll('.prim-tab').forEach(t => {
              t.classList.remove('active', 'r-active', 'd-active');
            });
            this.classList.add('active');
            if (target === 'rep') this.classList.add('r-active');
            if (target === 'dem') this.classList.add('d-active');
            
            container.querySelectorAll('.prim-panel').forEach(p => p.classList.remove('active'));
            container.querySelector('#panel-' + target).classList.add('active');
          });
        });
        
        // Dessiner le graphique
        drawDetailChart(data.polls, data.candidates);
      }, 100);
    }

    function drawDetailChart(polls, candidates) {
      const canvas = document.getElementById('detailChart');
      if (!canvas) return;
      const ctx = canvas.getContext('2d');
      const tooltip = document.getElementById('chartTooltip');
      
      const repAvg = [], demAvg = [];
      for (let i = 0; i < polls.length; i++) {
        let sR=0, sD=0, c=0;
        for (let j=Math.max(0,i-2); j<=i; j++) { sR+=polls[j].rep; sD+=polls[j].dem; c++; }
        repAvg.push(Math.round((sR/c)*10)/10);
        demAvg.push(Math.round((sD/c)*10)/10);
      }
      
      const pad={top:25, right:30, bottom:35, left:40}, minY=30, maxY=55;
      let points=[];
      
      function draw() {
        const w=canvas.width, h=canvas.height, cW=w-pad.left-pad.right, cH=h-pad.top-pad.bottom;
        ctx.clearRect(0,0,w,h);
        ctx.fillStyle='rgba(10,10,18,0.5)'; ctx.fillRect(pad.left,pad.top,cW,cH);
        
        const gX=i=>pad.left+(i/(polls.length-1))*cW;
        const gY=v=>pad.top+cH-((v-minY)/(maxY-minY))*cH;
        
        ctx.strokeStyle='rgba(255,255,255,0.06)'; ctx.lineWidth=0.6;
        for(let i=minY;i<=maxY;i+=5){const y=gY(i);ctx.beginPath();ctx.moveTo(pad.left,y);ctx.lineTo(pad.left+cW,y);ctx.stroke();ctx.fillStyle='rgba(255,255,255,0.4)';ctx.font='10px Segoe UI';ctx.textAlign='right';ctx.fillText(i+'%',pad.left-6,y);}
        
        ctx.fillStyle='rgba(255,255,255,0.5)'; ctx.font='10px Segoe UI'; ctx.textAlign='center';
        polls.forEach((p,i)=>ctx.fillText(p.date,gX(i),pad.top+cH+12));
        
        [{d:repAvg,c:'#ff8a7a'},{d:demAvg,c:'#8fc1ff'}].forEach(l=>{
          ctx.beginPath();ctx.moveTo(gX(0),gY(l.d[0]));
          for(let i=1;i<l.d.length;i++){const xc=gX(i),yc=gY(l.d[i]),xp=gX(i-1),yp=gY(l.d[i-1]);ctx.bezierCurveTo(xp+(xc-xp)*0.5,yp,xc-(xc-xp)*0.5,yc,xc,yc);}
          ctx.strokeStyle=l.c;ctx.lineWidth=2.5;ctx.stroke();
        });
        
        points=[];
        polls.forEach((p,i)=>{
          [{v:p.rep,t:'r',c:'rgba(180,40,40,0.5)'},{v:p.dem,t:'d',c:'rgba(30,80,180,0.5)'}].forEach(pt=>{
            const x=gX(i),y=gY(pt.v);
            points.push({x,y,type:pt.t,value:pt.v,date:p.date});
            ctx.beginPath();ctx.arc(x,y,6,0,2*Math.PI);ctx.fillStyle=pt.c;ctx.fill();ctx.strokeStyle='rgba(255,255,255,0.2)';ctx.stroke();
          });
        });
      }
      draw();
      
      canvas.onmousemove = function(e) {
        const rect=canvas.getBoundingClientRect(), sX=canvas.width/rect.width, sY=canvas.height/rect.height;
        const mx=(e.clientX-rect.left)*sX, my=(e.clientY-rect.top)*sY;
        let cl=null,md=20;
        points.forEach(p=>{const d=Math.hypot(mx-p.x,my-p.y);if(d<md){md=d;cl=p;}});
        if(cl){
          const name = cl.type==='r' ? candidates[0].name : candidates[1].name;
          tooltip.innerHTML='<strong>'+name+'</strong><br><span style="color:'+(cl.type==='r'?'#ff9e8f':'#8fc1ff')+';font-size:15px;">'+cl.value+'%</span><br><span style="opacity:0.6;">'+cl.date+' 2026</span>';
          tooltip.style.left=Math.max(5,Math.min(cl.x/sX-55,rect.width-110))+'px';
          tooltip.style.top=Math.max(5,cl.y/sY-55)+'px';
          tooltip.style.opacity='1';
        } else { tooltip.style.opacity='0'; }
      };
      canvas.onmouseleave = () => tooltip.style.opacity='0';
    }

    // Afficher Texas par défaut (premier chargement)
    showRaceDetail('senate-tx');
  })();
</script>

<div style="height:20px;"></div>
</body>
</html>
