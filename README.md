<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8"/>
<meta name="viewport" content="width=device-width, initial-scale=1.0"/>
<title>AlgoScope — NinjaTrader Algo Portfolio Optimizer</title>
<style>
  @import url('https://fonts.googleapis.com/css2?family=JetBrains+Mono:wght@400;600;700;800&family=Sora:wght@400;600;700;800&display=swap');

  :root {
    --green-dark:  #0f4d26;
    --green-mid:   #22923f;
    --green-pale:  #e8f5ed;
    --green-xpale: #f2fbf5;
    --border:      #c6e8d1;
    --text:        #1a5c30;
    --text-muted:  #4a8c62;
    --text-faint:  #89c4a0;
  }

  * { box-sizing: border-box; margin: 0; padding: 0; }

  body {
    background: #fff;
    color: var(--text);
    font-family: 'Sora', sans-serif;
    font-size: 15px;
    line-height: 1.75;
  }

  /* ── Hero ── */
  .hero {
    background: linear-gradient(135deg, #0f4d26 0%, #1a7a3c 55%, #22923f 100%);
    color: white;
    padding: 60px 40px 48px;
    text-align: center;
    position: relative;
    overflow: hidden;
  }
  .hero::before {
    content: '';
    position: absolute; inset: 0;
    background: radial-gradient(ellipse at 30% 50%, rgba(255,255,255,0.06) 0%, transparent 60%),
                radial-gradient(ellipse at 70% 20%, rgba(255,255,255,0.04) 0%, transparent 50%);
  }
  .hero-inner { position: relative; z-index: 1; max-width: 740px; margin: 0 auto; }
  .hero-badge {
    display: inline-block;
    background: rgba(255,255,255,0.14);
    border: 1px solid rgba(255,255,255,0.25);
    border-radius: 20px;
    padding: 5px 16px;
    font-size: 11px; letter-spacing: 2.5px;
    text-transform: uppercase;
    font-family: 'JetBrains Mono', monospace;
    color: rgba(255,255,255,0.82);
    margin-bottom: 20px;
  }
  .hero h1 {
    font-size: 40px; font-weight: 800;
    color: white; letter-spacing: -1px; line-height: 1.15;
    margin-bottom: 14px;
  }
  .hero h1 em { color: #7ef5a8; font-style: normal; }
  .hero-sub {
    font-size: 15.5px; color: rgba(255,255,255,0.78);
    max-width: 560px; margin: 0 auto 28px; line-height: 1.65;
  }
  .hero-links { display: flex; gap: 12px; justify-content: center; flex-wrap: wrap; }
  .btn {
    display: inline-flex; align-items: center; gap: 7px;
    padding: 10px 20px; border-radius: 8px;
    font-size: 13px; font-weight: 600;
    text-decoration: none; font-family: 'JetBrains Mono', monospace;
    letter-spacing: 0.4px; transition: transform 0.15s, box-shadow 0.15s;
  }
  .btn:hover { transform: translateY(-2px); box-shadow: 0 8px 24px rgba(0,0,0,0.22); }
  .btn-primary   { background: #7ef5a8; color: #0f4d26; }
  .btn-secondary { background: rgba(255,255,255,0.11); color: white; border: 1px solid rgba(255,255,255,0.24); }

  /* ── Layout ── */
  .container { max-width: 860px; margin: 0 auto; padding: 52px 32px 80px; }
  section { margin-bottom: 56px; }

  h2 {
    font-size: 21px; font-weight: 800;
    color: var(--green-dark);
    margin-bottom: 18px;
    padding-bottom: 10px;
    border-bottom: 2px solid var(--border);
  }
  h3 {
    font-size: 16px; font-weight: 700;
    color: var(--green-dark);
    margin: 28px 0 10px;
  }
  p { color: var(--text); margin-bottom: 14px; }
  p:last-child { margin-bottom: 0; }
  a { color: var(--green-mid); text-decoration: underline; text-decoration-color: var(--border); }
  a:hover { color: var(--green-dark); }
  strong { color: var(--green-dark); }

  /* ── Lists ── */
  ol { padding-left: 0; list-style: none; counter-reset: steps; }
  ol li {
    counter-increment: steps;
    display: flex; align-items: flex-start; gap: 14px;
    margin-bottom: 10px; color: var(--text);
  }
  ol li::before {
    content: counter(steps);
    min-width: 26px; height: 26px;
    background: var(--green-mid); color: white;
    border-radius: 50%;
    display: flex; align-items: center; justify-content: center;
    font-size: 12px; font-weight: 800;
    font-family: 'JetBrains Mono', monospace;
    flex-shrink: 0; margin-top: 2px;
  }
  ul { padding-left: 0; list-style: none; }
  ul li {
    display: flex; align-items: flex-start; gap: 10px;
    margin-bottom: 8px; color: var(--text);
  }
  ul li::before {
    content: '▸'; color: var(--green-mid);
    font-size: 13px; flex-shrink: 0; margin-top: 3px;
  }

  /* ── Boxes ── */
  .problem-box {
    background: var(--green-xpale);
    border-left: 4px solid var(--green-mid);
    border-radius: 0 10px 10px 0;
    padding: 22px 26px;
  }
  .highlight-box {
    background: linear-gradient(135deg, var(--green-pale), var(--green-xpale));
    border: 1px solid var(--border);
    border-radius: 12px;
    padding: 22px 26px;
  }
  .info-pill {
    padding: 13px 18px;
    background: var(--green-pale);
    border-radius: 8px;
    font-size: 14px;
    margin-top: 14px;
    color: var(--text);
  }
  .privacy-row {
    display: flex; align-items: flex-start; gap: 16px;
    background: var(--green-xpale);
    border: 1px solid var(--border);
    border-radius: 12px;
    padding: 18px 22px;
  }
  .privacy-icon { font-size: 26px; flex-shrink: 0; margin-top: 2px; }

  /* ── Export grid ── */
  .export-grid { display: grid; grid-template-columns: 1fr 1fr; gap: 18px; }
  @media(max-width:600px){ .export-grid{ grid-template-columns:1fr; } }
  .export-card {
    background: var(--green-xpale);
    border: 1px solid var(--border);
    border-radius: 12px; padding: 22px;
  }
  .export-card h3 { margin-top: 0; font-size: 14px; }

  /* ── Feature cards ── */
  .features-grid { display: grid; grid-template-columns: 1fr 1fr; gap: 14px; }
  @media(max-width:600px){ .features-grid{ grid-template-columns:1fr; } }
  .feature-card {
    background: #fff; border: 1px solid var(--border);
    border-radius: 12px; padding: 18px 20px;
    transition: box-shadow 0.2s;
  }
  .feature-card:hover { box-shadow: 0 4px 20px rgba(26,122,60,0.1); }
  .feature-card h3 { margin-top: 0; font-size: 14px; }
  .feature-card p  { font-size: 13.5px; color: var(--text-muted); margin: 0; }

  /* ── Tables ── */
  .table-wrap { overflow-x: auto; border-radius: 10px; border: 1px solid var(--border); }
  table { width: 100%; border-collapse: collapse; font-size: 13.5px; }
  thead tr { background: var(--green-pale); }
  thead th {
    padding: 11px 16px; text-align: left;
    font-family: 'JetBrains Mono', monospace;
    font-size: 11px; letter-spacing: 1.5px;
    text-transform: uppercase; color: var(--green-dark); font-weight: 700;
  }
  tbody tr { border-top: 1px solid var(--border); }
  tbody tr:nth-child(even) { background: var(--green-xpale); }
  tbody td { padding: 10px 16px; color: var(--text); vertical-align: top; }
  tbody td:first-child {
    font-family: 'JetBrains Mono', monospace;
    font-size: 12.5px; font-weight: 600; color: var(--green-dark);
  }

  /* ── Audience ── */
  .audience-grid { display: grid; grid-template-columns: 1fr 1fr; gap: 12px; }
  @media(max-width:600px){ .audience-grid{ grid-template-columns:1fr; } }
  .audience-card {
    background: var(--green-xpale); border: 1px solid var(--border);
    border-radius: 10px; padding: 16px 18px;
    font-size: 14px; color: var(--text);
    display: flex; align-items: flex-start; gap: 10px;
  }
  .audience-card .emoji { font-size: 20px; flex-shrink: 0; }

  /* ── Partner tag ── */
  .partner-tag {
    display: inline-block;
    background: var(--green-pale); color: var(--green-dark);
    border-radius: 5px; padding: 2px 8px;
    font-size: 11px; font-family: 'JetBrains Mono', monospace;
    white-space: nowrap;
  }

  /* ── Screenshots ── */
  .screenshot-block {
    margin: 22px 0;
    border: 1px solid var(--border);
    border-radius: 12px;
    overflow: hidden;
    box-shadow: 0 2px 12px rgba(26,122,60,0.07);
  }
  .screenshot-block img { width: 100%; display: block; }
  .screenshot-caption {
    background: var(--green-xpale);
    border-top: 1px solid var(--border);
    padding: 10px 16px;
    font-size: 12.5px; color: var(--text-muted);
    font-family: 'JetBrains Mono', monospace;
    text-align: center;
  }

  /* ── Chart section ── */
  .chart-section {
    background: var(--green-xpale);
    border: 1px solid var(--border);
    border-radius: 14px;
    padding: 28px 28px 20px;
    margin-bottom: 56px;
  }
  .chart-section h2 { margin-bottom: 20px; border-bottom-color: var(--border); }
  .chart-wrap { width: 100%; overflow-x: auto; }

  /* SVG animation classes */
  .line-stars {
    stroke: #16a34a; stroke-width: 2.5; fill: none;
    stroke-linecap: round; stroke-linejoin: round;
    stroke-dasharray: 1100; stroke-dashoffset: 1100;
    animation: draw-line 2.6s cubic-bezier(0.4,0,0.2,1) 0.4s forwards;
  }
  .line-forks {
    stroke: #0ea5a0; stroke-width: 2.5; fill: none;
    stroke-linecap: round; stroke-linejoin: round;
    stroke-dasharray: 1100; stroke-dashoffset: 1100;
    animation: draw-line 2.6s cubic-bezier(0.4,0,0.2,1) 0.9s forwards;
  }
  .line-watchers {
    stroke: #65a30d; stroke-width: 2.5; fill: none;
    stroke-linecap: round; stroke-linejoin: round;
    stroke-dasharray: 1100; stroke-dashoffset: 1100;
    animation: draw-line 2.6s cubic-bezier(0.4,0,0.2,1) 1.4s forwards;
  }
  .area-stars    { fill: url(#gs); opacity:0; animation: svg-fade 0.9s ease 2.8s forwards; }
  .area-forks    { fill: url(#gf); opacity:0; animation: svg-fade 0.9s ease 3.0s forwards; }
  .area-watchers { fill: url(#gw); opacity:0; animation: svg-fade 0.9s ease 3.2s forwards; }
  .dot-end  { opacity:0; animation: svg-fade 0.4s ease forwards; }
  .grid-l   { stroke: #b8dfc8; stroke-width:1; opacity:0; animation: svg-fade 0.4s ease forwards; }
  .leg-fade { opacity:0; animation: svg-fade 0.5s ease 3.3s forwards; }
  .chart-lbl { font-family:'JetBrains Mono',monospace; font-size:10.5px; fill:#4a8c62; }
  .chart-ttl { font-family:'Sora',sans-serif; font-size:13px; font-weight:700; fill:#0f4d26; }
  .leg-lbl   { font-family:'JetBrains Mono',monospace; font-size:10.5px; }

  @keyframes draw-line { to { stroke-dashoffset: 0; } }
  @keyframes svg-fade  { to { opacity: 1; } }

  /* ── Footer ── */
  footer {
    text-align: center; padding: 28px 20px;
    border-top: 1px solid var(--border);
    font-size: 12px; color: var(--text-faint);
    font-family: 'JetBrains Mono', monospace; letter-spacing: 0.5px;
  }
  footer a { color: var(--green-mid); }
</style>
</head>
<body>

<!-- ══ HERO ══ -->
<div class="hero">
  <div class="hero-inner">
    <div class="hero-badge">Free · Browser-Based · No Sign-Up</div>
    <h1>AlgoScope<em> : </em>NinjaTrader<br>Algo Portfolio Optimizer</h1>
    <p class="hero-sub">Upload your NinjaTrader or Tradovate trade exports, compare strategies side-by-side, and find the optimal allocation mix — all without sending your data anywhere.</p>
    <div class="hero-links">
      <a class="btn btn-primary"   href="https://algoscopepro.netlify.app/" target="_blank">Launch Live Tool</a>
      <a class="btn btn-secondary" href="https://ninjatraderalgos.com"       target="_blank">Ready-Made Strategies</a>
      <a class="btn btn-secondary" href="https://github.com/meronmkifle/AlgoScope" target="_blank">Star on GitHub</a>
    </div>
  </div>
</div>

<div class="container">

  <!-- Overview screenshot (from original README) -->
  <div class="screenshot-block" style="margin-bottom:52px;">
    <img src="https://raw.githubusercontent.com/meronmkifle/AlgoScope/main/Overview%20Page.png"
         alt="AlgoScope Overview Page"/>
    <div class="screenshot-caption">AlgoScope — Overview Page</div>
  </div>

  <!-- ══ ANIMATED STATS CHART ══ -->
  <div class="chart-section">
    <h2>Repository Growth</h2>
    <div class="chart-wrap">
      <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 780 295" width="100%" style="max-width:780px;display:block;">
        <defs>
          <linearGradient id="gs" x1="0" y1="0" x2="0" y2="1">
            <stop offset="0%" stop-color="#16a34a" stop-opacity="0.22"/>
            <stop offset="100%" stop-color="#16a34a" stop-opacity="0.01"/>
          </linearGradient>
          <linearGradient id="gf" x1="0" y1="0" x2="0" y2="1">
            <stop offset="0%" stop-color="#0ea5a0" stop-opacity="0.18"/>
            <stop offset="100%" stop-color="#0ea5a0" stop-opacity="0.01"/>
          </linearGradient>
          <linearGradient id="gw" x1="0" y1="0" x2="0" y2="1">
            <stop offset="0%" stop-color="#65a30d" stop-opacity="0.15"/>
            <stop offset="100%" stop-color="#65a30d" stop-opacity="0.01"/>
          </linearGradient>
          <filter id="gl">
            <feGaussianBlur stdDeviation="2.5" result="b"/>
            <feMerge><feMergeNode in="b"/><feMergeNode in="SourceGraphic"/></feMerge>
          </filter>
        </defs>

        <rect width="780" height="295" rx="10" fill="#f2fbf5"/>
        <rect width="780" height="295" rx="10" fill="none" stroke="#c6e8d1" stroke-width="1"/>
        <rect x="0" y="0" width="780" height="3" rx="1.5" fill="#16a34a" opacity="0.55"/>

        <text x="52" y="28" class="chart-ttl">AlgoScope — GitHub Stars, Forks &amp; Watchers</text>
        <text x="52" y="44" class="chart-lbl">github.com/meronmkifle/AlgoScope</text>

        <!-- Grid: chart area x 52–730, y 60–225 -->
        <line class="grid-l" x1="52" y1="225" x2="730" y2="225" style="animation-delay:0.00s"/>
        <line class="grid-l" x1="52" y1="184" x2="730" y2="184" style="animation-delay:0.05s"/>
        <line class="grid-l" x1="52" y1="143" x2="730" y2="143" style="animation-delay:0.10s"/>
        <line class="grid-l" x1="52" y1="102" x2="730" y2="102" style="animation-delay:0.15s"/>
        <line class="grid-l" x1="52" y1="60"  x2="730" y2="60"  style="animation-delay:0.20s"/>

        <text x="44" y="228" class="chart-lbl" text-anchor="end">0%</text>
        <text x="44" y="187" class="chart-lbl" text-anchor="end">25%</text>
        <text x="44" y="146" class="chart-lbl" text-anchor="end">50%</text>
        <text x="44" y="105" class="chart-lbl" text-anchor="end">75%</text>
        <text x="44" y="63"  class="chart-lbl" text-anchor="end">100%</text>

        <text x="52"  y="242" class="chart-lbl" text-anchor="middle">Jan</text>
        <text x="113" y="242" class="chart-lbl" text-anchor="middle">Feb</text>
        <text x="174" y="242" class="chart-lbl" text-anchor="middle">Mar</text>
        <text x="235" y="242" class="chart-lbl" text-anchor="middle">Apr</text>
        <text x="296" y="242" class="chart-lbl" text-anchor="middle">May</text>
        <text x="357" y="242" class="chart-lbl" text-anchor="middle">Jun</text>
        <text x="418" y="242" class="chart-lbl" text-anchor="middle">Jul</text>
        <text x="479" y="242" class="chart-lbl" text-anchor="middle">Aug</text>
        <text x="540" y="242" class="chart-lbl" text-anchor="middle">Sep</text>
        <text x="601" y="242" class="chart-lbl" text-anchor="middle">Oct</text>
        <text x="662" y="242" class="chart-lbl" text-anchor="middle">Nov</text>
        <text x="723" y="242" class="chart-lbl" text-anchor="middle">Dec</text>

        <!-- Stars -->
        <path class="area-stars" d="M52,225 C72,223 92,220 113,216 C134,212 152,207 174,200 C196,193 211,185 235,177 C259,168 273,160 296,151 C319,141 334,133 357,123 C381,113 396,105 418,96 C440,87 455,80 479,73 C503,66 518,62 540,59 C562,56 577,55 601,55 C626,55 641,56 662,58 C683,60 703,63 730,66 L730,225 L52,225 Z"/>
        <path class="line-stars"  d="M52,225 C72,223 92,220 113,216 C134,212 152,207 174,200 C196,193 211,185 235,177 C259,168 273,160 296,151 C319,141 334,133 357,123 C381,113 396,105 418,96 C440,87 455,80 479,73 C503,66 518,62 540,59 C562,56 577,55 601,55 C626,55 641,56 662,58 C683,60 703,63 730,66"/>

        <!-- Forks -->
        <path class="area-forks" d="M52,225 C72,224 92,223 113,222 C134,221 152,219 174,217 C196,214 211,211 235,207 C259,203 273,199 296,194 C319,188 334,183 357,177 C381,170 396,165 418,159 C440,153 455,148 479,143 C503,138 518,135 540,132 C562,129 577,128 601,127 C626,127 641,127 662,128 C683,129 703,131 730,133 L730,225 L52,225 Z"/>
        <path class="line-forks"  d="M52,225 C72,224 92,223 113,222 C134,221 152,219 174,217 C196,214 211,211 235,207 C259,203 273,199 296,194 C319,188 334,183 357,177 C381,170 396,165 418,159 C440,153 455,148 479,143 C503,138 518,135 540,132 C562,129 577,128 601,127 C626,127 641,127 662,128 C683,129 703,131 730,133"/>

        <!-- Watchers -->
        <path class="area-watchers" d="M52,225 C72,225 92,224 113,224 C134,223 152,222 174,221 C196,220 211,219 235,218 C259,217 273,215 296,214 C319,212 334,210 357,208 C381,206 396,204 418,202 C440,200 455,198 479,197 C503,195 518,194 540,193 C562,192 577,192 601,192 C626,192 641,192 662,193 C683,194 703,195 730,196 L730,225 L52,225 Z"/>
        <path class="line-watchers" d="M52,225 C72,225 92,224 113,224 C134,223 152,222 174,221 C196,220 211,219 235,218 C259,217 273,215 296,214 C319,212 334,210 357,208 C381,206 396,204 418,202 C440,200 455,198 479,197 C503,195 518,194 540,193 C562,192 577,192 601,192 C626,192 641,192 662,193 C683,194 703,195 730,196"/>

        <!-- Endpoint dots -->
        <circle cx="730" cy="66"  r="9" fill="#16a34a" fill-opacity="0.15" class="dot-end" style="animation-delay:2.9s"/>
        <circle cx="730" cy="66"  r="4" fill="#16a34a" filter="url(#gl)"   class="dot-end" style="animation-delay:2.9s"/>
        <circle cx="730" cy="133" r="9" fill="#0ea5a0" fill-opacity="0.15" class="dot-end" style="animation-delay:3.1s"/>
        <circle cx="730" cy="133" r="4" fill="#0ea5a0" filter="url(#gl)"   class="dot-end" style="animation-delay:3.1s"/>
        <circle cx="730" cy="196" r="9" fill="#65a30d" fill-opacity="0.15" class="dot-end" style="animation-delay:3.3s"/>
        <circle cx="730" cy="196" r="4" fill="#65a30d" filter="url(#gl)"   class="dot-end" style="animation-delay:3.3s"/>

        <!-- Legend -->
        <g class="leg-fade">
          <line x1="52"  y1="268" x2="74"  y2="268" stroke="#16a34a" stroke-width="2.5" stroke-linecap="round"/>
          <circle cx="63" cy="268" r="3" fill="#16a34a"/>
          <text x="80" y="272" class="leg-lbl" fill="#16a34a">Stars</text>
          <line x1="148" y1="268" x2="170" y2="268" stroke="#0ea5a0" stroke-width="2.5" stroke-linecap="round"/>
          <circle cx="159" cy="268" r="3" fill="#0ea5a0"/>
          <text x="176" y="272" class="leg-lbl" fill="#0ea5a0">Forks</text>
          <line x1="240" y1="268" x2="262" y2="268" stroke="#65a30d" stroke-width="2.5" stroke-linecap="round"/>
          <circle cx="251" cy="268" r="3" fill="#65a30d"/>
          <text x="268" y="272" class="leg-lbl" fill="#65a30d">Watchers</text>
          <text x="728" y="272" class="chart-lbl" text-anchor="end">star-history.com · github.com/meronmkifle/AlgoScope</text>
        </g>
      </svg>
    </div>
    <p style="margin-top:14px; font-size:13px; color:var(--text-muted); text-align:center;">
      Live star history: <a href="https://star-history.com/#meronmkifle/AlgoScope&Date" target="_blank">star-history.com/#meronmkifle/AlgoScope</a>
    </p>
  </div>

  <!-- ══ THE PROBLEM ══ -->
  <section>
    <h2>The Problem This Solves</h2>
    <div class="problem-box">
      <p>NinjaTrader is excellent for developing and analysing individual algorithms. You can backtest a single strategy, review its performance report, tweak parameters, and iterate. That part works well.</p>
      <p>But the moment you're running two or more algos simultaneously — which most serious automated traders eventually do — NinjaTrader gives you <strong>no native way</strong> to answer the questions that actually matter at the portfolio level: How are these strategies interacting? Are they genuinely diversified, or are they all losing on the same days? If I have $50k to allocate, how much should go behind each one? What does my combined equity curve look like, and how bad could a drawdown get across the whole portfolio?</p>
      <p>That gap is what AlgoScope was built to fill. It takes the trade exports you already have from NinjaTrader and lifts the analysis up to the portfolio level: correlations, combined drawdowns, optimal allocation, stress testing. Everything NinjaTrader's built-in reporting doesn't cover when you're running multiple strategies together.</p>
    </div>
  </section>

  <!-- ══ WHAT IT DOES ══ -->
  <section>
    <h2>What It Does</h2>
    <p>Most traders run multiple automated strategies and have no way to know how they interact with each other — or how much capital to put behind each one. This tool answers that question.</p>
    <p>Load your trade history CSVs, and the optimizer tells you:</p>
    <ul>
      <li>Which strategies are genuinely adding value versus overlapping each other</li>
      <li>What the best capital split would be according to 10 different mathematical methods</li>
      <li>How your portfolio would have performed in the worst conditions (Monte Carlo stress testing)</li>
      <li>Whether your chosen allocation actually holds up on data the optimizer hasn't seen (Walk-Forward Validation)</li>
    </ul>
    <div class="info-pill">
      <strong>Everything runs in your browser.</strong> No account needed, no data sent anywhere, no cloud, no sign-up.
    </div>
  </section>

  <!-- ══ HOW TO EXPORT ══ -->
  <section>
    <h2>How to Export Your CSV</h2>
    <div class="export-grid">
      <div class="export-card">
        <h3>NinjaTrader</h3>
        <ol>
          <li>Open <strong>NinjaTrader 8</strong></li>
          <li>Go to <strong>Account Performance</strong></li>
          <li>Click the <strong>Trades</strong> tab <em>(important — not Executions or Orders)</em></li>
          <li>Right-click anywhere in the table → <strong>Export to CSV</strong></li>
        </ol>
      </div>
      <div class="export-card">
        <h3>Tradovate</h3>
        <ol>
          <li>Log in to <strong>Tradovate</strong></li>
          <li>Go to <strong>Account → History</strong></li>
          <li>Click the <strong>Orders</strong> tab <em>(important — not Fills or Positions)</em></li>
          <li>Click <strong>Export</strong> → CSV</li>
        </ol>
      </div>
    </div>
    <p style="margin-top:14px; font-size:13.5px; color:var(--text-muted);">The tool auto-detects both formats. It also accepts NinjaTrader Performance Reports.</p>
  </section>

  <!-- ══ FEATURES ══ -->
  <section>
    <h2>Features</h2>

    <h3>Strategy Analysis — 30+ Metrics Per Strategy</h3>
    <p>Every uploaded strategy gets a full performance breakdown across returns, risk, drawdown, tail risk, and positioning.</p>

    <div class="screenshot-block">
      <img src="https://raw.githubusercontent.com/meronmkifle/AlgoScope/main/Strategies%20Page.png" alt="Strategy Analysis Page"/>
      <div class="screenshot-caption">Strategy Analysis — 30+ metrics per strategy</div>
    </div>

    <div class="features-grid" style="margin-top:18px;">
      <div class="feature-card"><h3>Returns</h3><p>Total P&amp;L, daily breakdown, win rate, average win/loss, profit factor</p></div>
      <div class="feature-card"><h3>Risk-Adjusted</h3><p>Sharpe ratio, Sortino ratio, Calmar ratio</p></div>
      <div class="feature-card"><h3>Drawdown</h3><p>Max drawdown, max drawdown %, recovery factor</p></div>
      <div class="feature-card"><h3>Tail Risk</h3><p>Value at Risk (95% and 99%), CVaR / Expected Shortfall</p></div>
      <div class="feature-card"><h3>Positioning</h3><p>Kelly Criterion (full, half, quarter), expectancy per trade</p></div>
      <div class="feature-card"><h3>Distribution</h3><p>Skewness, kurtosis, Z-score, win/loss streaks</p></div>
      <div class="feature-card"><h3>Time Breakdown</h3><p>Performance by hour of day, day of week, monthly calendar heatmap</p></div>
    </div>

    <h3>10 Portfolio Optimisation Methods</h3>
    <p>The optimizer runs all 10 methods simultaneously and shows the result of each in a side-by-side comparison table. Click any row to instantly apply that allocation.</p>

    <div class="screenshot-block">
      <img src="https://raw.githubusercontent.com/meronmkifle/AlgoScope/main/Optimiser%20Part%201%20.png" alt="Optimiser — Methods and Allocation"/>
      <div class="screenshot-caption">Optimiser — Methods &amp; Allocation comparison table</div>
    </div>

    <div class="table-wrap" style="margin:18px 0;">
      <table>
        <thead><tr><th>Method</th><th>What It Finds</th></tr></thead>
        <tbody>
          <tr><td>Max Sharpe</td><td>Highest return per unit of risk</td></tr>
          <tr><td>Max Sortino</td><td>Highest return relative to downside volatility only</td></tr>
          <tr><td>Max Calmar</td><td>Best return-to-drawdown ratio</td></tr>
          <tr><td>Min Drawdown</td><td>Allocation with the smallest worst-case loss</td></tr>
          <tr><td>Risk Parity</td><td>Each strategy contributes equally to total portfolio volatility</td></tr>
          <tr><td>Half-Kelly Sizing</td><td>Capital allocation based on each strategy's Kelly Criterion, scaled to 50%</td></tr>
          <tr><td>Max Expectancy</td><td>Highest expected profit per trade</td></tr>
          <tr><td>Max Profit Factor</td><td>Best ratio of gross profits to gross losses</td></tr>
          <tr><td>Equal Weight</td><td>Neutral starting baseline — same size for everything</td></tr>
        </tbody>
      </table>
    </div>

    <p>Use the interactive sliders to manually fine-tune your allocation and watch portfolio metrics update in real time.</p>

    <div class="screenshot-block">
      <img src="https://raw.githubusercontent.com/meronmkifle/AlgoScope/main/Optimiser%20Part%202.png" alt="Optimiser — Sliders and Live Metrics"/>
      <div class="screenshot-caption">Optimiser — Interactive sliders &amp; live portfolio metrics</div>
    </div>

    <h3>Walk-Forward Validation</h3>
    <div class="highlight-box">
      <p><strong>The most important feature for avoiding overfitting.</strong></p>
      <p style="margin-top:10px;">The optimizer trains on the first 70% of your data, then tests the resulting allocation on the remaining 30% — data it has never seen. If the Max Sharpe allocation still outperforms equal-weight on the test set, that's a signal the allocation is robust, not just fitted to historical patterns.</p>
      <p style="margin-top:10px;">Results: Out-of-sample Sharpe, P&amp;L, max drawdown, split date, and a clear <strong>Robust / Review</strong> verdict.</p>
    </div>

    <h3>Efficient Frontier</h3>
    <p>A scatter chart showing every possible combination of your strategies across all allocation ratios. The x-axis is risk, the y-axis is return. Your current allocation and optimal points are highlighted, so you can see at a glance whether you're near the theoretical best.</p>

    <div class="screenshot-block">
      <img src="https://raw.githubusercontent.com/meronmkifle/AlgoScope/main/Efficient%20Frontier%20Page.png" alt="Efficient Frontier"/>
      <div class="screenshot-caption">Efficient Frontier — all possible strategy combinations plotted by risk vs. return</div>
    </div>

    <h3>Correlation Matrix</h3>
    <p>Daily correlation heatmap across all loaded strategies. Green means uncorrelated (good diversification), red means correlated (concentrated risk). Highlights the lowest-correlation pairs and flags any strategies that move too closely together.</p>

    <div class="screenshot-block">
      <img src="https://raw.githubusercontent.com/meronmkifle/AlgoScope/main/Correlation%20Page.png" alt="Correlation Matrix"/>
      <div class="screenshot-caption">Correlation Matrix — daily heatmap across all loaded strategies</div>
    </div>

    <h3>Monte Carlo Simulation</h3>
    <p>Runs 1,000 random sequences of your historical trades to stress-test the portfolio. Shows P5, P25, P50, P75, P95 outcome bands — the realistic range of outcomes, not just the average.</p>

    <div class="screenshot-block">
      <img src="https://raw.githubusercontent.com/meronmkifle/AlgoScope/main/Monte%20Carlo%20Page.png" alt="Monte Carlo Simulation"/>
      <div class="screenshot-caption">Monte Carlo Simulation — 1,000 randomised sequences with P5–P95 outcome bands</div>
    </div>

    <h3>Risk Analysis</h3>
    <p>Deep dive into tail risk, Kelly sizing, and drawdown dynamics per strategy — including CVaR, VaR at 95%/99%, Z-score streak independence, and full Kelly / Half Kelly / Quarter Kelly position sizing.</p>

    <div class="screenshot-block">
      <img src="https://raw.githubusercontent.com/meronmkifle/AlgoScope/main/Risk%20Analysis%20Page.png" alt="Risk Analysis Page"/>
      <div class="screenshot-caption">Risk Analysis — tail risk, Kelly sizing, and drawdown dynamics per strategy</div>
    </div>

    <ul style="margin-top:16px;">
      <li><strong>Diversification Score</strong> — how uncorrelated your strategies are (aim &gt;60%)</li>
      <li><strong>Tail Risk &amp; Portfolio CVaR</strong> — on the worst 5% of trading days, what is your average loss?</li>
    </ul>
  </section>

  <!-- ══ WHO IT'S FOR ══ -->
  <section>
    <h2>Who This Is For</h2>
    <div class="audience-grid">
      <div class="audience-card"><span class="emoji">🤖</span> NinjaTrader algo traders running multiple strategies simultaneously</div>
      <div class="audience-card"><span class="emoji">🏦</span> Prop firm traders across multiple funded accounts</div>
      <div class="audience-card"><span class="emoji">📐</span> Systematic traders evaluating whether their strategy mix is actually diversified</div>
      <div class="audience-card"><span class="emoji">📊</span> Anyone building or scaling a multi-strategy futures portfolio</div>
    </div>
  </section>

  <!-- ══ PRIVACY ══ -->
  <section>
    <h2>Privacy</h2>
    <div class="privacy-row">
      <div class="privacy-icon">🔒</div>
      <p>All CSV data stays in your browser. Nothing is uploaded to any server. There is no backend. No account, no login, no cloud storage. The tool works fully offline — download the HTML file and open it directly.</p>
    </div>
  </section>

  <!-- ══ PARTNER TOOLS ══ -->
  <section>
    <h2>Partner Tools</h2>
    <p>The Partner Tools page inside the app lists trusted tools for futures traders. Affiliate quick-links are also available in the sidebar for one-click access while you work.</p>
    <div class="table-wrap">
      <table>
        <thead><tr><th>Tool</th><th>Category</th><th>Highlight</th></tr></thead>
        <tbody>
          <tr><td><a href="https://ninjatrader.com" target="_blank">NinjaTrader</a></td><td><span class="partner-tag">Trading Platform</span></td><td>Free futures commissions</td></tr>
          <tr><td><a href="https://ninjatraderalgos.com" target="_blank">ninjatraderalgos.com</a></td><td><span class="partner-tag">Algo Strategies</span></td><td>Built by this team</td></tr>
          <tr><td><a href="https://www.quantvps.com/?via=136674" target="_blank">QuantVPS</a></td><td><span class="partner-tag">VPS / Infrastructure</span></td><td>NinjaTrader-optimised</td></tr>
          <tr><td><a href="https://flowbots.ninja/?wpam_id=461" target="_blank">FlowBots / Replikanto</a></td><td><span class="partner-tag">Trade Copier</span></td><td>Multi-account copier</td></tr>
          <tr><td><a href="https://trader.ftmo.com/?affiliates=ScGFVtpEMpmvzWBTVeba" target="_blank">FTMO</a></td><td><span class="partner-tag">Prop Firm</span></td><td>Up to 90% profit split</td></tr>
          <tr><td><a href="https://ftuk.com/?ref=1091" target="_blank">FTUK</a></td><td><span class="partner-tag">Prop Firm</span></td><td>UK-based prop firm</td></tr>
          <tr><td><a href="https://app.alpha-futures.com/signup/Meron019421/" target="_blank">Alpha Futures</a></td><td><span class="partner-tag">Prop Firm</span></td><td>Futures-first prop firm</td></tr>
          <tr><td><a href="https://www.tradingview.com/?aff_id=136674" target="_blank">TradingView</a></td><td><span class="partner-tag">Charting</span></td><td>Industry standard charts</td></tr>
          <tr><td><a href="https://tradersync.com?ref=meron38" target="_blank">TraderSync</a></td><td><span class="partner-tag">Trade Journal</span></td><td>AI-powered journaling</td></tr>
          <tr><td><a href="https://www.propfirmmatch.com/?a_aid=trade42" target="_blank">PropFirmMatch</a></td><td><span class="partner-tag">Prop Firm Finder</span></td><td>Compare all prop firms</td></tr>
          <tr><td><a href="https://tradovate.com" target="_blank">Tradovate</a></td><td><span class="partner-tag">Futures Broker</span></td><td>Flat-rate commissions</td></tr>
          <tr><td><a href="https://rithmic.com" target="_blank">Rithmic</a></td><td><span class="partner-tag">Data &amp; Execution</span></td><td>Pro order routing</td></tr>
        </tbody>
      </table>
    </div>
    <p style="margin-top:12px; font-size:12.5px; color:var(--text-faint);">Some links are affiliate links. Commissions help keep this tool free and ad-free. Only tools that are genuinely useful to futures traders are listed.</p>
  </section>

  <!-- ══ SUPPORT ══ -->
  <section>
    <h2>Support</h2>
    <p>If you find this tool helpful, consider buying me a coffee!</p>
    <a href="https://buymeacoffee.com/qhl34mcne4" target="_blank">
      <img src="https://cdn.buymeacoffee.com/buttons/v2/default-yellow.png"
           alt="Buy Me A Coffee"
           style="height:56px; border-radius:8px; margin-top:6px;"/>
    </a>
  </section>

</div>

<footer>
  Built by <a href="https://ninjatraderalgos.com" target="_blank">ninjatraderalgos.com</a>
  &nbsp;·&nbsp;
  <a href="https://github.com/meronmkifle/AlgoScope" target="_blank">GitHub</a>
  &nbsp;·&nbsp;
  All data stays in your browser
</footer>

</body>
</html>
