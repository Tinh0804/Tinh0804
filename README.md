<!DOCTYPE html>
<html lang="vi">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Lê Hoàng Quách Tỉnh — Backend Engineer</title>
<link href="https://fonts.googleapis.com/css2?family=JetBrains+Mono:ital,wght@0,300;0,400;0,600;0,700;1,400&family=Space+Grotesk:wght@300;400;500;600;700&display=swap" rel="stylesheet">
<style>
  :root {
    --cyan: #00f5ff;
    --cyan-dim: #00c4cc;
    --cyan-dark: #003d40;
    --green: #39ff14;
    --purple: #b347ea;
    --orange: #ff6b35;
    --bg: #050b13;
    --bg2: #081420;
    --bg3: #0d1f30;
    --border: rgba(0,245,255,0.15);
    --border-bright: rgba(0,245,255,0.4);
    --text: #cde8f0;
    --text-dim: #6a8fa0;
    --mono: 'JetBrains Mono', monospace;
    --sans: 'Space Grotesk', sans-serif;
  }

  * { margin: 0; padding: 0; box-sizing: border-box; }

  body {
    background: var(--bg);
    color: var(--text);
    font-family: var(--sans);
    min-height: 100vh;
    overflow-x: hidden;
    line-height: 1.6;
  }

  /* ── CANVAS BACKGROUND ── */
  #canvas-bg {
    position: fixed; top: 0; left: 0;
    width: 100%; height: 100%;
    pointer-events: none; z-index: 0;
    opacity: 0.35;
  }

  /* ── SCAN LINE OVERLAY ── */
  body::after {
    content: '';
    position: fixed; top: 0; left: 0;
    width: 100%; height: 100%;
    background: repeating-linear-gradient(
      0deg,
      transparent,
      transparent 2px,
      rgba(0,0,0,0.03) 2px,
      rgba(0,0,0,0.03) 4px
    );
    pointer-events: none; z-index: 1000;
  }

  /* ── LAYOUT ── */
  .container {
    position: relative; z-index: 2;
    max-width: 900px;
    margin: 0 auto;
    padding: 60px 32px 100px;
  }

  /* ── HERO ── */
  .hero {
    text-align: center;
    padding: 80px 0 60px;
    position: relative;
  }

  .hero-glow {
    position: absolute; top: 50%; left: 50%;
    transform: translate(-50%, -50%);
    width: 600px; height: 600px;
    background: radial-gradient(circle, rgba(0,245,255,0.06) 0%, transparent 70%);
    pointer-events: none;
    animation: pulse-glow 4s ease-in-out infinite;
  }

  @keyframes pulse-glow {
    0%, 100% { opacity: 0.5; transform: translate(-50%, -50%) scale(1); }
    50% { opacity: 1; transform: translate(-50%, -50%) scale(1.1); }
  }

  .avatar-wrap {
    position: relative;
    display: inline-block;
    margin-bottom: 32px;
  }

  .avatar {
    width: 120px; height: 120px;
    border-radius: 50%;
    background: linear-gradient(135deg, var(--cyan-dark), #0a1628);
    border: 2px solid var(--cyan);
    display: flex; align-items: center; justify-content: center;
    font-family: var(--mono);
    font-size: 42px; font-weight: 700;
    color: var(--cyan);
    position: relative;
    animation: avatar-flicker 6s ease-in-out infinite;
    box-shadow: 0 0 40px rgba(0,245,255,0.3), inset 0 0 30px rgba(0,245,255,0.05);
  }

  @keyframes avatar-flicker {
    0%, 90%, 100% { box-shadow: 0 0 40px rgba(0,245,255,0.3), inset 0 0 30px rgba(0,245,255,0.05); }
    92% { box-shadow: 0 0 60px rgba(0,245,255,0.6), inset 0 0 40px rgba(0,245,255,0.1); }
    94% { box-shadow: 0 0 20px rgba(0,245,255,0.2), inset 0 0 15px rgba(0,245,255,0.03); }
  }

  .avatar-ring {
    position: absolute; top: -8px; left: -8px;
    width: calc(100% + 16px); height: calc(100% + 16px);
    border-radius: 50%;
    border: 1px solid transparent;
    border-top-color: var(--cyan);
    border-right-color: var(--cyan);
    animation: spin 3s linear infinite;
  }

  .avatar-ring-2 {
    position: absolute; top: -16px; left: -16px;
    width: calc(100% + 32px); height: calc(100% + 32px);
    border-radius: 50%;
    border: 1px solid transparent;
    border-bottom-color: rgba(0,245,255,0.4);
    border-left-color: rgba(0,245,255,0.4);
    animation: spin 5s linear infinite reverse;
  }

  @keyframes spin { to { transform: rotate(360deg); } }

  .hero-name {
    font-family: var(--mono);
    font-size: clamp(24px, 4vw, 38px);
    font-weight: 700;
    letter-spacing: -0.02em;
    color: #fff;
    margin-bottom: 8px;
  }

  .hero-name span { color: var(--cyan); }

  .hero-title {
    font-size: 14px;
    color: var(--text-dim);
    font-family: var(--mono);
    letter-spacing: 0.12em;
    text-transform: uppercase;
    margin-bottom: 24px;
  }

  /* ── TYPEWRITER ── */
  .typewriter-wrap {
    display: inline-flex;
    align-items: center;
    gap: 8px;
    background: var(--bg2);
    border: 1px solid var(--border);
    border-radius: 8px;
    padding: 10px 20px;
    font-family: var(--mono);
    font-size: 14px;
    color: var(--cyan);
    margin-bottom: 40px;
  }

  .prompt { color: var(--green); margin-right: 4px; }

  .typewriter {
    display: inline-block;
    overflow: hidden;
    white-space: nowrap;
    border-right: 2px solid var(--cyan);
    animation: blink-cursor 0.75s step-end infinite;
  }

  @keyframes blink-cursor {
    from, to { border-color: var(--cyan); }
    50% { border-color: transparent; }
  }

  /* ── BADGES ── */
  .badge-row {
    display: flex; flex-wrap: wrap;
    gap: 10px; justify-content: center;
    margin-top: 8px;
  }

  .badge {
    display: inline-flex; align-items: center; gap: 6px;
    padding: 6px 14px;
    border-radius: 999px;
    font-size: 12px; font-weight: 600;
    font-family: var(--mono);
    letter-spacing: 0.04em;
    border: 1px solid;
    transition: all 0.25s;
    cursor: default;
    animation: badge-float 3s ease-in-out infinite;
  }

  .badge:hover {
    transform: translateY(-3px) scale(1.05);
    box-shadow: 0 6px 20px rgba(0,245,255,0.2);
  }

  .badge.cyan  { color: var(--cyan); border-color: rgba(0,245,255,0.3); background: rgba(0,245,255,0.06); }
  .badge.green { color: var(--green); border-color: rgba(57,255,20,0.3); background: rgba(57,255,20,0.06); }
  .badge.purple{ color: var(--purple); border-color: rgba(179,71,234,0.3); background: rgba(179,71,234,0.06); }
  .badge.orange{ color: var(--orange); border-color: rgba(255,107,53,0.3); background: rgba(255,107,53,0.06); }

  .badge:nth-child(odd)  { animation-delay: 0s; }
  .badge:nth-child(even) { animation-delay: 0.5s; }

  @keyframes badge-float {
    0%, 100% { transform: translateY(0); }
    50% { transform: translateY(-4px); }
  }

  /* ── SECTION ── */
  .section {
    margin-top: 64px;
    opacity: 0; transform: translateY(24px);
    transition: opacity 0.6s ease, transform 0.6s ease;
  }

  .section.visible { opacity: 1; transform: translateY(0); }

  .section-header {
    display: flex; align-items: center; gap: 14px;
    margin-bottom: 28px;
  }

  .section-tag {
    font-family: var(--mono);
    font-size: 11px;
    color: var(--cyan);
    background: rgba(0,245,255,0.08);
    border: 1px solid var(--border);
    border-radius: 4px;
    padding: 2px 8px;
    letter-spacing: 0.1em;
  }

  .section-line {
    flex: 1; height: 1px;
    background: linear-gradient(90deg, var(--border-bright), transparent);
  }

  .section-title {
    font-size: 20px; font-weight: 600;
    color: #fff; margin-bottom: 0;
  }

  /* ── ABOUT / JSON CARD ── */
  .json-card {
    background: var(--bg2);
    border: 1px solid var(--border);
    border-left: 3px solid var(--cyan);
    border-radius: 12px;
    padding: 28px 32px;
    font-family: var(--mono);
    font-size: 13.5px;
    line-height: 1.9;
    position: relative;
    overflow: hidden;
  }

  .json-card::before {
    content: '';
    position: absolute; top: 0; left: 0; right: 0; height: 1px;
    background: linear-gradient(90deg, var(--cyan), transparent);
    opacity: 0.5;
  }

  .j-bracket { color: #5f8fa0; }
  .j-key     { color: #7fcfdf; }
  .j-str     { color: #a8ff78; }
  .j-arr     { color: #ff9f7f; }
  .j-num     { color: #ff8c42; }
  .j-colon   { color: #4a6880; }
  .j-indent  { padding-left: 20px; }
  .j-indent2 { padding-left: 40px; }

  /* ── TECH GRID ── */
  .tech-grid {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(130px, 1fr));
    gap: 12px;
  }

  .tech-card {
    background: var(--bg2);
    border: 1px solid var(--border);
    border-radius: 10px;
    padding: 16px 14px;
    text-align: center;
    cursor: default;
    transition: all 0.3s;
    position: relative;
    overflow: hidden;
  }

  .tech-card::before {
    content: '';
    position: absolute; top: 0; left: -100%;
    width: 100%; height: 100%;
    background: linear-gradient(90deg, transparent, rgba(0,245,255,0.06), transparent);
    transition: left 0.5s;
  }

  .tech-card:hover::before { left: 100%; }

  .tech-card:hover {
    border-color: var(--border-bright);
    transform: translateY(-4px);
    box-shadow: 0 8px 24px rgba(0,245,255,0.12);
  }

  .tech-icon {
    font-size: 28px;
    margin-bottom: 8px;
    display: block;
    filter: drop-shadow(0 0 6px currentColor);
  }

  .tech-name {
    font-size: 12px;
    font-weight: 600;
    color: var(--text);
    font-family: var(--mono);
  }

  .tech-type {
    font-size: 10px;
    color: var(--text-dim);
    margin-top: 2px;
  }

  /* ── SKILL BARS ── */
  .skill-list { display: flex; flex-direction: column; gap: 16px; }

  .skill-item {}

  .skill-meta {
    display: flex; justify-content: space-between;
    margin-bottom: 6px;
  }

  .skill-name {
    font-family: var(--mono); font-size: 13px;
    color: var(--text);
  }

  .skill-pct {
    font-family: var(--mono); font-size: 12px;
    color: var(--cyan);
  }

  .skill-bar-bg {
    height: 6px;
    background: rgba(255,255,255,0.06);
    border-radius: 999px;
    overflow: hidden;
  }

  .skill-bar-fill {
    height: 100%;
    border-radius: 999px;
    width: 0%;
    transition: width 1.4s cubic-bezier(0.22, 1, 0.36, 1);
    position: relative;
  }

  .skill-bar-fill::after {
    content: '';
    position: absolute; right: 0; top: 50%;
    transform: translateY(-50%);
    width: 8px; height: 8px;
    border-radius: 50%;
    background: inherit;
    box-shadow: 0 0 8px currentColor;
  }

  /* ── GOALS GRID ── */
  .goals-grid {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(200px, 1fr));
    gap: 14px;
  }

  .goal-card {
    background: var(--bg2);
    border: 1px solid var(--border);
    border-radius: 10px;
    padding: 18px;
    display: flex; align-items: flex-start; gap: 12px;
    transition: all 0.3s;
  }

  .goal-card:hover {
    border-color: rgba(57,255,20,0.3);
    box-shadow: 0 4px 16px rgba(57,255,20,0.08);
    transform: translateY(-2px);
  }

  .goal-icon {
    width: 32px; height: 32px; flex-shrink: 0;
    background: rgba(57,255,20,0.1);
    border: 1px solid rgba(57,255,20,0.2);
    border-radius: 8px;
    display: flex; align-items: center; justify-content: center;
    font-size: 16px;
  }

  .goal-text {
    font-size: 13px; line-height: 1.5;
    color: var(--text);
  }

  /* ── CONNECT ── */
  .connect-grid {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(180px, 1fr));
    gap: 12px;
  }

  .connect-card {
    display: flex; align-items: center; gap: 12px;
    background: var(--bg2);
    border: 1px solid var(--border);
    border-radius: 10px;
    padding: 14px 16px;
    text-decoration: none;
    color: var(--text);
    transition: all 0.3s;
    font-size: 13px;
    font-weight: 500;
  }

  .connect-card:hover {
    transform: translateY(-3px);
    border-color: var(--border-bright);
    box-shadow: 0 8px 24px rgba(0,245,255,0.1);
    color: #fff;
  }

  .connect-icon {
    width: 36px; height: 36px;
    border-radius: 8px;
    display: flex; align-items: center; justify-content: center;
    font-size: 18px; flex-shrink: 0;
  }

  /* ── FOOTER ── */
  .footer {
    margin-top: 80px;
    text-align: center;
    padding: 40px 0 20px;
    border-top: 1px solid var(--border);
    font-family: var(--mono);
    font-size: 12px;
    color: var(--text-dim);
  }

  .footer span { color: var(--cyan); }

  /* ── QUOTE CARD ── */
  .quote-card {
    background: var(--bg2);
    border: 1px solid var(--border);
    border-left: 3px solid var(--purple);
    border-radius: 12px;
    padding: 24px 28px;
    font-style: italic;
    font-size: 15px;
    color: var(--text);
    position: relative;
  }

  .quote-card::before {
    content: '"';
    position: absolute; top: -10px; left: 20px;
    font-size: 60px; color: var(--purple);
    opacity: 0.3; font-family: Georgia, serif;
    line-height: 1;
  }

  .quote-author {
    margin-top: 12px;
    font-size: 12px;
    color: var(--text-dim);
    font-style: normal;
    font-family: var(--mono);
  }

  /* ── PARTICLES ── */
  .particles { position: fixed; top: 0; left: 0; width: 100%; height: 100%; z-index: 0; pointer-events: none; }

  /* ── GLITCH ── */
  @keyframes glitch {
    0%, 90%, 100% { clip-path: none; transform: none; }
    91% { clip-path: inset(20% 0 60% 0); transform: translateX(-4px); color: var(--cyan); }
    92% { clip-path: inset(60% 0 10% 0); transform: translateX(4px); color: var(--purple); }
    93% { clip-path: none; transform: none; }
  }

  .glitch-text {
    position: relative;
    display: inline-block;
  }

  .glitch-text::before,
  .glitch-text::after {
    content: attr(data-text);
    position: absolute; top: 0; left: 0;
    width: 100%; height: 100%;
  }

  .glitch-text::before {
    animation: glitch 8s infinite;
    color: var(--cyan);
    z-index: -1;
  }

  /* ── RESPONSIVE ── */
  @media (max-width: 600px) {
    .container { padding: 40px 20px 80px; }
    .tech-grid { grid-template-columns: repeat(3, 1fr); }
    .goals-grid { grid-template-columns: 1fr 1fr; }
    .connect-grid { grid-template-columns: 1fr 1fr; }
  }
</style>
</head>
<body>

<canvas id="canvas-bg"></canvas>

<div class="container">

  <!-- HERO -->
  <section class="hero">
    <div class="hero-glow"></div>

    <div class="avatar-wrap">
      <div class="avatar-ring-2"></div>
      <div class="avatar-ring"></div>
      <div class="avatar">LT</div>
    </div>

    <h1 class="hero-name">
      <span class="glitch-text" data-text="Lê Hoàng Quách">Lê Hoàng Quách</span> Tỉnh
    </h1>
    <p class="hero-title">Backend Software Engineer · Việt Nam</p>

    <div class="typewriter-wrap">
      <span class="prompt">$</span>
      <span class="typewriter" id="typewriter"></span>
    </div>

    <div class="badge-row">
      <span class="badge cyan">☕ Clean Code Advocate</span>
      <span class="badge green">⚡ Scalable APIs</span>
      <span class="badge purple">🏗 Microservices</span>
      <span class="badge orange">📦 Docker / CI/CD</span>
    </div>
  </section>

  <!-- ABOUT -->
  <section class="section" id="s1">
    <div class="section-header">
      <span class="section-tag">01</span>
      <h2 class="section-title">Về tôi</h2>
      <div class="section-line"></div>
    </div>

    <div class="json-card">
      <div><span class="j-bracket">{</span></div>
      <div class="j-indent">
        <span class="j-key">"role"</span><span class="j-colon">: </span><span class="j-str">"Backend Software Engineer"</span><span class="j-colon">,</span>
      </div>
      <div class="j-indent">
        <span class="j-key">"focus"</span><span class="j-colon">: </span><span class="j-bracket">[</span>
        <span class="j-arr">"Scalable Web APIs"</span><span class="j-colon">, </span>
        <span class="j-arr">"Microservices"</span><span class="j-colon">, </span>
        <span class="j-arr">"Database Optimization"</span><span class="j-bracket">]</span><span class="j-colon">,</span>
      </div>
      <div class="j-indent">
        <span class="j-key">"tech_stack"</span><span class="j-colon">: </span><span class="j-bracket">{</span>
      </div>
      <div class="j-indent2">
        <span class="j-key">"languages"</span><span class="j-colon">: </span><span class="j-bracket">[</span><span class="j-arr">"Java / Spring Boot"</span><span class="j-colon">, </span><span class="j-arr">"C# / .NET"</span><span class="j-bracket">]</span><span class="j-colon">,</span>
      </div>
      <div class="j-indent2">
        <span class="j-key">"devops"</span><span class="j-colon">: </span><span class="j-bracket">[</span><span class="j-arr">"Docker"</span><span class="j-colon">, </span><span class="j-arr">"Git"</span><span class="j-colon">, </span><span class="j-arr">"CI/CD"</span><span class="j-bracket">]</span><span class="j-colon">,</span>
      </div>
      <div class="j-indent2">
        <span class="j-key">"database"</span><span class="j-colon">: </span><span class="j-bracket">[</span><span class="j-arr">"SQL Server"</span><span class="j-colon">, </span><span class="j-arr">"MongoDB"</span><span class="j-colon">, </span><span class="j-arr">"MySQL"</span><span class="j-bracket">]</span>
      </div>
      <div class="j-indent"><span class="j-bracket">}</span><span class="j-colon">,</span></div>
      <div class="j-indent">
        <span class="j-key">"motto"</span><span class="j-colon">: </span><span class="j-str">"Clean Code is Happy Code ✨"</span><span class="j-colon">,</span>
      </div>
      <div class="j-indent">
        <span class="j-key">"reading"</span><span class="j-colon">: </span><span class="j-str">"Designing Data-Intensive Applications"</span><span class="j-colon">,</span>
      </div>
      <div class="j-indent">
        <span class="j-key">"github"</span><span class="j-colon">: </span><span class="j-str">"github.com/Tinh0804"</span>
      </div>
      <div><span class="j-bracket">}</span></div>
    </div>
  </section>

  <!-- TECH STACK -->
  <section class="section" id="s2">
    <div class="section-header">
      <span class="section-tag">02</span>
      <h2 class="section-title">Tech Stack</h2>
      <div class="section-line"></div>
    </div>

    <div class="tech-grid">
      <div class="tech-card">
        <span class="tech-icon" style="color:#ed8b00">☕</span>
        <div class="tech-name">Java</div>
        <div class="tech-type">Language</div>
      </div>
      <div class="tech-card">
        <span class="tech-icon" style="color:#6db33f">🍃</span>
        <div class="tech-name">Spring Boot</div>
        <div class="tech-type">Framework</div>
      </div>
      <div class="tech-card">
        <span class="tech-icon" style="color:#9b59b6">◈</span>
        <div class="tech-name">C#</div>
        <div class="tech-type">Language</div>
      </div>
      <div class="tech-card">
        <span class="tech-icon" style="color:#512bd4">⬡</span>
        <div class="tech-name">.NET Core</div>
        <div class="tech-type">Framework</div>
      </div>
      <div class="tech-card">
        <span class="tech-icon" style="color:#cc2927">🗄</span>
        <div class="tech-name">SQL Server</div>
        <div class="tech-type">Database</div>
      </div>
      <div class="tech-card">
        <span class="tech-icon" style="color:#47a248">🍃</span>
        <div class="tech-name">MongoDB</div>
        <div class="tech-type">Database</div>
      </div>
      <div class="tech-card">
        <span class="tech-icon" style="color:#4479a1">🐬</span>
        <div class="tech-name">MySQL</div>
        <div class="tech-type">Database</div>
      </div>
      <div class="tech-card">
        <span class="tech-icon" style="color:#2496ed">🐳</span>
        <div class="tech-name">Docker</div>
        <div class="tech-type">DevOps</div>
      </div>
      <div class="tech-card">
        <span class="tech-icon" style="color:#f05032">⑂</span>
        <div class="tech-name">Git</div>
        <div class="tech-type">Version Control</div>
      </div>
      <div class="tech-card">
        <span class="tech-icon" style="color:#ff6c37">📮</span>
        <div class="tech-name">Postman</div>
        <div class="tech-type">Testing</div>
      </div>
    </div>
  </section>

  <!-- SKILLS -->
  <section class="section" id="s3">
    <div class="section-header">
      <span class="section-tag">03</span>
      <h2 class="section-title">Kỹ năng</h2>
      <div class="section-line"></div>
    </div>

    <div class="skill-list" id="skills">
      <div class="skill-item">
        <div class="skill-meta">
          <span class="skill-name">Java / Spring Boot</span>
          <span class="skill-pct">88%</span>
        </div>
        <div class="skill-bar-bg">
          <div class="skill-bar-fill" data-pct="88" style="background: linear-gradient(90deg, #ed8b00, #f0a500);"></div>
        </div>
      </div>
      <div class="skill-item">
        <div class="skill-meta">
          <span class="skill-name">C# / .NET Core</span>
          <span class="skill-pct">85%</span>
        </div>
        <div class="skill-bar-bg">
          <div class="skill-bar-fill" data-pct="85" style="background: linear-gradient(90deg, #512bd4, #7c5cbf);"></div>
        </div>
      </div>
      <div class="skill-item">
        <div class="skill-meta">
          <span class="skill-name">RESTful API Design</span>
          <span class="skill-pct">90%</span>
        </div>
        <div class="skill-bar-bg">
          <div class="skill-bar-fill" data-pct="90" style="background: linear-gradient(90deg, #00f5ff, #00a8b5);"></div>
        </div>
      </div>
      <div class="skill-item">
        <div class="skill-meta">
          <span class="skill-name">SQL / Database Design</span>
          <span class="skill-pct">82%</span>
        </div>
        <div class="skill-bar-bg">
          <div class="skill-bar-fill" data-pct="82" style="background: linear-gradient(90deg, #cc2927, #e05050);"></div>
        </div>
      </div>
      <div class="skill-item">
        <div class="skill-meta">
          <span class="skill-name">Docker / Microservices</span>
          <span class="skill-pct">78%</span>
        </div>
        <div class="skill-bar-bg">
          <div class="skill-bar-fill" data-pct="78" style="background: linear-gradient(90deg, #2496ed, #5ab3f0);"></div>
        </div>
      </div>
    </div>
  </section>

  <!-- GOALS -->
  <section class="section" id="s4">
    <div class="section-header">
      <span class="section-tag">04</span>
      <h2 class="section-title">Mục tiêu 2025</h2>
      <div class="section-line"></div>
    </div>

    <div class="goals-grid">
      <div class="goal-card">
        <div class="goal-icon">🚀</div>
        <div class="goal-text">Master Spring Boot &amp; Microservices Architecture</div>
      </div>
      <div class="goal-card">
        <div class="goal-icon">🌐</div>
        <div class="goal-text">Contribute to Open Source Projects</div>
      </div>
      <div class="goal-card">
        <div class="goal-icon">☁️</div>
        <div class="goal-text">Learn Cloud Platforms (Azure / AWS)</div>
      </div>
      <div class="goal-card">
        <div class="goal-icon">⚙️</div>
        <div class="goal-text">Build Production-Ready REST APIs</div>
      </div>
    </div>
  </section>

  <!-- QUOTE -->
  <section class="section" id="s5">
    <div class="section-header">
      <span class="section-tag">05</span>
      <h2 class="section-title">Dev Quote</h2>
      <div class="section-line"></div>
    </div>
    <div class="quote-card">
      Any fool can write code that a computer can understand. Good programmers write code that humans can understand.
      <div class="quote-author">— Martin Fowler</div>
    </div>
  </section>

  <!-- CONNECT -->
  <section class="section" id="s6">
    <div class="section-header">
      <span class="section-tag">06</span>
      <h2 class="section-title">Liên hệ</h2>
      <div class="section-line"></div>
    </div>

    <div class="connect-grid">
      <a class="connect-card" href="https://www.linkedin.com/in/lê-hoàng-quách-tỉnh-56a0a0376" target="_blank">
        <div class="connect-icon" style="background:rgba(0,119,181,0.15); color:#0077b5;">in</div>
        LinkedIn
      </a>
      <a class="connect-card" href="mailto:lhqtinh2005@gmail.com">
        <div class="connect-icon" style="background:rgba(209,72,54,0.15); color:#d14836; font-size:16px;">✉</div>
        Gmail
      </a>
      <a class="connect-card" href="https://zalo.me/0366900821" target="_blank">
        <div class="connect-icon" style="background:rgba(0,104,255,0.15); color:#0068ff; font-size:12px; font-weight:700;">Z</div>
        Zalo
      </a>
      <a class="connect-card" href="https://portfolio-seven-bice-65.vercel.app/" target="_blank">
        <div class="connect-icon" style="background:rgba(255,255,255,0.08); color:#fff; font-size:14px;">◈</div>
        Portfolio
      </a>
      <a class="connect-card" href="https://github.com/Tinh0804" target="_blank">
        <div class="connect-icon" style="background:rgba(255,255,255,0.08); color:#fff; font-size:18px;">⑂</div>
        GitHub
      </a>
    </div>
  </section>

  <footer class="footer">
    <span>Made with ❤️ by </span><span>Quách Tỉnh</span>
    <span> · Built with HTML + CSS + JS</span>
  </footer>

</div>

<script>
// ── MATRIX RAIN CANVAS ──
const canvas = document.getElementById('canvas-bg');
const ctx = canvas.getContext('2d');
let cols, drops;
const CHARS = '01アイウエオカキクケコサシスセソタチツテトナニヌネノハヒフヘホマミムメモ';

function resize() {
  canvas.width = window.innerWidth;
  canvas.height = window.innerHeight;
  cols = Math.floor(canvas.width / 20);
  drops = Array(cols).fill(1);
}

resize();
window.addEventListener('resize', resize);

function drawMatrix() {
  ctx.fillStyle = 'rgba(5,11,19,0.05)';
  ctx.fillRect(0, 0, canvas.width, canvas.height);
  ctx.fillStyle = '#00f5ff';
  ctx.font = '13px JetBrains Mono, monospace';
  for (let i = 0; i < cols; i++) {
    const ch = CHARS[Math.floor(Math.random() * CHARS.length)];
    ctx.globalAlpha = Math.random() * 0.4 + 0.1;
    ctx.fillText(ch, i * 20, drops[i] * 20);
    if (drops[i] * 20 > canvas.height && Math.random() > 0.975) drops[i] = 0;
    drops[i]++;
  }
  ctx.globalAlpha = 1;
}

setInterval(drawMatrix, 60);

// ── TYPEWRITER ──
const lines = [
  'echo "Hello, World!"',
  'git commit -m "Clean code ✨"',
  'docker run --rm spring-api',
  'SELECT * FROM passion WHERE lang = "Java"',
  'mvn spring-boot:run',
];
let li = 0, ci = 0, del = false;
const tw = document.getElementById('typewriter');

function type() {
  const line = lines[li];
  if (!del) {
    tw.textContent = line.substring(0, ++ci);
    if (ci === line.length) { del = true; setTimeout(type, 1800); return; }
    setTimeout(type, 65 + Math.random() * 40);
  } else {
    tw.textContent = line.substring(0, --ci);
    if (ci === 0) { del = false; li = (li + 1) % lines.length; setTimeout(type, 400); return; }
    setTimeout(type, 28);
  }
}

setTimeout(type, 800);

// ── INTERSECTION OBSERVER (section fade-in) ──
const io = new IntersectionObserver(entries => {
  entries.forEach(e => {
    if (e.isIntersecting) {
      e.target.classList.add('visible');
      // Animate skill bars when skills section is visible
      if (e.target.id === 's3') {
        setTimeout(() => {
          document.querySelectorAll('.skill-bar-fill').forEach(bar => {
            bar.style.width = bar.dataset.pct + '%';
          });
        }, 200);
      }
    }
  });
}, { threshold: 0.12 });

['s1','s2','s3','s4','s5','s6'].forEach(id => {
  const el = document.getElementById(id);
  if (el) io.observe(el);
});
</script>
</body>
</html>
