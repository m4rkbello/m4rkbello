<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8"/>
<meta name="viewport" content="width=device-width, initial-scale=1.0"/>
<title>Mark Bello — Developer Portfolio</title>
<link rel="preconnect" href="https://fonts.googleapis.com"/>
<link href="https://fonts.googleapis.com/css2?family=Orbitron:wght@400;600;700;900&family=Share+Tech+Mono&family=Exo+2:wght@300;400;500;700&display=swap" rel="stylesheet"/>
<style>
:root {
  --bg:       #06040f;
  --bg2:      #0e0820;
  --panel:    rgba(14,8,32,0.9);
  --pink:     #ff10f0;
  --blue:     #00e5ff;
  --pink-dim: rgba(255,16,240,0.12);
  --blue-dim: rgba(0,229,255,0.12);
  --pink-glow:rgba(255,16,240,0.55);
  --blue-glow:rgba(0,229,255,0.55);
  --border-p: rgba(255,16,240,0.25);
  --border-b: rgba(0,229,255,0.25);
  --text:     #e2d4f0;
  --text-dim: #6a5a80;
  --fd: 'Orbitron', monospace;
  --fm: 'Share Tech Mono', monospace;
  --fb: 'Exo 2', sans-serif;
}
*,*::before,*::after{box-sizing:border-box;margin:0;padding:0}
html{scroll-behavior:smooth}
body{
  background:var(--bg);
  color:var(--text);
  font-family:var(--fb);
  overflow-x:hidden;
  cursor:none;
}

/* CUSTOM CURSOR */
#cursor{
  position:fixed;width:12px;height:12px;border-radius:50%;
  background:var(--pink);pointer-events:none;z-index:9999;
  transition:transform .15s;mix-blend-mode:screen;
  box-shadow:0 0 12px var(--pink-glow);
}
#cursor-ring{
  position:fixed;width:32px;height:32px;border-radius:50%;
  border:1px solid var(--blue);pointer-events:none;z-index:9998;
  transition:all .08s;mix-blend-mode:screen;
  transform:translate(-10px,-10px);
}

/* GRID BG */
body::before{
  content:'';position:fixed;inset:0;
  background-image:
    linear-gradient(rgba(255,16,240,0.03) 1px,transparent 1px),
    linear-gradient(90deg,rgba(0,229,255,0.03) 1px,transparent 1px);
  background-size:60px 60px;
  pointer-events:none;z-index:0;
  animation:gridShift 20s linear infinite;
}
@keyframes gridShift{from{background-position:0 0}to{background-position:60px 60px}}

/* SCANLINES */
body::after{
  content:'';position:fixed;inset:0;
  background:repeating-linear-gradient(0deg,transparent,transparent 3px,rgba(0,0,0,0.05) 3px,rgba(0,0,0,0.05) 6px);
  pointer-events:none;z-index:1;
}

canvas#bg{position:fixed;inset:0;z-index:0;pointer-events:none;}

.container{position:relative;z-index:2;max-width:1200px;margin:0 auto;padding:0 28px;}

/* NAV */
nav{
  position:fixed;top:0;left:0;right:0;z-index:100;
  padding:14px 0;
  background:rgba(6,4,15,0.85);
  backdrop-filter:blur(16px);
  border-bottom:1px solid var(--border-p);
}
.nav-inner{
  max-width:1200px;margin:0 auto;padding:0 28px;
  display:flex;align-items:center;justify-content:space-between;
}
.nav-logo{
  font-family:var(--fd);font-size:13px;font-weight:900;
  letter-spacing:4px;text-transform:uppercase;
  background:linear-gradient(90deg,var(--pink),var(--blue));
  -webkit-background-clip:text;-webkit-text-fill-color:transparent;
}
.nav-links{display:flex;gap:32px;list-style:none;}
.nav-links a{
  font-family:var(--fm);font-size:11px;color:var(--text-dim);
  text-decoration:none;letter-spacing:3px;text-transform:uppercase;
  transition:all .2s;position:relative;
}
.nav-links a::after{
  content:'';position:absolute;bottom:-4px;left:0;width:0;height:1px;
  background:var(--pink);transition:width .3s;
}
.nav-links a:hover{color:var(--pink);}
.nav-links a:hover::after{width:100%;}
.nav-ham{display:none;flex-direction:column;gap:5px;background:none;border:none;cursor:none;}
.nav-ham span{display:block;width:22px;height:2px;background:var(--pink);}

/* HERO */
.hero{
  min-height:100vh;display:flex;align-items:center;justify-content:center;
  padding-top:80px;position:relative;z-index:2;
}
.hero-inner{display:grid;grid-template-columns:1fr 1fr;gap:60px;align-items:center;}

.hero-left{}
.hero-badge{
  display:inline-flex;align-items:center;gap:8px;
  font-family:var(--fm);font-size:11px;color:var(--blue);
  letter-spacing:3px;text-transform:uppercase;
  border:1px solid var(--border-b);padding:7px 16px;border-radius:2px;
  margin-bottom:28px;
  animation:fadeInDown .7s ease both;
}
.hero-badge .dot{width:6px;height:6px;border-radius:50%;background:var(--blue);animation:pulse 1.4s infinite;}
@keyframes pulse{0%,100%{opacity:1;transform:scale(1)}50%{opacity:.5;transform:scale(.8)}}

