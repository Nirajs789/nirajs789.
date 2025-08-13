<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <title>Niraj Singh • Projects Portfolio</title>
  <meta name="description" content="Interactive portfolio that auto-fetches GitHub repos and showcases featured projects with live links and filters." />
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
  <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700;800&display=swap" rel="stylesheet">
  <style>
    :root{
      --bg: #0b0f14; /* dark slate */
      --card: #121822;
      --muted: #a0b3c7;
      --text: #e6eef7;
      --accent: #60a5fa; /* blue */
      --accent-2: #34d399; /* green */
      --ring: rgba(96,165,250,.35);
      --shadow: 0 10px 30px rgba(0,0,0,.35);
    }
    *{box-sizing:border-box}
    html,body{height:100%}
    body{
      margin:0; font-family:Inter, system-ui, -apple-system, Segoe UI, Roboto, Arial, "Noto Sans", "Apple Color Emoji", "Segoe UI Emoji";
      background: radial-gradient(1200px 700px at 10% -10%, #122034 0%, transparent 60%),
                  radial-gradient(800px 500px at 120% 20%, #13223a 0%, transparent 60%),
                  var(--bg);
      color:var(--text);
      line-height:1.55;
    }
    a{color:inherit; text-decoration:none}

    .container{max-width:1100px; margin:0 auto; padding:24px}

    /* Header */
    header{
      position:sticky; top:0; z-index:10; backdrop-filter: blur(10px);
      background: linear-gradient(180deg, rgba(11,15,20,.8), rgba(11,15,20,.4));
      border-bottom: 1px solid rgba(148,163,184,.15);
    }
    .nav{display:flex; align-items:center; justify-content:space-between; gap:16px}
    .brand{display:flex; align-items:center; gap:12px}
    .logo{width:40px; height:40px; border-radius:12px; background: linear-gradient(135deg, var(--accent), var(--accent-2)); box-shadow: var(--shadow)}
    .title{font-weight:800; letter-spacing:.3px}

    .actions{display:flex; gap:10px; align-items:center}
    .btn{
      display:inline-flex; align-items:center; gap:8px; padding:10px 14px; border-radius:14px;
      border:1px solid rgba(148,163,184,.25); background: #0f1621; color: var(--text);
      outline:none; cursor:pointer; transition:.2s transform, .2s filter, .2s background;
    }
    .btn:hover{transform:translateY(-1px); filter:brightness(1.05)}
    .btn.primary{background: linear-gradient(135deg, var(--accent), var(--accent-2)); color:#07131f; font-weight:700; border:none}

    /* Hero */
    .hero{display:grid; grid-template-columns: 1.35fr .65fr; gap:24px; padding:28px 0 8px}
    .hero h1{font-size:clamp(28px, 4vw, 40px); line-height:1.15; margin:0 0 10px}
    .hero p{color:var(--muted); margin:6px 0 16px}
    .pill{
      display:inline-flex; align-items:center; gap:8px; padding:8px 12px; border-radius:999px; font-size:14px;
      background:rgba(96,165,250,.12); color:#bfe0ff; border:1px solid var(--ring);
    }
    .statbar{display:flex; gap:14px; flex-wrap:wrap; margin-top:10px}
    .stat{background:#0e1621; border:1px solid rgba(148,163,184,.2); padding:10px 12px; border-radius:12px; color:#cfe0f7}
    .avatar{justify-self:end; align-self:start; width:130px; height:130px; border-radius:20px; background:#0f1724; border:1px solid rgba(148,163,184,.2);
      display:grid; place-items:center; font-weight:800; font-size:42px; color:#9cc7ff}

    /* Controls */
    .controls{display:flex; gap:10px; flex-wrap:wrap; margin:20px 0 10px}
    .input, select{
      background:#0f1621; color:var(--text); border:1px solid rgba(148,163,184,.25); border-radius:12px; padding:10px 12px; outline:none;
    }
    .input:focus, select:focus{box-shadow:0 0 0 4px var(--ring)}

    /* Sections */
    section{margin:24px 0}
    .grid{display:grid; grid-template-columns:repeat(3, minmax(0, 1fr)); gap:16px}
    @media (max-width:1000px){.hero{grid-template-columns:1fr}.avatar{justify-self:start}.grid{grid-template-columns:repeat(2,1fr)}}
    @media (max-width:640px){.grid{grid-template-columns:1fr}}

    .card{
      background:linear-gradient(180deg, rgba(18,24,34,.85), rgba(18,24,34,.65)); border:1px solid rgba(148,163,184,.2); border-radius:18px; padding:16px;
      box-shadow: var(--shadow); display:flex; flex-direction:column; gap:10px; position:relative; overflow:hidden
    }
    .card .name{font-weight:700}
    .card .desc{color:var(--muted); font-size:14px; min-height:38px}
    .meta{display:flex; gap:10px; flex-wrap:wrap; color:#bdd1eb; font-size:12px}
    .badges{display:flex; gap:6px; flex-wrap:wrap}
    .badge{font-size:11px; padding:6px 8px; border-radius:999px; border:1px solid rgba(148,163,184,.25); background:#0d1520}
    .card .links{margin-top:auto; display:flex; gap:10px}
    .card .links a{flex:1; text-align:center}

    .divider{height:1px; background:linear-gradient(90deg, transparent, rgba(148,163,184,.25), transparent); margin:6px 0 14px}
    .subtle{color:#9fb4cb; font-weight:600; letter-spacing:.25px; margin:0 0 8px}

    /* Footer */
    footer{margin:32px 0; color:#98aec7; text-align:center; font-size:14px}
  </style>
</head>
<body>
  <header>
    <div class="container nav">
      <div class="brand">
        <div class="logo" aria-hidden="true"></div>
        <div>
          <div class="title">Niraj Singh</div>
          <div style="font-size:12px; color:#9db6d3">ECE • IoT • Web Development</div>
        </div>
      </div>
      <div class="actions">
        <a class="btn" id="resumeBtn" href="#" target="_blank" rel="noopener">📄 Resume</a>
        <a class="btn primary" id="githubBtn" href="https://github.com/Nirajs789" target="_blank" rel="noopener">⭐ GitHub</a>
      </div>
    </div>
  </header>

  <main class="container">
    <section class="hero">
      <div>
        <span class="pill">Available for Internships</span>
        <h1>Projects that connect <span style="color:var(--accent)">hardware</span> & <span style="color:var(--accent-2)">software</span>.</h1>
        <p>Interactive portfolio that auto-fetches my GitHub repositories, highlights featured projects, and lets you filter by language and sort by activity.</p>
        <div class="statbar" id="stats">
          <div class="stat" id="statRepos">Repos: …</div>
          <div class="stat" id="statStars">Stars: …</div>
          <div class="stat" id="statFollowers">Followers: …</div>
        </div>
      </div>
      <div class="avatar" aria-label="Avatar">NS</div>
    </section>

    <section>
      <div class="subtle">Featured Projects</div>
      <div class="grid" id="featuredGrid"></div>
    </section>

    <div class="divider"></div>

    <section>
      <div class="subtle">All Repositories</div>
      <div class="controls">
        <input id="search" class="input" placeholder="Search by name or description…" />
        <select id="lang">
          <option value="">All languages</option>
        </select>
        <select id="sort">
          <option value="updated">Sort: Recently updated</option>
          <option value="created">Sort: Recently created</option>
          <option value="stars">Sort: Most stars</option>
          <option value="name">Sort: Name (A→Z)</option>
        </select>
      </div>
      <div class="grid" id="repoGrid"></div>
    </section>

    <footer>
      Built with ❤ by Niraj • Deployed on GitHub Pages
    </footer>
  </main>

  <script>
    // =========================
    // CONFIG
    // =========================
    const GITHUB_USERNAME = 'Nirajs789';
    // Add or remove featured repo slugs as needed
    const FEATURED = [
      'Arduino-weather-station',
      'WeatherApp',
      'weather-app',
      'Stopwatch-web-Application',
      'Responsive-Landing-Page-',
      'Personal-portfolio-website-'
    ];
    // Optional: link your resume
    const RESUME_URL = '';
    if(RESUME_URL){
      document.getElementById('resumeBtn').href = RESUME_URL;
    } else {
      document.getElementById('resumeBtn').style.display = 'none';
    }

    const state = { repos: [], langs: new Set() };

    // =========================
    // UTILITIES
    // =========================
    const el = (tag, attrs = {}, children = []) => {
      const node = document.createElement(tag);
      for (const [k,v] of Object.entries(attrs)) {
        if (k === 'class') node.className = v;
        else if (k === 'html') node.innerHTML = v;
        else if (k.startsWith('on') && typeof v === 'function') node.addEventListener(k.substring(2), v);
        else node.setAttribute(k, v);
      }
      [].concat(children).filter(Boolean).forEach(c => node.appendChild(typeof c === 'string' ? document.createTextNode(c) : c));
      return node;
    };

    function fmtDate(iso){
      const d = new Date(iso);
      return d.toLocaleDateString(undefined, { year:'numeric', month:'short', day:'numeric' });
    }

    function repoCard(r){
      const desc = r.description || 'No description provided.';
      return el('div', { class:'card' }, [
        el('div', { class:'name' }, [ el('a', { href:r.html_url, target:'_blank', rel:'noopener' }, r.name ) ]),
        el('div', { class:'desc' }, desc),
        el('div', { class:'meta' }, [
          el('span', {}, `★ ${r.stargazers_count}`),
          el('span', {}, `⑂ ${r.forks_count}`),
          r.language ? el('span', {}, r.language) : null,
          el('span', {}, `Updated ${fmtDate(r.updated_at)}`),
        ]),
        el('div', { class:'badges' }, [
          r.homepage ? el('span', { class:'badge' }, 'Live Demo') : null,
          r.topics?.length ? el('span', { class:'badge' }, r.topics.slice(0,3).join(' • ')) : null
        ]),
        el('div', { class:'links' }, [
          el('a', { class:'btn', href:r.html_url, target:'_blank', rel:'noopener' }, 'Source Code'),
          el('a', { class:'btn primary', href: r.homepage || r.html_url, target:'_blank', rel:'noopener' }, r.homepage ? 'Open Demo' : 'Open Repo')
        ])
      ]);
    }

    function renderAll(){
      const grid = document.getElementById('repoGrid');
      grid.innerHTML = '';

      const q = document.getElementById('search').value.trim().toLowerCase();
      const lang = document.getElementById('lang').value;
      const sort = document.getElementById('sort').value;

      let data = state.repos.filter(r => !FEATURED.includes(r.name));
      if(q){
        data = data.filter(r => (r.name + ' ' + (r.description||'')).toLowerCase().includes(q));
      }
      if(lang){
        data = data.filter(r => (r.language||'') === lang);
      }
      if(sort === 'updated') data.sort((a,b)=> new Date(b.updated_at)-new Date(a.updated_at));
      if(sort === 'created') data.sort((a,b)=> new Date(b.created_at)-new Date(a.created_at));
      if(sort === 'stars') data.sort((a,b)=> b.stargazers_count-a.stargazers_count);
      if(sort === 'name') data.sort((a,b)=> a.name.localeCompare(b.name));

      data.forEach(r => grid.appendChild(repoCard(r)));
    }

    function renderFeatured(){
      const grid = document.getElementById('featuredGrid');
      grid.innerHTML = '';
      const items = state.repos.filter(r => FEATURED.includes(r.name));
      // keep original FEATURED order
      items.sort((a,b)=> FEATURED.indexOf(a.name) - FEATURED.indexOf(b.name));
      items.forEach(r => grid.appendChild(repoCard(r)));
    }

    function renderLangs(){
      const sel = document.getElementById('lang');
      const langs = Array.from(state.langs).filter(Boolean).sort();
      langs.forEach(l => sel.appendChild(el('option', { value:l }, l)));
    }

    async function fetchUser(){
      const res = await fetch(`https://api.github.com/users/${GITHUB_USERNAME}`);
      if(!res.ok) throw new Error('User not found');
      return res.json();
    }

    async function fetchRepos(){
      // Get up to 100 repos (GitHub API cap per page)
      const res = await fetch(`https://api.github.com/users/${GITHUB_USERNAME}/repos?per_page=100&sort=updated`);
      if(!res.ok) throw new Error('Repos not found');
      const data = await res.json();
      // Enrich: attempt to fetch topics & homepage via separate endpoint (optional)
      // Note: basic /repos already includes homepage; topics require preview header, so we skip extra call here.
      return data.filter(r => !r.fork); // hide forks by default
    }

    async function init(){
      try {
        const [user, repos] = await Promise.all([fetchUser(), fetchRepos()]);
        state.repos = repos;
        repos.forEach(r => state.langs.add(r.language));
        renderLangs();
        renderFeatured();
        renderAll();
        // Stats
        document.getElementById('statRepos').textContent = `Repos: ${user.public_repos}`;
        document.getElementById('statStars').textContent = `Stars: ${repos.reduce((s,r)=>s+r.stargazers_count,0)}`;
        document.getElementById('statFollowers').textContent = `Followers: ${user.followers}`;
        // Header buttons
        document.getElementById('githubBtn').href = user.html_url;
      } catch (err){
        console.error(err);
        document.getElementById('featuredGrid').innerHTML = '<div class="card">Failed to load repositories. Please try again later.</div>';
      }
    }

    // Events
    document.getElementById('search').addEventListener('input', renderAll);
    document.getElementById('lang').addEventListener('change', renderAll);
    document.getElementById('sort').addEventListener('change', renderAll);

    init();
  </script>
</body>
</html>
