<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<style>
  @import url('https://fonts.googleapis.com/css2?family=JetBrains+Mono:wght@300;400;500;700&family=Space+Grotesk:wght@300;400;500;600;700&display=swap');

  * { margin: 0; padding: 0; box-sizing: border-box; }

  :root {
    --bg: #0a0e17;
    --bg2: #0d1220;
    --bg3: #111827;
    --card: #131b2e;
    --card2: #162035;
    --border: #1e2d4a;
    --border2: #243556;
    --cyan: #00d4ff;
    --cyan2: #00a8cc;
    --blue: #4f8ef7;
    --purple: #8b5cf6;
    --green: #10d98b;
    --amber: #f59e0b;
    --red: #ef4444;
    --text: #e2e8f0;
    --muted: #8899b4;
    --faint: #3d5270;
    --mono: 'JetBrains Mono', monospace;
    --sans: 'Space Grotesk', sans-serif;
  }

  body {
    background: var(--bg);
    color: var(--text);
    font-family: var(--sans);
    min-height: 100vh;
    overflow-x: hidden;
  }

  .profile-wrap {
    max-width: 900px;
    margin: 0 auto;
    padding: 32px 24px 48px;
    position: relative;
  }

  /* Animated background grid */
  .bg-grid {
    position: fixed;
    top: 0; left: 0; right: 0; bottom: 0;
    background-image:
      linear-gradient(rgba(0,212,255,0.03) 1px, transparent 1px),
      linear-gradient(90deg, rgba(0,212,255,0.03) 1px, transparent 1px);
    background-size: 40px 40px;
    pointer-events: none;
    z-index: 0;
  }

  .bg-glow {
    position: fixed;
    top: -200px; left: 50%;
    transform: translateX(-50%);
    width: 700px; height: 400px;
    background: radial-gradient(ellipse, rgba(0,212,255,0.06) 0%, transparent 70%);
    pointer-events: none;
    z-index: 0;
  }

  .content { position: relative; z-index: 1; }

  /* ── HEADER ── */
  .header {
    display: flex;
    align-items: center;
    gap: 32px;
    margin-bottom: 40px;
    padding: 32px;
    background: var(--card);
    border: 1px solid var(--border);
    border-radius: 16px;
    position: relative;
    overflow: hidden;
  }

  .header::before {
    content: '';
    position: absolute;
    top: 0; left: 0; right: 0;
    height: 2px;
    background: linear-gradient(90deg, transparent, var(--cyan), var(--purple), transparent);
    animation: scanline 3s ease-in-out infinite;
  }

  @keyframes scanline {
    0%, 100% { opacity: 0.4; }
    50% { opacity: 1; }
  }

  .header-corner {
    position: absolute;
    top: 12px; right: 16px;
    font-family: var(--mono);
    font-size: 10px;
    color: var(--faint);
    letter-spacing: 0.05em;
  }

  .avatar-wrap {
    position: relative;
    flex-shrink: 0;
  }

  .avatar-ring {
    width: 96px; height: 96px;
    border-radius: 50%;
    background: linear-gradient(135deg, var(--cyan), var(--purple));
    padding: 2px;
    animation: rotate-ring 8s linear infinite;
    position: relative;
  }

  @keyframes rotate-ring {
    0% { filter: hue-rotate(0deg); }
    100% { filter: hue-rotate(360deg); }
  }

  .avatar-inner {
    width: 100%;
    height: 100%;
    border-radius: 50%;
    background: var(--bg2);
    display: flex;
    align-items: center;
    justify-content: center;
    font-family: var(--mono);
    font-size: 28px;
    font-weight: 700;
    color: var(--cyan);
    letter-spacing: -0.02em;
    position: relative;
  }

  .avatar-pulse {
    position: absolute;
    top: -6px; left: -6px; right: -6px; bottom: -6px;
    border-radius: 50%;
    border: 1px solid var(--cyan);
    opacity: 0.2;
    animation: pulse 2s ease-in-out infinite;
  }

  @keyframes pulse {
    0%, 100% { transform: scale(1); opacity: 0.2; }
    50% { transform: scale(1.08); opacity: 0.05; }
  }

  .status-dot {
    position: absolute;
    bottom: 6px; right: 6px;
    width: 14px; height: 14px;
    background: var(--green);
    border-radius: 50%;
    border: 2px solid var(--card);
    animation: blink 2s step-end infinite;
  }

  @keyframes blink {
    0%, 100% { opacity: 1; }
    50% { opacity: 0.3; }
  }

  .header-info { flex: 1; }

  .name-row {
    display: flex;
    align-items: baseline;
    gap: 10px;
    margin-bottom: 4px;
  }

  .name {
    font-size: 26px;
    font-weight: 700;
    color: var(--text);
    letter-spacing: -0.02em;
  }

  .handle {
    font-family: var(--mono);
    font-size: 13px;
    color: var(--cyan);
    letter-spacing: 0.02em;
  }

  .title-tag {
    font-family: var(--mono);
    font-size: 12px;
    color: var(--muted);
    margin-bottom: 12px;
  }

  .typing-wrap {
    display: flex;
    align-items: center;
    gap: 8px;
    margin-bottom: 14px;
  }

  .prompt-sym {
    font-family: var(--mono);
    font-size: 14px;
    color: var(--green);
  }

  #typing-text {
    font-family: var(--mono);
    font-size: 14px;
    color: var(--cyan);
    font-weight: 500;
    min-width: 200px;
  }

  .cursor {
    display: inline-block;
    width: 2px; height: 16px;
    background: var(--cyan);
    margin-left: 1px;
    vertical-align: text-bottom;
    animation: cursor-blink 0.8s step-end infinite;
  }

  @keyframes cursor-blink {
    0%, 100% { opacity: 1; }
    50% { opacity: 0; }
  }

  .header-badges {
    display: flex;
    flex-wrap: wrap;
    gap: 8px;
  }

  .badge {
    font-family: var(--mono);
    font-size: 11px;
    padding: 4px 10px;
    border-radius: 4px;
    border: 1px solid;
    font-weight: 500;
    letter-spacing: 0.03em;
  }

  .badge-cyan  { border-color: var(--cyan);   color: var(--cyan);   background: rgba(0,212,255,0.07); }
  .badge-purple{ border-color: var(--purple); color: var(--purple); background: rgba(139,92,246,0.07); }
  .badge-green { border-color: var(--green);  color: var(--green);  background: rgba(16,217,139,0.07); }
  .badge-amber { border-color: var(--amber);  color: var(--amber);  background: rgba(245,158,11,0.07); }
  .badge-blue  { border-color: var(--blue);   color: var(--blue);   background: rgba(79,142,247,0.07); }

  /* ── SECTION TITLE ── */
  .section-label {
    display: flex;
    align-items: center;
    gap: 10px;
    margin-bottom: 16px;
    margin-top: 32px;
  }

  .section-label .line {
    flex: 1;
    height: 1px;
    background: linear-gradient(90deg, var(--border2), transparent);
  }

  .section-label span {
    font-family: var(--mono);
    font-size: 11px;
    color: var(--muted);
    text-transform: uppercase;
    letter-spacing: 0.15em;
  }

  /* ── SYSTEM DIAGRAM ── */
  .sys-card {
    background: var(--card);
    border: 1px solid var(--border);
    border-radius: 14px;
    padding: 24px;
    margin-bottom: 20px;
    position: relative;
    overflow: hidden;
  }

  .sys-card::after {
    content: '';
    position: absolute;
    bottom: 0; right: 0;
    width: 180px; height: 180px;
    background: radial-gradient(ellipse at bottom right, rgba(79,142,247,0.05), transparent 70%);
    pointer-events: none;
  }

  .sys-title {
    font-family: var(--mono);
    font-size: 11px;
    color: var(--muted);
    letter-spacing: 0.1em;
    text-transform: uppercase;
    margin-bottom: 20px;
  }

  .pipeline {
    display: flex;
    align-items: center;
    gap: 0;
    overflow-x: auto;
    padding-bottom: 4px;
  }

  .pipe-node {
    flex-shrink: 0;
    background: var(--bg3);
    border: 1px solid var(--border2);
    border-radius: 8px;
    padding: 12px 14px;
    text-align: center;
    min-width: 100px;
    position: relative;
  }

  .pipe-node.active {
    border-color: var(--cyan);
    box-shadow: 0 0 12px rgba(0,212,255,0.12);
  }

  .pipe-icon {
    font-size: 20px;
    margin-bottom: 4px;
  }

  .pipe-label {
    font-family: var(--mono);
    font-size: 10px;
    color: var(--muted);
    display: block;
  }

  .pipe-arrow {
    flex: 1;
    min-width: 20px;
    text-align: center;
    color: var(--faint);
    font-size: 16px;
    position: relative;
  }

  .pipe-arrow::before {
    content: '';
    display: block;
    height: 1px;
    background: linear-gradient(90deg, var(--faint), var(--cyan2), var(--faint));
    animation: flow 2s linear infinite;
  }

  @keyframes flow {
    0% { background-position: -100px; }
    100% { background-position: 100px; }
  }

  /* ── TECH GRID ── */
  .tech-grid {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(130px, 1fr));
    gap: 10px;
    margin-bottom: 0;
  }

  .tech-item {
    background: var(--card);
    border: 1px solid var(--border);
    border-radius: 8px;
    padding: 10px 12px;
    display: flex;
    align-items: center;
    gap: 8px;
    transition: border-color 0.2s, transform 0.2s;
    cursor: default;
  }

  .tech-item:hover {
    border-color: var(--border2);
    transform: translateY(-1px);
  }

  .tech-dot {
    width: 8px; height: 8px;
    border-radius: 50%;
    flex-shrink: 0;
  }

  .tech-name {
    font-family: var(--mono);
    font-size: 11px;
    color: var(--text);
    font-weight: 500;
  }

  /* ── STATS STRIP ── */
  .stats-strip {
    display: grid;
    grid-template-columns: repeat(4, 1fr);
    gap: 12px;
    margin-bottom: 20px;
  }

  .stat-card {
    background: var(--card);
    border: 1px solid var(--border);
    border-radius: 10px;
    padding: 16px 14px;
    text-align: center;
    position: relative;
    overflow: hidden;
  }

  .stat-card::before {
    content: '';
    position: absolute;
    top: 0; left: 0; right: 0;
    height: 2px;
  }

  .stat-card.s1::before { background: var(--cyan); }
  .stat-card.s2::before { background: var(--purple); }
  .stat-card.s3::before { background: var(--green); }
  .stat-card.s4::before { background: var(--amber); }

  .stat-val {
    font-family: var(--mono);
    font-size: 22px;
    font-weight: 700;
    margin-bottom: 2px;
  }

  .s1 .stat-val { color: var(--cyan); }
  .s2 .stat-val { color: var(--purple); }
  .s3 .stat-val { color: var(--green); }
  .s4 .stat-val { color: var(--amber); }

  .stat-lbl {
    font-family: var(--mono);
    font-size: 10px;
    color: var(--muted);
    text-transform: uppercase;
    letter-spacing: 0.1em;
  }

  /* ── EXPERTISE BARS ── */
  .expertise-grid {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 10px;
  }

  .exp-row {
    background: var(--card);
    border: 1px solid var(--border);
    border-radius: 8px;
    padding: 12px 14px;
  }

  .exp-header {
    display: flex;
    justify-content: space-between;
    margin-bottom: 8px;
  }

  .exp-name {
    font-family: var(--mono);
    font-size: 11px;
    color: var(--text);
    font-weight: 500;
  }

  .exp-pct {
    font-family: var(--mono);
    font-size: 11px;
    color: var(--muted);
  }

  .bar-bg {
    height: 4px;
    background: var(--bg3);
    border-radius: 2px;
    overflow: hidden;
  }

  .bar-fill {
    height: 100%;
    border-radius: 2px;
    animation: grow 1.5s ease-out both;
  }

  @keyframes grow {
    from { width: 0 !important; }
  }

  /* ── CONNECT ── */
  .connect-row {
    display: flex;
    gap: 12px;
    flex-wrap: wrap;
  }

  .connect-btn {
    display: flex;
    align-items: center;
    gap: 8px;
    background: var(--card);
    border: 1px solid var(--border);
    border-radius: 8px;
    padding: 10px 16px;
    text-decoration: none;
    color: var(--muted);
    font-family: var(--mono);
    font-size: 12px;
    transition: border-color 0.2s, color 0.2s;
    cursor: pointer;
  }

  .connect-btn:hover {
    border-color: var(--cyan);
    color: var(--cyan);
  }

  .connect-icon {
    width: 18px; height: 18px;
    border-radius: 4px;
    display: flex;
    align-items: center;
    justify-content: center;
    font-size: 12px;
  }

  /* ── FOOTER ── */
  .profile-footer {
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 16px 20px;
    background: var(--card);
    border: 1px solid var(--border);
    border-radius: 10px;
    margin-top: 24px;
  }

  .footer-mono {
    font-family: var(--mono);
    font-size: 11px;
    color: var(--faint);
  }

  .views-badge {
    font-family: var(--mono);
    font-size: 11px;
    color: var(--cyan);
    background: rgba(0,212,255,0.07);
    border: 1px solid rgba(0,212,255,0.2);
    padding: 4px 12px;
    border-radius: 4px;
  }

