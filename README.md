<!DOCTYPE html>
<html lang="bs">
<head>
<meta charset="UTF-8">
<meta name="apple-mobile-web-app-capable" content="yes">
<meta name="apple-mobile-web-app-status-bar-style" content="black-translucent">
<meta name="apple-mobile-web-app-title" content="Life Audit">
<meta name="viewport" content="width=device-width, initial-scale=1, viewport-fit=cover">
<meta name="theme-color" content="#8B4A42">
<link rel="manifest" href="manifest.json">
<link rel="apple-touch-icon" href="icon.svg">
<title>Moj Life Audit</title>
<link href="https://fonts.googleapis.com/css2?family=Cormorant+Garamond:ital,wght@0,300;0,400;0,600;1,300;1,400&family=DM+Sans:wght@300;400;500&display=swap" rel="stylesheet">
<style>
  :root {
    --cream: #F5F0E8;
    --warm-white: #FAF7F2;
    --dark: #2C2420;
    --muted: #8A7B72;
    --accent: #8B4A42;
    --accent-light: #C4847B;
    --accent-pale: #F0E0DC;
    --border: #E5DDD5;
    --success: #5A7A5A;
    --safe-top: env(safe-area-inset-top, 0px);
    --safe-bottom: env(safe-area-inset-bottom, 0px);
  }

  * { box-sizing: border-box; margin: 0; padding: 0; -webkit-tap-highlight-color: transparent; }

  html, body {
    height: 100%;
    overflow: hidden;
    background: var(--cream);
    font-family: 'DM Sans', sans-serif;
    color: var(--dark);
  }

  /* APP SHELL */
  #app {
    display: flex;
    flex-direction: column;
    height: 100dvh;
    padding-top: var(--safe-top);
  }

  /* HEADER */
  #header {
    background: var(--warm-white);
    border-bottom: 1px solid var(--border);
    padding: 14px 20px 12px;
    flex-shrink: 0;
    text-align: center;
  }

  #header .eyebrow {
    font-size: 9px;
    letter-spacing: 0.22em;
    text-transform: uppercase;
    color: var(--muted);
    font-weight: 500;
    margin-bottom: 3px;
  }

  #header h1 {
    font-family: 'Cormorant Garamond', serif;
    font-size: 24px;
    font-weight: 300;
    letter-spacing: 0.02em;
    line-height: 1;
  }

  #header h1 em { font-style: italic; color: var(--accent); }

  /* SCROLL CONTENT */
  #content {
    flex: 1;
    overflow-y: auto;
    -webkit-overflow-scrolling: touch;
    padding: 16px 16px 8px;
  }

  /* VIEWS */
  .view { display: none; }
  .view.active { display: block; }

  /* TAB BAR */
  #tabbar {
    background: var(--warm-white);
    border-top: 1px solid var(--border);
    display: flex;
    padding-bottom: var(--safe-bottom);
    flex-shrink: 0;
  }

  .tab {
    flex: 1;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    padding: 8px 4px 6px;
    border: none;
    background: none;
    cursor: pointer;
    font-family: 'DM Sans', sans-serif;
    color: var(--muted);
    font-size: 9px;
    font-weight: 500;
    letter-spacing: 0.04em;
    gap: 3px;
    transition: color 0.15s;
  }

  .tab.active { color: var(--accent); }
  .tab .tab-icon { font-size: 20px; line-height: 1; }

  /* DAILY QUOTE */
  .quote-card {
    background: var(--accent);
    border-radius: 14px;
    padding: 16px 18px;
    margin-bottom: 16px;
    color: white;
  }

  .quote-card .ql { font-size: 9px; letter-spacing: 0.18em; text-transform: uppercase; opacity: 0.65; margin-bottom: 7px; }
  .quote-card .qt { font-family: 'Cormorant Garamond', serif; font-size: 17px; font-style: italic; font-weight: 300; line-height: 1.55; }

  /* OVERVIEW GRID */
  .ov-grid { display: grid; grid-template-columns: 1fr 1fr; gap: 10px; margin-bottom: 16px; }

  .ov-card {
    background: var(--warm-white);
    border: 1px solid var(--border);
    border-radius: 12px;
    padding: 14px;
    cursor: pointer;
    transition: border-color 0.2s;
    active: border-color var(--accent-light);
  }

  .ov-card:active { border-color: var(--accent-light); background: var(--accent-pale); }
  .ov-icon { font-size: 22px; margin-bottom: 8px; }
  .ov-name { font-size: 9px; letter-spacing: 0.1em; text-transform: uppercase; color: var(--muted); font-weight: 500; margin-bottom: 3px; }
  .ov-count { font-family: 'Cormorant Garamond', serif; font-size: 22px; font-weight: 300; }
  .ov-count span { font-size: 12px; color: var(--muted); }
  .ov-sub { font-size: 10px; color: var(--muted); margin-top: 1px; }
  .ov-bar { height: 3px; background: var(--border); border-radius: 2px; margin-top: 10px; overflow: hidden; }
  .ov-fill { height: 100%; background: var(--accent); border-radius: 2px; transition: width 0.4s; }

  /* SECTION LABEL */
  .slabel {
    font-size: 9px; letter-spacing: 0.16em; text-transform: uppercase;
    color: var(--muted); font-weight: 500; margin: 0 0 9px 2px;
  }

  /* AREA HEADER */
  .area-hdr {
    background: var(--warm-white);
    border: 1px solid var(--border);
    border-radius: 12px;
    padding: 16px;
    margin-bottom: 14px;
    display: flex;
    align-items: flex-start;
    gap: 12px;
  }

  .area-hdr-icon {
    width: 42px; height: 42px;
    background: var(--accent-pale);
    border-radius: 50%;
    display: flex; align-items: center; justify-content: center;
    font-size: 20px; flex-shrink: 0;
  }

  .area-hdr h2 { font-family: 'Cormorant Garamond', serif; font-size: 20px; font-weight: 400; margin-bottom: 3px; }
  .area-hdr p { font-size: 11px; color: var(--muted); line-height: 1.5; }

  /* PROGRESS */
  .prog-wrap { margin-bottom: 14px; }
  .prog-row { display: flex; justify-content: space-between; font-size: 11px; color: var(--muted); margin-bottom: 5px; }
  .prog-bg { background: var(--border); border-radius: 4px; height: 5px; overflow: hidden; }
  .prog-fill { height: 100%; background: var(--accent); border-radius: 4px; transition: width 0.4s; }

  /* REMINDER CARDS */
  .rem-list { display: flex; flex-direction: column; gap: 8px; margin-bottom: 16px; }

  .rem-card {
    background: var(--warm-white);
    border: 1px solid var(--border);
    border-radius: 10px;
    padding: 13px 14px;
    display: flex;
    align-items: center;
    gap: 11px;
    cursor: pointer;
    transition: border-color 0.15s;
  }

  .rem-card:active { border-color: var(--accent-light); }
  .rem-card.done { opacity: 0.48; }
  .rem-card.done .rem-text { text-decoration: line-through; }

  .check {
    width: 22px; height: 22px;
    border: 1.5px solid var(--border);
    border-radius: 50%;
    flex-shrink: 0;
    display: flex; align-items: center; justify-content: center;
    background: white;
    transition: all 0.2s;
  }

  .rem-card.done .check { background: var(--success); border-color: var(--success); }
  .check-svg { display: none; }
  .rem-card.done .check-svg { display: block; }

  .rem-body { flex: 1; min-width: 0; }
  .rem-text { font-size: 13px; line-height: 1.4; }
  .rem-meta { font-size: 10px; color: var(--muted); margin-top: 2px; }

  .freq-badge {
    font-size: 9px;
    background: var(--accent-pale);
    color: var(--accent);
    border-radius: 20px;
    padding: 3px 8px;
    font-weight: 500;
    flex-shrink: 0;
    white-space: nowrap;
  }

  /* ADD FORM */
  .add-form {
    background: var(--warm-white);
    border: 1px dashed var(--border);
    border-radius: 10px;
    padding: 13px 14px;
    margin-bottom: 20px;
  }

  .add-form input, .add-form select {
    width: 100%;
    border: 1px solid var(--border);
    border-radius: 8px;
    padding: 10px 12px;
    font-family: 'DM Sans', sans-serif;
    font-size: 14px;
    background: var(--cream);
    color: var(--dark);
    margin-bottom: 8px;
    outline: none;
    -webkit-appearance: none;
  }

  .add-form input:focus, .add-form select:focus { border-color: var(--accent-light); }

  .add-row { display: flex; gap: 8px; }
  .add-row select { margin-bottom: 0; flex: 1; }

  .btn-add {
    background: var(--accent);
    color: white;
    border: none;
    border-radius: 8px;
    padding: 10px 16px;
    font-family: 'DM Sans', sans-serif;
    font-size: 13px;
    font-weight: 500;
    cursor: pointer;
    flex-shrink: 0;
    transition: background 0.15s;
  }

  .btn-add:active { background: var(--accent-light); }

  /* INSTALL BANNER */
  #install-banner {
    background: var(--dark);
    color: white;
    padding: 12px 16px;
    font-size: 12px;
    line-height: 1.5;
    display: flex;
    align-items: center;
    gap: 10px;
    flex-shrink: 0;
  }

  #install-banner .ib-icon { font-size: 18px; flex-shrink: 0; }
  #install-banner .ib-text { flex: 1; }
  #install-banner .ib-text strong { display: block; font-size: 13px; margin-bottom: 1px; }
  #install-banner .ib-close {
    background: none; border: none; color: white; opacity: 0.6;
    font-size: 18px; cursor: pointer; padding: 4px; flex-shrink: 0;
  }

  /* TOAST */
  #toast {
    position: fixed; bottom: calc(70px + var(--safe-bottom)); left: 50%;
    transform: translateX(-50%) translateY(10px);
    background: var(--dark); color: white;
    padding: 9px 18px; border-radius: 30px;
    font-size: 12px; white-space: nowrap;
    opacity: 0; pointer-events: none;
    transition: opacity 0.25s, transform 0.25s;
    z-index: 999;
  }

  #toast.show { opacity: 1; transform: translateX(-50%) translateY(0); }

  /* RESET BTN */
  .reset-btn {
    width: 100%;
    background: none;
    border: 1px solid var(--border);
    border-radius: 8px;
    padding: 11px;
    font-family: 'DM Sans', sans-serif;
    font-size: 12px;
    color: var(--muted);
    cursor: pointer;
    margin-top: 8px;
  }
