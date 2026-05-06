# mantleflow-ai
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>MantleFlow AI — Autonomous RWA Yield Intelligence</title>
<link href="https://fonts.googleapis.com/css2?family=Space+Mono:wght@400;700&family=Syne:wght@400;600;700;800&display=swap" rel="stylesheet">
<script src="https://cdnjs.cloudflare.com/ajax/libs/Chart.js/4.4.1/chart.umd.min.js"></script>
<style>
  :root {
    --bg: #050810;
    --bg2: #090d1a;
    --bg3: #0d1221;
    --panel: #0f1527;
    --border: #1a2240;
    --border2: #243060;
    --green: #00ff88;
    --green2: #00cc6a;
    --cyan: #00d4ff;
    --orange: #ff6b35;
    --red: #ff3b3b;
    --gold: #ffd060;
    --muted: #4a5578;
    --text: #c8d4f0;
    --text2: #8090b8;
    --white: #e8f0ff;
    --font-data: 'Space Mono', monospace;
    --font-ui: 'Syne', sans-serif;
  }
  * { box-sizing: border-box; margin: 0; padding: 0; }
  body {
    background: var(--bg);
    color: var(--text);
    font-family: var(--font-ui);
    min-height: 100vh;
    overflow-x: hidden;
  }
  /* Noise overlay */
  body::before {
    content: '';
    position: fixed;
    inset: 0;
    background-image: url("data:image/svg+xml,%3Csvg viewBox='0 0 256 256' xmlns='http://www.w3.org/2000/svg'%3E%3Cfilter id='n'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='0.9' numOctaves='4' stitchTiles='stitch'/%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23n)' opacity='0.04'/%3E%3C/svg%3E");
    pointer-events: none;
    z-index: 0;
    opacity: 0.3;
  }

  /* HEADER */
  header {
    position: sticky;
    top: 0;
    z-index: 100;
    background: rgba(5,8,16,0.92);
    backdrop-filter: blur(20px);
    border-bottom: 1px solid var(--border);
    padding: 0 24px;
    height: 60px;
    display: flex;
    align-items: center;
    justify-content: space-between;
  }
  .logo {
    display: flex;
    align-items: center;
    gap: 10px;
  }
  .logo-icon {
    width: 32px;
    height: 32px;
    background: linear-gradient(135deg, var(--green), var(--cyan));
    border-radius: 8px;
    display: flex;
    align-items: center;
    justify-content: center;
    font-size: 14px;
    font-weight: 700;
    color: #000;
    font-family: var(--font-data);
    flex-shrink: 0;
  }
  .logo-text {
    font-size: 18px;
    font-weight: 800;
    color: var(--white);
    letter-spacing: -0.5px;
  }
  .logo-sub {
    font-family: var(--font-data);
    font-size: 9px;
    color: var(--green);
    letter-spacing: 2px;
    margin-top: 1px;
  }
  .header-right {
    display: flex;
    align-items: center;
    gap: 16px;
  }
  .live-badge {
    display: flex;
    align-items: center;
    gap: 6px;
    background: rgba(0,255,136,0.08);
    border: 1px solid rgba(0,255,136,0.3);
    border-radius: 20px;
    padding: 4px 10px;
    font-size: 11px;
    color: var(--green);
    font-family: var(--font-data);
    letter-spacing: 1px;
  }
  .live-dot {
    width: 6px;
    height: 6px;
    background: var(--green);
    border-radius: 50%;
    animation: pulse-dot 1.5s infinite;
  }
  @keyframes pulse-dot {
    0%, 100% { opacity: 1; transform: scale(1); }
    50% { opacity: 0.4; transform: scale(0.8); }
  }
  .agent-badge {
    display: flex;
    align-items: center;
    gap: 6px;
    background: rgba(0,212,255,0.06);
    border: 1px solid rgba(0,212,255,0.25);
    border-radius: 6px;
    padding: 5px 10px;
    font-size: 11px;
    color: var(--cyan);
    font-family: var(--font-data);
  }
  .hackathon-tag {
    font-size: 10px;
    color: var(--gold);
    font-family: var(--font-data);
    letter-spacing: 1px;
    opacity: 0.8;
  }

  /* MAIN LAYOUT */
  main {
    padding: 20px 24px;
    max-width: 1440px;
    margin: 0 auto;
    position: relative;
    z-index: 1;
  }

  /* TICKER */
  .ticker-bar {
    background: var(--bg2);
    border: 1px solid var(--border);
    border-radius: 8px;
    overflow: hidden;
    margin-bottom: 20px;
    height: 36px;
    display: flex;
    align-items: center;
  }
  .ticker-label {
    background: linear-gradient(135deg, var(--green), var(--cyan));
    color: #000;
    font-family: var(--font-data);
    font-size: 10px;
    font-weight: 700;
    letter-spacing: 1.5px;
    padding: 0 12px;
    height: 100%;
    display: flex;
    align-items: center;
    white-space: nowrap;
    flex-shrink: 0;
  }
  .ticker-track {
    display: flex;
    animation: ticker 30s linear infinite;
    gap: 0;
  }
  @keyframes ticker { from { transform: translateX(0); } to { transform: translateX(-50%); } }
  .ticker-item {
    display: flex;
    align-items: center;
    gap: 8px;
    padding: 0 20px;
    font-family: var(--font-data);
    font-size: 11px;
    white-space: nowrap;
    color: var(--text2);
    border-right: 1px solid var(--border);
  }
  .ticker-item .name { color: var(--white); font-weight: 700; }
  .ticker-item .up { color: var(--green); }
  .ticker-item .down { color: var(--red); }

  /* STAT CARDS */
  .stats-grid {
    display: grid;
    grid-template-columns: repeat(5, 1fr);
    gap: 12px;
    margin-bottom: 20px;
  }
  @media (max-width: 1100px) { .stats-grid { grid-template-columns: repeat(3, 1fr); } }
  .stat-card {
    background: var(--panel);
    border: 1px solid var(--border);
    border-radius: 10px;
    padding: 16px;
    position: relative;
    overflow: hidden;
    transition: border-color 0.3s;
  }
  .stat-card:hover { border-color: var(--border2); }
  .stat-card::before {
    content: '';
    position: absolute;
    top: 0; left: 0; right: 0;
    height: 2px;
    background: linear-gradient(90deg, var(--green), transparent);
  }
  .stat-card.cyan::before { background: linear-gradient(90deg, var(--cyan), transparent); }
  .stat-card.orange::before { background: linear-gradient(90deg, var(--orange), transparent); }
  .stat-card.gold::before { background: linear-gradient(90deg, var(--gold), transparent); }
  .stat-card.red::before { background: linear-gradient(90deg, var(--red), transparent); }
  .stat-label {
    font-size: 10px;
    letter-spacing: 1.5px;
    color: var(--muted);
    text-transform: uppercase;
    margin-bottom: 8px;
    font-family: var(--font-data);
  }
  .stat-value {
    font-size: 26px;
    font-weight: 800;
    color: var(--white);
    line-height: 1;
    margin-bottom: 6px;
    letter-spacing: -1px;
  }
  .stat-delta {
    font-family: var(--font-data);
    font-size: 11px;
    display: flex;
    align-items: center;
    gap: 4px;
  }
  .stat-delta.up { color: var(--green); }
  .stat-delta.down { color: var(--red); }

  /* MAIN GRID */
  .main-grid {
    display: grid;
    grid-template-columns: 1fr 340px;
    gap: 16px;
    margin-bottom: 16px;
  }
  .left-col { display: flex; flex-direction: column; gap: 16px; }
  .right-col { display: flex; flex-direction: column; gap: 16px; }

  /* PANEL */
  .panel {
    background: var(--panel);
    border: 1px solid var(--border);
    border-radius: 10px;
    overflow: hidden;
  }
  .panel-header {
    padding: 14px 18px;
    border-bottom: 1px solid var(--border);
    display: flex;
    align-items: center;
    justify-content: space-between;
  }
  .panel-title {
    font-size: 12px;
    font-weight: 700;
    letter-spacing: 2px;
    text-transform: uppercase;
    color: var(--text);
  }
  .panel-badge {
    font-family: var(--font-data);
    font-size: 10px;
    padding: 2px 8px;
    border-radius: 4px;
    letter-spacing: 1px;
  }
  .panel-badge.green { background: rgba(0,255,136,0.1); color: var(--green); border: 1px solid rgba(0,255,136,0.2); }
  .panel-badge.cyan { background: rgba(0,212,255,0.1); color: var(--cyan); border: 1px solid rgba(0,212,255,0.2); }
  .panel-badge.orange { background: rgba(255,107,53,0.1); color: var(--orange); border: 1px solid rgba(255,107,53,0.2); }
  .panel-body { padding: 18px; }

  /* PERFORMANCE CHART */
  .chart-wrap {
    position: relative;
    height: 220px;
    padding: 0 4px;
  }
  .chart-legend {
    display: flex;
    gap: 20px;
    padding: 12px 18px;
    border-top: 1px solid var(--border);
  }
  .legend-item {
    display: flex;
    align-items: center;
    gap: 8px;
    font-size: 12px;
  }
  .legend-dot { width: 8px; height: 8px; border-radius: 50%; }

  /* ALLOCATION */
  .allocation-wrap {
    display: flex;
    align-items: center;
    gap: 20px;
    padding: 18px;
  }
  .donut-wrap {
    position: relative;
    width: 140px;
    height: 140px;
    flex-shrink: 0;
  }
  .donut-center {
    position: absolute;
    inset: 0;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    pointer-events: none;
  }
  .donut-center-val {
    font-size: 18px;
    font-weight: 800;
    color: var(--white);
    letter-spacing: -0.5px;
  }
  .donut-center-lbl {
    font-family: var(--font-data);
    font-size: 8px;
    color: var(--muted);
    letter-spacing: 1px;
    margin-top: 2px;
  }
  .allocation-items { flex: 1; display: flex; flex-direction: column; gap: 10px; }
  .alloc-row {
    display: flex;
    align-items: center;
    gap: 8px;
  }
  .alloc-color { width: 10px; height: 10px; border-radius: 2px; flex-shrink: 0; }
  .alloc-name { font-size: 12px; color: var(--white); font-weight: 600; flex: 1; }
  .alloc-pct {
    font-family: var(--font-data);
    font-size: 11px;
    color: var(--text2);
    width: 36px;
    text-align: right;
  }
  .alloc-bar-wrap { flex: 2; height: 4px; background: var(--border); border-radius: 2px; overflow: hidden; }
  .alloc-bar { height: 100%; border-radius: 2px; transition: width 1s ease; }
  .alloc-yield {
    font-family: var(--font-data);
    font-size: 11px;
    color: var(--green);
    width: 44px;
    text-align: right;
  }

  /* HUMAN VS AI */
  .hvai-header {
    display: grid;
    grid-template-columns: 1fr auto 1fr;
    gap: 12px;
    align-items: center;
    padding: 16px 18px;
    background: rgba(0,0,0,0.2);
  }
  .hvai-side { text-align: center; }
  .hvai-label {
    font-size: 9px;
    letter-spacing: 2px;
    text-transform: uppercase;
    color: var(--muted);
    margin-bottom: 4px;
    font-family: var(--font-data);
  }
  .hvai-score {
    font-size: 28px;
    font-weight: 800;
    letter-spacing: -1px;
  }
  .hvai-score.ai { color: var(--green); }
  .hvai-score.human { color: var(--cyan); }
  .hvai-vs {
    font-family: var(--font-data);
    font-size: 11px;
    color: var(--muted);
    text-align: center;
    padding: 6px;
    border: 1px solid var(--border);
    border-radius: 6px;
  }
  .hvai-delta {
    font-size: 10px;
    font-family: var(--font-data);
  }
  .hvai-delta.positive { color: var(--green); }
  .hvai-bar-wrap { padding: 12px 18px; }
  .hvai-bar-track {
    height: 8px;
    background: var(--border);
    border-radius: 4px;
    overflow: hidden;
    position: relative;
  }
  .hvai-bar-ai {
    height: 100%;
    background: linear-gradient(90deg, var(--green), var(--cyan));
    border-radius: 4px;
    transition: width 1.5s ease;
  }
  .hvai-bar-labels {
    display: flex;
    justify-content: space-between;
    margin-top: 6px;
    font-family: var(--font-data);
    font-size: 10px;
    color: var(--muted);
  }

  /* DECISION FEED */
  .feed-list { max-height: 320px; overflow-y: auto; }
  .feed-list::-webkit-scrollbar { width: 4px; }
  .feed-list::-webkit-scrollbar-track { background: transparent; }
  .feed-list::-webkit-scrollbar-thumb { background: var(--border2); border-radius: 2px; }
  .feed-item {
    padding: 12px 18px;
    border-bottom: 1px solid var(--border);
    transition: background 0.2s;
    animation: feed-in 0.4s ease;
  }
  @keyframes feed-in {
    from { opacity: 0; transform: translateX(-8px); }
    to { opacity: 1; transform: translateX(0); }
  }
  .feed-item:hover { background: rgba(255,255,255,0.02); }
  .feed-item:last-child { border-bottom: none; }
  .feed-top {
    display: flex;
    align-items: center;
    gap: 8px;
    margin-bottom: 5px;
  }
  .feed-type {
    font-family: var(--font-data);
    font-size: 9px;
    letter-spacing: 1px;
    padding: 2px 6px;
    border-radius: 3px;
    text-transform: uppercase;
  }
  .feed-type.rebalance { background: rgba(0,255,136,0.1); color: var(--green); border: 1px solid rgba(0,255,136,0.2); }
  .feed-type.signal { background: rgba(0,212,255,0.1); color: var(--cyan); border: 1px solid rgba(0,212,255,0.2); }
  .feed-type.yield { background: rgba(255,208,96,0.1); color: var(--gold); border: 1px solid rgba(255,208,96,0.2); }
  .feed-type.risk { background: rgba(255,59,59,0.1); color: var(--red); border: 1px solid rgba(255,59,59,0.2); }
  .feed-time {
    font-family: var(--font-data);
    font-size: 10px;
    color: var(--muted);
    margin-left: auto;
  }
  .feed-text { font-size: 12px; color: var(--text); line-height: 1.5; }
  .feed-hash {
    font-family: var(--font-data);
    font-size: 9px;
    color: var(--muted);
    margin-top: 4px;
  }
  .feed-hash span { color: var(--cyan); cursor: pointer; text-decoration: underline; }

  /* SIGNAL MONITOR */
  .signal-grid {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 8px;
    padding: 14px 18px;
  }
  .signal-card {
    background: var(--bg2);
    border: 1px solid var(--border);
    border-radius: 8px;
    padding: 10px 12px;
  }
  .signal-source {
    font-family: var(--font-data);
    font-size: 9px;
    letter-spacing: 1.5px;
    color: var(--muted);
    text-transform: uppercase;
    margin-bottom: 4px;
  }
  .signal-val {
    font-size: 14px;
    font-weight: 700;
    color: var(--white);
    margin-bottom: 2px;
  }
  .signal-desc { font-size: 10px; color: var(--text2); }
  .signal-bar {
    height: 2px;
    border-radius: 1px;
    margin-top: 8px;
    transition: width 1s ease;
  }

  /* BOTTOM GRID */
  .bottom-grid {
    display: grid;
    grid-template-columns: 1fr 1fr 1fr;
    gap: 16px;
  }

  /* MINI METRICS */
  .mini-metrics { padding: 14px 18px; display: flex; flex-direction: column; gap: 10px; }
  .mini-row {
    display: flex;
    align-items: center;
    justify-content: space-between;
    font-size: 12px;
  }
  .mini-label { color: var(--text2); }
  .mini-val { font-family: var(--font-data); font-size: 12px; font-weight: 700; color: var(--white); }
  .mini-val.green { color: var(--green); }
  .mini-val.red { color: var(--red); }
  .mini-separator { height: 1px; background: var(--border); margin: 2px 0; }

  /* ERC-8004 PANEL */
  .nft-panel { padding: 16px 18px; }
  .nft-id-row {
    display: flex;
    align-items: center;
    gap: 10px;
    margin-bottom: 12px;
    background: var(--bg2);
    border: 1px solid var(--border);
    border-radius: 8px;
    padding: 10px 12px;
  }
  .nft-icon {
    width: 36px;
    height: 36px;
    background: linear-gradient(135deg, rgba(0,255,136,0.2), rgba(0,212,255,0.2));
    border: 1px solid rgba(0,212,255,0.3);
    border-radius: 8px;
    display: flex;
    align-items: center;
    justify-content: center;
    font-size: 16px;
    flex-shrink: 0;
  }
  .nft-info { flex: 1; }
  .nft-name { font-size: 13px; font-weight: 700; color: var(--white); }
  .nft-addr {
    font-family: var(--font-data);
    font-size: 10px;
    color: var(--cyan);
    cursor: pointer;
  }
  .milestones { display: flex; flex-direction: column; gap: 8px; }
  .milestone {
    display: flex;
    align-items: center;
    gap: 8px;
    font-size: 11px;
  }
  .milestone-icon { font-size: 14px; }
  .milestone-text { color: var(--text); flex: 1; }
  .milestone-date { font-family: var(--font-data); font-size: 10px; color: var(--muted); }
  .milestone-check { font-size: 12px; }

  /* FOOTER */
  footer {
    margin-top: 24px;
    border-top: 1px solid var(--border);
    padding: 16px 24px;
    display: flex;
    align-items: center;
    justify-content: space-between;
    font-family: var(--font-data);
    font-size: 10px;
    color: var(--muted);
    position: relative;
    z-index: 1;
  }
  footer span { color: var(--green); }

  /* GLOW EFFECTS */
  .glow-green { text-shadow: 0 0 20px rgba(0,255,136,0.5); }
  .glow-cyan { text-shadow: 0 0 20px rgba(0,212,255,0.5); }

  /* SCROLL AREA */
  .bottom-section { margin-bottom: 24px; }

  /* MINI CHART for signal */
  .mini-sparkline { height: 40px; }

  /* Animated number */
  .animated-num {
    display: inline-block;
    transition: color 0.3s;
  }
  .flash-green { animation: flash-g 0.6s ease; }
  .flash-red { animation: flash-r 0.6s ease; }
  @keyframes flash-g {
    0%, 100% { color: var(--white); }
    50% { color: var(--green); }
  }
  @keyframes flash-r {
    0%, 100% { color: var(--white); }
    50% { color: var(--red); }
  }
