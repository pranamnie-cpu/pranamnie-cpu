<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Pranam R — Full Stack Developer</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link href="https://fonts.googleapis.com/css2?family=JetBrains+Mono:wght@400;500;700&family=Fraunces:opsz,wght@9..144,400;9..144,600&family=Inter:wght@400;500;600&display=swap" rel="stylesheet">
<style>
  :root{
    --bg: #0B1210;
    --panel: #101A17;
    --panel-alt: #0D1614;
    --line: #21322C;
    --text: #E9EDE9;
    --muted: #8FA39A;
    --amber: #E8A33D;
    --teal: #4FD1B8;
    --red-dot: #E8735A;
  }
  *{box-sizing:border-box; margin:0; padding:0;}
  html,body{height:100%;}
  body{
    background: var(--bg);
    color: var(--text);
    font-family: 'Inter', sans-serif;
    display:flex;
    flex-direction:column;
    min-height:100vh;
    overflow-x:hidden;
  }

  /* ---------- Top hero ---------- */
  .hero{
    padding: 56px 32px 28px;
    max-width: 980px;
    margin: 0 auto;
    width:100%;
  }
  .hero-eyebrow{
    font-family:'JetBrains Mono', monospace;
    font-size:13px;
    color: var(--teal);
    margin-bottom:14px;
  }
  .hero-eyebrow::before{content:"$ ";color:var(--muted);}
  h1{
    font-family:'Fraunces', serif;
    font-weight:600;
    font-size: clamp(36px, 6vw, 58px);
    line-height:1.05;
    letter-spacing:-0.01em;
  }
  .hero-sub{
    margin-top:14px;
    font-size:17px;
    color: var(--muted);
    max-width:560px;
    line-height:1.55;
  }
  .hero-links{
    margin-top:26px;
    display:flex;
    gap:10px;
    flex-wrap:wrap;
  }
  .hero-links a{
    font-family:'JetBrains Mono', monospace;
    font-size:13px;
    color: var(--text);
    text-decoration:none;
    border:1px solid var(--line);
    padding:8px 14px;
    border-radius:6px;
    transition: border-color .15s ease, background .15s ease;
  }
  .hero-links a:hover{ border-color: var(--amber); background: rgba(232,163,61,0.07); }

  /* ---------- Editor window ---------- */
  .editor-wrap{
    max-width: 980px;
    margin: 8px auto 64px;
    padding: 0 32px;
    width:100%;
    flex:1;
  }
  .window{
    border: 1px solid var(--line);
    border-radius: 10px;
    overflow:hidden;
    background: var(--panel);
    box-shadow: 0 30px 60px -30px rgba(0,0,0,0.6);
  }
  .titlebar{
    display:flex;
    align-items:center;
    gap:8px;
    padding: 12px 16px;
    background: var(--panel-alt);
    border-bottom:1px solid var(--line);
  }
  .dot{ width:11px; height:11px; border-radius:50%; }
  .dot.r{ background:#E8735A55; border:1px solid #E8735A; }
  .dot.y{ background:#E8A33D55; border:1px solid #E8A33D; }
  .dot.g{ background:#4FD1B855; border:1px solid #4FD1B8; }
  .titlebar-name{
    margin-left:8px;
    font-family:'JetBrains Mono', monospace;
    font-size:12.5px;
    color: var(--muted);
  }

  .body-grid{
    display:grid;
    grid-template-columns: 190px 1fr;
    min-height: 480px;
  }
  @media (max-width: 640px){
    .body-grid{ grid-template-columns: 1fr; }
    .sidebar{ display:flex; overflow-x:auto; border-right:none !important; border-bottom:1px solid var(--line); }
    .sidebar .file{ white-space:nowrap; }
  }

  .sidebar{
    border-right: 1px solid var(--line);
    padding: 14px 0;
    background: var(--panel-alt);
  }
  .sidebar-label{
    font-family:'JetBrains Mono', monospace;
    font-size:11px;
    color: var(--muted);
    text-transform:lowercase;
    padding: 4px 18px 10px;
    letter-spacing:.02em;
  }
  .file{
    display:flex;
    align-items:center;
    gap:9px;
    width:100%;
    text-align:left;
    background:none;
    border:none;
    color: var(--muted);
    font-family:'JetBrains Mono', monospace;
    font-size:13px;
    padding: 9px 18px;
    cursor:pointer;
    border-left: 2px solid transparent;
    transition: color .12s ease, background .12s ease;
  }
  .file:hover{ color: var(--text); background: rgba(255,255,255,0.02); }
  .file.active{
    color: var(--amber);
    border-left-color: var(--amber);
    background: rgba(232,163,61,0.06);
  }
  .file .tag{ font-size:14px; opacity:.8; }

  .pane{ padding: 26px 32px 34px; }
  .tabline{
    font-family:'JetBrains Mono', monospace;
    font-size:12px;
    color: var(--muted);
    margin-bottom: 20px;
    padding-bottom: 12px;
    border-bottom: 1px solid var(--line);
  }
  .tabline span{ color: var(--teal); }

  .pane-content{ animation: fadeIn .25s ease; }
  @keyframes fadeIn{ from{opacity:0; transform:translateY(4px);} to{opacity:1; transform:translateY(0);} }

  h2.section-title{
    font-family:'Fraunces', serif;
    font-weight:600;
    font-size:24px;
    margin-bottom:14px;
  }
  p.body-text{ color:#CBD5CF; line-height:1.7; font-size:15px; max-width:600px; margin-bottom:12px; }
  .comment{ color: var(--muted); font-family:'JetBrains Mono', monospace; font-size:13px; }

  /* about */
  .facts{ margin-top:18px; display:grid; gap:10px; }
  .fact{ display:flex; gap:12px; font-size:14.5px; }
  .fact .k{ font-family:'JetBrains Mono', monospace; color: var(--teal); min-width:110px; }
  .fact .v{ color: var(--text); }

  /* skills */
  .skill-grid{ display:grid; grid-template-columns: repeat(auto-fill, minmax(210px,1fr)); gap:10px; margin-top:6px;}
  .skill-row{
    border:1px solid var(--line);
    border-radius:7px;
    padding:11px 13px;
    background: var(--panel-alt);
  }
  .skill-row-top{ display:flex; justify-content:space-between; font-size:13.5px; margin-bottom:8px; }
  .skill-row-top .name{ font-family:'JetBrains Mono', monospace; }
  .skill-row-top .lvl{ color: var(--muted); font-size:12px; }
  .bar{ height:5px; background:#1B2924; border-radius:4px; overflow:hidden; }
  .bar-fill{ height:100%; background: linear-gradient(90deg, var(--teal), var(--amber)); width:0%; transition: width 1s cubic-bezier(.2,.8,.2,1); border-radius:4px; }

  /* projects */
  .filters{ display:flex; gap:8px; margin-bottom:18px; flex-wrap:wrap; }
  .filter-btn{
    font-family:'JetBrains Mono', monospace;
    font-size:12px;
    background:none;
    border:1px solid var(--line);
    color: var(--muted);
    padding:6px 12px;
    border-radius:16px;
    cursor:pointer;
    transition: all .15s ease;
  }
  .filter-btn.active, .filter-btn:hover{ border-color:var(--teal); color:var(--teal); }
  .proj-list{ display:grid; gap:14px; }
  .proj{
    border:1px solid var(--line);
    border-radius:8px;
    padding:18px 20px;
    background: var(--panel-alt);
    cursor:pointer;
    transition: border-color .15s ease;
  }
  .proj:hover{ border-color: var(--amber); }
  .proj-head{ display:flex; justify-content:space-between; align-items:baseline; gap:10px; flex-wrap:wrap; }
  .proj-name{ font-family:'Fraunces', serif; font-size:19px; font-weight:600; }
  .proj-role{ font-family:'JetBrains Mono', monospace; font-size:11.5px; color: var(--teal); }
  .proj-desc{ color:#CBD5CF; font-size:14px; margin-top:8px; line-height:1.6; max-height:0; overflow:hidden; transition: max-height .3s ease, margin-top .3s ease; }
  .proj.open .proj-desc{ max-height:200px; margin-top:10px; }
  .proj-stack{ margin-top:10px; display:flex; gap:6px; flex-wrap:wrap; }
  .chip{ font-family:'JetBrains Mono', monospace; font-size:11px; color: var(--muted); border:1px solid var(--line); border-radius:4px; padding:2px 7px; }
  .chevron{ font-family:'JetBrains Mono', monospace; color: var(--muted); font-size:13px; transition: transform .2s ease; }
  .proj.open .chevron{ transform: rotate(90deg); color: var(--amber); }

  /* contact */
  .contact-line{ display:flex; align-items:center; gap:10px; font-family:'JetBrains Mono', monospace; font-size:14px; margin-bottom:12px; }
  .contact-line .p{ color: var(--muted); }
  .copy-btn{
    background:none; border:1px solid var(--line); color: var(--muted);
    font-family:'JetBrains Mono', monospace; font-size:11px; padding:3px 9px; border-radius:5px; cursor:pointer;
  }
  .copy-btn:hover{ border-color: var(--teal); color: var(--teal); }
  .copy-btn.copied{ border-color: var(--teal); color: var(--teal); }

  footer{
    text-align:center;
    padding: 18px;
    font-family:'JetBrains Mono', monospace;
    font-size:11.5px;
    color: var(--muted);
  }
</style>
</head>
<body>

<div class="hero">
  <div class="hero-eyebrow">whoami</div>
  <h1>Pranam R</h1>
  <p class="hero-sub">Full stack developer moving from a diploma in Computer Science into a B.Tech in CSE (AI &amp; ML) — I build with the MERN stack and I'm exploring machine learning.</p>
  <div class="hero-links">
    <a href="mailto:pranamn714@gmail.com">email</a>
    <a href="https://github.com/pranamnie-cpu" target="_blank" rel="noopener">github</a>
    <a href="#" onclick="return false;">Udupi, Karnataka</a>
  </div>
</div>

<div class="editor-wrap">
  <div class="window">
    <div class="titlebar">
      <div class="dot r"></div><div class="dot y"></div><div class="dot g"></div>
      <div class="titlebar-name">pranam-r — portfolio</div>
    </div>
    <div class="body-grid">
      <div class="sidebar">
        <div class="sidebar-label">// explorer</div>
        <button class="file active" data-target="about"><span class="tag">◆</span>about.md</button>
        <button class="file" data-target="skills"><span class="tag">{ }</span>skills.json</button>
        <button class="file" data-target="projects"><span class="tag">&lt;/&gt;</span>projects.js</button>
        <button class="file" data-target="contact"><span class="tag">$</span>contact.sh</button>
      </div>

      <div class="pane">
        <div class="tabline">~/pranam-r/<span id="tab-name">about.md</span></div>

        <div class="pane-content" id="pane-about">
          <h2 class="section-title">About</h2>
          <p class="body-text">Coming from a diploma background rather than a straight-through PU path, I built two full working applications before even starting engineering — that hands-on foundation is what I'm carrying into a lateral-entry B.Tech in CSE, with a growing focus on AI &amp; ML.</p>
          <div class="facts">
            <div class="fact"><span class="k">education</span><span class="v">B.Tech CSE (AI &amp; ML) — lateral entry, 3rd semester</span></div>
            <div class="fact"><span class="k">background</span><span class="v">Diploma in Computer Science, NRAM Polytechnic Nitte</span></div>
            <div class="fact"><span class="k">focus</span><span class="v">MERN stack development, exploring AI/ML</span></div>
            <div class="fact"><span class="k">location</span><span class="v">Udupi, Karnataka</span></div>
          </div>
        </div>

        <div class="pane-content" id="pane-skills" style="display:none;">
          <h2 class="section-title">Skills</h2>
          <p class="comment">// hover a bar isn't needed — levels load on open</p>
          <div class="skill-grid" id="skill-grid">
            <div class="skill-row" data-lvl="80"><div class="skill-row-top"><span class="name">JavaScript</span><span class="lvl">core</span></div><div class="bar"><div class="bar-fill"></div></div></div>
            <div class="skill-row" data-lvl="75"><div class="skill-row-top"><span class="name">React</span><span class="lvl">core</span></div><div class="bar"><div class="bar-fill"></div></div></div>
            <div class="skill-row" data-lvl="75"><div class="skill-row-top"><span class="name">Node.js / Express</span><span class="lvl">core</span></div><div class="bar"><div class="bar-fill"></div></div></div>
            <div class="skill-row" data-lvl="70"><div class="skill-row-top"><span class="name">MongoDB</span><span class="lvl">core</span></div><div class="bar"><div class="bar-fill"></div></div></div>
            <div class="skill-row" data-lvl="65"><div class="skill-row-top"><span class="name">Java</span><span class="lvl">working</span></div><div class="bar"><div class="bar-fill"></div></div></div>
            <div class="skill-row" data-lvl="55"><div class="skill-row-top"><span class="name">Python</span><span class="lvl">learning</span></div><div class="bar"><div class="bar-fill"></div></div></div>
            <div class="skill-row" data-lvl="60"><div class="skill-row-top"><span class="name">Git / GitHub</span><span class="lvl">working</span></div><div class="bar"><div class="bar-fill"></div></div></div>
            <div class="skill-row" data-lvl="45"><div class="skill-row-top"><span class="name">HTML / CSS</span><span class="lvl">working</span></div><div class="bar"><div class="bar-fill"></div></div></div>
          </div>
        </div>

        <div class="pane-content" id="pane-projects" style="display:none;">
          <h2 class="section-title">Projects</h2>
          <div class="filters">
            <button class="filter-btn active" data-filter="all">all</button>
            <button class="filter-btn" data-filter="MERN">MERN</button>
            <button class="filter-btn" data-filter="Full Stack">Full Stack</button>
          </div>
          <div class="proj-list" id="proj-list">
            <div class="proj" data-stack="MERN">
              <div class="proj-head">
                <span class="proj-name">Contractor Finder &amp; Booking</span>
                <span class="chevron">›</span>
              </div>
              <span class="proj-role">three-role platform — user / contractor / admin</span>
              <div class="proj-desc">
                A booking platform connecting users with contractors, built with JWT-based auth and separate dashboards per role. Backend admin modules, image upload and persistence handling, and responsive layouts were all built from scratch.
              </div>
              <div class="proj-stack">
                <span class="chip">MongoDB</span><span class="chip">Express</span><span class="chip">React</span><span class="chip">Node.js</span><span class="chip">JWT</span>
              </div>
            </div>

            <div class="proj" data-stack="Full Stack">
              <div class="proj-head">
                <span class="proj-name">Digital Menu System</span>
                <span class="chevron">›</span>
              </div>
              <span class="proj-role">QR-based contactless restaurant menu</span>
              <div class="proj-desc">
                A digital menu restaurants can deploy via QR code, replacing physical menus with a fast, role-based ordering flow — built with localStorage-backed auth for simplicity and speed.
              </div>
              <div class="proj-stack">
                <span class="chip">React</span><span class="chip">Node.js</span><span class="chip">Full Stack</span>
              </div>
            </div>
          </div>
        </div>

        <div class="pane-content" id="pane-contact" style="display:none;">
          <h2 class="section-title">Contact</h2>
          <p class="comment">// reach out</p>
          <div style="margin-top:14px;">
            <div class="contact-line"><span class="p">email</span> pranamn714@gmail.com <button class="copy-btn" onclick="copyText('pranamn714@gmail.com', this)">copy</button></div>
            <div class="contact-line"><span class="p">github</span> <a href="https://github.com/pranamnie-cpu" target="_blank" rel="noopener" style="color:var(--teal); text-decoration:none;">github.com/pranamnie-cpu</a></div>
          </div>
        </div>

      </div>
    </div>
  </div>
</div>

<footer>built by hand — no template, just markup</footer>

<script>
  const files = document.querySelectorAll('.file');
  const panes = { about: 'pane-about', skills: 'pane-skills', projects: 'pane-projects', contact: 'pane-contact' };
  const tabName = document.getElementById('tab-name');
  const names = { about: 'about.md', skills: 'skills.json', projects: 'projects.js', contact: 'contact.sh' };

  files.forEach(btn => {
    btn.addEventListener('click', () => {
      files.forEach(f => f.classList.remove('active'));
      btn.classList.add('active');
      const target = btn.dataset.target;
      Object.values(panes).forEach(id => document.getElementById(id).style.display = 'none');
      document.getElementById(panes[target]).style.display = 'block';
      tabName.textContent = names[target];
      if (target === 'skills') animateSkills();
    });
  });

  function animateSkills(){
    document.querySelectorAll('.skill-row').forEach(row => {
      const lvl = row.dataset.lvl;
      const fill = row.querySelector('.bar-fill');
      requestAnimationFrame(() => { fill.style.width = lvl + '%'; });
    });
  }

  document.querySelectorAll('.proj').forEach(p => {
    p.addEventListener('click', () => p.classList.toggle('open'));
  });

  document.querySelectorAll('.filter-btn').forEach(btn => {
    btn.addEventListener('click', () => {
      document.querySelectorAll('.filter-btn').forEach(b => b.classList.remove('active'));
      btn.classList.add('active');
      const f = btn.dataset.filter;
      document.querySelectorAll('.proj').forEach(p => {
        p.style.display = (f === 'all' || p.dataset.stack === f) ? 'block' : 'none';
      });
    });
  });

  function copyText(text, btn){
    navigator.clipboard.writeText(text).then(() => {
      const old = btn.textContent;
      btn.textContent = 'copied';
      btn.classList.add('copied');
      setTimeout(() => { btn.textContent = old; btn.classList.remove('copied'); }, 1500);
    });
  }
</script>

</body>
</html>