</style>
</head>
<body>

<div id="app">

  <!-- INSTALL BANNER -->
  <div id="install-banner">
    <div class="ib-icon">📱</div>
    <div class="ib-text">
      <strong>Dodaj na Home Screen</strong>
      Safari → Dijeli → "Dodaj na početni ekran"
    </div>
    <button class="ib-close" onclick="document.getElementById('install-banner').style.display='none'">×</button>
  </div>

  <!-- HEADER -->
  <div id="header">
    <div class="eyebrow">Tvoj personalni sistem</div>
    <h1>Moj <em>Life Audit</em></h1>
  </div>

  <!-- CONTENT -->
  <div id="content">

    <!-- OVERVIEW -->
    <div class="view active" id="view-home">
      <div class="quote-card">
        <div class="ql">Misao dana</div>
        <div class="qt" id="daily-quote"></div>
      </div>
      <p class="slabel">Tvoje oblasti</p>
      <div class="ov-grid" id="ov-grid"></div>
    </div>

    <!-- ZDRAVLJE -->
    <div class="view" id="view-zdravlje">
      <div class="area-hdr">
        <div class="area-hdr-icon">💪</div>
        <div><h2>Zdravlje & Fitnes</h2><p>Tijelo je tvoj alat. Svaki dan mali korak prema energiji koja ti treba.</p></div>
      </div>
      <div id="prog-zdravlje" class="prog-wrap"></div>
      <p class="slabel">Podsjetnici</p>
      <div class="rem-list" id="list-zdravlje"></div>
      <div class="add-form">
        <input type="text" id="inp-zdravlje" placeholder="Novi podsjetnik...">
        <div class="add-row">
          <select id="frq-zdravlje"><option>Dnevno</option><option>Sedmično</option><option>Jednom</option></select>
          <button class="btn-add" onclick="addRem('zdravlje')">+ Dodaj</button>
        </div>
      </div>
    </div>

    <!-- MENTAL -->
    <div class="view" id="view-mental">
      <div class="area-hdr">
        <div class="area-hdr-icon">🧠</div>
        <div><h2>Mentalno zdravlje</h2><p>Um treba njegu jednako kao i tijelo. Mir se gradi svaki dan.</p></div>
      </div>
      <div id="prog-mental" class="prog-wrap"></div>
      <p class="slabel">Podsjetnici</p>
      <div class="rem-list" id="list-mental"></div>
      <div class="add-form">
        <input type="text" id="inp-mental" placeholder="Novi podsjetnik...">
        <div class="add-row">
          <select id="frq-mental"><option>Dnevno</option><option>Sedmično</option><option>Jednom</option></select>
          <button class="btn-add" onclick="addRem('mental')">+ Dodaj</button>
        </div>
      </div>
    </div>

    <!-- FINANSIJE -->
    <div class="view" id="view-finansije">
      <div class="area-hdr">
        <div class="area-hdr-icon">💼</div>
        <div><h2>Finansije & Karijera</h2><p>Svjesnost o novcu je moć. Jasni ciljevi vode do jasnih rezultata.</p></div>
      </div>
      <div id="prog-finansije" class="prog-wrap"></div>
      <p class="slabel">Podsjetnici</p>
      <div class="rem-list" id="list-finansije"></div>
      <div class="add-form">
        <input type="text" id="inp-finansije" placeholder="Novi podsjetnik...">
        <div class="add-row">
          <select id="frq-finansije"><option>Dnevno</option><option>Sedmično</option><option>Jednom</option></select>
          <button class="btn-add" onclick="addRem('finansije')">+ Dodaj</button>
        </div>
      </div>
    </div>

    <!-- ODNOSI -->
    <div class="view" id="view-odnosi">
      <div class="area-hdr">
        <div class="area-hdr-icon">🤝</div>
        <div><h2>Odnosi & Društvo</h2><p>Veze se grade pažnjom. Ko su tvoji ljudi? Jesi li prisutan?</p></div>
      </div>
      <div id="prog-odnosi" class="prog-wrap"></div>
      <p class="slabel">Podsjetnici</p>
      <div class="rem-list" id="list-odnosi"></div>
      <div class="add-form">
        <input type="text" id="inp-odnosi" placeholder="Novi podsjetnik...">
        <div class="add-row">
          <select id="frq-odnosi"><option>Dnevno</option><option>Sedmično</option><option>Jednom</option></select>
          <button class="btn-add" onclick="addRem('odnosi')">+ Dodaj</button>
        </div>
      </div>
    </div>

    <!-- RAST -->
    <div class="view" id="view-rast">
      <div class="area-hdr">
        <div class="area-hdr-icon">🌱</div>
        <div><h2>Lični rast & Vještine</h2><p>Rast nije slučajan. Čitaj, uči, razvijaj se svaki dan.</p></div>
      </div>
      <div id="prog-rast" class="prog-wrap"></div>
      <p class="slabel">Podsjetnici</p>
      <div class="rem-list" id="list-rast"></div>
      <div class="add-form">
        <input type="text" id="inp-rast" placeholder="Novi podsjetnik...">
        <div class="add-row">
          <select id="frq-rast"><option>Dnevno</option><option>Sedmično</option><option>Jednom</option></select>
          <button class="btn-add" onclick="addRem('rast')">+ Dodaj</button>
        </div>
      </div>
    </div>

    <!-- ZABAVA -->
    <div class="view" id="view-zabava">
      <div class="area-hdr">
        <div class="area-hdr-icon">✨</div>
        <div><h2>Zabava & Ispunjenje</h2><p>Šta te puni energijom? Radost je jednako važna kao i obaveze.</p></div>
      </div>
      <div id="prog-zabava" class="prog-wrap"></div>
      <p class="slabel">Podsjetnici</p>
      <div class="rem-list" id="list-zabava"></div>
      <div class="add-form">
        <input type="text" id="inp-zabava" placeholder="Novi podsjetnik...">
        <div class="add-row">
          <select id="frq-zabava"><option>Dnevno</option><option>Sedmično</option><option>Jednom</option></select>
          <button class="btn-add" onclick="addRem('zabava')">+ Dodaj</button>
        </div>
      </div>
      <button class="reset-btn" onclick="resetDay()">↺ Resetuj sve za novi dan</button>
    </div>

  </div><!-- /content -->

  <!-- TAB BAR -->
  <div id="tabbar">
    <button class="tab active" onclick="showTab('home')"><span class="tab-icon">🏠</span>Pregled</button>
    <button class="tab" onclick="showTab('zdravlje')"><span class="tab-icon">💪</span>Zdravlje</button>
    <button class="tab" onclick="showTab('mental')"><span class="tab-icon">🧠</span>Mental</button>
    <button class="tab" onclick="showTab('finansije')"><span class="tab-icon">💼</span>Finansije</button>
    <button class="tab" onclick="showTab('odnosi')"><span class="tab-icon">🤝</span>Odnosi</button>
    <button class="tab" onclick="showTab('rast')"><span class="tab-icon">🌱</span>Rast</button>
    <button class="tab" onclick="showTab('zabava')"><span class="tab-icon">✨</span>Zabava</button>
  </div>

