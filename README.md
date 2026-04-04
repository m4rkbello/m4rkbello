<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8"/>
<meta name="viewport" content="width=device-width, initial-scale=1.0"/>
<title>Mark Bello — Developer Portfolio</title>
<link rel="preconnect" href="https://fonts.googleapis.com"/>
<link href="https://fonts.googleapis.com/css2?family=Orbitron:wght@400;600;700;900&family=Share+Tech+Mono&family=Rajdhani:wght@300;400;500;600&display=swap" rel="stylesheet"/>
<style>
  :root {
    --bg: #050509;
    --bg2: #0b0b14;
    --panel: rgba(10,10,22,0.85);
    --cyan: #00e5ff;
    --cyan-dim: rgba(0,229,255,0.15);
    --cyan-glow: rgba(0,229,255,0.5);
    --green: #39ff14;
    --green-dim: rgba(57,255,20,0.1);
    --purple: #bf5fff;
    --border: rgba(0,229,255,0.2);
    --text: #c8d6e0;
    --text-dim: #5a7a8a;
    --font-display: 'Orbitron', monospace;
    --font-mono: 'Share Tech Mono', monospace;
    --font-body: 'Rajdhani', sans-serif;
  }

  *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }

  html { scroll-behavior: smooth; }

  body {
    background: var(--bg);
    color: var(--text);
    font-family: var(--font-body);
    font-size: 16px;
    min-height: 100vh;
    overflow-x: hidden;
  }

  /* ── GRID BACKGROUND ── */
  body::before {
    content: '';
    position: fixed; inset: 0;
    background-image:
      linear-gradient(rgba(0,229,255,0.04) 1px, transparent 1px),
      linear-gradient(90deg, rgba(0,229,255,0.04) 1px, transparent 1px);
    background-size: 50px 50px;
    pointer-events: none; z-index: 0;
  }

  /* ── SCANLINES ── */
  body::after {
    content: '';
    position: fixed; inset: 0;
    background: repeating-linear-gradient(
      0deg,
      transparent,
      transparent 2px,
      rgba(0,0,0,0.07) 2px,
      rgba(0,0,0,0.07) 4px
    );
    pointer-events: none; z-index: 1;
  }

  /* ── CANVAS PARTICLES ── */
  #particles { position: fixed; inset: 0; z-index: 0; pointer-events: none; }

  /* ── LAYOUT ── */
  .container {
    position: relative; z-index: 2;
    max-width: 1100px;
    margin: 0 auto;
    padding: 0 24px;
  }

  /* ── NAV ── */
  nav {
    position: fixed; top: 0; left: 0; right: 0;
    z-index: 100;
    padding: 16px 0;
    background: rgba(5,5,9,0.8);
    backdrop-filter: blur(12px);
    border-bottom: 1px solid var(--border);
  }
  .nav-inner {
    max-width: 1100px; margin: 0 auto; padding: 0 24px;
    display: flex; align-items: center; justify-content: space-between;
  }
  .nav-logo {
    font-family: var(--font-display);
    font-size: 14px; font-weight: 700;
    color: var(--cyan);
    letter-spacing: 3px;
    text-transform: uppercase;
  }
  .nav-logo span { color: var(--green); }
  .nav-links { display: flex; gap: 28px; list-style: none; }
  .nav-links a {
    font-family: var(--font-mono);
    font-size: 11px;
    color: var(--text-dim);
    text-decoration: none;
    letter-spacing: 2px;
    text-transform: uppercase;
    transition: color .2s;
  }
  .nav-links a:hover { color: var(--cyan); }
  .nav-hamburger {
    display: none;
    flex-direction: column; gap: 5px; cursor: pointer; background: none; border: none;
  }
  .nav-hamburger span {
    display: block; width: 22px; height: 2px;
    background: var(--cyan);
    transition: all .3s;
  }

  /* ── HERO ── */
  .hero {
    min-height: 100vh;
    display: flex; align-items: center; justify-content: center;
    padding-top: 80px;
    position: relative; z-index: 2;
  }
  .hero-content { text-align: center; }

  .hero-badge {
    display: inline-block;
    font-family: var(--font-mono);
    font-size: 11px;
    color: var(--green);
    letter-spacing: 4px;
    text-transform: uppercase;
    border: 1px solid rgba(57,255,20,0.3);
    padding: 6px 16px;
    border-radius: 2px;
    margin-bottom: 32px;
    animation: fadeInDown .8s ease both;
  }
  .hero-badge::before { content: '> '; color: var(--text-dim); }

  .hero-name {
    font-family: var(--font-display);
    font-size: clamp(42px, 8vw, 90px);
    font-weight: 900;
    letter-spacing: -1px;
    line-height: 1;
    text-transform: uppercase;
    animation: fadeInUp .8s .1s ease both;
    position: relative;
  }
  .hero-name .first { color: #fff; }
  .hero-name .last {
    color: var(--cyan);
    text-shadow: 0 0 40px var(--cyan-glow), 0 0 80px rgba(0,229,255,0.2);
  }

  /* GLITCH */
  .glitch { position: relative; display: inline-block; }
  .glitch::before, .glitch::after {
    content: attr(data-text);
    position: absolute; top: 0; left: 0; width: 100%;
  }
  .glitch::before {
    color: var(--purple);
    clip-path: polygon(0 0,100% 0,100% 40%,0 40%);
    animation: glitch1 3s infinite;
  }
  .glitch::after {
    color: var(--green);
    clip-path: polygon(0 60%,100% 60%,100% 100%,0 100%);
    animation: glitch2 3s infinite;
  }
  @keyframes glitch1 {
    0%,90%,100% { transform: translate(0); opacity: 0; }
    92% { transform: translate(-3px,1px); opacity: .8; }
    94% { transform: translate(3px,-1px); opacity: .8; }
    96% { transform: translate(-2px); opacity: .8; }
  }
  @keyframes glitch2 {
    0%,90%,100% { transform: translate(0); opacity: 0; }
    93% { transform: translate(3px,1px); opacity: .8; }
    95% { transform: translate(-3px,-1px); opacity: .8; }
    97% { transform: translate(2px); opacity: .8; }
  }

  .hero-role {
    font-family: var(--font-mono);
    font-size: clamp(12px,2vw,16px);
    color: var(--text-dim);
    letter-spacing: 3px;
    text-transform: uppercase;
    margin-top: 16px;
    animation: fadeInUp .8s .2s ease both;
  }
  .hero-role span { color: var(--cyan); }

  .hero-quote {
    font-family: var(--font-body);
    font-size: clamp(14px,1.8vw,18px);
    font-weight: 300;
    color: var(--text-dim);
    max-width: 500px;
    margin: 28px auto 0;
    line-height: 1.6;
    border-left: 2px solid var(--cyan);
    padding-left: 16px;
    text-align: left;
    animation: fadeInUp .8s .3s ease both;
  }

  .hero-ctas {
    display: flex; gap: 16px; justify-content: center; flex-wrap: wrap;
    margin-top: 40px;
    animation: fadeInUp .8s .4s ease both;
  }
  .btn {
    font-family: var(--font-mono);
    font-size: 12px;
    letter-spacing: 2px;
    text-transform: uppercase;
    padding: 14px 28px;
    border-radius: 2px;
    text-decoration: none;
    cursor: pointer;
    transition: all .25s;
    position: relative;
    overflow: hidden;
  }
  .btn-primary {
    background: var(--cyan);
    color: #000;
    border: none;
  }
  .btn-primary:hover {
    box-shadow: 0 0 25px var(--cyan-glow), 0 0 50px rgba(0,229,255,0.2);
    transform: translateY(-2px);
  }
  .btn-outline {
    background: transparent;
    color: var(--cyan);
    border: 1px solid var(--cyan);
  }
  .btn-outline:hover {
    background: var(--cyan-dim);
    box-shadow: 0 0 20px var(--cyan-glow);
    transform: translateY(-2px);
  }

  .hero-scroll {
    position: absolute; bottom: 32px; left: 50%; transform: translateX(-50%);
    display: flex; flex-direction: column; align-items: center; gap: 8px;
    animation: fadeIn 1s 1s ease both;
  }
  .hero-scroll span {
    font-family: var(--font-mono); font-size: 10px;
    color: var(--text-dim); letter-spacing: 3px;
  }
  .scroll-line {
    width: 1px; height: 50px;
    background: linear-gradient(var(--cyan), transparent);
    animation: scrollPulse 1.5s infinite;
  }
  @keyframes scrollPulse {
    0%,100% { opacity: .3; } 50% { opacity: 1; }
  }

  /* ── SECTION BASE ── */
  section {
    padding: 100px 0;
    position: relative; z-index: 2;
  }
  .section-header { margin-bottom: 56px; }
  .section-label {
    font-family: var(--font-mono);
    font-size: 11px;
    color: var(--green);
    letter-spacing: 4px;
    text-transform: uppercase;
    margin-bottom: 12px;
  }
  .section-label::before { content: '// '; color: var(--text-dim); }
  .section-title {
    font-family: var(--font-display);
    font-size: clamp(24px,4vw,40px);
    font-weight: 700;
    color: #fff;
    text-transform: uppercase;
    letter-spacing: 2px;
  }
  .section-title span { color: var(--cyan); }
  .section-line {
    width: 60px; height: 2px;
    background: linear-gradient(90deg, var(--cyan), transparent);
    margin-top: 16px;
  }

  /* ── ABOUT ── */
  .about-grid {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 40px;
    align-items: center;
  }
  .about-text p {
    font-size: 18px; font-weight: 400;
    color: var(--text); line-height: 1.8;
    margin-bottom: 16px;
  }
  .about-text p span { color: var(--cyan); }
  .about-stats {
    display: grid; grid-template-columns: 1fr 1fr; gap: 16px;
  }
  .stat-card {
    background: var(--panel);
    border: 1px solid var(--border);
    padding: 24px 20px;
    border-radius: 4px;
    position: relative; overflow: hidden;
    transition: border-color .3s, transform .3s;
  }
  .stat-card:hover {
    border-color: var(--cyan);
    transform: translateY(-4px);
    box-shadow: 0 8px 30px rgba(0,229,255,0.1);
  }
  .stat-card::before {
    content: '';
    position: absolute; top: 0; left: 0; right: 0; height: 2px;
    background: linear-gradient(90deg, var(--cyan), transparent);
  }
  .stat-num {
    font-family: var(--font-display);
    font-size: 32px; font-weight: 900;
    color: var(--cyan);
  }
  .stat-label {
    font-family: var(--font-mono);
    font-size: 11px; color: var(--text-dim);
    letter-spacing: 2px; text-transform: uppercase;
    margin-top: 4px;
  }

  /* ── TECH STACK ── */
  .stack-categories { display: flex; flex-direction: column; gap: 48px; }

  .stack-category-title {
    font-family: var(--font-mono);
    font-size: 12px;
    color: var(--text-dim);
    letter-spacing: 3px;
    text-transform: uppercase;
    margin-bottom: 16px;
    display: flex; align-items: center; gap: 12px;
  }
  .stack-category-title::after {
    content: '';
    flex: 1; height: 1px;
    background: var(--border);
  }

  .tech-grid {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(130px, 1fr));
    gap: 12px;
  }
  .tech-pill {
    background: var(--panel);
    border: 1px solid var(--border);
    border-radius: 3px;
    padding: 12px 14px;
    font-family: var(--font-mono);
    font-size: 12px;
    color: var(--text-dim);
    letter-spacing: 1px;
    cursor: default;
    transition: all .25s;
    position: relative; overflow: hidden;
    display: flex; align-items: center; gap: 8px;
    white-space: nowrap;
  }
  .tech-pill .dot {
    width: 6px; height: 6px; border-radius: 50%;
    flex-shrink: 0;
    transition: all .25s;
  }
  .tech-pill:hover {
    color: #fff;
    transform: translateY(-3px);
  }
  .tech-pill:hover .dot { box-shadow: 0 0 8px currentColor; }

  /* color families */
  .tech-pill.c-cyan { --c: var(--cyan); border-color: rgba(0,229,255,0.15); }
  .tech-pill.c-cyan .dot { background: var(--cyan); }
  .tech-pill.c-cyan:hover { border-color: var(--cyan); box-shadow: 0 4px 20px rgba(0,229,255,0.15); }

  .tech-pill.c-green { --c: var(--green); border-color: rgba(57,255,20,0.15); }
  .tech-pill.c-green .dot { background: var(--green); }
  .tech-pill.c-green:hover { border-color: var(--green); box-shadow: 0 4px 20px rgba(57,255,20,0.1); }

  .tech-pill.c-purple { --c: var(--purple); border-color: rgba(191,95,255,0.15); }
  .tech-pill.c-purple .dot { background: var(--purple); }
  .tech-pill.c-purple:hover { border-color: var(--purple); box-shadow: 0 4px 20px rgba(191,95,255,0.1); }

  .tech-pill.c-orange { --c: #ff7b00; border-color: rgba(255,123,0,0.15); }
  .tech-pill.c-orange .dot { background: #ff7b00; }
  .tech-pill.c-orange:hover { border-color: #ff7b00; box-shadow: 0 4px 20px rgba(255,123,0,0.1); }

  /* ── FULL STACK HIGHLIGHT ── */
  .fullstack-banner {
    background: var(--panel);
    border: 1px solid var(--border);
    border-radius: 4px;
    padding: 32px;
    display: grid;
    grid-template-columns: repeat(auto-fit,minmax(200px,1fr));
    gap: 24px;
    margin-top: 48px;
    position: relative; overflow: hidden;
  }
  .fullstack-banner::before {
    content: '';
    position: absolute; top: 0; left: 0; right: 0; height: 2px;
    background: linear-gradient(90deg, var(--cyan), var(--purple), var(--green));
  }
  .fs-item { text-align: center; }
  .fs-label {
    font-family: var(--font-mono);
    font-size: 10px; color: var(--text-dim);
    letter-spacing: 3px; text-transform: uppercase;
    margin-bottom: 12px;
  }
  .fs-stack {
    font-family: var(--font-mono);
    font-size: 13px; color: var(--cyan);
    line-height: 1.8;
  }

  /* ── CONNECT ── */
  .connect-grid {
    display: grid;
    grid-template-columns: repeat(auto-fill,minmax(220px,1fr));
    gap: 20px;
  }
  .connect-card {
    background: var(--panel);
    border: 1px solid var(--border);
    border-radius: 4px;
    padding: 28px 24px;
    text-decoration: none;
    display: flex; align-items: center; gap: 16px;
    transition: all .3s;
    position: relative; overflow: hidden;
  }
  .connect-card::after {
    content: '→';
    position: absolute; right: 20px;
    font-family: var(--font-mono);
    color: var(--cyan); opacity: 0;
    transition: all .3s;
    transform: translateX(-8px);
  }
  .connect-card:hover::after { opacity: 1; transform: translateX(0); }
  .connect-card:hover {
    border-color: var(--cyan);
    box-shadow: 0 8px 30px rgba(0,229,255,0.1);
    transform: translateY(-3px);
  }
  .connect-icon {
    width: 44px; height: 44px; border-radius: 4px;
    display: flex; align-items: center; justify-content: center;
    font-size: 20px;
    flex-shrink: 0;
  }
  .connect-name {
    font-family: var(--font-display);
    font-size: 12px; font-weight: 600;
    color: #fff; letter-spacing: 1px;
    text-transform: uppercase;
  }
  .connect-handle {
    font-family: var(--font-mono);
    font-size: 11px; color: var(--text-dim);
    margin-top: 3px;
  }

  /* ── FOOTER ── */
  footer {
    position: relative; z-index: 2;
    border-top: 1px solid var(--border);
    padding: 32px 0;
    text-align: center;
  }
  .footer-text {
    font-family: var(--font-mono);
    font-size: 11px; color: var(--text-dim);
    letter-spacing: 2px;
  }
  .footer-text span { color: var(--cyan); }

  /* ── ANIMATIONS ── */
  @keyframes fadeIn { from { opacity:0 } to { opacity:1 } }
  @keyframes fadeInDown { from { opacity:0; transform:translateY(-20px) } to { opacity:1; transform:none } }
  @keyframes fadeInUp { from { opacity:0; transform:translateY(20px) } to { opacity:1; transform:none } }
  @keyframes fadeInLeft { from { opacity:0; transform:translateX(-30px) } to { opacity:1; transform:none } }

  .reveal {
    opacity: 0; transform: translateY(30px);
    transition: opacity .7s ease, transform .7s ease;
  }
  .reveal.visible { opacity: 1; transform: none; }

  /* ── SCROLLBAR ── */
  ::-webkit-scrollbar { width: 4px; }
  ::-webkit-scrollbar-track { background: var(--bg); }
  ::-webkit-scrollbar-thumb { background: var(--cyan); border-radius: 2px; }

  /* ── RESPONSIVE ── */
  @media (max-width: 768px) {
    .nav-links { display: none; position: absolute; top: 60px; left: 0; right: 0;
      flex-direction: column; background: var(--bg2); padding: 20px;
      border-bottom: 1px solid var(--border); gap: 16px; }
    .nav-links.open { display: flex; }
    .nav-hamburger { display: flex; }

    .about-grid { grid-template-columns: 1fr; }
    .about-stats { grid-template-columns: 1fr 1fr; }

    section { padding: 60px 0; }
  }

  @media (max-width: 480px) {
    .hero-ctas { flex-direction: column; align-items: center; }
    .btn { width: 220px; text-align: center; }
    .about-stats { grid-template-columns: 1fr; }
  }
</style>
</head>
<body>

<canvas id="particles"></canvas>

<!-- NAV -->
<nav>
  <div class="nav-inner">
    <div class="nav-logo">M4RK<span>.</span>DEV</div>
    <ul class="nav-links" id="navLinks">
      <li><a href="#about">About</a></li>
      <li><a href="#stack">Stack</a></li>
      <li><a href="#connect">Connect</a></li>
    </ul>
    <button class="nav-hamburger" id="hamburger" aria-label="Menu">
      <span></span><span></span><span></span>
    </button>
  </div>
</nav>

<!-- HERO -->
<section class="hero">
  <div class="container">
    <div class="hero-content">
      <div class="hero-badge">Full-Stack Developer · Mobile · API Integration</div>

      <h1 class="hero-name">
        <span class="first">Mark </span><br/>
        <span class="last glitch" data-text="Bello">Bello</span>
      </h1>

      <p class="hero-role">
        <span>React</span> · Laravel · Node.js · React Native
      </p>

      <blockquote class="hero-quote">
        "You do not need to be perfect. You just need to be better than yesterday."
      </blockquote>

      <div class="hero-ctas">
        <a href="https://github.com/m4rkbello" target="_blank" class="btn btn-primary">GitHub Profile</a>
        <a href="mailto:markamarcortejopanesbello@gmail.com" class="btn btn-outline">Get In Touch</a>
      </div>
    </div>
  </div>
  <div class="hero-scroll">
    <span>Scroll</span>
    <div class="scroll-line"></div>
  </div>
</section>

<!-- ABOUT -->
<section id="about">
  <div class="container">
    <div class="section-header reveal">
      <div class="section-label">Profile</div>
      <h2 class="section-title">About <span>Me</span></h2>
      <div class="section-line"></div>
    </div>
    <div class="about-grid">
      <div class="about-text reveal">
        <p>I'm a <span>Full-Stack Web and Mobile Developer</span> with a strong focus on React, Laravel, and modern UI systems.</p>
        <p>Passionate about <span>clean architecture</span>, performance optimization, and continuous improvement in every project I touch.</p>
        <p>Currently expanding into <span>Mobile Development</span>, JavaScript Backend, API Integration, and Development Optimization.</p>
      </div>
      <div class="about-stats reveal">
        <div class="stat-card">
          <div class="stat-num">5+</div>
          <div class="stat-label">Technologies</div>
        </div>
        <div class="stat-card">
          <div class="stat-num">3+</div>
          <div class="stat-label">Databases</div>
        </div>
        <div class="stat-card">
          <div class="stat-num">6+</div>
          <div class="stat-label">Deployments</div>
        </div>
        <div class="stat-card">
          <div class="stat-num">∞</div>
          <div class="stat-label">Growth Mindset</div>
        </div>
      </div>
    </div>
  </div>
</section>

<!-- TECH STACK -->
<section id="stack">
  <div class="container">
    <div class="section-header reveal">
      <div class="section-label">Technologies</div>
      <h2 class="section-title">Tech <span>Stack</span></h2>
      <div class="section-line"></div>
    </div>

    <div class="stack-categories">

      <div class="reveal">
        <div class="stack-category-title">Languages</div>
        <div class="tech-grid">
          <div class="tech-pill c-cyan"><span class="dot"></span>JavaScript</div>
          <div class="tech-pill c-purple"><span class="dot"></span>TypeScript</div>
          <div class="tech-pill c-orange"><span class="dot"></span>PHP</div>
        </div>
      </div>

      <div class="reveal">
        <div class="stack-category-title">Frontend Frameworks</div>
        <div class="tech-grid">
          <div class="tech-pill c-cyan"><span class="dot"></span>React.js</div>
          <div class="tech-pill c-cyan"><span class="dot"></span>Next.js</div>
          <div class="tech-pill c-cyan"><span class="dot"></span>Vite</div>
          <div class="tech-pill c-cyan"><span class="dot"></span>Create React App</div>
        </div>
      </div>

      <div class="reveal">
        <div class="stack-category-title">UI Libraries</div>
        <div class="tech-grid">
          <div class="tech-pill c-cyan"><span class="dot"></span>TailwindCSS</div>
          <div class="tech-pill c-cyan"><span class="dot"></span>DaisyUI</div>
          <div class="tech-pill c-purple"><span class="dot"></span>shadcn/ui</div>
          <div class="tech-pill c-purple"><span class="dot"></span>Mantine</div>
          <div class="tech-pill c-orange"><span class="dot"></span>Bootstrap</div>
          <div class="tech-pill c-orange"><span class="dot"></span>React Bootstrap</div>
        </div>
      </div>

      <div class="reveal">
        <div class="stack-category-title">State Management</div>
        <div class="tech-grid">
          <div class="tech-pill c-purple"><span class="dot"></span>Redux</div>
          <div class="tech-pill c-purple"><span class="dot"></span>Redux Toolkit</div>
          <div class="tech-pill c-cyan"><span class="dot"></span>TanStack Query</div>
          <div class="tech-pill c-green"><span class="dot"></span>Zustand</div>
        </div>
      </div>

      <div class="reveal">
        <div class="stack-category-title">Backend</div>
        <div class="tech-grid">
          <div class="tech-pill c-orange"><span class="dot"></span>Laravel</div>
          <div class="tech-pill c-green"><span class="dot"></span>Node.js</div>
          <div class="tech-pill c-green"><span class="dot"></span>Express.js</div>
          <div class="tech-pill c-green"><span class="dot"></span>Bun.js</div>
          <div class="tech-pill c-green"><span class="dot"></span>ElysiaJS</div>
        </div>
      </div>

      <div class="reveal">
        <div class="stack-category-title">Databases</div>
        <div class="tech-grid">
          <div class="tech-pill c-cyan"><span class="dot"></span>MySQL</div>
          <div class="tech-pill c-green"><span class="dot"></span>MongoDB</div>
          <div class="tech-pill c-cyan"><span class="dot"></span>PostgreSQL</div>
          <div class="tech-pill c-orange"><span class="dot"></span>SQLite</div>
          <div class="tech-pill c-orange"><span class="dot"></span>Firebase</div>
          <div class="tech-pill c-green"><span class="dot"></span>Upstash</div>
        </div>
      </div>

      <div class="reveal">
        <div class="stack-category-title">Mobile Development</div>
        <div class="tech-grid">
          <div class="tech-pill c-cyan"><span class="dot"></span>React Native</div>
          <div class="tech-pill c-purple"><span class="dot"></span>Expo</div>
        </div>
      </div>

      <div class="reveal">
        <div class="stack-category-title">Hosting & Deployment</div>
        <div class="tech-grid">
          <div class="tech-pill c-purple"><span class="dot"></span>Vercel</div>
          <div class="tech-pill c-cyan"><span class="dot"></span>Netlify</div>
          <div class="tech-pill c-green"><span class="dot"></span>Render</div>
          <div class="tech-pill c-orange"><span class="dot"></span>Hostinger</div>
          <div class="tech-pill c-orange"><span class="dot"></span>cPanel</div>
          <div class="tech-pill c-purple"><span class="dot"></span>GitHub Pages</div>
        </div>
      </div>

      <div class="reveal">
        <div class="stack-category-title">Tools & Design</div>
        <div class="tech-grid">
          <div class="tech-pill c-orange"><span class="dot"></span>Figma</div>
          <div class="tech-pill c-orange"><span class="dot"></span>Photoshop</div>
          <div class="tech-pill c-orange"><span class="dot"></span>Illustrator</div>
          <div class="tech-pill c-cyan"><span class="dot"></span>Git</div>
          <div class="tech-pill c-purple"><span class="dot"></span>GitHub</div>
          <div class="tech-pill c-green"><span class="dot"></span>Postman</div>
          <div class="tech-pill c-green"><span class="dot"></span>Thunder Client</div>
          <div class="tech-pill c-cyan"><span class="dot"></span>Axios</div>
        </div>
      </div>

    </div>

    <!-- Full stack highlight banner -->
    <div class="fullstack-banner reveal">
      <div class="fs-item">
        <div class="fs-label">Frontend</div>
        <div class="fs-stack">React · Next.js<br/>TailwindCSS · TypeScript</div>
      </div>
      <div class="fs-item">
        <div class="fs-label">Backend</div>
        <div class="fs-stack">Laravel · Node.js<br/>Express · ElysiaJS</div>
      </div>
      <div class="fs-item">
        <div class="fs-label">Database</div>
        <div class="fs-stack">MySQL · PostgreSQL<br/>MongoDB · Firebase</div>
      </div>
      <div class="fs-item">
        <div class="fs-label">Mobile</div>
        <div class="fs-stack">React Native<br/>Expo</div>
      </div>
    </div>
  </div>
</section>

<!-- CONNECT -->
<section id="connect">
  <div class="container">
    <div class="section-header reveal">
      <div class="section-label">Social</div>
      <h2 class="section-title">Connect <span>With Me</span></h2>
      <div class="section-line"></div>
    </div>
    <div class="connect-grid">
      <a href="https://github.com/m4rkbello" target="_blank" class="connect-card reveal">
        <div class="connect-icon" style="background:rgba(255,255,255,0.05)">
          <svg width="22" height="22" viewBox="0 0 24 24" fill="white"><path d="M12 0C5.37 0 0 5.37 0 12c0 5.31 3.435 9.795 8.205 11.385.6.105.825-.255.825-.57 0-.285-.015-1.23-.015-2.235-3.015.555-3.795-.735-4.035-1.41-.135-.345-.72-1.41-1.23-1.695-.42-.225-1.02-.78-.015-.795.945-.015 1.62.87 1.845 1.23 1.08 1.815 2.805 1.305 3.495.99.105-.78.42-1.305.765-1.605-2.67-.3-5.46-1.335-5.46-5.925 0-1.305.465-2.385 1.23-3.225-.12-.3-.54-1.53.12-3.18 0 0 1.005-.315 3.3 1.23.96-.27 1.98-.405 3-.405s2.04.135 3 .405c2.295-1.56 3.3-1.23 3.3-1.23.66 1.65.24 2.88.12 3.18.765.84 1.23 1.905 1.23 3.225 0 4.605-2.805 5.625-5.475 5.925.435.375.81 1.095.81 2.22 0 1.605-.015 2.895-.015 3.3 0 .315.225.69.825.57A12.02 12.02 0 0024 12c0-6.63-5.37-12-12-12z"/></svg>
        </div>
        <div>
          <div class="connect-name">GitHub</div>
          <div class="connect-handle">@m4rkbello</div>
        </div>
      </a>
      <a href="mailto:markamarcortejopanesbello@gmail.com" class="connect-card reveal">
        <div class="connect-icon" style="background:rgba(234,67,53,0.1)">
          <svg width="22" height="22" viewBox="0 0 24 24" fill="none" stroke="#ea4335" stroke-width="2"><rect x="2" y="4" width="20" height="16" rx="2"/><path d="m2 7 10 7 10-7"/></svg>
        </div>
        <div>
          <div class="connect-name">Gmail</div>
          <div class="connect-handle">markamarcortejo...</div>
        </div>
      </a>
      <a href="https://www.youtube.com/@m4rkbello" target="_blank" class="connect-card reveal">
        <div class="connect-icon" style="background:rgba(255,0,0,0.1)">
          <svg width="22" height="22" viewBox="0 0 24 24" fill="#ff0000"><path d="M23.498 6.186a3.016 3.016 0 00-2.122-2.136C19.505 3.545 12 3.545 12 3.545s-7.505 0-9.377.505A3.017 3.017 0 00.502 6.186C0 8.07 0 12 0 12s0 3.93.502 5.814a3.016 3.016 0 002.122 2.136c1.871.505 9.376.505 9.376.505s7.505 0 9.377-.505a3.015 3.015 0 002.122-2.136C24 15.93 24 12 24 12s0-3.93-.502-5.814zM9.545 15.568V8.432L15.818 12l-6.273 3.568z"/></svg>
        </div>
        <div>
          <div class="connect-name">YouTube</div>
          <div class="connect-handle">@m4rkbello</div>
        </div>
      </a>
      <a href="https://dev.to/m4rkbello" target="_blank" class="connect-card reveal">
        <div class="connect-icon" style="background:rgba(255,255,255,0.05)">
          <svg width="22" height="22" viewBox="0 0 448 512" fill="white"><path d="M120.12 208.29c-3.88-2.9-7.77-4.35-11.65-4.35H91.03v104.47h17.45c3.88 0 7.77-1.45 11.65-4.35 3.88-2.9 5.82-7.25 5.82-13.06v-69.65c-.01-5.8-1.96-10.16-5.83-13.06zM404.1 32H43.9C19.7 32 .06 51.59 0 75.8v360.4C.06 460.41 19.7 480 43.9 480h360.2c24.21 0 43.84-19.59 43.9-43.8V75.8c-.06-24.21-19.7-43.8-43.9-43.8zM154.2 291.19c0 18.81-11.61 47.31-48.36 47.25h-46.4V172.98h47.38c35.44 0 47.36 28.46 47.37 47.28l.01 70.93zm100.68-88.66H201.6v38.42h32.57v29.57H201.6v38.41h53.29v29.57h-62.18c-11.16.29-20.44-8.53-20.72-19.69V193.7c-.27-11.15 8.56-20.41 19.71-20.69h63.19l-.01 29.52zm103.64 115.29c-13.2 30.75-36.85 24.63-47.44 0l-38.53-144.8h32.57l29.71 113.72 29.57-113.72h32.58l-38.46 144.8z"/></svg>
        </div>
        <div>
          <div class="connect-name">Dev.to</div>
          <div class="connect-handle">@m4rkbello</div>
        </div>
      </a>
    </div>
  </div>
</section>

<!-- FOOTER -->
<footer>
  <div class="container">
    <p class="footer-text">
      &copy; 2025 <span>Mark Bello</span> · Built with precision · Stay curious, keep building
    </p>
  </div>
</footer>

<script>
// ── PARTICLES ──
const canvas = document.getElementById('particles');
const ctx = canvas.getContext('2d');
let W, H, particles = [];

function resize() {
  W = canvas.width = window.innerWidth;
  H = canvas.height = window.innerHeight;
}
resize();
window.addEventListener('resize', () => { resize(); init(); });

function Particle() {
  this.reset = function() {
    this.x = Math.random() * W;
    this.y = Math.random() * H;
    this.size = Math.random() * 1.5 + .3;
    this.speedX = (Math.random() - .5) * .4;
    this.speedY = (Math.random() - .5) * .4;
    this.opacity = Math.random() * .5 + .1;
    this.color = Math.random() > .6 ? '#00e5ff' : Math.random() > .5 ? '#39ff14' : '#bf5fff';
  };
  this.reset();
}

function init() {
  particles = [];
  const count = Math.floor((W * H) / 15000);
  for (let i = 0; i < count; i++) particles.push(new Particle());
}
init();

function draw() {
  ctx.clearRect(0,0,W,H);
  particles.forEach(p => {
    ctx.beginPath();
    ctx.arc(p.x, p.y, p.size, 0, Math.PI*2);
    ctx.fillStyle = p.color;
    ctx.globalAlpha = p.opacity;
    ctx.fill();

    p.x += p.speedX;
    p.y += p.speedY;
    if (p.x < 0 || p.x > W || p.y < 0 || p.y > H) p.reset();
  });
  ctx.globalAlpha = 1;
  requestAnimationFrame(draw);
}
draw();

// ── SCROLL REVEAL ──
const observer = new IntersectionObserver(entries => {
  entries.forEach(e => { if (e.isIntersecting) e.target.classList.add('visible'); });
}, { threshold: .12 });
document.querySelectorAll('.reveal').forEach(el => observer.observe(el));

// ── HAMBURGER ──
const hamburger = document.getElementById('hamburger');
const navLinks = document.getElementById('navLinks');
hamburger.addEventListener('click', () => navLinks.classList.toggle('open'));
navLinks.querySelectorAll('a').forEach(a => a.addEventListener('click', () => navLinks.classList.remove('open')));
</script>
</body>
</html>
