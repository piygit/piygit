<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8"/>
<meta name="viewport" content="width=device-width, initial-scale=1.0"/>
<title>Piyush Sharma — Dev × Designer</title>
<link rel="preconnect" href="https://fonts.googleapis.com"/>
<link href="https://fonts.googleapis.com/css2?family=Space+Mono:ital,wght@0,400;0,700;1,400&family=Syne:wght@400;700;800&display=swap" rel="stylesheet"/>
<script src="https://cdnjs.cloudflare.com/ajax/libs/Chart.js/4.4.1/chart.umd.js"></script>
<style>
  *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }

  :root {
    --bg: #0d0d0f;
    --bg2: #141416;
    --bg3: #1a1a1e;
    --border: rgba(255,255,255,0.08);
    --border2: rgba(255,255,255,0.14);
    --text: #e8e6f0;
    --text2: #9896a8;
    --text3: #5a5868;
    --purple: #7F77DD;
    --teal: #1D9E75;
    --amber: #EF9F27;
    --coral: #E24B4A;
    --blue: #378ADD;
    --gray: #888780;
    --green: #639922;
    --r: 10px;
    --r-sm: 6px;
  }

  html { scroll-behavior: smooth; }

  body {
    background: var(--bg);
    color: var(--text);
    font-family: 'Space Mono', monospace;
    min-height: 100vh;
    overflow-x: hidden;
  }

  /* NOISE OVERLAY */
  body::before {
    content: '';
    position: fixed;
    inset: 0;
    background-image: url("data:image/svg+xml,%3Csvg viewBox='0 0 256 256' xmlns='http://www.w3.org/2000/svg'%3E%3Cfilter id='n'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='0.9' numOctaves='4' stitchTiles='stitch'/%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23n)' opacity='0.03'/%3E%3C/svg%3E");
    pointer-events: none;
    z-index: 0;
    opacity: 0.4;
  }

  .wrap {
    position: relative;
    z-index: 1;
    max-width: 860px;
    margin: 0 auto;
    padding: 2rem 1.5rem 4rem;
  }

  /* HERO */
  .hero {
    display: grid;
    grid-template-columns: 1fr auto;
    gap: 2rem;
    align-items: start;
    padding: 3rem 2.5rem 2.5rem;
    background: var(--bg2);
    border: 0.5px solid var(--border);
    border-radius: var(--r);
    margin-bottom: 1.25rem;
    position: relative;
    overflow: hidden;
  }

  .hero::after {
    content: '';
    position: absolute;
    top: -60px;
    right: -60px;
    width: 280px;
    height: 280px;
    background: radial-gradient(circle, rgba(127,119,221,0.12) 0%, transparent 70%);
    pointer-events: none;
  }

  .hero-tag {
    font-size: 10px;
    letter-spacing: 0.2em;
    text-transform: uppercase;
    color: var(--text3);
    margin-bottom: 0.6rem;
  }

  .hero-name {
    font-family: 'Syne', sans-serif;
    font-size: clamp(32px, 5vw, 48px);
    font-weight: 800;
    line-height: 1.0;
    background: linear-gradient(135deg, #7F77DD 0%, #1D9E75 55%, #EF9F27 100%);
    -webkit-background-clip: text;
    -webkit-text-fill-color: transparent;
    background-clip: text;
    margin-bottom: 0.4rem;
  }

  .hero-subtitle {
    font-size: 10px;
    letter-spacing: 0.12em;
    color: var(--text3);
    text-transform: uppercase;
    margin-bottom: 1rem;
  }

  .hero-bio {
    font-size: 12px;
    line-height: 1.9;
    color: var(--text2);
    max-width: 380px;
  }

  .hero-bio strong { color: var(--text); font-weight: 700; }

  .hero-status {
    display: inline-flex;
    align-items: center;
    gap: 7px;
    font-size: 10px;
    padding: 5px 12px;
    border: 0.5px solid var(--border2);
    border-radius: 99px;
    color: var(--text2);
    margin-top: 1.2rem;
    background: var(--bg3);
  }

  .dot-live {
    width: 6px; height: 6px; border-radius: 50%; background: var(--teal);
    animation: pulse 2s ease-in-out infinite;
  }

  @keyframes pulse {
    0%,100% { opacity:1; transform:scale(1); }
    50% { opacity:0.5; transform:scale(0.75); }
  }

  /* TERMINAL */
  .terminal {
    background: var(--bg3);
    border: 0.5px solid var(--border);
    border-radius: var(--r);
    padding: 1rem 1.25rem;
    min-width: 210px;
    max-width: 240px;
  }

  .t-bar { display: flex; gap: 5px; margin-bottom: 0.8rem; }
  .t-dot { width: 9px; height: 9px; border-radius: 50%; }
  .t-line { font-size: 10px; line-height: 1.9; }
  .t-prompt { color: var(--purple); }
  .t-cmd { color: var(--teal); }
  .t-out { color: var(--text3); }
  .t-cursor {
    display: inline-block; width: 7px; height: 12px;
    background: var(--purple); vertical-align: -2px;
    animation: blink 1s step-end infinite;
  }
  @keyframes blink { 0%,100%{opacity:1} 50%{opacity:0} }

  /* GRID LAYOUT */
  .grid-2 { display: grid; grid-template-columns: 1fr 1fr; gap: 1.25rem; margin-bottom: 1.25rem; }
  .grid-3 { display: grid; grid-template-columns: repeat(3,1fr); gap: 1rem; margin-bottom: 1.25rem; }
  .full { grid-column: 1 / -1; }

  /* CARD */
  .card {
    background: var(--bg2);
    border: 0.5px solid var(--border);
    border-radius: var(--r);
    padding: 1.5rem;
  }

  .card-label {
    font-size: 9px;
    letter-spacing: 0.2em;
    text-transform: uppercase;
    color: var(--text3);
    margin-bottom: 1rem;
  }

  /* STAT CARDS */
  .stat { text-align: center; padding: 1.25rem; }
  .stat-num {
    font-family: 'Syne', sans-serif;
    font-size: 28px;
    font-weight: 800;
    background: linear-gradient(135deg, var(--purple), var(--teal));
    -webkit-background-clip: text;
    -webkit-text-fill-color: transparent;
    background-clip: text;
  }
  .stat-lbl { font-size: 9px; letter-spacing: 0.15em; text-transform: uppercase; color: var(--text3); margin-top: 4px; }

  /* SKILL CHIPS */
  .chip-grid { display: flex; flex-wrap: wrap; gap: 6px; }
  .chip {
    font-size: 10px;
    padding: 5px 10px;
    border: 0.5px solid var(--border);
    border-radius: 4px;
    color: var(--text2);
    display: flex;
    align-items: center;
    gap: 6px;
    transition: border-color 0.2s, color 0.2s, background 0.2s;
    cursor: default;
  }
  .chip:hover { border-color: var(--purple); color: var(--text); background: rgba(127,119,221,0.08); }
  .chip-dot { width: 5px; height: 5px; border-radius: 50%; flex-shrink: 0; }

  /* BARS */
  .bar-row { margin-bottom: 12px; }
  .bar-header { display: flex; justify-content: space-between; font-size: 10px; color: var(--text2); margin-bottom: 5px; }
  .bar-track { height: 3px; background: var(--bg3); border-radius: 2px; overflow: hidden; }
  .bar-fill { height: 100%; border-radius: 2px; width: 0; transition: width 1.2s cubic-bezier(0.4,0,0.2,1); }

  /* HEATMAP */
  .heatmap-scroll { overflow-x: auto; padding-bottom: 0.5rem; }
  .heatmap-scroll::-webkit-scrollbar { height: 4px; }
  .heatmap-scroll::-webkit-scrollbar-track { background: var(--bg3); }
  .heatmap-scroll::-webkit-scrollbar-thumb { background: var(--border2); border-radius: 2px; }

  .heatmap-grid {
    display: grid;
    grid-template-rows: repeat(7, 10px);
    grid-auto-flow: column;
    gap: 2px;
    width: max-content;
  }

  .hmap-cell {
    width: 10px; height: 10px; border-radius: 2px;
    transition: opacity 0.2s;
  }
  .hmap-cell:hover { opacity: 0.7; }

  .hmap-months {
    display: flex;
    gap: 0;
    font-size: 9px;
    color: var(--text3);
    margin-bottom: 4px;
    width: max-content;
  }

  .hmap-days {
    display: grid;
    grid-template-rows: repeat(7, 10px);
    gap: 2px;
    font-size: 9px;
    color: var(--text3);
    margin-right: 6px;
    flex-shrink: 0;
  }

  .hmap-wrap { display: flex; }

  .hmap-legend {
    display: flex;
    align-items: center;
    gap: 4px;
    font-size: 9px;
    color: var(--text3);
    margin-top: 8px;
    justify-content: flex-end;
  }

  .hmap-leg-cell { width: 10px; height: 10px; border-radius: 2px; }

  /* STREAK */
  .streak-wrap {
    display: flex;
    align-items: center;
    justify-content: space-around;
    gap: 1rem;
    flex-wrap: wrap;
  }

  .streak-block { text-align: center; }
  .streak-val {
    font-family: 'Syne', sans-serif;
    font-size: 32px;
    font-weight: 800;
    color: var(--purple);
  }
  .streak-sub { font-size: 9px; letter-spacing: 0.15em; text-transform: uppercase; color: var(--text3); margin-top: 2px; }
  .streak-sep { width: 0.5px; height: 50px; background: var(--border2); }

  /* TIMELINE */
  .timeline { position: relative; padding-left: 1.5rem; }
  .timeline::before {
    content: ''; position: absolute; left: 5px; top: 0; bottom: 0;
    width: 0.5px; background: var(--border2);
  }
  .tl-item { position: relative; margin-bottom: 1.25rem; }
  .tl-dot {
    position: absolute; left: -1.5rem; top: 4px;
    width: 10px; height: 10px; border-radius: 50%;
    border: 2px solid var(--bg2);
  }
  .tl-title { font-size: 12px; font-weight: 700; color: var(--text); }
  .tl-sub { font-size: 10px; color: var(--text3); margin-top: 2px; line-height: 1.5; }

  /* CONTACT */
  .contact-grid { display: grid; grid-template-columns: 1fr 1fr; gap: 8px; }
  .contact-card {
    display: flex; align-items: center; gap: 10px;
    padding: 10px 14px;
    border: 0.5px solid var(--border);
    border-radius: var(--r-sm);
    text-decoration: none;
    transition: border-color 0.2s, background 0.2s;
    cursor: pointer;
  }
  .contact-card:hover { border-color: var(--border2); background: var(--bg3); }
  .contact-icon {
    width: 30px; height: 30px; border-radius: 6px;
    display: flex; align-items: center; justify-content: center; flex-shrink: 0;
  }
  .contact-icon svg { width: 15px; height: 15px; }
  .contact-name { font-size: 11px; font-weight: 700; color: var(--text); }
  .contact-handle { font-size: 10px; color: var(--text3); margin-top: 1px; }

  /* CHART WRAPS */
  .chart-wrap { position: relative; width: 100%; }
  .donut-wrap { display: flex; align-items: center; gap: 1.5rem; flex-wrap: wrap; }
  .donut-legend { display: flex; flex-direction: column; gap: 7px; }
  .legend-row { display: flex; align-items: center; gap: 7px; font-size: 10px; color: var(--text2); }
  .legend-swatch { width: 9px; height: 9px; border-radius: 2px; flex-shrink: 0; }

  /* QUOTE */
  .quote {
    font-size: 11px; font-style: italic; line-height: 1.9;
    color: var(--text2); border-left: 2px solid var(--purple);
    padding-left: 1rem; margin-top: 1.5rem;
  }

  /* FOOTER */
  .footer { text-align: center; font-size: 10px; color: var(--text3); margin-top: 2rem; letter-spacing: 0.1em; }

  /* NAV */
  .nav {
    display: flex; gap: 1px; margin-bottom: 1.25rem;
    background: var(--bg2); border: 0.5px solid var(--border);
    border-radius: var(--r); padding: 4px; overflow-x: auto;
    scrollbar-width: none;
  }
  .nav::-webkit-scrollbar { display: none; }
  .nav-btn {
    font-family: 'Space Mono', monospace; font-size: 10px;
    letter-spacing: 0.06em; padding: 7px 14px; border-radius: 7px;
    border: none; background: none; color: var(--text3);
    cursor: pointer; white-space: nowrap;
    transition: background 0.15s, color 0.15s;
  }
  .nav-btn:hover { color: var(--text2); background: var(--bg3); }
  .nav-btn.active { background: var(--bg3); color: var(--purple); border: 0.5px solid var(--border2); }

  .panel { display: none; }
  .panel.active { display: block; }

  /* SECTION ANIMATIONS */
  .fade-in { animation: fadeUp 0.4s ease forwards; }
  @keyframes fadeUp { from { opacity: 0; transform: translateY(8px); } to { opacity:1; transform: translateY(0); } }

  @media (max-width: 600px) {
    .hero { grid-template-columns: 1fr; }
    .terminal { max-width: 100%; min-width: unset; }
    .hero::after { display: none; }
    .grid-2, .grid-3 { grid-template-columns: 1fr; }
    .contact-grid { grid-template-columns: 1fr; }
    .streak-sep { display: none; }
  }
</style>
</head>
<body>
<div class="wrap">

  <!-- HERO -->
  <div class="hero">
    <div>
      <p class="hero-tag">// github.com/piygit</p>
      <h1 class="hero-name">Piyush<br>Sharma</h1>
      <p class="hero-subtitle">Developer × Designer &nbsp;·&nbsp; Full Stack &nbsp;·&nbsp; DSA &nbsp;·&nbsp; GenAI</p>
      <p class="hero-bio">
        Code on one side, <strong>creativity</strong> on the other.<br>
        Building products at the intersection of<br>
        <strong>engineering precision</strong> and <strong>design intuition</strong>.
      </p>
      <span class="hero-status"><span class="dot-live"></span>open to collabs &amp; opportunities</span>
    </div>
    <div class="terminal">
      <div class="t-bar">
        <span class="t-dot" style="background:#E24B4A"></span>
        <span class="t-dot" style="background:#EF9F27"></span>
        <span class="t-dot" style="background:#639922"></span>
      </div>
      <div class="t-line"><span class="t-prompt">~$</span> <span class="t-cmd">whoami</span></div>
      <div class="t-line t-out">piyush.sharma</div>
      <div class="t-line" style="margin-top:6px"><span class="t-prompt">~$</span> <span class="t-cmd">cat role.txt</span></div>
      <div class="t-line t-out">fullstack dev</div>
      <div class="t-line t-out">ui/ux designer</div>
      <div class="t-line t-out">genai builder</div>
      <div class="t-line" style="margin-top:6px"><span class="t-prompt">~$</span> <span class="t-cmd">cat vibe.txt</span></div>
      <div class="t-line t-out">ship it. make it beautiful.</div>
      <div class="t-line" style="margin-top:6px"><span class="t-prompt">~$</span> <span class="t-cursor"></span></div>
    </div>
  </div>

  <!-- NAV -->
  <nav class="nav" role="tablist" aria-label="Profile sections">
    <button class="nav-btn active" data-tab="stats">// stats</button>
    <button class="nav-btn" data-tab="stack">// stack</button>
    <button class="nav-btn" data-tab="heatmap">// activity</button>
    <button class="nav-btn" data-tab="journey">// journey</button>
    <button class="nav-btn" data-tab="connect">// connect</button>
  </nav>

  <!-- STATS TAB -->
  <div id="tab-stats" class="panel active fade-in">
    <div class="grid-3">
      <div class="card stat"><div class="stat-num" id="cnt-commits">0</div><div class="stat-lbl">total commits</div></div>
      <div class="card stat"><div class="stat-num" id="cnt-repos">0</div><div class="stat-lbl">repositories</div></div>
      <div class="card stat"><div class="stat-num" id="cnt-stars">0</div><div class="stat-lbl">stars earned</div></div>
    </div>

    <div class="grid-2">
      <div class="card">
        <p class="card-label">language breakdown</p>
        <div class="donut-wrap">
          <div class="chart-wrap" style="width:150px;height:150px;flex-shrink:0">
            <canvas id="donut" width="150" height="150" role="img" aria-label="Donut chart: JS 28%, Python 22%, C++ 15%, Dart 14%, Java 12%, Other 9%">JS 28%, Python 22%, C++ 15%, Dart 14%, Java 12%, Other 9%</canvas>
          </div>
          <div class="donut-legend" id="donut-legend"></div>
        </div>
      </div>
      <div class="card">
        <p class="card-label">weekly activity (hrs)</p>
        <div class="chart-wrap" style="height:170px">
          <canvas id="activity" role="img" aria-label="Bar chart of weekly coding hours by day of week"></canvas>
        </div>
      </div>
    </div>

    <div class="card">
      <p class="card-label">proficiency radar</p>
      <div style="display:flex;align-items:center;gap:2rem;flex-wrap:wrap">
        <div class="chart-wrap" style="width:220px;height:220px;flex-shrink:0">
          <canvas id="radar" width="220" height="220" role="img" aria-label="Radar chart: Frontend 90, Backend 75, Mobile 70, GenAI 65, DSA 80, Design 88"></canvas>
        </div>
        <div class="donut-legend" id="radar-legend"></div>
      </div>
    </div>
  </div>

  <!-- STACK TAB -->
  <div id="tab-stack" class="panel">
    <div class="card" style="margin-bottom:1.25rem">
      <p class="card-label">languages</p>
      <div class="chip-grid" id="lang-chips"></div>
    </div>
    <div class="card" style="margin-bottom:1.25rem">
      <p class="card-label">frameworks &amp; tools</p>
      <div class="chip-grid" id="fw-chips"></div>
    </div>
    <div class="card" style="margin-bottom:1.25rem">
      <p class="card-label">design &amp; creative</p>
      <div class="chip-grid" id="design-chips"></div>
    </div>
    <div class="card">
      <p class="card-label">domain depth</p>
      <div id="domain-bars"></div>
    </div>
  </div>

  <!-- HEATMAP TAB -->
  <div id="tab-heatmap" class="panel">
    <div class="card" style="margin-bottom:1.25rem">
      <p class="card-label">contribution streak</p>
      <div class="streak-wrap">
        <div class="streak-block"><div class="streak-val">47</div><div class="streak-sub">current streak</div></div>
        <div class="streak-sep"></div>
        <div class="streak-block"><div class="streak-val" style="color:var(--teal)">94</div><div class="streak-sub">longest streak</div></div>
        <div class="streak-sep"></div>
        <div class="streak-block"><div class="streak-val" style="color:var(--amber)">1,240</div><div class="streak-sub">total contributions</div></div>
      </div>
    </div>
    <div class="card">
      <p class="card-label">contribution heatmap — last 52 weeks</p>
      <div style="display:flex;gap:6px;align-items:flex-start">
        <div class="hmap-days" id="hmap-days"></div>
        <div>
          <div class="hmap-months" id="hmap-months"></div>
          <div class="heatmap-scroll">
            <div class="heatmap-grid" id="heatmap-grid"></div>
          </div>
          <div class="hmap-legend">
            <span>less</span>
            <span class="hmap-leg-cell" style="background:#1a1a1e;border:0.5px solid rgba(255,255,255,0.1)"></span>
            <span class="hmap-leg-cell" style="background:rgba(127,119,221,0.2)"></span>
            <span class="hmap-leg-cell" style="background:rgba(127,119,221,0.45)"></span>
            <span class="hmap-leg-cell" style="background:rgba(127,119,221,0.72)"></span>
            <span class="hmap-leg-cell" style="background:#7F77DD"></span>
            <span>more</span>
          </div>
        </div>
      </div>
    </div>
  </div>

  <!-- JOURNEY TAB -->
  <div id="tab-journey" class="panel">
    <div class="grid-2">
      <div class="card">
        <p class="card-label">dev timeline</p>
        <div class="timeline" id="timeline"></div>
      </div>
      <div class="card">
        <p class="card-label">what i'm building rn</p>
        <div id="building-list"></div>
        <div class="quote" id="quote"></div>
      </div>
    </div>
  </div>

  <!-- CONNECT TAB -->
  <div id="tab-connect" class="panel">
    <div class="card">
      <p class="card-label">find me at</p>
      <div class="contact-grid" id="contact-grid"></div>
    </div>
  </div>

  <div class="footer">// crafted with Space Mono &amp; Syne &nbsp;·&nbsp; piygit &nbsp;·&nbsp; 2025</div>
</div>

<script>
// ── DATA ────────────────────────────────────────────────────────────────
const LANGS = [
  { name:'JavaScript', color:'#EF9F27' }, { name:'Python', color:'#378ADD' },
  { name:'C++', color:'#5DCAA5' },        { name:'Java', color:'#D85A30' },
  { name:'Dart', color:'#7F77DD' },       { name:'Swift', color:'#E24B4A' },
  { name:'C', color:'#888780' },          { name:'HTML/CSS', color:'#1D9E75' },
];

const FW = [
  { name:'React', color:'#7F77DD' },         { name:'React Native', color:'#7F77DD' },
  { name:'Flutter', color:'#378ADD' },        { name:'Node.js', color:'#639922' },
  { name:'Django', color:'#1D9E75' },         { name:'TailwindCSS', color:'#5DCAA5' },
  { name:'Three.js', color:'#888780' },       { name:'TensorFlow', color:'#EF9F27' },
  { name:'Firebase', color:'#EF9F27' },       { name:'MongoDB', color:'#639922' },
  { name:'MySQL', color:'#378ADD' },          { name:'Google Cloud', color:'#D85A30' },
  { name:'Vercel', color:'#888780' },         { name:'Netlify', color:'#5DCAA5' },
];

const DESIGN = [
  { name:'Figma', color:'#E24B4A' },              { name:'Adobe Illustrator', color:'#EF9F27' },
  { name:'Adobe Photoshop', color:'#378ADD' },     { name:'After Effects', color:'#7F77DD' },
  { name:'Premiere Pro', color:'#7F77DD' },        { name:'Lightroom', color:'#378ADD' },
  { name:'Canva', color:'#5DCAA5' },
];

const DOMAINS = [
  { label:'Frontend Dev', val:90, color:'#7F77DD' },
  { label:'Backend Dev', val:75, color:'#1D9E75' },
  { label:'Mobile Dev', val:70, color:'#EF9F27' },
  { label:'GenAI / ML', val:65, color:'#5DCAA5' },
  { label:'DSA', val:80, color:'#378ADD' },
  { label:'Design / UI', val:88, color:'#E24B4A' },
];

const TIMELINE = [
  { title:'GenAI & LLM Apps', sub:'2024 → now · TensorFlow, API pipelines, agents', color:'#7F77DD' },
  { title:'Full Stack Projects', sub:'2023 → now · React + Node + Firebase', color:'#1D9E75' },
  { title:'Mobile Development', sub:'2023 · Flutter & React Native', color:'#EF9F27' },
  { title:'Design Systems', sub:'2022 → now · Figma, Premiere, Illustrator', color:'#E24B4A' },
  { title:'DSA Fundamentals', sub:'2022 · 500+ problems · Java & C++', color:'#378ADD' },
];

const BUILDING = [
  'AI-powered design tool w/ Anthropic API',
  'Cross-platform mobile app in Flutter',
  'Interactive 3D portfolio w/ Three.js',
];

const QUOTES = [
  '"Code is design. Design is code. The boundary is a lie."',
  '"Every pixel is a decision. Every function is a commitment."',
  '"Build fast. Ship beautiful. Learn always. — piygit"',
];

const CONTACTS = [
  { name:'LinkedIn', handle:'piyush-sharma-a8249430a', url:'https://linkedin.com/in/piyush-sharma-a8249430a', color:'#378ADD',
    icon:`<svg viewBox="0 0 24 24" fill="currentColor"><path d="M20.447 20.452h-3.554v-5.569c0-1.328-.027-3.037-1.852-3.037-1.853 0-2.136 1.445-2.136 2.939v5.667H9.351V9h3.414v1.561h.046c.477-.9 1.637-1.85 3.37-1.85 3.601 0 4.267 2.37 4.267 5.455v6.286zM5.337 7.433c-1.144 0-2.063-.926-2.063-2.065 0-1.138.92-2.063 2.063-2.063 1.14 0 2.064.925 2.064 2.063 0 1.139-.925 2.065-2.064 2.065zm1.782 13.019H3.555V9h3.564v11.452zM22.225 0H1.771C.792 0 0 .774 0 1.729v20.542C0 23.227.792 24 1.771 24h20.451C23.2 24 24 23.227 24 22.271V1.729C24 .774 23.2 0 22.222 0h.003z"/></svg>` },
  { name:'GitHub', handle:'piygit', url:'https://github.com/piygit', color:'#888780',
    icon:`<svg viewBox="0 0 24 24" fill="currentColor"><path d="M12 .297c-6.63 0-12 5.373-12 12 0 5.303 3.438 9.8 8.205 11.385.6.113.82-.258.82-.577 0-.285-.01-1.04-.015-2.04-3.338.724-4.042-1.61-4.042-1.61C4.422 18.07 3.633 17.7 3.633 17.7c-1.087-.744.084-.729.084-.729 1.205.084 1.838 1.236 1.838 1.236 1.07 1.835 2.809 1.305 3.495.998.108-.776.417-1.305.76-1.605-2.665-.3-5.466-1.332-5.466-5.93 0-1.31.465-2.38 1.235-3.22-.135-.303-.54-1.523.105-3.176 0 0 1.005-.322 3.3 1.23.96-.267 1.98-.399 3-.405 1.02.006 2.04.138 3 .405 2.28-1.552 3.285-1.23 3.285-1.23.645 1.653.24 2.873.12 3.176.765.84 1.23 1.91 1.23 3.22 0 4.61-2.805 5.625-5.475 5.92.42.36.81 1.096.81 2.22 0 1.606-.015 2.896-.015 3.286 0 .315.21.69.825.57C20.565 22.092 24 17.592 24 12.297c0-6.627-5.373-12-12-12"/></svg>` },
  { name:'Medium', handle:'@piyush.shrma05', url:'https://medium.com/@piyush.shrma05', color:'#5F5E5A',
    icon:`<svg viewBox="0 0 24 24" fill="currentColor"><path d="M13.54 12a6.8 6.8 0 01-6.77 6.82A6.8 6.8 0 010 12a6.8 6.8 0 016.77-6.82A6.8 6.8 0 0113.54 12zM20.96 12c0 3.54-1.51 6.42-3.38 6.42-1.87 0-3.39-2.88-3.39-6.42s1.52-6.42 3.39-6.42 3.38 2.88 3.38 6.42M24 12c0 3.17-.53 5.75-1.19 5.75-.66 0-1.19-2.58-1.19-5.75s.53-5.75 1.19-5.75C23.47 6.25 24 8.83 24 12z"/></svg>` },
  { name:'X / Twitter', handle:'@peiyush_x', url:'https://x.com/@peiyush_x', color:'#2C2C2A',
    icon:`<svg viewBox="0 0 24 24" fill="currentColor"><path d="M18.244 2.25h3.308l-7.227 8.26 8.502 11.24H16.17l-4.714-6.231-5.401 6.231H2.744l7.73-8.835L1.254 2.25H8.08l4.253 5.622zm-1.161 17.52h1.833L7.084 4.126H5.117z"/></svg>` },
  { name:'Email', handle:'piyush.shrma05@gmail.com', url:'mailto:piyush.shrma05@gmail.com', color:'#D85A30',
    icon:`<svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><rect x="2" y="4" width="20" height="16" rx="2"/><polyline points="2,4 12,13 22,4"/></svg>` },
];

// ── CHIPS ────────────────────────────────────────────────────────────────
function buildChips(id, items) {
  const el = document.getElementById(id);
  items.forEach(it => {
    const c = document.createElement('div');
    c.className = 'chip';
    c.innerHTML = `<span class="chip-dot" style="background:${it.color}"></span>${it.name}`;
    el.appendChild(c);
  });
}

buildChips('lang-chips', LANGS);
buildChips('fw-chips', FW);
buildChips('design-chips', DESIGN);

// ── DOMAIN BARS ──────────────────────────────────────────────────────────
const bc = document.getElementById('domain-bars');
DOMAINS.forEach(d => {
  bc.innerHTML += `<div class="bar-row"><div class="bar-header"><span>${d.label}</span><span>${d.val}%</span></div><div class="bar-track"><div class="bar-fill" data-val="${d.val}" style="background:${d.color}"></div></div></div>`;
});

function animateBars() {
  document.querySelectorAll('.bar-fill').forEach(el => {
    setTimeout(() => { el.style.width = el.dataset.val + '%'; }, 80);
  });
}

// ── TIMELINE ─────────────────────────────────────────────────────────────
const tl = document.getElementById('timeline');
TIMELINE.forEach(t => {
  tl.innerHTML += `<div class="tl-item"><span class="tl-dot" style="background:${t.color}"></span><div class="tl-title">${t.title}</div><div class="tl-sub">${t.sub}</div></div>`;
});

// building list
const bl = document.getElementById('building-list');
BUILDING.forEach(b => {
  bl.innerHTML += `<div style="font-size:11px;color:var(--text2);padding:6px 0;border-bottom:0.5px solid var(--border);display:flex;gap:8px;align-items:flex-start"><span style="color:var(--purple);flex-shrink:0">→</span>${b}</div>`;
});

document.getElementById('quote').textContent = QUOTES[Math.floor(Math.random() * QUOTES.length)];

// ── CONTACTS ─────────────────────────────────────────────────────────────
const cg = document.getElementById('contact-grid');
CONTACTS.forEach(c => {
  const el = document.createElement('a');
  el.className = 'contact-card';
  el.href = c.url;
  el.innerHTML = `<span class="contact-icon" style="background:${c.color}22;color:${c.color}">${c.icon}</span><div><div class="contact-name">${c.name}</div><div class="contact-handle">${c.handle}</div></div>`;
  cg.appendChild(el);
});

// ── HEATMAP ──────────────────────────────────────────────────────────────
function buildHeatmap() {
  const grid = document.getElementById('heatmap-grid');
  const months = document.getElementById('hmap-months');
  const days = document.getElementById('hmap-days');

  const dayLabels = ['', 'Mon', '', 'Wed', '', 'Fri', ''];
  days.innerHTML = dayLabels.map(d => `<div style="height:10px;line-height:10px">${d}</div>`).join('');

  const WEEKS = 52;
  const today = new Date();
  const startDate = new Date(today);
  startDate.setDate(today.getDate() - (WEEKS * 7 - 1));

  // Generate pseudo-random but realistic contribution data
  function seededRand(seed) {
    let s = seed;
    return function() {
      s = (s * 1664525 + 1013904223) & 0xffffffff;
      return (s >>> 0) / 0xffffffff;
    };
  }
  const rand = seededRand(42);

  const cells = [];
  for (let w = 0; w < WEEKS; w++) {
    for (let d = 0; d < 7; d++) {
      const date = new Date(startDate);
      date.setDate(startDate.getDate() + w * 7 + d);
      if (date > today) { cells.push({ date, level: -1 }); continue; }
      const r = rand();
      let level = 0;
      if (d < 5) { // weekdays more active
        if (r > 0.45) level = 1;
        if (r > 0.65) level = 2;
        if (r > 0.80) level = 3;
        if (r > 0.93) level = 4;
      } else {
        if (r > 0.55) level = 1;
        if (r > 0.75) level = 2;
        if (r > 0.88) level = 3;
        if (r > 0.96) level = 4;
      }
      cells.push({ date, level });
    }
  }

  const lvlColors = [
    'rgba(255,255,255,0.04)', // 0
    'rgba(127,119,221,0.22)', // 1
    'rgba(127,119,221,0.45)', // 2
    'rgba(127,119,221,0.72)', // 3
    '#7F77DD',                 // 4
  ];

  cells.forEach(c => {
    const el = document.createElement('div');
    el.className = 'hmap-cell';
    if (c.level === -1) {
      el.style.background = 'transparent';
    } else {
      el.style.background = lvlColors[c.level];
      if (c.level === 0) el.style.border = '0.5px solid rgba(255,255,255,0.06)';
      el.title = c.date.toDateString() + ' — ' + (c.level * 3) + ' contributions';
    }
    grid.appendChild(el);
  });

  // Month labels
  const monthNames = ['Jan','Feb','Mar','Apr','May','Jun','Jul','Aug','Sep','Oct','Nov','Dec'];
  let lastMonth = -1;
  let monthHtml = '';
  for (let w = 0; w < WEEKS; w++) {
    const d = new Date(startDate);
    d.setDate(startDate.getDate() + w * 7);
    const m = d.getMonth();
    if (m !== lastMonth) {
      monthHtml += `<span style="width:${(WEEKS - w) * 12}px;display:inline-block;font-size:9px;color:var(--text3)">${monthNames[m]}</span>`;
      lastMonth = m;
    }
  }
  months.innerHTML = monthHtml;
}

// ── COUNTER ANIM ─────────────────────────────────────────────────────────
function animateCounter(id, target) {
  const el = document.getElementById(id);
  if (!el) return;
  let cur = 0;
  const step = Math.ceil(target / 50);
  const t = setInterval(() => {
    cur = Math.min(cur + step, target);
    el.textContent = cur >= 1000 ? (cur / 1000).toFixed(1) + 'k' : cur;
    if (cur >= target) clearInterval(t);
  }, 25);
}

// ── CHARTS ───────────────────────────────────────────────────────────────
let chartsBuilt = false;

function buildCharts() {
  if (chartsBuilt) return;
  chartsBuilt = true;

  const gridColor = 'rgba(255,255,255,0.06)';
  const tickColor = '#5a5868';

  // DONUT
  const donutData = [28, 22, 15, 14, 12, 9];
  const donutLabels = ['JavaScript', 'Python', 'C++', 'Dart', 'Java', 'Other'];
  const donutColors = ['#EF9F27', '#378ADD', '#5DCAA5', '#7F77DD', '#D85A30', '#888780'];

  new Chart(document.getElementById('donut'), {
    type: 'doughnut',
    data: { labels: donutLabels, datasets: [{ data: donutData, backgroundColor: donutColors, borderWidth: 0, hoverOffset: 4 }] },
    options: {
      responsive: false, cutout: '65%',
      plugins: { legend: { display: false }, tooltip: { callbacks: { label: c => c.label + ': ' + c.raw + '%' } } }
    }
  });

  const dl = document.getElementById('donut-legend');
  donutLabels.forEach((l, i) => {
    dl.innerHTML += `<div class="legend-row"><span class="legend-swatch" style="background:${donutColors[i]}"></span>${l} <span style="color:var(--text3)">${donutData[i]}%</span></div>`;
  });

  // ACTIVITY BAR
  const days = ['Mon', 'Tue', 'Wed', 'Thu', 'Fri', 'Sat', 'Sun'];
  const hrs = [3.2, 4.8, 6.1, 5.5, 4.2, 7.3, 2.8];

  new Chart(document.getElementById('activity'), {
    type: 'bar',
    data: {
      labels: days,
      datasets: [{
        label: 'Hours', data: hrs,
        backgroundColor: hrs.map((_, i) => i === 5 ? '#7F77DD' : 'rgba(127,119,221,0.3)'),
        borderRadius: 4, borderSkipped: false,
      }]
    },
    options: {
      responsive: true, maintainAspectRatio: false,
      plugins: { legend: { display: false }, tooltip: { callbacks: { label: c => c.raw.toFixed(1) + ' hrs' } } },
      scales: {
        x: { grid: { display: false }, ticks: { color: tickColor, font: { size: 9, family: 'Space Mono' } } },
        y: { grid: { color: gridColor }, ticks: { color: tickColor, font: { size: 9 }, callback: v => v + 'h' }, max: 10 }
      }
    }
  });

  // RADAR
  const radarLabels = ['Frontend', 'Backend', 'Mobile', 'GenAI', 'DSA', 'Design'];
  const radarData = [90, 75, 70, 65, 80, 88];
  const radarColors = ['#7F77DD','#1D9E75','#EF9F27','#5DCAA5','#378ADD','#E24B4A'];

  new Chart(document.getElementById('radar'), {
    type: 'radar',
    data: {
      labels: radarLabels,
      datasets: [{
        data: radarData,
        backgroundColor: 'rgba(127,119,221,0.12)',
        borderColor: '#7F77DD', borderWidth: 1.5,
        pointBackgroundColor: radarColors, pointRadius: 4, pointHoverRadius: 6,
      }]
    },
    options: {
      responsive: false,
      plugins: { legend: { display: false }, tooltip: { callbacks: { label: c => c.raw + '%' } } },
      scales: {
        r: {
          min: 0, max: 100,
          ticks: { display: false, stepSize: 25 },
          grid: { color: gridColor },
          angleLines: { color: gridColor },
          pointLabels: { color: tickColor, font: { size: 10, family: 'Space Mono' } }
        }
      }
    }
  });

  const rl = document.getElementById('radar-legend');
  radarLabels.forEach((l, i) => {
    rl.innerHTML += `<div class="legend-row"><span class="legend-swatch" style="background:${radarColors[i]}"></span>${l} — ${radarData[i]}%</div>`;
  });

  // counters
  animateCounter('cnt-commits', 1240);
  animateCounter('cnt-repos', 34);
  animateCounter('cnt-stars', 87);
}

// ── NAV ──────────────────────────────────────────────────────────────────
let heatmapBuilt = false;

document.querySelectorAll('.nav-btn').forEach(btn => {
  btn.addEventListener('click', () => {
    document.querySelectorAll('.nav-btn').forEach(b => b.classList.remove('active'));
    document.querySelectorAll('.panel').forEach(p => { p.classList.remove('active'); p.classList.remove('fade-in'); });
    btn.classList.add('active');
    const tab = btn.dataset.tab;
    const panel = document.getElementById('tab-' + tab);
    panel.classList.add('active');
    void panel.offsetWidth;
    panel.classList.add('fade-in');

    if (tab === 'stats') buildCharts();
    if (tab === 'stack') animateBars();
    if (tab === 'heatmap' && !heatmapBuilt) { buildHeatmap(); heatmapBuilt = true; }
  });
});

// init charts on load (default tab)
buildCharts();
</script>
</body>
</html>