</div><!-- /app -->

<div id="toast"></div>

<script>
// ── DATA ──────────────────────────────────────────
const AREAS = ['zdravlje','mental','finansije','odnosi','rast','zabava'];

const DEFAULTS = {
  zdravlje: [
    { text:'Popij 8 čaša vode', freq:'Dnevno' },
    { text:'30 minuta kretanja ili šetnje', freq:'Dnevno' },
    { text:'Idi spat do ponoći', freq:'Dnevno' },
    { text:'Pripremi zdravu hranu za sedmicu', freq:'Sedmično' },
  ],
  mental: [
    { text:'10 minuta meditacije ili disanja', freq:'Dnevno' },
    { text:'Napiši 3 stvari za koje si zahvalan/a', freq:'Dnevno' },
    { text:'Sat vremena bez ekrana', freq:'Dnevno' },
    { text:'Provjeri kako se osjećaš ove sedmice', freq:'Sedmično' },
  ],
  finansije: [
    { text:'Provjeri stanje na računu', freq:'Dnevno' },
    { text:'Zabilježi sve troškove dana', freq:'Dnevno' },
    { text:'Pregledaj sedmični budžet', freq:'Sedmično' },
    { text:'Radi na jednoj karijernоj vještini', freq:'Sedmično' },
  ],
  odnosi: [
    { text:'Javi se nekome koga dugo nisi čuo/la', freq:'Dnevno' },
    { text:'Reci nekome da ga cijeniš', freq:'Dnevno' },
    { text:'Provedi kvalitetno vrijeme s porodicom', freq:'Sedmično' },
    { text:'Organizuj izlazak ili susret', freq:'Sedmično' },
  ],
  rast: [
    { text:'Čitaj 20 stranica knjige', freq:'Dnevno' },
    { text:'Nauči nešto novo — podcast ili video', freq:'Dnevno' },
    { text:'Uradi jedan korak ka svom cilju', freq:'Dnevno' },
    { text:'Refleksija: šta sam naučio/la ove sedmice?', freq:'Sedmično' },
  ],
  zabava: [
    { text:'Posveti se hobiju barem 20 minuta', freq:'Dnevno' },
    { text:'Uradi nešto samo zbog zadovoljstva', freq:'Dnevno' },
    { text:'Planiraj nešto lijepo za vikend', freq:'Sedmično' },
    { text:'Odmori bez grižnje savjesti', freq:'Sedmično' },
  ],
};