</style>
</head>
<body>

<!-- HEADER -->
<header>
  <div class="logo">
    <div class="logo-icon">MF</div>
    <div>
      <div class="logo-text">MantleFlow AI</div>
      <div class="logo-sub">AUTONOMOUS RWA YIELD INTELLIGENCE</div>
    </div>
  </div>
  <div class="header-right">
    <span class="hackathon-tag">⚡ MANTLE TURING TEST 2026 — AI×RWA</span>
    <div class="agent-badge">🤖 ERC-8004 <strong>#0041</strong></div>
    <div class="live-badge"><div class="live-dot"></div>LIVE ON MANTLE</div>
  </div>
</header>

<main>

  <!-- TICKER -->
  <div class="ticker-bar">
    <div class="ticker-label">LIVE SIGNALS</div>
    <div style="overflow:hidden;flex:1;display:flex">
      <div class="ticker-track" id="ticker">
        <!-- populated by JS -->
      </div>
    </div>
  </div>

  <!-- STATS -->
  <div class="stats-grid">
    <div class="stat-card">
      <div class="stat-label">Total AUM</div>
      <div class="stat-value animated-num" id="stat-aum">$847K</div>
      <div class="stat-delta up" id="stat-aum-delta">▲ +$12.4K today</div>
    </div>
    <div class="stat-card cyan">
      <div class="stat-label">Agent APY</div>
      <div class="stat-value animated-num" id="stat-apy">14.7%</div>
      <div class="stat-delta up">▲ +2.1% vs benchmark</div>
    </div>
    <div class="stat-card orange">
      <div class="stat-label">AI Alpha vs Human</div>
      <div class="stat-value animated-num glow-green" id="stat-alpha">+6.3%</div>
      <div class="stat-delta up">▲ AI winning — 40-day track</div>
    </div>
    <div class="stat-card gold">
      <div class="stat-label">Decisions Logged</div>
      <div class="stat-value animated-num" id="stat-decisions">1,847</div>
      <div class="stat-delta up">▲ +23 last hour</div>
    </div>
    <div class="stat-card">
      <div class="stat-label">ERC-8004 Score</div>
      <div class="stat-value animated-num" id="stat-score">98.2</div>
      <div class="stat-delta up">▲ Top 1% — on-chain</div>
    </div>
  </div>

  <!-- MAIN GRID -->
  <div class="main-grid">
    <div class="left-col">

      <!-- PERFORMANCE CHART -->
      <div class="panel">
        <div class="panel-header">
          <span class="panel-title">Cumulative Performance</span>
          <div style="display:flex;gap:8px">
            <span class="panel-badge cyan">40-DAY TRACK</span>
            <span class="panel-badge green">LIVE</span>
          </div>
        </div>
        <div class="chart-wrap" style="padding:14px 14px 0">
          <canvas id="perfChart"></canvas>
        </div>
        <div class="chart-legend">
          <div class="legend-item">
            <div class="legend-dot" style="background:var(--green)"></div>
            <span style="color:var(--text2);font-size:11px">MantleFlow AI Agent</span>
          </div>
          <div class="legend-item">
            <div class="legend-dot" style="background:var(--cyan)"></div>
            <span style="color:var(--text2);font-size:11px">Human Portfolio Manager</span>
          </div>
          <div class="legend-item">
            <div class="legend-dot" style="background:var(--muted)"></div>
            <span style="color:var(--text2);font-size:11px">USDY Benchmark</span>
          </div>
        </div>
      </div>

      <!-- PORTFOLIO ALLOCATION -->
      <div class="panel">
        <div class="panel-header">
          <span class="panel-title">Portfolio Allocation</span>
          <span class="panel-b