.hero-name{
  font-family:var(--fd);font-weight:900;
  font-size:clamp(44px,6vw,80px);
  line-height:1;text-transform:uppercase;
  letter-spacing:-1px;
  animation:fadeInUp .7s .1s ease both;
}
.hero-name .line1{color:#fff;}
.hero-name .line2{
  background:linear-gradient(90deg,var(--pink),var(--blue));
  -webkit-background-clip:text;-webkit-text-fill-color:transparent;
  position:relative;display:inline-block;
}
/* GLITCH */
.glitch{position:relative;}
.glitch::before,.glitch::after{
  content:attr(data-text);position:absolute;top:0;left:0;
  background:linear-gradient(90deg,var(--pink),var(--blue));
  -webkit-background-clip:text;-webkit-text-fill-color:transparent;
}
.glitch::before{clip-path:polygon(0 20%,100% 20%,100% 40%,0 40%);animation:gb 4s infinite;}
.glitch::after{clip-path:polygon(0 65%,100% 65%,100% 80%,0 80%);animation:ga 4s infinite;}
@keyframes gb{0%,85%,100%{transform:translate(0);opacity:0}87%{transform:translate(-4px,1px);opacity:.9}89%{transform:translate(4px,-1px);opacity:.9}91%{transform:translate(0);opacity:0}}
@keyframes ga{0%,88%,100%{transform:translate(0);opacity:0}90%{transform:translate(4px,2px);opacity:.9}92%{transform:translate(-3px);opacity:.9}94%{transform:translate(0);opacity:0}}

.hero-role{
  font-family:var(--fm);font-size:clamp(11px,1.5vw,14px);
  color:var(--text-dim);letter-spacing:3px;text-transform:uppercase;
  margin-top:18px;animation:fadeInUp .7s .2s ease both;
}
.hero-role .hi{color:var(--pink);}
.hero-role .ha{color:var(--blue);}

.hero-quote{
  font-family:var(--fb);font-size:15px;font-weight:300;
  color:var(--text-dim);line-height:1.7;
  margin-top:24px;
  padding:14px 18px;
  border-left:2px solid var(--pink);
  background:var(--pink-dim);
  border-radius:0 4px 4px 0;
  animation:fadeInUp .7s .3s ease both;
}

.hero-btns{
  display:flex;gap:14px;flex-wrap:wrap;
  margin-top:32px;animation:fadeInUp .7s .4s ease both;
}
.btn{
  font-family:var(--fm);font-size:11px;letter-spacing:2px;
  text-transform:uppercase;padding:13px 26px;border-radius:2px;
  text-decoration:none;transition:all .25s;cursor:none;
}
.btn-p{background:var(--pink);color:#000;border:none;}
.btn-p:hover{box-shadow:0 0 30px var(--pink-glow),0 0 60px rgba(255,16,240,.2);transform:translateY(-2px);}
.btn-b{background:transparent;color:var(--blue);border:1px solid var(--blue);}
.btn-b:hover{background:var(--blue-dim);box-shadow:0 0 25px var(--blue-glow);transform:translateY(-2px);}

/* HERO RIGHT — TERMINAL */
.hero-right{animation:fadeInLeft .8s .2s ease both;}
.terminal{
  background:rgba(6,4,15,.95);
  border:1px solid var(--border-p);border-radius:8px;
  overflow:hidden;
  box-shadow:0 0 40px rgba(255,16,240,.12),0 0 80px rgba(0,0,0,.4);
}
.term-bar{
  display:flex;align-items:center;gap:8px;
  padding:10px 16px;
  background:rgba(255,16,240,.07);
  border-bottom:1px solid var(--border-p);
}
.term-dot{width:11px;height:11px;border-radius:50%;}
.td1{background:#ff5f57;}.td2{background:#febc2e;}.td3{background:#28c840;}
.term-title{
  flex:1;text-align:center;
  font-family:var(--fm);font-size:11px;color:var(--text-dim);letter-spacing:2px;
}
.term-body{padding:20px 22px;font-family:var(--fm);font-size:13px;line-height:2;}
.tc{color:var(--text-dim);}
.tp{color:var(--pink);}
.tb{color:var(--blue);}
.tg{color:#a8ff78;}
.ty{color:#ffd700;}
.tw{color:#fff;}
.caret{
  display:inline-block;width:8px;height:14px;
  background:var(--pink);
  animation:blink .8s step-end infinite;
  vertical-align:middle;margin-left:2px;
}
@keyframes blink{50%{opacity:0}}

/* SECTION */
section{padding:100px 0;position:relative;z-index:2;}
.section-header{margin-bottom:56px;}
.section-tag{
  font-family:var(--fm);font-size:10px;color:var(--blue);
  letter-spacing:5px;text-transform:uppercase;margin-bottom:10px;
}
.section-tag::before{content:'// ';color:var(--text-dim);}
.section-h{
  font-family:var(--fd);font-size:clamp(22px,3.5vw,38px);
  font-weight:700;color:#fff;text-transform:uppercase;letter-spacing:2px;
}
.section-h .hp{color:var(--pink);}
.section-h .hb{color:var(--blue);}
.section-bar{
  width:50px;height:2px;margin-top:14px;
  background:linear-gradient(90deg,var(--pink),var(--blue),transparent);
}

/* ── STATS GRID ── */
.stats-grid{
  display:grid;
  grid-template-columns:repeat(4,1fr);
  gap:16px;margin-bottom:60px;
}
.stat-card{
  background:var(--panel);
  border-radius:6px;padding:24px 20px;
  position:relative;overflow:hidden;
  transition:transform .3s,box-shadow .3s;
  border:1px solid transparent;
}
.stat-card:nth-child(odd){border-color:var(--border-p);}
.stat-card:nth-child(even){border-color:var(--border-b);}
.stat-card::before{
  content:'';position:absolute;top:0;left:0;right:0;height:2px;
}
.stat-card:nth-child(odd)::before{background:linear-gradient(90deg,var(--pink),transparent);}
.stat-card:nth-child(even)::before{background:linear-gradient(90deg,var(--blue),transparent);}
.stat-card:hover{transform:translateY(-5px);}
.stat-card:nth-child(odd):hover{box-shadow:0 12px 40px rgba(255,16,240,.15);}
.stat-card:nth-child(even):hover{box-shadow:0 12px 40px rgba(0,229,255,.15);}
.stat-num{
  font-family:var(--fd);font-size:34px;font-weight:900;
}
.stat-card:nth-child(odd) .stat-num{color:var(--pink);}
.stat-card:nth-child(even) .stat-num{color:var(--blue);}
.stat-label{
  font-family:var(--fm);font-size:10px;color:var(--text-dim);
  letter-spacing:2px;text-transform:uppercase;margin-top:4px;
}
.stat-icon{
  position:absolute;right:16px;top:50%;transform:translateY(-50%);
  font-size:28px;opacity:.15;
}

/* ── GITHUB STATS CARDS ── */
.gh-stats{
  display:grid;grid-template-columns:1fr 1fr;gap:20px;margin-bottom:24px;
}
.gh-card{
  background:var(--panel);border-radius:6px;overflow:hidden;
  border:1px solid var(--border-p);
  transition:transform .3s,box-shadow .3s;
}
.gh-card:nth-child(even){border-color:var(--border-b);}
.gh-card:hover{transform:translateY(-4px);}
.gh-card:nth-child(odd):hover{box-shadow:0 10px 35px rgba(255,16,240,.15);}
.gh-card:nth-child(even):hover{box-shadow:0 10px 35px rgba(0,229,255,.15);}
.gh-card img{width:100%;display:block;}
.gh-streak{
  background:var(--panel);border:1px solid var(--border-b);
  border-radius:6px;overflow:hidden;
  transition:transform .3s;
}
.gh-streak:hover{transform:translateY(-4px);box-shadow:0 10px 35px rgba(0,229,255,.15);}
.gh-streak img{width:100%;display:block;}

/* CONTRIB GRAPH */
.contrib-wrap{
  background:var(--panel);border:1px solid var(--border-p);
  border-radius:6px;overflow:hidden;margin-top:20px;
  transition:box-shadow .3s;
}
.contrib-wrap:hover{box-shadow:0 0 40px rgba(255,16,240,.12);}
.contrib-wrap img{width:100%;display:block;}

/* ── TECH STACK ── */
.stack-wrap{display:flex;flex-direction:column;gap:44px;}
.stack-row-title{
  font-family:var(--fm);font-size:11px;color:var(--text-dim);
  letter-spacing:3px;text-transform:uppercase;margin-bottom:14px;
  display:flex;align-items:center;gap:12px;
}
.stack-row-title::after{content:'';flex:1;height:1px;background:linear-gradient(90deg,var(--border-p),transparent);}
.tech-grid{display:flex;flex-wrap:wrap;gap:10px;}
.tech-pill{
  font-family:var(--fm);font-size:11px;letter-spacing:1px;
  padding:8px 14px;border-radius:3px;
  display:flex;align-items:center;gap:7px;
  cursor:default;transition:all .22s;
  position:relative;overflow:hidden;
  white-space:nowrap;
}
.tech-pill::before{
  content:'';position:absolute;inset:0;opacity:0;
  transition:opacity .22s;
}
.tech-pill:hover::before{opacity:1;}
.tech-pill:hover{transform:translateY(-3px);}

.tp-pink{
  background:var(--pink-dim);border:1px solid rgba(255,16,240,.2);
  color:rgba(255,16,240,.8);
}
.tp-pink::before{background:linear-gradient(135deg,rgba(255,16,240,.1),transparent);}
.tp-pink:hover{border-color:var(--pink);color:var(--pink);box-shadow:0 6px 20px rgba(255,16,240,.2);}

.tp-blue{
  background:var(--blue-dim);border:1px solid rgba(0,229,255,.2);
  color:rgba(0,229,255,.8);
}
.tp-blue::before{background:linear-gradient(135deg,rgba(0,229,255,.1),transparent);}
.tp-blue:hover{border-color:var(--blue);color:var(--blue);box-shadow:0 6px 20px rgba(0,229,255,.2);}

.tp-dot{width:5px;height:5px;border-radius:50%;flex-shrink:0;}
.tp-pink .tp-dot{background:var(--pink);}
.tp-blue .tp-dot{background:var(--blue);}

/* ── FULL STACK ARCH ── */
.arch-table{
  width:100%;border-collapse:collapse;
  background:var(--panel);
  border:1px solid var(--border-p);border-radius:6px;overflow:hidden;
  margin-top:48px;
}
.arch-table th{
  font-family:var(--fm);font-size:10px;letter-spacing:3px;
  text-transform:uppercase;padding:14px 20px;text-align:left;
  background:rgba(255,16,240,.08);
  border-bottom:1px solid var(--border-p);
}
.arch-table th:first-child{color:var(--pink);}
.arch-table th:last-child{color:var(--blue);}
.arch-table td{
  padding:14px 20px;
  font-family:var(--fm);font-size:12px;
  border-bottom:1px solid rgba(255,16,240,.06);
  transition:background .2s;
}
.arch-table tr:last-child td{border-bottom:none;}
.arch-table tr:hover td{background:rgba(255,16,240,.04);}
.arch-table td:first-child{
  color:var(--pink);font-weight:600;letter-spacing:1px;
}
.arch-table td:last-child{color:var(--text);line-height:1.8;}

/* ── TROPHIES SECTION ── */
.trophy-wrap{
  background:var(--panel);border:1px solid var(--border-b);
  border-radius:6px;overflow:hidden;margin-top:20px;
  transition:box-shadow .3s;
}
.trophy-wrap:hover{box-shadow:0 0 40px rgba(0,229,255,.12);}
.trophy-wrap img{width:100%;display:block;}

/* ── CONNECT ── */
.connect-grid{
  display:grid;grid-template-columns:repeat(auto-fill,minmax(230px,1fr));gap:18px;
}
.connect-card{
  background:var(--panel);border-radius:6px;padding:26px 22px;
  text-decoration:none;display:flex;align-items:center;gap:16px;
  transition:all .3s;position:relative;overflow:hidden;
  border:1px solid transparent;
}
.connect-card:nth-child(odd){border-color:var(--border-p);}
.connect-card:nth-child(even){border-color:var(--border-b);}
.connect-card::before{
  content:'';position:absolute;inset:0;opacity:0;transition:opacity .3s;
}
.connect-card:nth-child(odd)::before{background:linear-gradient(135deg,rgba(255,16,240,.06),transparent);}
.connect-card:nth-child(even)::before{background:linear-gradient(135deg,rgba(0,229,255,.06),transparent);}
.connect-card:hover::before{opacity:1;}
.connect-card:nth-child(odd):hover{border-color:var(--pink);box-shadow:0 10px 35px rgba(255,16,240,.15);transform:translateY(-4px);}
.connect-card:nth-child(even):hover{border-color:var(--blue);box-shadow:0 10px 35px rgba(0,229,255,.15);transform:translateY(-4px);}
.connect-card::after{
  content:'→';position:absolute;right:18px;
  font-family:var(--fm);opacity:0;transition:all .3s;
  transform:translateX(-8px);
}
.connect-card:nth-child(odd)::after{color:var(--pink);}
.connect-card:nth-child(even)::after{color:var(--blue);}
.connect-card:hover::after{opacity:1;transform:translateX(0);}
.cc-icon{width:44px;height:44px;border-radius:6px;display:flex;align-items:center;justify-content:center;flex-shrink:0;}
.cc-name{font-family:var(--fd);font-size:11px;font-weight:700;color:#fff;letter-spacing:1px;text-transform:uppercase;}
.cc-handle{font-family:var(--fm);font-size:11px;color:var(--text-dim);margin-top:3px;}

/* FOOTER */
footer{
  position:relative;z-index:2;
  border-top:1px solid var(--border-p);
  padding:28px 0;text-align:center;
}
.footer-txt{
  font-family:var(--fm);font-size:11px;color:var(--text-dim);letter-spacing:2px;
}
.footer-txt .fp{color:var(--pink);}
.footer-txt .fb{color:var(--blue);}

/* DIVIDER */
.neon-divider{
  width:100%;height:1px;
  background:linear-gradient(90deg,transparent,var(--pink),var(--blue),transparent);
  margin:4px 0;opacity:.4;
}

/* SCROLL INDICATOR */
.hero-scroll{
  position:absolute;bottom:30px;left:50%;transform:translateX(-50%);
  display:flex;flex-direction:column;align-items:center;gap:6px;
  animation:fadeIn 1s 1.2s ease both;
}
.hero-scroll span{font-family:var(--fm);font-size:9px;color:var(--text-dim);letter-spacing:3px;}
.scroll-line{width:1px;height:48px;background:linear-gradient(var(--pink),var(--blue),transparent);animation:spulse 1.6s infinite;}
@keyframes spulse{0%,100%{opacity:.3}50%{opacity:1}}

/* ANIMATIONS */
@keyframes fadeIn{from{opacity:0}to{opacity:1}}
@keyframes fadeInDown{from{opacity:0;transform:translateY(-18px)}to{opacity:1;transform:none}}
@keyframes fadeInUp{from{opacity:0;transform:translateY(20px)}to{opacity:1;transform:none}}
@keyframes fadeInLeft{from{opacity:0;transform:translateX(30px)}to{opacity:1;transform:none}}

.reveal{opacity:0;transform:translateY(28px);transition:opacity .65s ease,transform .65s ease;}
.reveal.in{opacity:1;transform:none;}

/* SCROLLBAR */
::-webkit-scrollbar{width:4px;}
::-webkit-scrollbar-track{background:var(--bg);}
::-webkit-scrollbar-thumb{background:linear-gradient(var(--pink),var(--blue));border-radius:2px;}

/* RESPONSIVE */
@media(max-width:900px){
  .hero-inner{grid-template-columns:1fr;}
  .hero-right{display:none;}
  .stats-grid{grid-template-columns:repeat(2,1fr);}
  .gh-stats{grid-template-columns:1fr;}
}
@media(max-width:768px){
  .nav-links{
    display:none;position:absolute;top:52px;left:0;right:0;
    flex-direction:column;background:rgba(6,4,15,.97);
    padding:20px;border-bottom:1px solid var(--border-p);gap:16px;
  }
  .nav-links.open{display:flex;}
  .nav-ham{display:flex;}
  section{padding:60px 0;}
}
@media(max-width:480px){
  .stats-grid{grid-template-columns:1fr 1fr;}
  .hero-btns{flex-direction:column;}
  .btn{text-align:center;}
}
</style>
</head>
<body>

<div id="cursor"></div>
<div id="cursor-ring"></div>
<canvas id="bg"></canvas>

<!-- NAV -->
<nav>
  <div class="nav-inner">
    <div class="nav-logo">M4RK.DEV</div>
    <ul class="nav-links" id="navLinks">
      <li><a href="#about">About</a></li>
      <li><a href="#stats">Stats</a></li>
      <li><a href="#stack">Stack</a></li>
      <li><a href="#connect">Connect</a></li>
    </ul>
    <button class="nav-ham" id="ham" aria-label="Menu">
      <span></span><span></span><span></span>
    </button>
  </div>
</nav>

<!-- HERO -->
<section class="hero">
  <div class="container">
    <div class="hero-inner">
      <div class="hero-left">
        <div class="hero-badge"><span class="dot"></span>Available for Collaboration</div>
        <h1 class="hero-name">
          <div class="line1">Mark</div>
          <div class="line2 glitch" data-text="Bello">Bello</div>
        </h1>
        <p class="hero-role">
          <span class="hi">React</span> · <span class="ha">Laravel</span> · <span class="hi">Node.js</span> · <span class="ha">React Native</span>
        </p>
        <blockquote class="hero-quote">
          "You do not need to be perfect.<br/>You just need to be better than yesterday."
        </blockquote>
        <div class="hero-btns">
          <a href="https://github.com/m4rkbello" target="_blank" class="btn btn-p">GitHub Profile</a>
          <a href="mailto:markamarcortejopanesbello@gmail.com" class="btn btn-b">Get In Touch</a>
        </div>
      </div>

      <!-- TERMINAL -->
      <div class="hero-right">
        <div class="terminal">
          <div class="term-bar">
            <div class="term-dot td1"></div>
            <div class="term-dot td2"></div>
            <div class="term-dot td3"></div>
            <div class="term-title">~/markbello — zsh</div>
          </div>
          <div class="term-body">
            <div><span class="tp">❯</span> <span class="tb">cat</span> <span class="tw">developer.ts</span></div>
            <div>&nbsp;</div>
            <div><span class="ty">const</span> <span class="tb">markBello</span> <span class="tc">= {</span></div>
            <div>&nbsp; <span class="tp">role</span><span class="tc">:</span> <span class="tg">"Full-Stack Developer"</span><span class="tc">,</span></div>
            <div>&nbsp; <span class="tp">focus</span><span class="tc">: [</span></div>
            <div>&nbsp;&nbsp;&nbsp; <span class="tg">"React"</span><span class="tc">,</span> <span class="tg">"Laravel"</span><span class="tc">,</span></div>
            <div>&nbsp;&nbsp;&nbsp; <span class="tg">"Modern UI Systems"</span></div>
            <div>&nbsp; <span class="tc">],</span></div>
            <div>&nbsp; <span class="tp">learning</span><span class="tc">: [</span><span class="tg">"Mobile"</span><span class="tc">,</span> <span class="tg">"JS Backend"</span><span class="tc">],</span></div>
            <div>&nbsp; <span class="tp">motto</span><span class="tc">:</span> <span class="tg">"Better than yesterday"</span></div>
            <div><span class="tc">};</span></div>
            <div>&nbsp;</div>
            <div><span class="tp">❯</span> <span class="tc">_</span><span class="caret"></span></div>
          </div>
        </div>
      </div>
    </div>
  </div>
  <div class="hero-scroll">
    <span>Scroll</span>
    <div class="scroll-line"></div>
  </div>
</section>

<div class="neon-divider"></div>

<!-- ABOUT -->
<section id="about">
  <div class="container">
    <div class="section-header reveal">
      <div class="section-tag">Profile</div>
      <h2 class="section-h">About <span class="hp">Me</span></h2>
      <div class="section-bar"></div>
    </div>
    <div class="stats-grid">
      <div class="stat-card reveal"><div class="stat-num">9+</div><div class="stat-label">Technologies</div><div class="stat-icon">⚡</div></div>
      <div class="stat-card reveal" style="animation-delay:.1s"><div class="stat-num">6+</div><div class="stat-label">Databases</div><div class="stat-icon">🗄️</div></div>
      <div class="stat-card reveal" style="animation-delay:.2s"><div class="stat-num">6+</div><div class="stat-label">Deployments</div><div class="stat-icon">☁️</div></div>
      <div class="stat-card reveal" style="animation-delay:.3s"><div class="stat-num">∞</div><div class="stat-label">Growth Mindset</div><div class="stat-icon">🚀</div></div>
    </div>
  </div>
</section>

<div class="neon-divider"></div>

<!-- GITHUB STATS -->
<section id="stats">
  <div class="container">
    <div class="section-header reveal">
      <div class="section-tag">Analytics</div>
      <h2 class="section-h"><span class="hb">GitHub</span> Stats</h2>
      <div class="section-bar"></div>
    </div>

    <div class="gh-stats reveal">
      <div class="gh-card">
        <img src="https://github-readme-stats.vercel.app/api?username=m4rkbello&show_icons=true&theme=tokyonight&border_color=ff10f0&bg_color=0e0820&title_color=ff10f0&icon_color=00e5ff&text_color=e2d4f0&hide_border=false&rank_icon=github&count_private=true" alt="GitHub Stats" loading="lazy"/>
      </div>
      <div class="gh-card">
        <img src="https://github-readme-stats.vercel.app/api/top-langs/?username=m4rkbello&layout=compact&theme=tokyonight&border_color=00e5ff&bg_color=0e0820&title_color=00e5ff&text_color=e2d4f0&hide_border=false" alt="Top Languages" loading="lazy"/>
      </div>
    </div>

    <div class="gh-streak reveal">
      <img src="https://github-readme-streak-stats.herokuapp.com?user=m4rkbello&theme=tokyonight&border=ff10f0&background=0e0820&stroke=ff10f0&ring=ff10f0&fire=00e5ff&currStreakLabel=ff10f0&sideLabels=e2d4f0&dates=6a5a80&sideNums=00e5ff&currStreakNum=ff10f0" alt="Streak Stats" loading="lazy" style="width:100%;display:block;"/>
    </div>

    <div class="contrib-wrap reveal">
      <img src="https://github-readme-activity-graph.vercel.app/graph?username=m4rkbello&bg_color=0e0820&color=ff10f0&line=00e5ff&point=ff10f0&area_color=ff10f0&area=true&hide_border=false&border_color=ff10f0&title_color=00e5ff" alt="Activity Graph" loading="lazy"/>
    </div>

    <div class="trophy-wrap reveal">
      <img src="https://github-profile-trophy.vercel.app/?username=m4rkbello&theme=tokyonight&no-frame=false&no-bg=false&margin-w=8&column=7&title=Stars,Commits,Repositories,Followers,PullRequest,Issues,Reviews" alt="Trophies" loading="lazy"/>
    </div>
  </div>
</section>

<div class="neon-divider"></div>

<!-- TECH STACK -->
<section id="stack">
  <div class="container">
    <div class="section-header reveal">
      <div class="section-tag">Technologies</div>
      <h2 class="section-h">Tech <span class="hp">Stack</span></h2>
      <div class="section-bar"></div>
    </div>

    <div class="stack-wrap">
      <div class="reveal">
        <div class="stack-row-title">Languages</div>
        <div class="tech-grid">
          <div class="tech-pill tp-blue"><span class="tp-dot"></span>JavaScript</div>
          <div class="tech-pill tp-pink"><span class="tp-dot"></span>TypeScript</div>
          <div class="tech-pill tp-blue"><span class="tp-dot"></span>PHP</div>
        </div>
      </div>

      <div class="reveal">
        <div class="stack-row-title">Frontend</div>
        <div class="tech-grid">
          <div class="tech-pill tp-blue"><span class="tp-dot"></span>React.js</div>
          <div class="tech-pill tp-pink"><span class="tp-dot"></span>Next.js</div>
          <div class="tech-pill tp-blue"><span class="tp-dot"></span>Vite</div>
          <div class="tech-pill tp-pink"><span class="tp-dot"></span>TailwindCSS</div>
          <div class="tech-pill tp-blue"><span class="tp-dot"></span>DaisyUI</div>
          <div class="tech-pill tp-pink"><span class="tp-dot"></span>shadcn/ui</div>
          <div class="tech-pill tp-blue"><span class="tp-dot"></span>Mantine</div>
          <div class="tech-pill tp-pink"><span class="tp-dot"></span>Bootstrap</div>
          <div class="tech-pill tp-blue"><span class="tp-dot"></span>React Bootstrap</div>
        </div>
      </div>

      <div class="reveal">
        <div class="stack-row-title">State Management</div>
        <div class="tech-grid">
          <div class="tech-pill tp-pink"><span class="tp-dot"></span>Redux</div>
          <div class="tech-pill tp-blue"><span class="tp-dot"></span>Redux Toolkit</div>
          <div class="tech-pill tp-pink"><span class="tp-dot"></span>TanStack Query</div>
          <div class="tech-pill tp-blue"><span class="tp-dot"></span>Zustand</div>
          <div class="tech-pill tp-pink"><span class="tp-dot"></span>Axios</div>
        </div>
      </div>

      <div class="reveal">
        <div class="stack-row-title">Backend</div>
        <div class="tech-grid">
          <div class="tech-pill tp-pink"><span class="tp-dot"></span>Laravel</div>
          <div class="tech-pill tp-blue"><span class="tp-dot"></span>Node.js</div>
          <div class="tech-pill tp-pink"><span class="tp-dot"></span>Express.js</div>
          <div class="tech-pill tp-blue"><span class="tp-dot"></span>Bun.js</div>
          <div class="tech-pill tp-pink"><span class="tp-dot"></span>ElysiaJS</div>
        </div>
      </div>

      <div class="reveal">
        <div class="stack-row-title">Databases</div>
        <div class="tech-grid">
          <div class="tech-pill tp-blue"><span class="tp-dot"></span>MySQL</div>
          <div class="tech-pill tp-pink"><span class="tp-dot"></span>PostgreSQL</div>
          <div class="tech-pill tp-blue"><span class="tp-dot"></span>MongoDB</div>
          <div class="tech-pill tp-pink"><span class="tp-dot"></span>SQLite</div>
          <div class="tech-pill tp-blue"><span class="tp-dot"></span>Firebase</div>
          <div class="tech-pill tp-pink"><span class="tp-dot"></span>Upstash</div>
        </div>
      </div>

      <div class="reveal">
        <div class="stack-row-title">Mobile</div>
        <div class="tech-grid">
          <div class="tech-pill tp-blue"><span class="tp-dot"></span>React Native</div>
          <div class="tech-pill tp-pink"><span class="tp-dot"></span>Expo</div>
        </div>
      </div>

      <div class="reveal">
        <div class="stack-row-title">Hosting & Deployment</div>
        <div class="tech-grid">
          <div class="tech-pill tp-pink"><span class="tp-dot"></span>Vercel</div>
          <div class="tech-pill tp-blue"><span class="tp-dot"></span>Netlify</div>
          <div class="tech-pill tp-pink"><span class="tp-dot"></span>Render</div>
          <div class="tech-pill tp-blue"><span class="tp-dot"></span>Hostinger</div>
          <div class="tech-pill tp-pink"><span class="tp-dot"></span>cPanel</div>
          <div class="tech-pill tp-blue"><span class="tp-dot"></span>GitHub Pages</div>
        </div>
      </div>

      <div class="reveal">
        <div class="stack-row-title">Design & Tools</div>
        <div class="tech-grid">
          <div class="tech-pill tp-pink"><span class="tp-dot"></span>Figma</div>
          <div class="tech-pill tp-blue"><span class="tp-dot"></span>Photoshop</div>
          <div class="tech-pill tp-pink"><span class="tp-dot"></span>Illustrator</div>
          <div class="tech-pill tp-blue"><span class="tp-dot"></span>Git</div>
          <div class="tech-pill tp-pink"><span class="tp-dot"></span>GitHub</div>
          <div class="tech-pill tp-blue"><span class="tp-dot"></span>Postman</div>
          <div class="tech-pill tp-pink"><span class="tp-dot"></span>Thunder Client</div>
        </div>
      </div>
    </div>

    <!-- ARCH TABLE -->
    <div class="reveal">
      <table class="arch-table">
        <thead>
          <tr>
            <th>Layer</th>
            <th>Stack</th>
          </tr>
        </thead>
        <tbody>
          <tr><td>Frontend</td><td>React.js · Next.js · TailwindCSS · TypeScript · Vite</td></tr>
          <tr><td>State</td><td>Redux Toolkit · TanStack Query · Zustand · Axios</td></tr>
          <tr><td>Backend</td><td>Laravel (API/Web) · Node.js · Express · ElysiaJS · Bun</td></tr>
          <tr><td>Database</td><td>MySQL · PostgreSQL · MongoDB · Firebase · SQLite · Upstash</td></tr>
          <tr><td>Mobile</td><td>React Native · Expo</td></tr>
          <tr><td>Deploy</td><td>Vercel · Netlify · Render · Hostinger · cPanel</td></tr>
        </tbody>
      </table>
    </div>
  </div>
</section>

<div class="neon-divider"></div>

<!-- CONNECT -->
<section id="connect">
  <div class="container">
    <div class="section-header reveal">
      <div class="section-tag">Social</div>
      <h2 class="section-h">Connect <span class="hb">With Me</span></h2>
      <div class="section-bar"></div>
    </div>
    <div class="connect-grid">
      <a href="https://github.com/m4rkbello" target="_blank" class="connect-card reveal">
        <div class="cc-icon" style="background:rgba(255,16,240,.1)">
          <svg width="22" height="22" viewBox="0 0 24 24" fill="#ff10f0"><path d="M12 0C5.37 0 0 5.37 0 12c0 5.31 3.435 9.795 8.205 11.385.6.105.825-.255.825-.57 0-.285-.015-1.23-.015-2.235-3.015.555-3.795-.735-4.035-1.41-.135-.345-.72-1.41-1.23-1.695-.42-.225-1.02-.78-.015-.795.945-.015 1.62.87 1.845 1.23 1.08 1.815 2.805 1.305 3.495.99.105-.78.42-1.305.765-1.605-2.67-.3-5.46-1.335-5.46-5.925 0-1.305.465-2.385 1.23-3.225-.12-.3-.54-1.53.12-3.18 0 0 1.005-.315 3.3 1.23.96-.27 1.98-.405 3-.405s2.04.135 3 .405c2.295-1.56 3.3-1.23 3.3-1.23.66 1.65.24 2.88.12 3.18.765.84 1.23 1.905 1.23 3.225 0 4.605-2.805 5.625-5.475 5.925.435.375.81 1.095.81 2.22 0 1.605-.015 2.895-.015 3.3 0 .315.225.69.825.57A12.02 12.02 0 0024 12c0-6.63-5.37-12-12-12z"/></svg>
        </div>
        <div><div class="cc-name">GitHub</div><div class="cc-handle">@m4rkbello</div></div>
      </a>
      <a href="mailto:markamarcortejopanesbello@gmail.com" class="connect-card reveal">
        <div class="cc-icon" style="background:rgba(0,229,255,.1)">
          <svg width="22" height="22" viewBox="0 0 24 24" fill="none" stroke="#00e5ff" stroke-width="2"><rect x="2" y="4" width="20" height="16" rx="2"/><path d="m2 7 10 7 10-7"/></svg>
        </div>
        <div><div class="cc-name">Gmail</div><div class="cc-handle">markamarcortejo...</div></div>
      </a>
      <a href="https://www.youtube.com/@m4rkbello" target="_blank" class="connect-card reveal">
        <div class="cc-icon" style="background:rgba(255,16,240,.1)">
          <svg width="22" height="22" viewBox="0 0 24 24" fill="#ff10f0"><path d="M23.498 6.186a3.016 3.016 0 00-2.122-2.136C19.505 3.545 12 3.545 12 3.545s-7.505 0-9.377.505A3.017 3.017 0 00.502 6.186C0 8.07 0 12 0 12s0 3.93.502 5.814a3.016 3.016 0 002.122 2.136c1.871.505 9.376.505 9.376.505s7.505 0 9.377-.505a3.015 3.015 0 002.122-2.136C24 15.93 24 12 24 12s0-3.93-.502-5.814zM9.545 15.568V8.432L15.818 12l-6.273 3.568z"/></svg>
        </div>
        <div><div class="cc-name">YouTube</div><div class="cc-handle">@m4rkbello</div></div>
      </a>
      <a href="https://dev.to/m4rkbello" target="_blank" class="connect-card reveal">
        <div class="cc-icon" style="background:rgba(0,229,255,.1)">
          <svg width="22" height="22" viewBox="0 0 448 512" fill="#00e5ff"><path d="M120.12 208.29c-3.88-2.9-7.77-4.35-11.65-4.35H91.03v104.47h17.45c3.88 0 7.77-1.45 11.65-4.35 3.88-2.9 5.82-7.25 5.82-13.06v-69.65c-.01-5.8-1.96-10.16-5.83-13.06zM404.1 32H43.9C19.7 32 .06 51.59 0 75.8v360.4C.06 460.41 19.7 480 43.9 480h360.2c24.21 0 43.84-19.59 43.9-43.8V75.8c-.06-24.21-19.7-43.8-43.9-43.8zM154.2 291.19c0 18.81-11.61 47.31-48.36 47.25h-46.4V172.98h47.38c35.44 0 47.36 28.46 47.37 47.28l.01 70.93zm100.68-88.66H201.6v38.42h32.57v29.57H201.6v38.41h53.29v29.57h-62.18c-11.16.29-20.44-8.53-20.72-19.69V193.7c-.27-11.15 8.56-20.41 19.71-20.69h63.19l-.01 29.52zm103.64 115.29c-13.2 30.75-36.85 24.63-47.44 0l-38.53-144.8h32.57l29.71 113.72 29.57-113.72h32.58l-38.46 144.8z"/></svg>
        </div>
        <div><div class="cc-name">Dev.to</div><div class="cc-handle">@m4rkbello</div></div>
      </a>
    </div>
  </div>
</section>

<!-- FOOTER -->
<footer>
  <div class="container">
    <p class="footer-txt">
      &copy; 2025 <span class="fp">Mark Bello</span> · Built with precision ·
      <span class="fb">Always Shipping ⚡</span>
    </p>
  </div>
</footer>

<script>
// ── CURSOR ──
const cur = document.getElementById('cursor');
const ring = document.getElementById('cursor-ring');
let mx=0,my=0,rx=0,ry=0;
document.addEventListener('mousemove',e=>{
  mx=e.clientX; my=e.clientY;
  cur.style.left=(mx-6)+'px'; cur.style.top=(my-6)+'px';
});
(function animRing(){
  rx+=(mx-rx-16)*.12; ry+=(my-ry-16)*.12;
  ring.style.left=rx+'px'; ring.style.top=ry+'px';
  requestAnimationFrame(animRing);
})();
document.querySelectorAll('a,button,.tech-pill,.stat-card').forEach(el=>{
  el.addEventListener('mouseenter',()=>{cur.style.transform='scale(2)';ring.style.transform='scale(1.5)';});
  el.addEventListener('mouseleave',()=>{cur.style.transform='scale(1)';ring.style.transform='scale(1)';});
});

// ── PARTICLES ──
const canvas=document.getElementById('bg');
const ctx=canvas.getContext('2d');
let W,H,pts=[];
function resize(){W=canvas.width=innerWidth;H=canvas.height=innerHeight;}
resize(); window.addEventListener('resize',()=>{resize();init();});
function Pt(){
  this.reset=function(){
    this.x=Math.random()*W; this.y=Math.random()*H;
    this.r=Math.random()*1.2+.3;
    this.vx=(Math.random()-.5)*.35; this.vy=(Math.random()-.5)*.35;
    this.o=Math.random()*.45+.05;
    this.c=Math.random()>.5?'#ff10f0':'#00e5ff';
  };
  this.reset();
}
function init(){pts=[];const n=Math.floor(W*H/14000);for(let i=0;i<n;i++)pts.push(new Pt());}
init();
// Lines between close particles
function drawLines(){
  for(let i=0;i<pts.length;i++){
    for(let j=i+1;j<pts.length;j++){
      const dx=pts[i].x-pts[j].x,dy=pts[i].y-pts[j].y;
      const d=Math.sqrt(dx*dx+dy*dy);
      if(d<120){
        ctx.beginPath();
        ctx.moveTo(pts[i].x,pts[i].y);
        ctx.lineTo(pts[j].x,pts[j].y);
        ctx.strokeStyle=pts[i].c;
        ctx.globalAlpha=(1-d/120)*.08;
        ctx.lineWidth=.5;
        ctx.stroke();
      }
    }
  }
}
function draw(){
  ctx.clearRect(0,0,W,H);
  pts.forEach(p=>{
    ctx.beginPath();ctx.arc(p.x,p.y,p.r,0,Math.PI*2);
    ctx.fillStyle=p.c;ctx.globalAlpha=p.o;ctx.fill();
    p.x+=p.vx;p.y+=p.vy;
    if(p.x<0||p.x>W||p.y<0||p.y>H)p.reset();
  });
  drawLines();
  ctx.globalAlpha=1;
  requestAnimationFrame(draw);
}
draw();

// ── SCROLL REVEAL ──
const obs=new IntersectionObserver(entries=>{
  entries.forEach(e=>{if(e.isIntersecting)e.target.classList.add('in');});
},{threshold:.1});
document.querySelectorAll('.reveal').forEach(el=>obs.observe(el));

// ── NAV HAMBURGER ──
const ham=document.getElementById('ham');
const nav=document.getElementById('navLinks');
ham.addEventListener('click',()=>nav.classList.toggle('open'));
nav.querySelectorAll('a').forEach(a=>a.addEventListener('click',()=>nav.classList.remove('open')));

// ── COUNTER ANIMATION ──
function animCount(el){
  const target=el.dataset.target;
  if(target==='∞'){el.textContent='∞';return;}
  const num=parseInt(target);
  let cur=0;const step=Math.ceil(num/40);
  const t=setInterval(()=>{
    cur=Math.min(cur+step,num);
    el.textContent=cur+'+';
    if(cur>=num)clearInterval(t);
  },30);
}
// Attach to stat numbers
document.querySelectorAll('.stat-num').forEach(el=>{
  const txt=el.textContent;
  if(txt==='∞'){el.dataset.target='∞';}
  else{el.dataset.target=parseInt(txt);el.textContent='0';}
});
const statObs=new IntersectionObserver(entries=>{
  entries.forEach(e=>{
    if(e.isIntersecting){
      animCount(e.target);
      statObs.unobserve(e.target);
    }
  });
},{threshold:.6});
document.querySelectorAll('.stat-num').forEach(el=>statObs.observe(el));
</script>
</body>
</html>