const QUOTES = [
  'Revizija života nije o savršenstvu — nego o svjesnosti.',
  'Svaki dan je novi pokušaj.',
  'Mijenjaj polako. Promjene koje traju su tihe.',
  'Šta bi se promijenilo kad bi počeo/la pažljivije slušati sebe?',
  'Nema malih koraka — svaki korak je naprijed.',
  'Disciplina je forma ljubavi prema sebi.',
  'Prisustvo je rijetko. Prakticiranje prisustva je dar.',
];

let state = JSON.parse(localStorage.getItem('la_v2') || 'null');
if (!state) {
  state = {};
  AREAS.forEach(a => {
    state[a] = DEFAULTS[a].map((r, i) => ({ ...r, id: a+i, done: false }));
  });
  save();
}

function save() { localStorage.setItem('la_v2', JSON.stringify(state)); }

// ── NAVIGATION ────────────────────────────────────
let currentTab = 'home';

function showTab(tab) {
  document.querySelectorAll('.view').forEach(v => v.classList.remove('active'));
  document.querySelectorAll('.tab').forEach(b => b.classList.remove('active'));
  document.getElementById('view-' + tab).classList.add('active');
  document.querySelectorAll('.tab').forEach(b => {
    if (b.getAttribute('onclick').includes("'" + tab + "'")) b.classList.add('active');
  });
  document.getElementById('content').scrollTop = 0;
  currentTab = tab;
  if (tab === 'home') renderOverview();
  else renderArea(tab);
}

