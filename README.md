<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Musa — Developer Portfolio</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Space+Grotesk:wght@300;400;500;600;700&family=Space+Mono:ital,wght@0,400;0,700;1,400&family=Inter:wght@300;400;500&display=swap" rel="stylesheet">
<style>
  *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }

  :root {
    --bg: #060810;
    --bg2: #0b0f1a;
    --bg3: #111827;
    --cyan: #00d4ff;
    --cyan-dim: rgba(0, 212, 255, 0.15);
    --text: #e8eaf0;
    --text-muted: #6b7280;
    --text-dim: #9ca3af;
    --border: rgba(255,255,255,0.07);
    --border-cyan: rgba(0, 212, 255, 0.3);
    --radius: 12px;
    --nav-h: 64px;
  }

  html { scroll-behavior: smooth; }

  body {
    background: var(--bg);
    color: var(--text);
    font-family: 'Inter', sans-serif;
    font-size: 16px;
    line-height: 1.6;
    min-height: 100vh;
    overflow-x: hidden;
  }

  ::selection { background: rgba(0,212,255,0.2); color: #fff; }

  nav {
    position: fixed;
    top: 0; left: 0; right: 0;
    height: var(--nav-h);
    z-index: 100;
    display: flex;
    align-items: center;
    justify-content: space-between;
    padding: 0 2rem;
    background: rgba(6, 8, 16, 0.7);
    backdrop-filter: blur(16px);
    border-bottom: 1px solid var(--border);
  }

  .nav-logo {
    font-family: 'Space Mono', monospace;
    font-size: 14px;
    color: var(--cyan);
    text-decoration: none;
    letter-spacing: 0.08em;
  }

  .nav-links {
    display: flex;
    gap: 2rem;
    list-style: none;
  }

  .nav-links a {
    font-family: 'Space Grotesk', sans-serif;
    font-size: 13px;
    font-weight: 500;
    color: var(--text-dim);
    text-decoration: none;
    letter-spacing: 0.05em;
    text-transform: uppercase;
    transition: color 0.2s;
    cursor: pointer;
  }

  .nav-links a:hover,
  .nav-links a.active { color: var(--cyan); }

  .page {
    display: none;
    min-height: 100vh;
    padding-top: var(--nav-h);
    opacity: 0;
    transform: translateY(12px);
    transition: opacity 0.35s ease, transform 0.35s ease;
  }

  .page.active { display: block; }
  .page.visible { opacity: 1; transform: translateY(0); }

  #hero-canvas {
    position: absolute;
    top: 0; left: 0;
    width: 100%; height: 100%;
    pointer-events: none;
  }

  .hero {
    position: relative;
    min-height: 100vh;
    display: flex;
    align-items: center;
    justify-content: center;
    text-align: center;
    padding: 4rem 2rem;
    overflow: hidden;
  }

  .hero-content { position: relative; z-index: 1; max-width: 800px; }

  .hero-eyebrow {
    font-family: 'Space Mono', monospace;
    font-size: 11px;
    color: var(--cyan);
    letter-spacing: 0.2em;
    text-transform: uppercase;
    margin-bottom: 2rem;
  }

  .hero-name {
    font-family: 'Space Grotesk', sans-serif;
    font-size: clamp(3.5rem, 8vw, 7rem);
    font-weight: 700;
    line-height: 1;
    letter-spacing: -0.03em;
    color: #fff;
  }

  .hero-name .cursor-blink {
    color: var(--cyan);
    animation: blink 1s step-end infinite;
  }

  .hero-title {
    font-family: 'Space Grotesk', sans-serif;
    font-size: clamp(1rem, 2.5vw, 1.4rem);
    font-weight: 300;
    color: var(--text-dim);
    margin-top: 1.25rem;
    letter-spacing: 0.02em;
  }

  .hero-title span { color: var(--cyan); font-weight: 500; }

  .hero-stats {
    display: flex;
    gap: 3rem;
    justify-content: center;
    margin-top: 3rem;
  }

  .hero-stat-val {
    font-family: 'Space Grotesk', sans-serif;
    font-size: 2rem;
    font-weight: 700;
    color: var(--cyan);
    display: block;
  }

  .hero-stat-label {
    font-size: 11px;
    color: var(--text-muted);
    letter-spacing: 0.1em;
    text-transform: uppercase;
  }

  .btn {
    font-family: 'Space Grotesk', sans-serif;
    font-size: 13px;
    font-weight: 600;
    letter-spacing: 0.08em;
    text-transform: uppercase;
    padding: 0.75rem 1.75rem;
    border-radius: 6px;
    border: none;
    cursor: pointer;
    text-decoration: none;
    display: inline-flex;
    align-items: center;
    gap: 0.5rem;
    transition: all 0.2s;
  }

  .btn-primary {
    background: var(--cyan);
    color: #000;
  }

  .btn-primary:hover {
    background: #33deff;
    transform: translateY(-1px);
  }

  .btn-outline {
    background: transparent;
    color: var(--cyan);
    border: 1px solid var(--border-cyan);
  }

  .btn-outline:hover {
    background: var(--cyan-dim);
    transform: translateY(-1px);
  }

  .section {
    max-width: 1100px;
    margin: 0 auto;
    padding: 5rem 2rem;
  }

  .section-title {
    font-family: 'Space Grotesk', sans-serif;
    font-size: clamp(1.8rem, 4vw, 2.8rem);
    font-weight: 700;
    color: #fff;
    margin-bottom: 1rem;
  }

  .projects-grid {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(320px, 1fr));
    gap: 1.25rem;
  }

  .project-card {
    padding: 1.75rem;
    background: rgba(255,255,255,0.03);
    border: 1px solid var(--border);
    border-radius: var(--radius);
    transition: all 0.3s;
  }

  .project-card:hover {
    border-color: var(--border-cyan);
    background: rgba(0,212,255,0.04);
    transform: translateY(-4px);
  }

  .project-name {
    font-family: 'Space Grotesk', sans-serif;
    font-size: 1.2rem;
    font-weight: 600;
    color: #fff;
    margin-bottom: 0.75rem;
  }

  .project-desc {
    color: var(--text-dim);
    margin-bottom: 1rem;
    font-size: 14px;
    line-height: 1.6;
  }

  .project-link {
    color: var(--cyan);
    text-decoration: none;
    font-family: 'Space Mono', monospace;
    font-size: 13px;
  }

  @keyframes blink { 50% { opacity: 0; } }
