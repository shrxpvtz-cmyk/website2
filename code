<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>FocusFlow — AI-Powered Student Productivity</title>

  <!-- Google Fonts: Syne (display) + DM Sans (body) -->
  <link rel="preconnect" href="https://fonts.googleapis.com" />
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin />
  <link href="https://fonts.googleapis.com/css2?family=Syne:wght@400;600;700;800&family=DM+Sans:ital,wght@0,300;0,400;0,500;1,400&display=swap" rel="stylesheet"/>

  <style>
    /* =========================================================
       DESIGN TOKENS & RESET
    ========================================================= */
    :root {
      --bg:          #070711;
      --bg2:         #0d0d1f;
      --surface:     rgba(255,255,255,0.04);
      --border:      rgba(255,255,255,0.08);
      --cyan:        #00e5ff;
      --violet:      #a855f7;
      --pink:        #f472b6;
      --gold:        #fbbf24;
      --text:        #e8e8f0;
      --muted:       #7878a0;
      --radius:      14px;
      --font-display:'Syne', sans-serif;
      --font-body:   'DM Sans', sans-serif;
    }

    *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }

    html { scroll-behavior: smooth; }

    body {
      background: var(--bg);
      color: var(--text);
      font-family: var(--font-body);
      font-size: 16px;
      line-height: 1.65;
      overflow-x: hidden;
    }

    /* =========================================================
       GLOBAL NOISE OVERLAY
    ========================================================= */
    body::before {
      content: '';
      position: fixed; inset: 0;
      background-image: url("data:image/svg+xml,%3Csvg viewBox='0 0 256 256' xmlns='http://www.w3.org/2000/svg'%3E%3Cfilter id='n'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='0.9' numOctaves='4' stitchTiles='stitch'/%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23n)' opacity='1'/%3E%3C/svg%3E");
      opacity: 0.025;
      pointer-events: none;
      z-index: 9999;
    }

    /* =========================================================
       TYPOGRAPHY HELPERS
    ========================================================= */
    h1,h2,h3,h4 { font-family: var(--font-display); font-weight: 800; letter-spacing: -0.02em; }

    .grad-text {
      background: linear-gradient(135deg, var(--cyan) 0%, var(--violet) 60%, var(--pink) 100%);
      -webkit-background-clip: text;
      -webkit-text-fill-color: transparent;
      background-clip: text;
    }

    .section-label {
      font-family: var(--font-display);
      font-size: 0.72rem;
      font-weight: 600;
      letter-spacing: 0.18em;
      text-transform: uppercase;
      color: var(--cyan);
      opacity: 0.85;
    }

    /* =========================================================
       LAYOUT UTILITIES
    ========================================================= */
    .container { max-width: 1140px; margin: 0 auto; padding: 0 24px; }
    .section    { padding: 96px 0; }
    .section-sm { padding: 56px 0; }

    .grid-2 { display: grid; grid-template-columns: 1fr 1fr; gap: 32px; }
    .grid-3 { display: grid; grid-template-columns: repeat(3,1fr); gap: 28px; }
    .grid-4 { display: grid; grid-template-columns: repeat(4,1fr); gap: 24px; }

    @media(max-width:900px){
      .grid-3,.grid-4 { grid-template-columns: 1fr 1fr; }
    }
    @media(max-width:640px){
      .grid-2,.grid-3,.grid-4 { grid-template-columns: 1fr; }
    }

    /* =========================================================
       CARD GLASS
    ========================================================= */
    .card {
      background: var(--surface);
      border: 1px solid var(--border);
      border-radius: var(--radius);
      padding: 28px;
      transition: transform .3s ease, box-shadow .3s ease, border-color .3s ease;
      position: relative;
      overflow: hidden;
    }
    .card::before {
      content:'';
      position:absolute; inset:0;
      background: linear-gradient(135deg, rgba(0,229,255,.04) 0%, transparent 60%);
      pointer-events:none;
    }
    .card:hover {
      transform: translateY(-6px);
      box-shadow: 0 24px 60px rgba(0,0,0,.5), 0 0 0 1px rgba(0,229,255,.18);
      border-color: rgba(0,229,255,.22);
    }

    /* =========================================================
       BUTTONS
    ========================================================= */
    .btn {
      display: inline-flex;
      align-items: center;
      gap: 8px;
      font-family: var(--font-display);
      font-weight: 700;
      font-size: .9rem;
      letter-spacing: .04em;
      padding: 13px 28px;
      border-radius: 50px;
      cursor: pointer;
      transition: all .25s ease;
      border: none;
      text-decoration: none;
    }
    .btn-primary {
      background: linear-gradient(135deg, var(--cyan), var(--violet));
      color: #fff;
      box-shadow: 0 0 24px rgba(0,229,255,.25);
    }
    .btn-primary:hover {
      transform: translateY(-2px) scale(1.03);
      box-shadow: 0 0 40px rgba(0,229,255,.45);
    }
    .btn-outline {
      background: transparent;
      color: var(--text);
      border: 1px solid var(--border);
    }
    .btn-outline:hover {
      border-color: var(--cyan);
      color: var(--cyan);
      box-shadow: 0 0 16px rgba(0,229,255,.12);
    }
    .btn-sm { padding: 9px 18px; font-size: .82rem; }

    /* =========================================================
       NAV
    ========================================================= */
    #nav {
      position: fixed; top: 0; left: 0; right: 0;
      z-index: 1000;
      padding: 0 24px;
      background: rgba(7,7,17,.7);
      backdrop-filter: blur(18px);
      border-bottom: 1px solid var(--border);
      transition: background .3s;
    }
    .nav-inner {
      max-width: 1140px;
      margin: 0 auto;
      display: flex;
      align-items: center;
      height: 64px;
      gap: 0;
    }
    .nav-logo {
      font-family: var(--font-display);
      font-weight: 800;
      font-size: 1.25rem;
      text-decoration: none;
      color: var(--text);
      margin-right: auto;
    }
    .nav-logo span { color: var(--cyan); }

    .nav-links {
      display: flex;
      gap: 6px;
      list-style: none;
    }
    .nav-links a {
      text-decoration: none;
      color: var(--muted);
      font-size: .88rem;
      font-weight: 500;
      padding: 7px 14px;
      border-radius: 8px;
      transition: color .2s, background .2s;
    }
    .nav-links a:hover,
    .nav-links a.active { color: var(--cyan); background: rgba(0,229,255,.07); }

    .nav-cta { margin-left: 16px; }

    /* Hamburger */
    .hamburger {
      display: none;
      flex-direction: column;
      gap: 5px;
      cursor: pointer;
      margin-left: 16px;
    }
    .hamburger span {
      display: block; width: 24px; height: 2px;
      background: var(--text);
      border-radius: 2px;
      transition: all .3s;
    }
    .hamburger.open span:nth-child(1) { transform: translateY(7px) rotate(45deg); }
    .hamburger.open span:nth-child(2) { opacity: 0; }
    .hamburger.open span:nth-child(3) { transform: translateY(-7px) rotate(-45deg); }

    .mobile-menu {
      display: none;
      position: fixed;
      top: 64px; left: 0; right: 0;
      background: rgba(7,7,17,.97);
      backdrop-filter: blur(20px);
      border-bottom: 1px solid var(--border);
      padding: 20px 24px;
      z-index: 999;
      flex-direction: column;
      gap: 6px;
    }
    .mobile-menu.open { display: flex; }
    .mobile-menu a {
      text-decoration: none;
      color: var(--text);
      font-weight: 500;
      padding: 12px 0;
      border-bottom: 1px solid var(--border);
      font-size: 1rem;
    }

    @media(max-width:768px){
      .nav-links, .nav-cta { display: none; }
      .hamburger { display: flex; }
    }

    /* =========================================================
       PAGE SYSTEM — show/hide pages
    ========================================================= */
    .page { display: none; }
    .page.active { display: block; }

    /* =========================================================
       ✦  PAGE: HOME
    ========================================================= */

    /* Ambient blobs */
    .hero {
      min-height: 100vh;
      display: flex;
      align-items: center;
      position: relative;
      overflow: hidden;
      padding-top: 80px;
    }
    .blob {
      position: absolute;
      border-radius: 50%;
      filter: blur(90px);
      opacity: 0.18;
      pointer-events: none;
    }
    .blob-1 {
      width: 600px; height: 600px;
      background: radial-gradient(circle, var(--violet), transparent);
      top: -200px; right: -150px;
      animation: blobPulse 8s ease-in-out infinite;
    }
    .blob-2 {
      width: 500px; height: 500px;
      background: radial-gradient(circle, var(--cyan), transparent);
      bottom: -200px; left: -100px;
      animation: blobPulse 10s ease-in-out infinite reverse;
    }
    .blob-3 {
      width: 300px; height: 300px;
      background: radial-gradient(circle, var(--pink), transparent);
      top: 40%; left: 40%;
      animation: blobPulse 7s ease-in-out infinite 2s;
    }
    @keyframes blobPulse {
      0%,100% { transform: scale(1) translate(0,0); }
      50% { transform: scale(1.12) translate(20px, -20px); }
    }

    .hero-content { position: relative; z-index: 2; max-width: 720px; }
    .hero-badge {
      display: inline-flex;
      align-items: center;
      gap: 8px;
      background: rgba(0,229,255,.08);
      border: 1px solid rgba(0,229,255,.2);
      border-radius: 50px;
      padding: 6px 16px;
      font-size: .8rem;
      font-weight: 600;
      color: var(--cyan);
      letter-spacing: .06em;
      text-transform: uppercase;
      margin-bottom: 24px;
      animation: fadeUp .7s ease both;
    }
    .hero-badge .dot {
      width: 6px; height: 6px;
      background: var(--cyan);
      border-radius: 50%;
      animation: dotPulse 1.4s ease-in-out infinite;
    }
    @keyframes dotPulse {
      0%,100% { opacity: 1; transform: scale(1); }
      50% { opacity: .3; transform: scale(.6); }
    }

    .hero h1 {
      font-size: clamp(2.6rem, 6vw, 4.8rem);
      line-height: 1.08;
      margin-bottom: 20px;
      animation: fadeUp .8s ease .1s both;
    }
    .hero p {
      font-size: 1.15rem;
      color: var(--muted);
      max-width: 560px;
      margin-bottom: 36px;
      animation: fadeUp .8s ease .2s both;
    }
    .hero-actions {
      display: flex;
      gap: 14px;
      flex-wrap: wrap;
      animation: fadeUp .8s ease .3s both;
    }
    .hero-stats {
      display: flex;
      gap: 40px;
      margin-top: 56px;
      animation: fadeUp .8s ease .4s both;
    }
    .hero-stat h3 {
      font-size: 2rem;
      color: var(--cyan);
    }
    .hero-stat p { font-size: .85rem; color: var(--muted); margin: 0; }

    @keyframes fadeUp {
      from { opacity: 0; transform: translateY(24px); }
      to   { opacity: 1; transform: translateY(0); }
    }

    /* Floating device mockup */
    .hero-visual {
      position: absolute;
      right: -60px;
      top: 50%;
      transform: translateY(-50%);
      width: 420px;
      animation: floatDevice 6s ease-in-out infinite, fadeUp .9s ease .2s both;
      z-index: 1;
      pointer-events: none;
    }
    @keyframes floatDevice {
      0%,100% { transform: translateY(-50%) translateY(0); }
      50% { transform: translateY(-50%) translateY(-18px); }
    }
    .mock-window {
      background: rgba(13,13,31,0.9);
      border: 1px solid var(--border);
      border-radius: 16px;
      padding: 20px;
      box-shadow: 0 40px 80px rgba(0,0,0,.6), 0 0 0 1px rgba(0,229,255,.1);
      backdrop-filter: blur(10px);
    }
    .mock-titlebar {
      display: flex;
      align-items: center;
      gap: 6px;
      margin-bottom: 16px;
    }
    .mock-dot { width: 10px; height: 10px; border-radius: 50%; }
    .mock-dot.r { background: #ff5f57; }
    .mock-dot.y { background: #febc2e; }
    .mock-dot.g { background: #28c840; }
    .mock-title-bar-text { font-size: .75rem; color: var(--muted); margin-left: 8px; }

    .mock-timer-ring {
      width: 120px; height: 120px;
      border-radius: 50%;
      background: conic-gradient(var(--cyan) 0% 65%, var(--surface) 65% 100%);
      display: flex;
      align-items: center;
      justify-content: center;
      margin: 0 auto 16px;
      position: relative;
      box-shadow: 0 0 30px rgba(0,229,255,.2);
    }
    .mock-timer-ring::after {
      content: '';
      position: absolute;
      inset: 10px;
      border-radius: 50%;
      background: var(--bg2);
    }
    .mock-timer-text {
      position: relative;
      z-index: 1;
      font-family: var(--font-display);
      font-size: 1.4rem;
      font-weight: 800;
      color: var(--cyan);
    }
    .mock-task-list { display: flex; flex-direction: column; gap: 8px; }
    .mock-task {
      display: flex;
      align-items: center;
      gap: 10px;
      background: rgba(255,255,255,.03);
      border: 1px solid var(--border);
      border-radius: 8px;
      padding: 8px 12px;
      font-size: .78rem;
      color: var(--muted);
    }
    .mock-task-check {
      width: 14px; height: 14px;
      border-radius: 50%;
      border: 1.5px solid var(--cyan);
      flex-shrink: 0;
    }
    .mock-task-check.done {
      background: var(--cyan);
      border-color: var(--cyan);
    }

    @media(max-width:1000px){ .hero-visual { display: none; } }
    @media(max-width:640px){
      .hero-stats { gap: 24px; flex-wrap: wrap; }
      .hero-stat h3 { font-size: 1.5rem; }
    }

    /* --- FEATURES section --- */
    .section-heading {
      text-align: center;
      margin-bottom: 56px;
    }
    .section-heading h2 {
      font-size: clamp(1.8rem, 4vw, 2.8rem);
      margin-top: 10px;
      margin-bottom: 14px;
    }
    .section-heading p {
      font-size: 1.05rem;
      color: var(--muted);
      max-width: 520px;
      margin: 0 auto;
    }

    .feat-icon {
      width: 48px; height: 48px;
      border-radius: 12px;
      display: flex;
      align-items: center;
      justify-content: center;
      font-size: 1.4rem;
      margin-bottom: 16px;
    }
    .feat-icon.c  { background: rgba(0,229,255,.12); }
    .feat-icon.v  { background: rgba(168,85,247,.12); }
    .feat-icon.p  { background: rgba(244,114,182,.12); }
    .feat-icon.g  { background: rgba(251,191,36,.1); }

    .card h3 { font-size: 1.1rem; margin-bottom: 8px; }
    .card p   { font-size: .9rem; color: var(--muted); }

    /* --- HOW IT WORKS --- */
    .steps-wrap {
      display: flex;
      flex-direction: column;
      gap: 0;
      position: relative;
    }
    .steps-wrap::before {
      content: '';
      position: absolute;
      left: 28px;
      top: 0; bottom: 0;
      width: 2px;
      background: linear-gradient(to bottom, var(--cyan), var(--violet), var(--pink));
      opacity: .3;
    }
    .step {
      display: flex;
      gap: 28px;
      padding: 32px 0;
      animation: fadeUp .6s ease both;
    }
    .step-num {
      flex-shrink: 0;
      width: 56px; height: 56px;
      border-radius: 50%;
      background: linear-gradient(135deg, var(--cyan), var(--violet));
      display: flex;
      align-items: center;
      justify-content: center;
      font-family: var(--font-display);
      font-weight: 800;
      font-size: 1.1rem;
      color: #fff;
      position: relative;
      z-index: 1;
      box-shadow: 0 0 20px rgba(0,229,255,.3);
    }
    .step-body h3 { font-size: 1.2rem; margin-bottom: 8px; }
    .step-body p  { font-size: .92rem; color: var(--muted); }

    /* --- TESTIMONIALS --- */
    .testi-grid {
      display: grid;
      grid-template-columns: repeat(3,1fr);
      gap: 24px;
    }
    @media(max-width:900px){ .testi-grid { grid-template-columns: 1fr 1fr; } }
    @media(max-width:600px){ .testi-grid { grid-template-columns: 1fr; } }

    .testi-card {
      background: var(--surface);
      border: 1px solid var(--border);
      border-radius: var(--radius);
      padding: 28px;
      transition: transform .3s, box-shadow .3s;
    }
    .testi-card:hover {
      transform: translateY(-4px);
      box-shadow: 0 20px 50px rgba(0,0,0,.4);
    }
    .stars { color: var(--gold); font-size: .85rem; margin-bottom: 14px; letter-spacing: 2px; }
    .testi-card p { font-size: .9rem; color: var(--muted); font-style: italic; margin-bottom: 20px; }
    .testi-author { display: flex; align-items: center; gap: 12px; }
    .avatar {
      width: 38px; height: 38px;
      border-radius: 50%;
      display: flex;
      align-items: center;
      justify-content: center;
      font-weight: 700;
      font-size: .9rem;
      color: #fff;
      flex-shrink: 0;
    }
    .av1 { background: linear-gradient(135deg, #00e5ff, #a855f7); }
    .av2 { background: linear-gradient(135deg, #f472b6, #fbbf24); }
    .av3 { background: linear-gradient(135deg, #a855f7, #f472b6); }
    .av4 { background: linear-gradient(135deg, #00e5ff, #28c840); }
    .av5 { background: linear-gradient(135deg, #fbbf24, #f472b6); }
    .av6 { background: linear-gradient(135deg, #28c840, #00e5ff); }
    .testi-author-info strong { font-size: .88rem; display: block; }
    .testi-author-info span  { font-size: .78rem; color: var(--muted); }

    /* =========================================================
       ✦  PAGE: FEATURES
    ========================================================= */
    .feat-hero {
      padding: 140px 0 80px;
      text-align: center;
      position: relative;
      overflow: hidden;
    }
    .feat-hero h1 { font-size: clamp(2rem, 5vw, 3.5rem); margin: 12px 0; }
    .feat-hero p  { font-size: 1.1rem; color: var(--muted); max-width: 540px; margin: 0 auto; }

    .feat-detail {
      display: grid;
      grid-template-columns: 1fr 1fr;
      gap: 48px;
      align-items: center;
      padding: 72px 0;
      border-bottom: 1px solid var(--border);
    }
    .feat-detail:last-child { border-bottom: none; }
    .feat-detail.reverse .feat-detail-visual { order: -1; }
    @media(max-width:768px){
      .feat-detail { grid-template-columns: 1fr; }
      .feat-detail.reverse .feat-detail-visual { order: unset; }
    }

    .feat-tag {
      display: inline-block;
      font-size: .72rem;
      font-weight: 700;
      letter-spacing: .12em;
      text-transform: uppercase;
      padding: 4px 12px;
      border-radius: 50px;
      margin-bottom: 16px;
    }
    .tag-cyan   { background: rgba(0,229,255,.12); color: var(--cyan); }
    .tag-violet { background: rgba(168,85,247,.12); color: var(--violet); }
    .tag-pink   { background: rgba(244,114,182,.12); color: var(--pink); }
    .tag-gold   { background: rgba(251,191,36,.1);  color: var(--gold); }

    .feat-detail-text h2 { font-size: clamp(1.6rem, 3.5vw, 2.2rem); margin-bottom: 14px; }
    .feat-detail-text p  { color: var(--muted); margin-bottom: 20px; font-size: .95rem; }

    .feat-bullets { list-style: none; display: flex; flex-direction: column; gap: 10px; }
    .feat-bullets li {
      display: flex;
      align-items: center;
      gap: 10px;
      font-size: .9rem;
      color: var(--muted);
    }
    .feat-bullets li::before {
      content: '✦';
      color: var(--cyan);
      font-size: .7rem;
      flex-shrink: 0;
    }

    .feat-detail-visual {
      border-radius: 20px;
      overflow: hidden;
      border: 1px solid var(--border);
      background: var(--surface);
      padding: 28px;
      box-shadow: 0 32px 80px rgba(0,0,0,.5);
      min-height: 280px;
      display: flex;
      flex-direction: column;
      justify-content: center;
      position: relative;
    }
    .feat-detail-visual::before {
      content:'';
      position:absolute; inset:0;
      background: linear-gradient(135deg, rgba(0,229,255,.04) 0%, transparent 60%);
      pointer-events:none;
    }

    /* Analytics mock chart */
    .bar-chart {
      display: flex;
      align-items: flex-end;
      gap: 8px;
      height: 120px;
      padding-top: 20px;
    }
    .bar-col {
      flex: 1;
      display: flex;
      flex-direction: column;
      align-items: center;
      gap: 6px;
    }
    .bar {
      width: 100%;
      border-radius: 6px 6px 0 0;
      transition: height .5s ease;
    }
    .bar-label { font-size: .65rem; color: var(--muted); }

    /* AI card mock */
    .ai-suggestions { display: flex; flex-direction: column; gap: 12px; }
    .ai-card {
      background: rgba(168,85,247,.07);
      border: 1px solid rgba(168,85,247,.18);
      border-radius: 10px;
      padding: 12px 16px;
      font-size: .82rem;
      display: flex;
      gap: 10px;
      align-items: flex-start;
    }
    .ai-icon { font-size: 1rem; flex-shrink: 0; }
    .ai-text strong { display: block; color: var(--text); margin-bottom: 2px; }
    .ai-text span   { color: var(--muted); }

    /* =========================================================
       ✦  PAGE: TOOLS
    ========================================================= */
    .tools-hero {
      padding: 140px 0 60px;
      text-align: center;
    }
    .tools-hero h1 { font-size: clamp(2rem, 5vw, 3.2rem); margin: 12px 0; }
    .tools-hero p  { font-size: 1.05rem; color: var(--muted); }

    .tools-grid {
      display: grid;
      grid-template-columns: 1fr 1fr;
      gap: 28px;
      padding-bottom: 96px;
    }
    @media(max-width:768px){ .tools-grid { grid-template-columns: 1fr; } }

    .tool-card {
      background: var(--surface);
      border: 1px solid var(--border);
      border-radius: 20px;
      padding: 32px;
      position: relative;
      overflow: hidden;
    }
    .tool-card::before {
      content:'';
      position:absolute; inset:0;
      background: linear-gradient(135deg, rgba(0,229,255,.03) 0%, transparent 70%);
      pointer-events:none;
    }
    .tool-card-header {
      display: flex;
      align-items: center;
      gap: 12px;
      margin-bottom: 28px;
    }
    .tool-icon {
      width: 44px; height: 44px;
      border-radius: 12px;
      display: flex; align-items: center; justify-content: center;
      font-size: 1.2rem;
    }
    .tool-card-header h3 { font-size: 1.15rem; }
    .tool-card-header p  { font-size: .8rem; color: var(--muted); margin: 0; }

    /* --- POMODORO TIMER --- */
    .pomo-ring-wrap {
      display: flex;
      justify-content: center;
      margin-bottom: 24px;
    }
    .pomo-ring {
      width: 180px; height: 180px;
      position: relative;
    }
    .pomo-ring svg {
      width: 100%; height: 100%;
      transform: rotate(-90deg);
    }
    .pomo-ring-bg { fill: none; stroke: rgba(255,255,255,.06); stroke-width: 8; }
    .pomo-ring-progress {
      fill: none;
      stroke: url(#timerGrad);
      stroke-width: 8;
      stroke-linecap: round;
      stroke-dasharray: 502;
      stroke-dashoffset: 0;
      transition: stroke-dashoffset .5s ease;
    }
    .pomo-time {
      position: absolute;
      inset: 0;
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: center;
      font-family: var(--font-display);
    }
    .pomo-time .time-display {
      font-size: 2.4rem;
      font-weight: 800;
      color: var(--text);
      line-height: 1;
    }
    .pomo-time .time-label {
      font-size: .72rem;
      color: var(--muted);
      letter-spacing: .1em;
      text-transform: uppercase;
      margin-top: 4px;
    }
    .pomo-mode {
      display: flex;
      gap: 8px;
      margin-bottom: 20px;
      justify-content: center;
    }
    .pomo-mode-btn {
      padding: 6px 14px;
      border-radius: 50px;
      border: 1px solid var(--border);
      background: transparent;
      color: var(--muted);
      font-size: .78rem;
      font-weight: 600;
      cursor: pointer;
      font-family: var(--font-body);
      transition: all .2s;
    }
    .pomo-mode-btn.active {
      background: rgba(0,229,255,.12);
      border-color: rgba(0,229,255,.3);
      color: var(--cyan);
    }
    .pomo-controls {
      display: flex;
      gap: 10px;
      justify-content: center;
    }
    .pomo-controls button {
      padding: 10px 22px;
      border-radius: 50px;
      border: none;
      font-family: var(--font-display);
      font-weight: 700;
      font-size: .85rem;
      cursor: pointer;
      transition: all .2s;
    }
    #pomoStart {
      background: linear-gradient(135deg, var(--cyan), var(--violet));
      color: #fff;
      min-width: 90px;
    }
    #pomoStart:hover { transform: scale(1.05); box-shadow: 0 0 20px rgba(0,229,255,.3); }
    #pomoReset {
      background: rgba(255,255,255,.06);
      color: var(--muted);
      border: 1px solid var(--border);
    }
    #pomoReset:hover { color: var(--text); border-color: rgba(255,255,255,.2); }
    .pomo-sessions {
      text-align: center;
      margin-top: 14px;
      font-size: .8rem;
      color: var(--muted);
    }
    .pomo-sessions span { color: var(--cyan); font-weight: 700; }

    /* --- TODO LIST --- */
    .todo-input-row {
      display: flex;
      gap: 10px;
      margin-bottom: 16px;
    }
    .todo-input-row input {
      flex: 1;
      background: rgba(255,255,255,.04);
      border: 1px solid var(--border);
      border-radius: 10px;
      padding: 11px 16px;
      color: var(--text);
      font-family: var(--font-body);
      font-size: .9rem;
      outline: none;
      transition: border-color .2s;
    }
    .todo-input-row input::placeholder { color: var(--muted); }
    .todo-input-row input:focus { border-color: rgba(0,229,255,.4); box-shadow: 0 0 12px rgba(0,229,255,.08); }
    .todo-input-row button {
      padding: 11px 18px;
      background: linear-gradient(135deg, var(--cyan), var(--violet));
      border: none;
      border-radius: 10px;
      color: #fff;
      font-size: 1.1rem;
      cursor: pointer;
      font-weight: 700;
      transition: transform .2s;
    }
    .todo-input-row button:hover { transform: scale(1.07); }

    .todo-filters {
      display: flex;
      gap: 8px;
      margin-bottom: 14px;
    }
    .filter-btn {
      padding: 5px 14px;
      border-radius: 50px;
      border: 1px solid var(--border);
      background: transparent;
      color: var(--muted);
      font-size: .78rem;
      font-weight: 600;
      cursor: pointer;
      font-family: var(--font-body);
      transition: all .2s;
    }
    .filter-btn.active {
      background: rgba(168,85,247,.12);
      border-color: rgba(168,85,247,.3);
      color: var(--violet);
    }

    .todo-list {
      display: flex;
      flex-direction: column;
      gap: 8px;
      max-height: 260px;
      overflow-y: auto;
      padding-right: 4px;
    }
    .todo-list::-webkit-scrollbar { width: 4px; }
    .todo-list::-webkit-scrollbar-track { background: transparent; }
    .todo-list::-webkit-scrollbar-thumb { background: var(--border); border-radius: 4px; }

    .todo-item {
      display: flex;
      align-items: center;
      gap: 12px;
      background: rgba(255,255,255,.025);
      border: 1px solid var(--border);
      border-radius: 10px;
      padding: 12px 16px;
      transition: all .25s ease;
      animation: slideIn .25s ease;
    }
    @keyframes slideIn {
      from { opacity: 0; transform: translateX(-12px); }
      to   { opacity: 1; transform: translateX(0); }
    }
    .todo-item.done { opacity: .5; }
    .todo-item.done .todo-text { text-decoration: line-through; }

    .todo-check {
      width: 20px; height: 20px;
      border-radius: 50%;
      border: 2px solid var(--border);
      display: flex; align-items: center; justify-content: center;
      cursor: pointer;
      flex-shrink: 0;
      transition: all .2s;
      font-size: .7rem;
      color: transparent;
    }
    .todo-check.checked {
      background: linear-gradient(135deg, var(--cyan), var(--violet));
      border-color: transparent;
      color: #fff;
    }

    .todo-text { flex: 1; font-size: .9rem; cursor: pointer; user-select: none; }
    .todo-priority {
      font-size: .65rem;
      font-weight: 700;
      padding: 2px 8px;
      border-radius: 50px;
      letter-spacing: .06em;
    }
    .pri-high   { background: rgba(244,114,182,.15); color: var(--pink); }
    .pri-medium { background: rgba(251,191,36,.12);  color: var(--gold); }
    .pri-low    { background: rgba(0,229,255,.1);    color: var(--cyan); }

    .todo-delete {
      background: none; border: none;
      color: var(--muted);
      cursor: pointer;
      font-size: .9rem;
      padding: 2px 4px;
      border-radius: 4px;
      transition: color .2s;
      line-height: 1;
    }
    .todo-delete:hover { color: var(--pink); }

    .todo-footer {
      margin-top: 12px;
      display: flex;
      justify-content: space-between;
      align-items: center;
      font-size: .8rem;
      color: var(--muted);
    }
    #clearCompleted {
      background: none; border: none;
      color: var(--muted);
      font-size: .78rem;
      cursor: pointer;
      font-family: var(--font-body);
      transition: color .2s;
    }
    #clearCompleted:hover { color: var(--pink); }

    /* --- PRODUCTIVITY SCORE --- */
    .score-wrap { display: flex; flex-direction: column; gap: 20px; }
    .score-item label {
      display: flex;
      justify-content: space-between;
      font-size: .85rem;
      color: var(--muted);
      margin-bottom: 6px;
    }
    .score-item label span { color: var(--cyan); font-weight: 700; }
    .score-slider {
      width: 100%;
      -webkit-appearance: none;
      height: 5px;
      border-radius: 10px;
      outline: none;
      cursor: pointer;
      transition: opacity .2s;
    }
    .score-slider::-webkit-slider-thumb {
      -webkit-appearance: none;
      width: 18px; height: 18px;
      border-radius: 50%;
      background: linear-gradient(135deg, var(--cyan), var(--violet));
      cursor: pointer;
      box-shadow: 0 0 10px rgba(0,229,255,.4);
    }
    .score-result {
      background: rgba(0,229,255,.05);
      border: 1px solid rgba(0,229,255,.15);
      border-radius: var(--radius);
      padding: 20px;
      text-align: center;
      margin-top: 8px;
    }
    .score-big {
      font-family: var(--font-display);
      font-size: 3.5rem;
      font-weight: 800;
      line-height: 1;
    }
    .score-grade {
      font-size: .85rem;
      color: var(--muted);
      margin-top: 8px;
    }
    .score-tip {
      font-size: .82rem;
      color: var(--muted);
      font-style: italic;
      margin-top: 10px;
      padding-top: 10px;
      border-top: 1px solid var(--border);
    }

    /* =========================================================
       ✦  PAGE: CONTACT
    ========================================================= */
    .contact-hero {
      padding: 140px 0 60px;
      text-align: center;
    }
    .contact-hero h1 { font-size: clamp(2rem, 5vw, 3.2rem); margin: 12px 0; }
    .contact-hero p  { font-size: 1.05rem; color: var(--muted); }

    .contact-layout {
      display: grid;
      grid-template-columns: 1fr 1.5fr;
      gap: 48px;
      padding-bottom: 96px;
    }
    @media(max-width:768px){ .contact-layout { grid-template-columns: 1fr; } }

    .contact-info h3 { font-size: 1.3rem; margin-bottom: 12px; }
    .contact-info p  { color: var(--muted); font-size: .93rem; margin-bottom: 28px; }

    .contact-detail {
      display: flex;
      align-items: center;
      gap: 14px;
      padding: 16px;
      background: var(--surface);
      border: 1px solid var(--border);
      border-radius: var(--radius);
      margin-bottom: 12px;
      transition: border-color .2s;
    }
    .contact-detail:hover { border-color: rgba(0,229,255,.2); }
    .contact-detail-icon {
      width: 40px; height: 40px;
      border-radius: 10px;
      background: rgba(0,229,255,.1);
      display: flex; align-items: center; justify-content: center;
      font-size: 1.1rem;
      flex-shrink: 0;
    }
    .contact-detail strong { display: block; font-size: .88rem; }
    .contact-detail span  { font-size: .8rem; color: var(--muted); }

    .contact-form { display: flex; flex-direction: column; gap: 18px; }

    .form-row { display: grid; grid-template-columns: 1fr 1fr; gap: 16px; }
    @media(max-width:480px){ .form-row { grid-template-columns: 1fr; } }

    .form-group { display: flex; flex-direction: column; gap: 7px; }
    .form-group label {
      font-size: .82rem;
      font-weight: 600;
      color: var(--muted);
      letter-spacing: .04em;
    }
    .form-control {
      background: rgba(255,255,255,.04);
      border: 1px solid var(--border);
      border-radius: 10px;
      padding: 12px 16px;
      color: var(--text);
      font-family: var(--font-body);
      font-size: .92rem;
      outline: none;
      transition: border-color .2s, box-shadow .2s;
      width: 100%;
    }
    .form-control::placeholder { color: var(--muted); }
    .form-control:focus {
      border-color: rgba(0,229,255,.4);
      box-shadow: 0 0 16px rgba(0,229,255,.08);
    }
    textarea.form-control { resize: vertical; min-height: 120px; }

    .form-select-wrap { position: relative; }
    .form-select-wrap select {
      -webkit-appearance: none;
      width: 100%;
    }
    .form-select-wrap::after {
      content: '▾';
      position: absolute;
      right: 14px; top: 50%;
      transform: translateY(-50%);
      color: var(--muted);
      pointer-events: none;
    }

    .contact-success {
      display: none;
      background: rgba(40,200,64,.08);
      border: 1px solid rgba(40,200,64,.25);
      border-radius: var(--radius);
      padding: 20px 24px;
      text-align: center;
      animation: fadeUp .4s ease;
    }
    .contact-success.show { display: block; }
    .contact-success h4 { font-size: 1.1rem; color: #28c840; margin-bottom: 6px; }
    .contact-success p  { font-size: .9rem; color: var(--muted); margin: 0; }

    /* =========================================================
       FOOTER
    ========================================================= */
    footer {
      border-top: 1px solid var(--border);
      padding: 56px 0 32px;
    }
    .footer-grid {
      display: grid;
      grid-template-columns: 1.5fr 1fr 1fr 1fr;
      gap: 40px;
      margin-bottom: 48px;
    }
    @media(max-width:768px){
      .footer-grid { grid-template-columns: 1fr 1fr; }
    }
    @media(max-width:440px){
      .footer-grid { grid-template-columns: 1fr; }
    }

    .footer-brand p { font-size: .88rem; color: var(--muted); margin: 12px 0 20px; max-width: 240px; }
    .footer-social {
      display: flex;
      gap: 10px;
    }
    .social-btn {
      width: 36px; height: 36px;
      border-radius: 8px;
      background: var(--surface);
      border: 1px solid var(--border);
      display: flex; align-items: center; justify-content: center;
      font-size: .95rem;
      cursor: pointer;
      transition: all .2s;
      text-decoration: none;
    }
    .social-btn:hover { border-color: var(--cyan); background: rgba(0,229,255,.08); transform: translateY(-2px); }

    .footer-col h4 {
      font-size: .85rem;
      font-weight: 700;
      letter-spacing: .08em;
      text-transform: uppercase;
      color: var(--muted);
      margin-bottom: 16px;
    }
    .footer-col ul { list-style: none; display: flex; flex-direction: column; gap: 10px; }
    .footer-col a {
      text-decoration: none;
      color: var(--muted);
      font-size: .88rem;
      transition: color .2s;
    }
    .footer-col a:hover { color: var(--cyan); }

    .footer-bottom {
      padding-top: 28px;
      border-top: 1px solid var(--border);
      display: flex;
      justify-content: space-between;
      align-items: center;
      font-size: .8rem;
      color: var(--muted);
      flex-wrap: wrap;
      gap: 12px;
    }

    /* =========================================================
       VIVA NOTES SECTION
    ========================================================= */
    .viva-section {
      background: rgba(168,85,247,.04);
      border: 1px solid rgba(168,85,247,.15);
      border-radius: 20px;
      padding: 40px;
      margin: 0 0 80px;
    }
    .viva-section h2 { font-size: 1.6rem; margin-bottom: 4px; }
    .viva-section > p { color: var(--muted); font-size: .9rem; margin-bottom: 32px; }
    .viva-grid {
      display: grid;
      grid-template-columns: repeat(2,1fr);
      gap: 24px;
    }
    @media(max-width:640px){ .viva-grid { grid-template-columns: 1fr; } }
    .viva-card {
      background: rgba(255,255,255,.025);
      border: 1px solid var(--border);
      border-radius: var(--radius);
      padding: 22px;
    }
    .viva-card h4 {
      font-size: .95rem;
      font-weight: 700;
      color: var(--violet);
      margin-bottom: 10px;
      display: flex;
      align-items: center;
      gap: 8px;
    }
    .viva-card p, .viva-card li {
      font-size: .85rem;
      color: var(--muted);
      line-height: 1.7;
    }
    .viva-card ul { padding-left: 16px; }
    .viva-card li { margin-bottom: 4px; }

    /* =========================================================
       SCROLL ANIMATIONS
    ========================================================= */
    .reveal {
      opacity: 0;
      transform: translateY(30px);
      transition: opacity .65s ease, transform .65s ease;
    }
    .reveal.visible {
      opacity: 1;
      transform: translateY(0);
    }
    .reveal-delay-1 { transition-delay: .1s; }
    .reveal-delay-2 { transition-delay: .2s; }
    .reveal-delay-3 { transition-delay: .3s; }

    /* =========================================================
       MISC UTILITIES
    ========================================================= */
    .text-center { text-align: center; }
    .mt-8  { margin-top: 8px; }
    .mt-16 { margin-top: 16px; }
    .mt-32 { margin-top: 32px; }
    .mb-24 { margin-bottom: 24px; }
    .mb-48 { margin-bottom: 48px; }

    /* Divider */
    .divider {
      width: 60px; height: 3px;
      background: linear-gradient(90deg, var(--cyan), var(--violet));
      border-radius: 2px;
      margin: 12px auto 20px;
    }

    /* Badge */
    .new-badge {
      display: inline-block;
      font-size: .6rem;
      font-weight: 800;
      letter-spacing: .1em;
      background: var(--cyan);
      color: var(--bg);
      padding: 2px 7px;
      border-radius: 4px;
      text-transform: uppercase;
      vertical-align: middle;
      margin-left: 6px;
    }
  </style>
</head>

<body>

<!-- ====================================================
     NAVIGATION
==================================================== -->
<nav id="nav">
  <div class="nav-inner">
    <a class="nav-logo" href="#" onclick="showPage('home')">Focus<span>Flow</span></a>
    <ul class="nav-links">
      <li><a href="#" onclick="showPage('home')"    id="nav-home"    class="active">Home</a></li>
      <li><a href="#" onclick="showPage('features')" id="nav-features">Features</a></li>
      <li><a href="#" onclick="showPage('tools')"    id="nav-tools">Tools <span class="new-badge">Live</span></a></li>
      <li><a href="#" onclick="showPage('contact')"  id="nav-contact">Contact</a></li>
    </ul>
    <a class="btn btn-primary btn-sm nav-cta" href="#" onclick="showPage('tools')">Try Free →</a>
    <div class="hamburger" id="hamburger" onclick="toggleMenu()">
      <span></span><span></span><span></span>
    </div>
  </div>
</nav>

<!-- Mobile menu -->
<div class="mobile-menu" id="mobileMenu">
  <a href="#" onclick="showPage('home');closeMenu()">🏠 Home</a>
  <a href="#" onclick="showPage('features');closeMenu()">✦ Features</a>
  <a href="#" onclick="showPage('tools');closeMenu()">⚙️ Tools</a>
  <a href="#" onclick="showPage('contact');closeMenu()">📬 Contact</a>
</div>

<!-- ====================================================
     PAGE: HOME
==================================================== -->
<div id="page-home" class="page active">

  <!-- HERO -->
  <section class="hero">
    <div class="blob blob-1"></div>
    <div class="blob blob-2"></div>
    <div class="blob blob-3"></div>

    <div class="container">
      <div class="hero-content">
        <div class="hero-badge">
          <div class="dot"></div>
          AI-Powered · Built for Students
        </div>
        <h1>
          Study Smarter,<br/>
          <span class="grad-text">Not Harder.</span>
        </h1>
        <p>FocusFlow uses AI to help you manage tasks, beat procrastination, and build study habits that actually stick — all in one beautiful platform.</p>
        <div class="hero-actions">
          <a class="btn btn-primary" href="#" onclick="showPage('tools')">Get Started Free →</a>
          <a class="btn btn-outline" href="#" onclick="showPage('features')">Explore Features</a>
        </div>
        <div class="hero-stats">
          <div class="hero-stat"><h3>50K+</h3><p>Active students</p></div>
          <div class="hero-stat"><h3>92%</h3><p>Grade improvement</p></div>
          <div class="hero-stat"><h3>4.9★</h3><p>User rating</p></div>
        </div>
      </div>
    </div>

    <!-- Floating window mockup -->
    <div class="hero-visual">
      <div class="mock-window">
        <div class="mock-titlebar">
          <div class="mock-dot r"></div>
          <div class="mock-dot y"></div>
          <div class="mock-dot g"></div>
          <span class="mock-title-bar-text">FocusFlow — Study Session</span>
        </div>
        <div class="mock-timer-ring" id="mockRing">
          <span class="mock-timer-text" id="mockTime">18:42</span>
        </div>
        <div class="mock-task-list">
          <div class="mock-task"><div class="mock-task-check done"></div>Review Chapter 4 Notes</div>
          <div class="mock-task"><div class="mock-task-check"></div>Complete Data Structures Lab</div>
          <div class="mock-task"><div class="mock-task-check"></div>Watch OS lecture recording</div>
        </div>
      </div>
    </div>
  </section>

  <!-- FEATURES CARDS -->
  <section class="section" style="padding-top:48px;">
    <div class="container">
      <div class="section-heading reveal">
        <span class="section-label">Why FocusFlow</span>
        <h2>Everything a student needs</h2>
        <p>Smart tools designed around how students actually study — not how teachers think they do.</p>
      </div>
      <div class="grid-4">
        <div class="card reveal reveal-delay-1">
          <div class="feat-icon c">🗂️</div>
          <h3>Smart Task Manager</h3>
          <p>AI prioritizes your tasks based on deadlines, difficulty, and your past completion patterns.</p>
        </div>
        <div class="card reveal reveal-delay-2">
          <div class="feat-icon v">⏱️</div>
          <h3>Pomodoro Timer</h3>
          <p>Science-backed focus intervals that adapt to your attention span over time.</p>
        </div>
        <div class="card reveal reveal-delay-3">
          <div class="feat-icon p">📊</div>
          <h3>Study Analytics</h3>
          <p>Visualise your daily focus hours, task completion rates, and productivity trends.</p>
        </div>
        <div class="card reveal reveal-delay-3">
          <div class="feat-icon g">🤖</div>
          <h3>AI Suggestions</h3>
          <p>Get personalised study tips and schedule recommendations powered by GPT-style analysis.</p>
        </div>
      </div>
    </div>
  </section>

  <!-- HOW IT WORKS -->
  <section class="section" style="background: linear-gradient(180deg, transparent, rgba(168,85,247,.03), transparent);">
    <div class="container">
      <div style="display:grid; grid-template-columns:1fr 1fr; gap:80px; align-items:center;">
        <div>
          <div class="section-heading" style="text-align:left; margin-bottom:40px;">
            <span class="section-label">How It Works</span>
            <h2 style="margin-top:10px;">Up and running<br/>in 3 steps</h2>
          </div>
          <div class="steps-wrap">
            <div class="step reveal">
              <div class="step-num">01</div>
              <div class="step-body">
                <h3>Set Your Goals</h3>
                <p>Tell FocusFlow what you're studying and when your exams are. The AI builds your personalized roadmap.</p>
              </div>
            </div>
            <div class="step reveal reveal-delay-1">
              <div class="step-num">02</div>
              <div class="step-body">
                <h3>Follow the Flow</h3>
                <p>Work through guided Pomodoro sessions with smart breaks. Your dashboard tracks every minute.</p>
              </div>
            </div>
            <div class="step reveal reveal-delay-2">
              <div class="step-num">03</div>
              <div class="step-body">
                <h3>Improve Over Time</h3>
                <p>Weekly AI insights show what's working. Adjust your habits and watch your grades climb.</p>
              </div>
            </div>
          </div>
        </div>
        <div class="reveal" style="position:relative;">
          <div style="background: var(--surface); border: 1px solid var(--border); border-radius:20px; padding:28px; box-shadow:0 32px 80px rgba(0,0,0,.4);">
            <div style="font-size:.75rem; color:var(--muted); margin-bottom:16px; font-weight:600; letter-spacing:.1em; text-transform:uppercase;">📈 Weekly Progress</div>
            <div class="bar-chart" id="howChart"></div>
            <div style="display:flex; justify-content:space-between; margin-top:20px; padding-top:16px; border-top:1px solid var(--border);">
              <div><div style="font-size:1.4rem; font-weight:800; font-family:var(--font-display); color:var(--cyan);">14h 20m</div><div style="font-size:.75rem; color:var(--muted);">This week</div></div>
              <div><div style="font-size:1.4rem; font-weight:800; font-family:var(--font-display); color:var(--violet);">+28%</div><div style="font-size:.75rem; color:var(--muted);">vs last week</div></div>
              <div><div style="font-size:1.4rem; font-weight:800; font-family:var(--font-display); color:var(--pink);">87%</div><div style="font-size:.75rem; color:var(--muted);">Completion</div></div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>

  <!-- TESTIMONIALS -->
  <section class="section">
    <div class="container">
      <div class="section-heading reveal">
        <span class="section-label">Testimonials</span>
        <h2>Students love FocusFlow</h2>
        <p>Real reviews from students across India, the US, and beyond.</p>
      </div>
      <div class="testi-grid">
        <div class="testi-card reveal reveal-delay-1">
          <div class="stars">★★★★★</div>
          <p>"I went from barely passing to topping my class in one semester. The AI suggestions are scarily accurate."</p>
          <div class="testi-author">
            <div class="avatar av1">AK</div>
            <div class="testi-author-info">
              <strong>Arjun Kumar</strong>
              <span>3rd Year, IIT Delhi · CS</span>
            </div>
          </div>
        </div>
        <div class="testi-card reveal reveal-delay-2">
          <div class="stars">★★★★★</div>
          <p>"The Pomodoro timer changed everything. I can now focus for hours without feeling burnt out."</p>
          <div class="testi-author">
            <div class="avatar av2">PS</div>
            <div class="testi-author-info">
              <strong>Priya Sharma</strong>
              <span>2nd Year, BITS Pilani · ECE</span>
            </div>
          </div>
        </div>
        <div class="testi-card reveal reveal-delay-3">
          <div class="stars">★★★★☆</div>
          <p>"The analytics dashboard showed me that I waste 2 hours a day. Fixing that alone improved my productivity massively."</p>
          <div class="testi-author">
            <div class="avatar av3">RV</div>
            <div class="testi-author-info">
              <strong>Rahul Verma</strong>
              <span>4th Year, NIT Trichy · MECH</span>
            </div>
          </div>
        </div>
        <div class="testi-card reveal">
          <div class="stars">★★★★★</div>
          <p>"Finally an app that understands exam season. It automatically adjusted my schedule before my board exams."</p>
          <div class="testi-author">
            <div class="avatar av4">SN</div>
            <div class="testi-author-info">
              <strong>Sneha Nair</strong>
              <span>Final Year, MSRIT · ISE</span>
            </div>
          </div>
        </div>
        <div class="testi-card reveal reveal-delay-1">
          <div class="stars">★★★★★</div>
          <p>"I recommended FocusFlow to my entire study group. We've all seen significant improvement in our GPA."</p>
          <div class="testi-author">
            <div class="avatar av5">MT</div>
            <div class="testi-author-info">
              <strong>Mohammed Talha</strong>
              <span>MS Student, IIIT Bangalore</span>
            </div>
          </div>
        </div>
        <div class="testi-card reveal reveal-delay-2">
          <div class="stars">★★★★★</div>
          <p>"The task manager with priority scoring is a game changer. Never miss a deadline anymore."</p>
          <div class="testi-author">
            <div class="avatar av6">DG</div>
            <div class="testi-author-info">
              <strong>Divya Gupta</strong>
              <span>1st Year MBA, IIM Bangalore</span>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>

  <!-- CTA BANNER -->
  <section class="section-sm">
    <div class="container">
      <div style="background: linear-gradient(135deg, rgba(0,229,255,.07), rgba(168,85,247,.07)); border:1px solid rgba(0,229,255,.15); border-radius:24px; padding:56px 48px; text-align:center; position:relative; overflow:hidden;" class="reveal">
        <div style="position:absolute; inset:0; background: radial-gradient(ellipse at 50% 0%, rgba(168,85,247,.12), transparent 70%); pointer-events:none;"></div>
        <span class="section-label" style="position:relative;">Start Today</span>
        <h2 style="font-size:clamp(1.8rem, 4vw, 2.8rem); margin:12px 0; position:relative;">Ready to unlock your<br/><span class="grad-text">full potential?</span></h2>
        <p style="color:var(--muted); margin-bottom:28px; position:relative;">Join 50,000+ students already studying smarter with FocusFlow.</p>
        <a class="btn btn-primary" href="#" onclick="showPage('tools')" style="position:relative;">Launch the Tools →</a>
      </div>
    </div>
  </section>

</div><!-- /page-home -->

<!-- ====================================================
     PAGE: FEATURES
==================================================== -->
<div id="page-features" class="page">

  <!-- Hero -->
  <div class="feat-hero">
    <div class="blob blob-1" style="opacity:.1;"></div>
    <div class="container">
      <span class="section-label">Features</span>
      <h1>Powerful tools, <span class="grad-text">built for focus</span></h1>
      <p>Each feature is designed around behavioural science and real student feedback.</p>
    </div>
  </div>

  <div class="container">

    <!-- Task Manager -->
    <div class="feat-detail reveal">
      <div class="feat-detail-text">
        <span class="feat-tag tag-cyan">Task Manager</span>
        <h2>AI-prioritised task management</h2>
        <p>Never wonder what to study next. FocusFlow's AI analyses your upcoming deadlines, subject weights, and past performance to build a live priority queue that updates automatically.</p>
        <ul class="feat-bullets">
          <li>Smart priority scoring based on deadlines & difficulty</li>
          <li>Subtask breakdown for complex assignments</li>
          <li>Calendar sync and deadline reminders</li>
          <li>Recurring tasks for daily study habits</li>
          <li>Local storage — your tasks are always saved</li>
        </ul>
      </div>
      <div class="feat-detail-visual">
        <div style="font-size:.75rem; color:var(--muted); margin-bottom:14px; font-weight:600; text-transform:uppercase; letter-spacing:.1em;">📋 Today's Priority Queue</div>
        <div style="display:flex; flex-direction:column; gap:8px;">
          <div class="mock-task" style="border-color:rgba(244,114,182,.3); background:rgba(244,114,182,.05);">
            <div class="mock-task-check done" style="border-color:var(--pink); background:var(--pink);"></div>
            <span style="flex:1; font-size:.82rem;">DBMS Assignment (Due Today)</span>
            <span style="font-size:.65rem; background:rgba(244,114,182,.15); color:var(--pink); padding:2px 8px; border-radius:50px; font-weight:700;">HIGH</span>
          </div>
          <div class="mock-task">
            <div class="mock-task-check"></div>
            <span style="flex:1; font-size:.82rem;">OS Module 4 Revision</span>
            <span style="font-size:.65rem; background:rgba(251,191,36,.12); color:var(--gold); padding:2px 8px; border-radius:50px; font-weight:700;">MED</span>
          </div>
          <div class="mock-task">
            <div class="mock-task-check"></div>
            <span style="flex:1; font-size:.82rem;">CN Lab Report (3 days left)</span>
            <span style="font-size:.65rem; background:rgba(0,229,255,.1); color:var(--cyan); padding:2px 8px; border-radius:50px; font-weight:700;">LOW</span>
          </div>
          <div class="mock-task">
            <div class="mock-task-check"></div>
            <span style="flex:1; font-size:.82rem;">Maths Problem Set Ch.7</span>
            <span style="font-size:.65rem; background:rgba(0,229,255,.1); color:var(--cyan); padding:2px 8px; border-radius:50px; font-weight:700;">LOW</span>
          </div>
        </div>
      </div>
    </div>

    <!-- Pomodoro Timer -->
    <div class="feat-detail reverse reveal">
      <div class="feat-detail-text">
        <span class="feat-tag tag-violet">Focus Timer</span>
        <h2>Pomodoro system that adapts to you</h2>
        <p>The classic Pomodoro technique, made smarter. FocusFlow tracks your focus sessions and automatically adjusts interval lengths based on your concentration data.</p>
        <ul class="feat-bullets">
          <li>25-min focus / 5-min break by default</li>
          <li>Long break every 4 sessions</li>
          <li>Session history and streak tracking</li>
          <li>Background ambient sound selector</li>
          <li>Desktop notifications when time is up</li>
        </ul>
      </div>
      <div class="feat-detail-visual" style="align-items:center;">
        <div style="text-align:center;">
          <div style="font-size:.75rem; color:var(--muted); margin-bottom:16px; font-weight:600; text-transform:uppercase; letter-spacing:.1em;">⏱️ Active Focus Session</div>
          <div style="width:140px; height:140px; border-radius:50%; background: conic-gradient(var(--violet) 0% 72%, rgba(255,255,255,.06) 72% 100%); display:flex; align-items:center; justify-content:center; margin: 0 auto 16px; box-shadow:0 0 40px rgba(168,85,247,.25); position:relative;">
            <div style="position:absolute; inset:12px; border-radius:50%; background:var(--bg2); display:flex; flex-direction:column; align-items:center; justify-content:center;">
              <div style="font-family:var(--font-display); font-weight:800; font-size:1.6rem; color:var(--violet);">18:02</div>
              <div style="font-size:.65rem; color:var(--muted); text-transform:uppercase; letter-spacing:.1em;">Focus</div>
            </div>
          </div>
          <div style="display:flex; gap:8px; justify-content:center;">
            <div style="width:10px; height:10px; border-radius:50%; background:var(--violet);"></div>
            <div style="width:10px; height:10px; border-radius:50%; background:var(--violet);"></div>
            <div style="width:10px; height:10px; border-radius:50%; background:var(--violet);"></div>
            <div style="width:10px; height:10px; border-radius:50%; background:rgba(255,255,255,.1);"></div>
          </div>
          <div style="font-size:.78rem; color:var(--muted); margin-top:8px;">Session 3 of 4 · 🔥 5 day streak</div>
        </div>
      </div>
    </div>

    <!-- Analytics -->
    <div class="feat-detail reveal">
      <div class="feat-detail-text">
        <span class="feat-tag tag-pink">Analytics</span>
        <h2>See exactly how you study</h2>
        <p>FocusFlow's dashboard turns your study habits into actionable data. Discover your peak focus hours, your most productive days, and which subjects drain you most.</p>
        <ul class="feat-bullets">
          <li>Daily and weekly focus hour charts</li>
          <li>Subject-wise time breakdown</li>
          <li>Task completion velocity trends</li>
          <li>Distraction pattern detection</li>
          <li>Exportable weekly report PDF</li>
        </ul>
      </div>
      <div class="feat-detail-visual">
        <div style="font-size:.75rem; color:var(--muted); margin-bottom:16px; font-weight:600; text-transform:uppercase; letter-spacing:.1em;">📊 Focus Hours — This Week</div>
        <div id="featChart" style="display:flex; align-items:flex-end; gap:8px; height:100px;"></div>
        <div style="display:flex; gap:16px; margin-top:16px; flex-wrap:wrap;">
          <div style="display:flex; align-items:center; gap:6px; font-size:.75rem; color:var(--muted);">
            <div style="width:10px; height:10px; border-radius:2px; background:var(--cyan);"></div>Focus
          </div>
          <div style="display:flex; align-items:center; gap:6px; font-size:.75rem; color:var(--muted);">
            <div style="width:10px; height:10px; border-radius:2px; background:var(--violet);"></div>Review
          </div>
        </div>
      </div>
    </div>

    <!-- AI Suggestions -->
    <div class="feat-detail reverse reveal" style="border-bottom:none;">
      <div class="feat-detail-text">
        <span class="feat-tag tag-gold">AI Brain</span>
        <h2>Your personal AI study coach</h2>
        <p>FocusFlow's AI doesn't just track — it thinks. Every week it analyses your patterns and generates specific, actionable suggestions tailored to your learning style.</p>
        <ul class="feat-bullets">
          <li>Subject-specific study tips</li>
          <li>Schedule gap filling recommendations</li>
          <li>Distraction pattern alerts</li>
          <li>Exam readiness score</li>
          <li>Peer comparison (anonymised)</li>
        </ul>
      </div>
      <div class="feat-detail-visual">
        <div style="font-size:.75rem; color:var(--muted); margin-bottom:14px; font-weight:600; text-transform:uppercase; letter-spacing:.1em;">🤖 AI Insights · Today</div>
        <div class="ai-suggestions">
          <div class="ai-card">
            <div class="ai-icon">⚡</div>
            <div class="ai-text">
              <strong>Peak hours detected</strong>
              <span>You focus 40% better between 9–11 AM. Schedule hard topics there.</span>
            </div>
          </div>
          <div class="ai-card" style="background:rgba(244,114,182,.07); border-color:rgba(244,114,182,.18);">
            <div class="ai-icon">📉</div>
            <div class="ai-text">
              <strong>DBMS needs attention</strong>
              <span>You've spent only 3.2h this week. Exam is in 9 days — add 2 sessions.</span>
            </div>
          </div>
          <div class="ai-card" style="background:rgba(251,191,36,.06); border-color:rgba(251,191,36,.18);">
            <div class="ai-icon">🎯</div>
            <div class="ai-text">
              <strong>Great streaks!</strong>
              <span>5 consecutive days of completing your task list. Keep it up!</span>
            </div>
          </div>
        </div>
      </div>
    </div>

  </div><!-- /container -->

  <!-- VIVA NOTES -->
  <div class="container">
    <div class="viva-section reveal">
      <span class="section-label" style="margin-bottom:8px; display:block;">📚 Viva Reference</span>
      <h2>Project Notes for Viva</h2>
      <p>Refer to these points during your project presentation or viva examination.</p>
      <div class="viva-grid">
        <div class="viva-card">
          <h4>🏗️ What is FocusFlow?</h4>
          <p>FocusFlow is an AI-powered Student Productivity Platform built as a multi-page web application. It helps students manage tasks, track study time, reduce distractions, and receive AI-generated study recommendations — all without any backend server. The entire state is managed client-side using JavaScript and the browser's localStorage API.</p>
        </div>
        <div class="viva-card">
          <h4>🛠️ Technologies Used</h4>
          <ul>
            <li><strong>HTML5</strong> — Semantic page structure, forms, SVG graphics</li>
            <li><strong>CSS3</strong> — CSS Variables, Grid, Flexbox, animations, gradients, glassmorphism</li>
            <li><strong>Vanilla JavaScript</strong> — DOM manipulation, localStorage, setInterval, event listeners</li>
            <li><strong>Google Fonts</strong> — Syne (display), DM Sans (body)</li>
            <li><strong>SVG</strong> — Animated progress ring for Pomodoro timer</li>
          </ul>
        </div>
        <div class="viva-card">
          <h4>⚙️ Key Technical Features</h4>
          <ul>
            <li>Single-page app pattern (SPA) with JS page routing</li>
            <li>localStorage for persistent to-do list across sessions</li>
            <li>setInterval for real-time countdown timer</li>
            <li>SVG stroke-dashoffset animation for timer ring</li>
            <li>IntersectionObserver for scroll-triggered reveal animations</li>
            <li>Responsive design using CSS Grid + media queries</li>
            <li>Task filter system (All / Active / Done)</li>
          </ul>
        </div>
        <div class="viva-card">
          <h4>🚀 Future Improvements</h4>
          <ul>
            <li>Backend integration (Node.js + MongoDB) for cloud sync</li>
            <li>Real AI API (OpenAI / Gemini) for genuine suggestions</li>
            <li>User authentication (Google OAuth)</li>
            <li>Mobile app using React Native</li>
            <li>Chrome extension for distraction blocking</li>
            <li>Collaborative study rooms (WebRTC / Socket.io)</li>
            <li>Calendar integration (Google Calendar API)</li>
          </ul>
        </div>
      </div>
    </div>
  </div>

</div><!-- /page-features -->

<!-- ====================================================
     PAGE: TOOLS
==================================================== -->
<div id="page-tools" class="page">

  <div class="tools-hero">
    <div class="container">
      <span class="section-label">Interactive Tools</span>
      <h1>Your productivity <span class="grad-text">toolkit</span></h1>
      <p>All tools work live in the browser. Your tasks are saved automatically.</p>
    </div>
  </div>

  <div class="container">
    <div class="tools-grid">

      <!-- ========== POMODORO TIMER ========== -->
      <div class="tool-card">
        <div class="tool-card-header">
          <div class="tool-icon" style="background:rgba(0,229,255,.1);">⏱️</div>
          <div>
            <h3>Pomodoro Timer</h3>
            <p>Focus · Short Break · Long Break</p>
          </div>
        </div>

        <!-- Mode selector -->
        <div class="pomo-mode">
          <button class="pomo-mode-btn active" onclick="setPomoMode(this,25,'Focus')" data-mins="25">Focus</button>
          <button class="pomo-mode-btn" onclick="setPomoMode(this,5,'Short Break')" data-mins="5">Short Break</button>
          <button class="pomo-mode-btn" onclick="setPomoMode(this,15,'Long Break')" data-mins="15">Long Break</button>
        </div>

        <!-- SVG Ring -->
        <div class="pomo-ring-wrap">
          <div class="pomo-ring">
            <svg viewBox="0 0 180 180">
              <defs>
                <linearGradient id="timerGrad" x1="0%" y1="0%" x2="100%" y2="0%">
                  <stop offset="0%"   stop-color="#00e5ff"/>
                  <stop offset="100%" stop-color="#a855f7"/>
                </linearGradient>
              </defs>
              <circle class="pomo-ring-bg"       cx="90" cy="90" r="80"/>
              <circle class="pomo-ring-progress" cx="90" cy="90" r="80" id="pomoRingProgress"/>
            </svg>
            <div class="pomo-time">
              <span class="time-display" id="pomoDisplay">25:00</span>
              <span class="time-label"  id="pomoLabel">Focus</span>
            </div>
          </div>
        </div>

        <!-- Controls -->
        <div class="pomo-controls">
          <button id="pomoStart" onclick="togglePomodoro()">▶ Start</button>
          <button id="pomoReset" onclick="resetPomodoro()">↺ Reset</button>
        </div>
        <div class="pomo-sessions">
          Completed sessions: <span id="pomoSessions">0</span> &nbsp;·&nbsp; 🔥 Streak: <span id="pomoStreak">0</span>
        </div>
      </div>

      <!-- ========== TO-DO LIST ========== -->
      <div class="tool-card">
        <div class="tool-card-header">
          <div class="tool-icon" style="background:rgba(168,85,247,.1);">✅</div>
          <div>
            <h3>Smart To-Do List</h3>
            <p>Saved automatically to your browser</p>
          </div>
        </div>

        <div class="todo-input-row">
          <input type="text" id="todoInput" placeholder="Add a new task..." onkeydown="if(event.key==='Enter')addTodo()" maxlength="80"/>
          <select id="todoPriority" style="background:rgba(255,255,255,.04); border:1px solid var(--border); border-radius:10px; padding:0 12px; color:var(--text); font-family:var(--font-body); font-size:.82rem; outline:none; cursor:pointer; min-width:80px;">
            <option value="low"    style="background:#0d0d1f;">🔵 Low</option>
            <option value="medium" style="background:#0d0d1f;">🟡 Med</option>
            <option value="high"   style="background:#0d0d1f;">🔴 High</option>
          </select>
          <button onclick="addTodo()">+</button>
        </div>

        <div class="todo-filters">
          <button class="filter-btn active" onclick="filterTodos('all',this)">All</button>
          <button class="filter-btn" onclick="filterTodos('active',this)">Active</button>
          <button class="filter-btn" onclick="filterTodos('done',this)">Done</button>
        </div>

        <div class="todo-list" id="todoList"></div>

        <div class="todo-footer">
          <span id="todoCount">0 tasks</span>
          <button id="clearCompleted" onclick="clearDone()">Clear completed</button>
        </div>
      </div>

      <!-- ========== PRODUCTIVITY SCORE ========== -->
      <div class="tool-card" style="grid-column: 1 / -1;">
        <div class="tool-card-header">
          <div class="tool-icon" style="background:rgba(244,114,182,.1);">📊</div>
          <div>
            <h3>Productivity Score Calculator</h3>
            <p>Rate your habits — get your real productivity score</p>
          </div>
        </div>

        <div style="display:grid; grid-template-columns:1fr 1fr; gap:40px; align-items:start;">
          <div class="score-wrap" id="scoreSliders">

            <div class="score-item">
              <label>Study hours today <span id="lbl-study">5</span>h</label>
              <input type="range" class="score-slider" min="0" max="12" value="5" id="sl-study"
                     style="background: linear-gradient(to right, var(--cyan) 0%, var(--cyan) 41.7%, rgba(255,255,255,.08) 41.7%);"
                     oninput="updateScore()" />
            </div>

            <div class="score-item">
              <label>Tasks completed <span id="lbl-tasks">6</span></label>
              <input type="range" class="score-slider" min="0" max="15" value="6" id="sl-tasks"
                     style="background: linear-gradient(to right, var(--violet) 0%, var(--violet) 40%, rgba(255,255,255,.08) 40%);"
                     oninput="updateScore()" />
            </div>

            <div class="score-item">
              <label>Focus consistency <span id="lbl-focus">7</span>/10</label>
              <input type="range" class="score-slider" min="0" max="10" value="7" id="sl-focus"
                     style="background: linear-gradient(to right, var(--pink) 0%, var(--pink) 70%, rgba(255,255,255,.08) 70%);"
                     oninput="updateScore()" />
            </div>

            <div class="score-item">
              <label>Breaks taken <span id="lbl-breaks">3</span></label>
              <input type="range" class="score-slider" min="0" max="8" value="3" id="sl-breaks"
                     style="background: linear-gradient(to right, var(--gold) 0%, var(--gold) 37.5%, rgba(255,255,255,.08) 37.5%);"
                     oninput="updateScore()" />
            </div>

            <div class="score-item">
              <label>Distractions avoided <span id="lbl-dist">6</span>/10</label>
              <input type="range" class="score-slider" min="0" max="10" value="6" id="sl-dist"
                     style="background: linear-gradient(to right, var(--cyan) 0%, var(--cyan) 60%, rgba(255,255,255,.08) 60%);"
                     oninput="updateScore()" />
            </div>
          </div>

          <div>
            <div class="score-result">
              <div class="score-big grad-text" id="scoreDisplay">74</div>
              <div style="font-size:.75rem; color:var(--muted); margin-top:6px; letter-spacing:.08em; text-transform:uppercase;">Productivity Score</div>
              <div class="score-grade" id="scoreGrade">⚡ Good Focus Day</div>
              <div class="score-tip" id="scoreTip">You're performing well! Try to get 1–2 more tasks done and reduce screen time after 10 PM.</div>
            </div>

            <div style="margin-top:20px; display:flex; flex-direction:column; gap:8px;">
              <div style="font-size:.78rem; color:var(--muted); font-weight:600; text-transform:uppercase; letter-spacing:.08em;">Score Breakdown</div>
              <div id="scoreBreakdown"></div>
            </div>
          </div>
        </div>
      </div>

    </div><!-- /tools-grid -->
  </div><!-- /container -->
</div><!-- /page-tools -->

<!-- ====================================================
     PAGE: CONTACT
==================================================== -->
<div id="page-contact" class="page">

  <div class="contact-hero">
    <div class="blob blob-1" style="opacity:.08;"></div>
    <div class="container">
      <span class="section-label">Contact</span>
      <h1>Get in <span class="grad-text">touch</span></h1>
      <p>Have a question, suggestion, or want to collaborate? We'd love to hear from you.</p>
    </div>
  </div>

  <div class="container">
    <div class="contact-layout">
      <div class="contact-info reveal">
        <h3>Let's talk</h3>
        <p>Whether you're a student with feedback, a developer interested in contributing, or a college wanting to integrate FocusFlow — reach out.</p>

        <div class="contact-detail">
          <div class="contact-detail-icon">📧</div>
          <div>
            <strong>Email</strong>
            <span>hello@focusflow.app</span>
          </div>
        </div>
        <div class="contact-detail">
          <div class="contact-detail-icon">💬</div>
          <div>
            <strong>Discord Community</strong>
            <span>discord.gg/focusflow</span>
          </div>
        </div>
        <div class="contact-detail">
          <div class="contact-detail-icon">🐙</div>
          <div>
            <strong>GitHub</strong>
            <span>github.com/focusflow-app</span>
          </div>
        </div>
        <div class="contact-detail">
          <div class="contact-detail-icon">📍</div>
          <div>
            <strong>Location</strong>
            <span>Bengaluru, Karnataka, India</span>
          </div>
        </div>

        <div style="margin-top:24px; padding:20px; background:rgba(0,229,255,.05); border:1px solid rgba(0,229,255,.12); border-radius:var(--radius);">
          <div style="font-size:.8rem; color:var(--cyan); font-weight:700; margin-bottom:6px;">⚡ Response Time</div>
          <div style="font-size:.85rem; color:var(--muted);">We typically reply within 24 hours on weekdays.</div>
        </div>
      </div>

      <div class="reveal reveal-delay-1">
        <!-- Success message -->
        <div class="contact-success" id="contactSuccess">
          <h4>✅ Message sent successfully!</h4>
          <p>Thanks for reaching out. We'll get back to you within 24 hours.</p>
        </div>

        <!-- Form -->
        <div id="contactFormWrap">
          <div class="contact-form">
            <div class="form-row">
              <div class="form-group">
                <label>Full Name</label>
                <input type="text" class="form-control" id="cf-name" placeholder="Rahul Sharma" />
              </div>
              <div class="form-group">
                <label>Email Address</label>
                <input type="email" class="form-control" id="cf-email" placeholder="you@college.edu" />
              </div>
            </div>
            <div class="form-group">
              <label>Subject</label>
              <div class="form-select-wrap">
                <select class="form-control" id="cf-subject">
                  <option>General Inquiry</option>
                  <option>Feature Request</option>
                  <option>Bug Report</option>
                  <option>College Partnership</option>
                  <option>Developer Collaboration</option>
                </select>
              </div>
            </div>
            <div class="form-group">
              <label>Message</label>
              <textarea class="form-control" id="cf-message" placeholder="Tell us about your experience or question…"></textarea>
            </div>
            <div style="display:flex; gap:12px; align-items:center; flex-wrap:wrap;">
              <button class="btn btn-primary" onclick="submitContact()" style="min-width:160px;">Send Message →</button>
              <span id="formError" style="font-size:.82rem; color:var(--pink); display:none;">Please fill in all fields.</span>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>

</div><!-- /page-contact -->

<!-- ====================================================
     FOOTER (shared)
==================================================== -->
<footer>
  <div class="container">
    <div class="footer-grid">
      <div class="footer-brand">
        <div style="font-family:var(--font-display); font-weight:800; font-size:1.3rem; margin-bottom:8px;">Focus<span style="color:var(--cyan);">Flow</span></div>
        <p>AI-powered productivity platform built for students who want to study smarter, not harder.</p>
        <div class="footer-social">
          <a class="social-btn" title="Twitter">𝕏</a>
          <a class="social-btn" title="GitHub">⬡</a>
          <a class="social-btn" title="Instagram">◈</a>
          <a class="social-btn" title="Discord">☁</a>
        </div>
      </div>
      <div class="footer-col">
        <h4>Product</h4>
        <ul>
          <li><a href="#" onclick="showPage('features')">Features</a></li>
          <li><a href="#" onclick="showPage('tools')">Tools</a></li>
          <li><a href="#">Roadmap</a></li>
          <li><a href="#">Changelog</a></li>
        </ul>
      </div>
      <div class="footer-col">
        <h4>Resources</h4>
        <ul>
          <li><a href="#">Documentation</a></li>
          <li><a href="#">Blog</a></li>
          <li><a href="#">Study Guides</a></li>
          <li><a href="#">API</a></li>
        </ul>
      </div>
      <div class="footer-col">
        <h4>Company</h4>
        <ul>
          <li><a href="#">About</a></li>
          <li><a href="#" onclick="showPage('contact')">Contact</a></li>
          <li><a href="#">Privacy</a></li>
          <li><a href="#">Terms</a></li>
        </ul>
      </div>
    </div>
    <div class="footer-bottom">
      <span>© 2025 FocusFlow. Built with ♥ for students.</span>
      <span>IT Project · Web Technologies · B.E. CSE</span>
    </div>
  </div>
</footer>

<!-- ====================================================
     JAVASCRIPT
==================================================== -->
<script>
/* ============================================================
   PAGE ROUTING
   Show/hide pages and update nav active state
============================================================ */
function showPage(name) {
  // Hide all pages
  document.querySelectorAll('.page').forEach(p => p.classList.remove('active'));
  // Show requested page
  document.getElementById('page-' + name).classList.add('active');

  // Update nav active link
  document.querySelectorAll('.nav-links a').forEach(a => a.classList.remove('active'));
  const navLink = document.getElementById('nav-' + name);
  if (navLink) navLink.classList.add('active');

  // Scroll to top
  window.scrollTo({ top: 0, behavior: 'smooth' });

  // Run page-specific init
  if (name === 'features') initFeatChart();
  if (name === 'tools')    { initTodos(); updateScore(); }

  // Trigger reveal animations
  setTimeout(initReveal, 100);
  return false;
}

/* ============================================================
   MOBILE MENU
============================================================ */
function toggleMenu() {
  const menu = document.getElementById('mobileMenu');
  const ham  = document.getElementById('hamburger');
  menu.classList.toggle('open');
  ham.classList.toggle('open');
}
function closeMenu() {
  document.getElementById('mobileMenu').classList.remove('open');
  document.getElementById('hamburger').classList.remove('open');
}

/* ============================================================
   SCROLL REVEAL — uses IntersectionObserver
============================================================ */
function initReveal() {
  const observer = new IntersectionObserver((entries) => {
    entries.forEach(e => {
      if (e.isIntersecting) {
        e.target.classList.add('visible');
        observer.unobserve(e.target);
      }
    });
  }, { threshold: 0.12 });

  document.querySelectorAll('.reveal').forEach(el => {
    el.classList.remove('visible');
    observer.observe(el);
  });
}

/* ============================================================
   HOME PAGE — Animated mock timer clock
============================================================ */
(function animateMockClock() {
  let s = 18 * 60 + 42;
  setInterval(() => {
    if (s > 0) s--;
    const m = Math.floor(s / 60);
    const sec = s % 60;
    const el = document.getElementById('mockTime');
    if (el) el.textContent = String(m).padStart(2,'0') + ':' + String(sec).padStart(2,'0');
  }, 1000);
})();

/* ============================================================
   HOME PAGE — Bar chart (how it works section)
============================================================ */
(function buildHomeChart() {
  const data = [
    { d:'Mon', focus:2.5, rev:1.5 },
    { d:'Tue', focus:3.0, rev:1.0 },
    { d:'Wed', focus:1.5, rev:2.0 },
    { d:'Thu', focus:4.0, rev:1.5 },
    { d:'Fri', focus:3.5, rev:2.0 },
    { d:'Sat', focus:2.0, rev:1.0 },
    { d:'Sun', focus:3.8, rev:1.8 },
  ];
  const max = 6;
  const wrap = document.getElementById('howChart');
  if (!wrap) return;
  data.forEach(item => {
    const col = document.createElement('div');
    col.className = 'bar-col';
    col.innerHTML = `
      <div class="bar" style="height:${(item.focus/max)*90}px; background:linear-gradient(180deg, #00e5ff, rgba(0,229,255,.4));"></div>
      <div class="bar" style="height:${(item.rev/max)*90}px; background:linear-gradient(180deg, #a855f7, rgba(168,85,247,.4));"></div>
      <div class="bar-label">${item.d}</div>
    `;
    wrap.appendChild(col);
  });
})();

/* ============================================================
   FEATURES PAGE — Analytics chart
============================================================ */
function initFeatChart() {
  const wrap = document.getElementById('featChart');
  if (!wrap || wrap.children.length > 0) return;
  const data = [
    { d:'M', v:3.2 }, { d:'T', v:4.1 }, { d:'W', v:2.8 },
    { d:'T', v:5.0 }, { d:'F', v:3.6 }, { d:'S', v:1.9 }, { d:'S', v:4.4 }
  ];
  const max = 5.5;
  data.forEach((item,i) => {
    const col = document.createElement('div');
    col.className = 'bar-col';
    const h = Math.round((item.v / max) * 90);
    const color = i % 2 === 0
      ? 'linear-gradient(180deg, #00e5ff, rgba(0,229,255,.3))'
      : 'linear-gradient(180deg, #a855f7, rgba(168,85,247,.3))';
    col.innerHTML = `
      <div class="bar" style="height:${h}px; background:${color};"></div>
      <div class="bar-label">${item.d}</div>
    `;
    wrap.appendChild(col);
  });
}

/* ============================================================
   POMODORO TIMER
============================================================ */
let pomoState = {
  totalSeconds: 25 * 60,
  remaining:    25 * 60,
  running:      false,
  interval:     null,
  label:        'Focus',
  sessions:     parseInt(localStorage.getItem('ff_pomo_sessions') || '0'),
  streak:       parseInt(localStorage.getItem('ff_pomo_streak')   || '0'),
};
const CIRCUM = 2 * Math.PI * 80; // SVG circle circumference

function renderPomo() {
  const { remaining, totalSeconds, label } = pomoState;
  const m   = Math.floor(remaining / 60);
  const s   = remaining % 60;
  const pct = 1 - (remaining / totalSeconds);
  const offset = CIRCUM * pct;

  document.getElementById('pomoDisplay').textContent =
    String(m).padStart(2,'0') + ':' + String(s).padStart(2,'0');
  document.getElementById('pomoLabel').textContent = label;

  const ring = document.getElementById('pomoRingProgress');
  if (ring) {
    ring.style.strokeDasharray  = CIRCUM;
    ring.style.strokeDashoffset = CIRCUM - offset * CIRCUM / CIRCUM * CIRCUM;
    // Simpler: offset proportion
    ring.style.strokeDashoffset = CIRCUM * (1 - pct);
  }

  document.getElementById('pomoSessions').textContent = pomoState.sessions;
  document.getElementById('pomoStreak').textContent   = pomoState.streak;
}

function togglePomodoro() {
  const btn = document.getElementById('pomoStart');
  if (pomoState.running) {
    // Pause
    clearInterval(pomoState.interval);
    pomoState.running = false;
    btn.innerHTML = '▶ Resume';
    btn.style.background = 'linear-gradient(135deg, #a855f7, #f472b6)';
  } else {
    // Start / resume
    pomoState.running = true;
    btn.innerHTML = '⏸ Pause';
    btn.style.background = 'linear-gradient(135deg, #00e5ff, #a855f7)';
    pomoState.interval = setInterval(() => {
      pomoState.remaining--;
      renderPomo();
      if (pomoState.remaining <= 0) {
        clearInterval(pomoState.interval);
        pomoState.running = false;
        pomoState.sessions++;
        pomoState.streak++;
        localStorage.setItem('ff_pomo_sessions', pomoState.sessions);
        localStorage.setItem('ff_pomo_streak',   pomoState.streak);
        btn.innerHTML = '▶ Start';
        btn.style.background = 'linear-gradient(135deg, #00e5ff, #a855f7)';
        renderPomo();
        // Browser notification if permission granted
        if (Notification && Notification.permission === 'granted') {
          new Notification('FocusFlow', { body: pomoState.label + ' session complete! 🎉' });
        }
      }
    }, 1000);
  }
}

function resetPomodoro() {
  clearInterval(pomoState.interval);
  pomoState.running  = false;
  pomoState.remaining = pomoState.totalSeconds;
  const btn = document.getElementById('pomoStart');
  btn.innerHTML = '▶ Start';
  btn.style.background = 'linear-gradient(135deg, #00e5ff, #a855f7)';
  renderPomo();
}

function setPomoMode(btn, mins, label) {
  // Reset running timer
  clearInterval(pomoState.interval);
  pomoState.running     = false;
  pomoState.totalSeconds = mins * 60;
  pomoState.remaining   = mins * 60;
  pomoState.label       = label;
  document.getElementById('pomoStart').innerHTML = '▶ Start';
  document.getElementById('pomoStart').style.background = 'linear-gradient(135deg, #00e5ff, #a855f7)';

  // Update active button
  document.querySelectorAll('.pomo-mode-btn').forEach(b => b.classList.remove('active'));
  btn.classList.add('active');
  renderPomo();
}

// Init on page load
renderPomo();

/* ============================================================
   TO-DO LIST  — localStorage persistent
============================================================ */
let todos       = [];
let todoFilter  = 'all'; // 'all' | 'active' | 'done'

function initTodos() {
  const stored = localStorage.getItem('ff_todos');
  todos = stored ? JSON.parse(stored) : [
    { id: 1, text: 'Read OS Chapter 3', priority: 'high',   done: false },
    { id: 2, text: 'Solve 10 DSA problems', priority: 'medium', done: false },
    { id: 3, text: 'Watch DBMS ER Model lecture', priority: 'low',    done: true  },
  ];
  renderTodos();
}

function saveTodos() {
  localStorage.setItem('ff_todos', JSON.stringify(todos));
}

function renderTodos() {
  const list = document.getElementById('todoList');
  if (!list) return;
  list.innerHTML = '';

  const filtered = todos.filter(t =>
    todoFilter === 'all'    ? true :
    todoFilter === 'active' ? !t.done :
    t.done
  );

  if (filtered.length === 0) {
    list.innerHTML = `<div style="text-align:center; color:var(--muted); font-size:.88rem; padding:20px 0;">
      ${todoFilter === 'done' ? '🎉 No completed tasks yet.' : '✨ All clear! Add some tasks above.'}
    </div>`;
  } else {
    filtered.forEach(t => {
      const item = document.createElement('div');
      item.className = 'todo-item' + (t.done ? ' done' : '');
      item.innerHTML = `
        <div class="todo-check ${t.done ? 'checked' : ''}" onclick="toggleTodo(${t.id})">
          ${t.done ? '✓' : ''}
        </div>
        <span class="todo-text" onclick="toggleTodo(${t.id})">${escHtml(t.text)}</span>
        <span class="todo-priority pri-${t.priority}">${t.priority.toUpperCase()}</span>
        <button class="todo-delete" onclick="deleteTodo(${t.id})">✕</button>
      `;
      list.appendChild(item);
    });
  }

  // Update count
  const active = todos.filter(t => !t.done).length;
  document.getElementById('todoCount').textContent = active + ' task' + (active !== 1 ? 's' : '') + ' remaining';
}

function addTodo() {
  const input = document.getElementById('todoInput');
  const pri   = document.getElementById('todoPriority');
  const text  = input.value.trim();
  if (!text) {
    input.style.borderColor = 'rgba(244,114,182,.5)';
    setTimeout(() => input.style.borderColor = '', 1000);
    return;
  }
  todos.unshift({
    id:       Date.now(),
    text:     text,
    priority: pri.value,
    done:     false,
  });
  input.value = '';
  saveTodos();
  renderTodos();
}

function toggleTodo(id) {
  const t = todos.find(t => t.id === id);
  if (t) t.done = !t.done;
  saveTodos();
  renderTodos();
}

function deleteTodo(id) {
  todos = todos.filter(t => t.id !== id);
  saveTodos();
  renderTodos();
}

function filterTodos(f, btn) {
  todoFilter = f;
  document.querySelectorAll('.filter-btn').forEach(b => b.classList.remove('active'));
  btn.classList.add('active');
  renderTodos();
}

function clearDone() {
  todos = todos.filter(t => !t.done);
  saveTodos();
  renderTodos();
}

function escHtml(str) {
  return str.replace(/&/g,'&amp;').replace(/</g,'&lt;').replace(/>/g,'&gt;').replace(/"/g,'&quot;');
}

/* ============================================================
   PRODUCTIVITY SCORE CALCULATOR
============================================================ */
function updateScore() {
  const study  = +document.getElementById('sl-study').value;
  const tasks  = +document.getElementById('sl-tasks').value;
  const focus  = +document.getElementById('sl-focus').value;
  const breaks = +document.getElementById('sl-breaks').value;
  const dist   = +document.getElementById('sl-dist').value;

  // Update labels
  document.getElementById('lbl-study').textContent  = study;
  document.getElementById('lbl-tasks').textContent  = tasks;
  document.getElementById('lbl-focus').textContent  = focus;
  document.getElementById('lbl-breaks').textContent = breaks;
  document.getElementById('lbl-dist').textContent   = dist;

  // Weighted score formula
  const studyScore  = Math.min(study  / 8  * 100, 100);
  const taskScore   = Math.min(tasks  / 10 * 100, 100);
  const focusScore  = focus  / 10 * 100;
  const breakScore  = Math.min(breaks / 4  * 100, 100);
  const distScore   = dist   / 10 * 100;

  const raw = studyScore*0.30 + taskScore*0.25 + focusScore*0.25 + breakScore*0.10 + distScore*0.10;
  const score = Math.round(raw);

  // Update slider track colors dynamically
  updateSliderTrack('sl-study',  study,  12, '#00e5ff');
  updateSliderTrack('sl-tasks',  tasks,  15, '#a855f7');
  updateSliderTrack('sl-focus',  focus,  10, '#f472b6');
  updateSliderTrack('sl-breaks', breaks,  8, '#fbbf24');
  updateSliderTrack('sl-dist',   dist,   10, '#00e5ff');

  // Animated counter
  animateCount('scoreDisplay', score);

  // Grade & tip
  let grade, tip, color;
  if (score >= 90) {
    grade = '🏆 Peak Performance'; color = '#00e5ff';
    tip   = 'Exceptional day! You are in the top 5% of FocusFlow users. Rest well tonight.';
  } else if (score >= 75) {
    grade = '⚡ High Performer'; color = '#a855f7';
    tip   = 'Great work! Squeeze in one more focused session before the day ends.';
  } else if (score >= 55) {
    grade = '📚 Steady Progress'; color = '#fbbf24';
    tip   = 'Decent effort. Try the Pomodoro timer to boost focus consistency tomorrow.';
  } else if (score >= 35) {
    grade = '⚠️ Needs Improvement'; color = '#f472b6';
    tip   = 'Low score today — but that\'s okay! Identify your biggest distraction and eliminate it.';
  } else {
    grade = '😴 Rest Day'; color = '#7878a0';
    tip   = 'Everyone has off days. Get a good sleep and start fresh tomorrow!';
  }

  document.getElementById('scoreGrade').innerHTML = `<span style="color:${color}">${grade}</span>`;
  document.getElementById('scoreTip').textContent  = tip;

  // Breakdown bars
  const breakdown = document.getElementById('scoreBreakdown');
  if (breakdown) {
    const items = [
      { label:'Study Hours',  val:Math.round(studyScore),  color:'#00e5ff' },
      { label:'Tasks Done',   val:Math.round(taskScore),   color:'#a855f7' },
      { label:'Focus Quality',val:Math.round(focusScore),  color:'#f472b6' },
      { label:'Healthy Breaks',val:Math.round(breakScore), color:'#fbbf24' },
      { label:'Distraction',  val:Math.round(distScore),   color:'#28c840' },
    ];
    breakdown.innerHTML = items.map(i => `
      <div style="margin-bottom:8px;">
        <div style="display:flex; justify-content:space-between; font-size:.75rem; color:var(--muted); margin-bottom:4px;">
          <span>${i.label}</span><span style="color:${i.color}; font-weight:700;">${i.val}%</span>
        </div>
        <div style="height:4px; background:rgba(255,255,255,.06); border-radius:4px; overflow:hidden;">
          <div style="height:100%; width:${i.val}%; background:${i.color}; border-radius:4px; transition:width .5s ease;"></div>
        </div>
      </div>
    `).join('');
  }
}

function updateSliderTrack(id, val, max, color) {
  const el  = document.getElementById(id);
  const pct = (val / max) * 100;
  el.style.background = `linear-gradient(to right, ${color} 0%, ${color} ${pct}%, rgba(255,255,255,.08) ${pct}%)`;
}

function animateCount(id, target) {
  const el   = document.getElementById(id);
  const start = parseInt(el.textContent) || 0;
  const diff  = target - start;
  const steps = 20;
  let   step  = 0;
  const timer = setInterval(() => {
    step++;
    el.textContent = Math.round(start + diff * (step / steps));
    if (step >= steps) clearInterval(timer);
  }, 16);
}

/* ============================================================
   CONTACT FORM
============================================================ */
function submitContact() {
  const name    = document.getElementById('cf-name').value.trim();
  const email   = document.getElementById('cf-email').value.trim();
  const message = document.getElementById('cf-message').value.trim();
  const errEl   = document.getElementById('formError');

  if (!name || !email || !message) {
    errEl.style.display = 'inline';
    setTimeout(() => errEl.style.display = 'none', 3000);
    return;
  }

  // Simulate form submission
  document.getElementById('contactFormWrap').style.display = 'none';
  document.getElementById('contactSuccess').classList.add('show');
}

/* ============================================================
   INIT ON LOAD
============================================================ */
window.addEventListener('load', () => {
  initReveal();
  // Request notification permission for timer
  if (Notification && Notification.permission === 'default') {
    Notification.requestPermission();
  }
});

// Re-run reveal on scroll
window.addEventListener('scroll', () => {
  initReveal();
}, { passive: true });
</script>

</body>
</html>