// ── RENDER OVERVIEW ───────────────────────────────
const META = {
  zdravlje:  { name:'Zdravlje',  emoji:'💪' },
  mental:    { name:'Mental',    emoji:'🧠' },
  finansije: { name:'Finansije', emoji:'💼' },
  odnosi:    { name:'Odnosi',    emoji:'🤝' },
  rast:      { name:'Rast',      emoji:'🌱' },
  zabava:    { name:'Zabava',    emoji:'✨' },
};

function renderOverview() {
  const grid = document.getElementById('ov-grid');
  grid.innerHTML = '';
  AREAS.forEach(a => {
    const items = state[a] || [];
    const done = items.filter(r => r.done).length;
    const pct = items.length ? Math.round(done/items.length*100) : 0;
    const card = document.createElement('div');
    card.className = 'ov-card';
    card.innerHTML = `
      <div class="ov-icon">${META[a].emoji}</div>
      <div class="ov-name">${META[a].name}</div>
      <div class="ov-count">${done}<span>/${items.length}</span></div>
      <div class="ov-sub">${pct}% završeno</div>
      <div class="ov-bar"><div class="ov-fill" style="width:${pct}%"></div></div>
    `;
    card.onclick = () => showTab(a);
    grid.appendChild(card);
  });
}

// ── RENDER AREA ───────────────────────────────────
function renderArea(area) {
  const items = state[area] || [];
  const done = items.filter(r => r.done).length;
  const pct = items.length ? Math.round(done/items.length*100) : 0;

  document.getElementById('prog-' + area).innerHTML = `
    <div class="prog-row"><span>Danas završeno</span><span>${done} / ${items.length}</span></div>
    <div class="prog-bg"><div class="prog-fill" style="width:${pct}%"></div></div>
  `;

  const list = document.getElementById('list-' + area);
  list.innerHTML = '';
  items.forEach(item => {
    const div = document.createElement('div');
    div.className = 'rem-card' + (item.done ? ' done' : '');
    div.innerHTML = `
      <div class="check">
        <svg class="check-svg" width="11" height="11" viewBox="0 0 12 12" fill="none">
          <path d="M2 6l3 3 5-5" stroke="white" stroke-width="1.8" stroke-linecap="round" stroke-linejoin="round"/>
        </svg>
      </div>
      <div class="rem-body">
        <div class="rem-text">${item.text}</div>
        <div class="rem-meta">${item.freq}</div>
      </div>
      <div class="freq-badge">${item.freq}</div>
    `;
    div.onclick = () => toggle(area, item.id);
    list.appendChild(div);
  });
}