</style>
</head>
<body>

<nav>
  <a class="nav-logo" onclick="showPage('home')">MUSA.DEV</a>
  <ul class="nav-links">
    <li><a onclick="showPage('home')" data-page="home" class="active">Home</a></li>
    <li><a onclick="showPage('projects')" data-page="projects">Projects</a></li>
    <li><a onclick="showPage('about')" data-page="about">About</a></li>
  </ul>
</nav>

<!-- HERO -->
<div id="page-home" class="page active">
  <section class="hero">
    <canvas id="hero-canvas"></canvas>
    <div class="hero-content">
      <p class="hero-eyebrow">// initialising portfolio.exe</p>
      <h1 class="hero-name">MUSA<span class="cursor-blink">_</span></h1>
      <p class="hero-title">Just having fun</p>
      <div style="margin-top: 3rem; display: flex; gap: 2rem; justify-content: center;">
        <a class="btn btn-primary" onclick="showPage('projects')">Explore Projects</a>
      </div>
    </div>
  </section>
</div>

<!-- PROJECTS -->
<div id="page-projects" class="page">
  <div class="section">
    <h2 class="section-title">Featured Projects</h2>
    <div class="projects-grid">

      <div class="project-card">
        <div class="project-name">Steam.exe</div>
        <div class="project-desc">Disguised executable that forces system shutdown and creates heavy files. Security / prank tool built with Cursor.</div>
        <a href="#" class="project-link">↓ Download (Windows)</a>
      </div>

      <div class="project-card">
        <div class="project-name">BFC.exe (Bruteforcer)</div>
        <div class="project-desc">Brute force tool for security research and testing.</div>
        <a href="#" class="project-link">↓ Download</a>
      </div>

      <div class="project-card">
        <div class="project-name">Pak Storm Watch</div>
        <div class="project-desc">Live weather/storm monitoring app.</div>
        <a href="https://pak-storm-watch.lovable.app" target="_blank" class="project-link">→ Live Demo</a>
      </div>

      <div class="project-card">
        <div class="project-name">Ooorbit</div>
        <div class="project-desc">Orbit simulation / space-themed project.</div>
        <a href="https://ooorbit.lovable.app" target="_blank" class="project-link">→ Live Demo</a>
      </div>

      <div class="project-card">
        <div class="project-name">Suitcase Packer</div>
        <div class="project-desc">Smart packing list / travel assistant.</div>
        <a href="https://suitcasepacker.lovable.app" target="_blank" class="project-link">→ Live Demo</a>
      </div>

      <div class="project-card">
        <div class="project-name">Marketier</div>
        <div class="project-desc">Market / e-commerce related tool.</div>
        <a href="https://marketier.lovable.app" target="_blank" class="project-link">→ Live Demo</a>
      </div>

      <div class="project-card">
        <div class="project-name">GymChimp</div>
        <div class="project-desc">Fitness / gym tracking app (Lovable).</div>
        <a href="https://gymchimp.lovable.app" target="_blank" class="project-link">→ Live Demo</a>
      </div>

      <div class="project-card">
        <div class="project-name">Keepy Uppy World Cup</div>
        <div class="project-desc">Fun football-themed mini-game.</div>
        <a href="https://keepy-uppy-world-cup-challenge.lovable.app" target="_blank" class="project-link">→ Live Demo</a>
      </div>

    </div>
  </div>
</div>

<!-- ABOUT -->
<div id="page-about" class="page">
  <div class="section">
    <h2 class="section-title">About Me</h2>
    <p> Dabble in security, AI, web apps, and building cool stuff.</p>
  </div>
</div>

<script>
  function showPage(page) {
    document.querySelectorAll('.page').forEach(p => p.classList.remove('active', 'visible'));
    const target = document.getElementById(`page-${page}`);
    if (target) {
      target.classList.add('active');
      setTimeout(() => target.classList.add('visible'), 50);
    }
    document.querySelectorAll('.nav-links a').forEach(a => {
      a.classList.toggle('active', a.getAttribute('data-page') === page);
    });
  }

  // Starfield
  const canvas = document.getElementById('hero-canvas');
  const ctx = canvas.getContext('2d');
  let W, H, stars = [];

  function resize() {
    W = canvas.width = canvas.offsetWidth;
    H = canvas.height = canvas.offsetHeight;
    stars = [];
    for (let i = 0; i < 300; i++) {
      stars.push({
        x: Math.random() * W,
        y: Math.random() * H,
        r: Math.random() * 1.5,
        speed: Math.random() * 0.5 + 0.2
      });
    }
  }

  function draw() {
    ctx.clearRect(0, 0, W, H);
    ctx.fillStyle = '#a0d8ff';
    stars.forEach(s => {
      ctx.beginPath();
      ctx.arc(s.x, s.y, s.r, 0, Math.PI * 2);
      ctx.fill();
      s.y -= s.speed;
      if (s.y < 0) s.y = H;
    });
    requestAnimationFrame(draw);
  }

  window.addEventListener('resize', resize);
  resize();
  draw();

  // Start on home
  showPage('home');
</script>
</body>
</html>