</style>
</head>
<body>
<div class="bg-grid"></div>
<div class="bg-glow"></div>

<div class="profile-wrap content">

  <!-- HEADER -->
  <div class="header">
    <div class="header-corner">// v2.4.1 · production</div>
    <div class="avatar-wrap">
      <div class="avatar-ring">
        <div class="avatar-inner">
          R
          <div class="avatar-pulse"></div>
        </div>
      </div>
      <div class="status-dot" title="Available"></div>
    </div>
    <div class="header-info">
      <div class="name-row">
        <span class="name">Rishvanth</span>
        <span class="handle">@rishvanth</span>
      </div>
      <div class="title-tag">// AI Developer · ML Engineer · Full Stack</div>
      <div class="typing-wrap">
        <span class="prompt-sym">❯</span>
        <span id="typing-text"></span><span class="cursor"></span>
      </div>
      <div class="header-badges">
        <span class="badge badge-cyan">Machine Learning</span>
        <span class="badge badge-purple">Generative AI</span>
        <span class="badge badge-green">Computer Vision</span>
        <span class="badge badge-amber">LangChain · RAG</span>
        <span class="badge badge-blue">Full Stack</span>
      </div>
    </div>
  </div>

  <!-- STATS -->
  <div class="section-label">
    <span>metrics</span>
    <div class="line"></div>
  </div>
  <div class="stats-strip">
    <div class="stat-card s1"><div class="stat-val">12+</div><div class="stat-lbl">Projects</div></div>
    <div class="stat-card s2"><div class="stat-val">8+</div><div class="stat-lbl">ML Models</div></div>
    <div class="stat-card s3"><div class="stat-val">5+</div><div class="stat-lbl">Frameworks</div></div>
    <div class="stat-card s4"><div class="stat-val">3+</div><div class="stat-lbl">Years Exp</div></div>
  </div>

  <!-- AI PIPELINE DIAGRAM -->
  <div class="section-label">
    <span>system architecture</span>
    <div class="line"></div>
  </div>
  <div class="sys-card">
    <div class="sys-title">// AI · ML pipeline overview</div>
    <div class="pipeline">
      <div class="pipe-node">
        <div class="pipe-icon">📦</div>
        <span class="pipe-label">Data</span>
      </div>
      <div class="pipe-arrow"></div>
      <div class="pipe-node">
        <div class="pipe-icon">⚙️</div>
        <span class="pipe-label">Process</span>
      </div>
      <div class="pipe-arrow"></div>
      <div class="pipe-node active">
        <div class="pipe-icon">🧠</div>
        <span class="pipe-label">Train</span>
      </div>
      <div class="pipe-arrow"></div>
      <div class="pipe-node">
        <div class="pipe-icon">🔍</div>
        <span class="pipe-label">Evaluate</span>
      </div>
      <div class="pipe-arrow"></div>
      <div class="pipe-node">
        <div class="pipe-icon">🚀</div>
        <span class="pipe-label">Deploy</span>
      </div>
      <div class="pipe-arrow"></div>
      <div class="pipe-node">
        <div class="pipe-icon">📡</div>
        <span class="pipe-label">Monitor</span>
      </div>
    </div>
  </div>

  <!-- EXPERTISE BARS -->
  <div class="section-label">
    <span>expertise</span>
    <div class="line"></div>
  </div>
  <div class="expertise-grid" style="margin-bottom: 20px;">
    <div class="exp-row">
      <div class="exp-header"><span class="exp-name">Machine Learning</span><span class="exp-pct">92%</span></div>
      <div class="bar-bg"><div class="bar-fill" style="width:92%; background: var(--cyan);"></div></div>
    </div>
    <div class="exp-row">
      <div class="exp-header"><span class="exp-name">Computer Vision</span><span class="exp-pct">85%</span></div>
      <div class="bar-bg"><div class="bar-fill" style="width:85%; background: var(--purple);"></div></div>
    </div>
    <div class="exp-row">
      <div class="exp-header"><span class="exp-name">Generative AI / LLMs</span><span class="exp-pct">88%</span></div>
      <div class="bar-bg"><div class="bar-fill" style="width:88%; background: var(--green);"></div></div>
    </div>
    <div class="exp-row">
      <div class="exp-header"><span class="exp-name">Full Stack / Django</span><span class="exp-pct">80%</span></div>
      <div class="bar-bg"><div class="bar-fill" style="width:80%; background: var(--blue);"></div></div>
    </div>
    <div class="exp-row">
      <div class="exp-header"><span class="exp-name">RAG Systems</span><span class="exp-pct">82%</span></div>
      <div class="bar-bg"><div class="bar-fill" style="width:82%; background: var(--amber);"></div></div>
    </div>
    <div class="exp-row">
      <div class="exp-header"><span class="exp-name">Deep Learning</span><span class="exp-pct">87%</span></div>
      <div class="bar-bg"><div class="bar-fill" style="width:87%; background: var(--red);"></div></div>
    </div>
  </div>

  <!-- TECH STACK -->
  <div class="section-label">
    <span>tech stack</span>
    <div class="line"></div>
  </div>
  <div class="tech-grid" style="margin-bottom: 20px;">
    <div class="tech-item"><div class="tech-dot" style="background:var(--cyan)"></div><span class="tech-name">Python</span></div>
    <div class="tech-item"><div class="tech-dot" style="background:var(--cyan)"></div><span class="tech-name">TensorFlow</span></div>
    <div class="tech-item"><div class="tech-dot" style="background:var(--cyan)"></div><span class="tech-name">PyTorch</span></div>
    <div class="tech-item"><div class="tech-dot" style="background:var(--cyan)"></div><span class="tech-name">OpenCV</span></div>
    <div class="tech-item"><div class="tech-dot" style="background:var(--purple)"></div><span class="tech-name">LangChain</span></div>
    <div class="tech-item"><div class="tech-dot" style="background:var(--purple)"></div><span class="tech-name">RAG</span></div>
    <div class="tech-item"><div class="tech-dot" style="background:var(--purple)"></div><span class="tech-name">YOLO</span></div>
    <div class="tech-item"><div class="tech-dot" style="background:var(--green)"></div><span class="tech-name">Django</span></div>
    <div class="tech-item"><div class="tech-dot" style="background:var(--green)"></div><span class="tech-name">React</span></div>
    <div class="tech-item"><div class="tech-dot" style="background:var(--green)"></div><span class="tech-name">Node.js</span></div>
    <div class="tech-item"><div class="tech-dot" style="background:var(--amber)"></div><span class="tech-name">PostgreSQL</span></div>
    <div class="tech-item"><div class="tech-dot" style="background:var(--amber)"></div><span class="tech-name">MongoDB</span></div>
    <div class="tech-item"><div class="tech-dot" style="background:var(--blue)"></div><span class="tech-name">Docker</span></div>
    <div class="tech-item"><div class="tech-dot" style="background:var(--blue)"></div><span class="tech-name">AWS</span></div>
    <div class="tech-item"><div class="tech-dot" style="background:var(--blue)"></div><span class="tech-name">Streamlit</span></div>
    <div class="tech-item"><div class="tech-dot" style="background:var(--faint)"></div><span class="tech-name">Scikit-learn</span></div>
  </div>

  <!-- CONNECT -->
  <div class="section-label">
    <span>connect</span>
    <div class="line"></div>
  </div>
  <div class="connect-row" style="margin-bottom: 24px;">
    <div class="connect-btn">
      <div class="connect-icon" style="background:rgba(0,119,181,0.15); color:#0077b5;">in</div>
      LinkedIn
    </div>
    <div class="connect-btn">
      <div class="connect-icon" style="background:rgba(234,67,53,0.15); color:#ea4335;">✉</div>
      Email
    </div>
    <div class="connect-btn">
      <div class="connect-icon" style="background:rgba(255,255,255,0.06); color:#ccc;">⎇</div>
      GitHub
    </div>
  </div>

  <!-- FOOTER -->
  <div class="profile-footer">
    <span class="footer-mono">// rishvanth · ml_engineer · open_to_collab</span>
    <span class="views-badge">👁 profile_views++</span>
  </div>

</div>

<script>
const phrases = [
  "Building AI that matters.",
  "Training models, shipping products.",
  "Computer Vision + LLMs + Vibes.",
  "RAG pipelines from scratch.",
  "Generative AI developer.",
];
let pi = 0, ci = 0, deleting = false;
const el = document.getElementById('typing-text');
function type() {
  const phrase = phrases[pi];
  if (!deleting) {
    el.textContent = phrase.slice(0, ++ci);
    if (ci === phrase.length) { deleting = true; setTimeout(type, 1800); return; }
  } else {
    el.textContent = phrase.slice(0, --ci);
    if (ci === 0) { deleting = false; pi = (pi + 1) % phrases.length; setTimeout(type, 300); return; }
  }
  setTimeout(type, deleting ? 40 : 65);
}
type();
</script>
</body>
</html>