function toggle(area, id) {
  const item = state[area].find(r => r.id === id);
  if (!item) return;
  item.done = !item.done;
  save();
  renderArea(area);
  renderOverview();
  toast(item.done ? '✓ Označeno' : 'Vraćeno na listu');
}

// ── ADD REMINDER ──────────────────────────────────
function addRem(area) {
  const inp = document.getElementById('inp-' + area);
  const frq = document.getElementById('frq-' + area);
  const text = inp.value.trim();
  if (!text) { toast('Upiši tekst podsjetnika'); return; }
  state[area].push({ id: area + Date.now(), text, freq: frq.value, done: false });
  save();
  inp.value = '';
  renderArea(area);
  renderOverview();
  toast('Podsjetnik dodan 🌿');
}

// Enter key support
AREAS.forEach(a => {
  const inp = document.getElementById('inp-' + a);
  if (inp) inp.addEventListener('keydown', e => { if (e.key === 'Enter') addRem(a); });
});

// ── RESET DAY ─────────────────────────────────────
function resetDay() {
  if (!confirm('Resetovati sve checkboxe za novi dan?')) return;
  AREAS.forEach(a => state[a].forEach(r => r.done = false));
  save();
  renderArea(currentTab);
  renderOverview();
  toast('Novi dan, novi početak 🌅');
}

// ── TOAST ─────────────────────────────────────────
function toast(msg) {
  const t = document.getElementById('toast');
  t.textContent = msg;
  t.classList.add('show');
  setTimeout(() => t.classList.remove('show'), 2200);
}

// ── INIT ──────────────────────────────────────────
document.getElementById('daily-quote').textContent =
  '"' + QUOTES[new Date().getDay() % QUOTES.length] + '"';

renderOverview();

// Hide install banner if already standalone
if (window.navigator.standalone) {
  document.getElementById('install-banner').style.display = 'none';
}

// Service Worker
if ('serviceWorker' in navigator) {
  navigator.serviceWorker.register('service-worker.js').catch(() => {});
}
</script>
</body>
</html>
