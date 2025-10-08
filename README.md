<!doctype html>
<html lang="en" data-theme="auto">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <meta name="color-scheme" content="light dark" />
  <meta name="theme-color" content="#0ea5e9" />
  <title>Your Name – Portfolio</title>
  <meta name="description" content="Personal portfolio of Your Name: projects, skills, and contact information." />
  <!--
  ==========================================================
  PERSONAL PORTFOLIO – SINGLE FILE (HTML + CSS + JS)
  ==========================================================
  ▶ What this is
    A clean, responsive portfolio you can deploy as-is. No libraries.

  ▶ Step-by-step (Quick Start)
    1) Save this file as index.html.
    2) Open it in your browser to preview.
    3) Replace placeholder text (Your Name, role, bio).
    4) Add your projects inside the #projects section (cards).
    5) Update skills in #skills (labels + level %).
    6) Change the email in the contact form handler (look for TODO in JS).
    7) Replace resume link (href="#") with your PDF file.
    8) Deploy: upload index.html to hosting, or use GitHub Pages / Netlify / Vercel.

  ▶ Customize theme/colors
    - Edit CSS variables under :root and [data-theme="dark"].
    - Use the Moon/Sun button to toggle theme (saved in localStorage).

  ▶ Structure overview
    <header>   sticky nav + theme + mobile menu
    <main>
      <section id="hero">    intro/CTA
      <section id="about">   bio
      <section id="projects">cards grid
      <section id="skills">  bars grid
      <section id="contact"> form (front-end only)
    <footer>   socials + copyright

  ▶ Notes
    - Form uses basic client-side validation only (no backend). Connect to email/API later.
    - Images are CSS gradients (no external files). Replace with your own if you want.
    - IntersectionObserver powers subtle reveal animations.
  -->
  <style>
    /* =====================
       DESIGN TOKENS (THEME)
       ===================== */
    :root {
      --bg: #0b1220;
      --bg-soft: #0f172a;
      --text: #e5e7eb;
      --muted: #94a3b8;
      --primary: #0ea5e9;
      --primary-strong: #0284c7;
      --card: #111827;
      --card-border: #233044;
      --accent: #22c55e;
      --danger: #ef4444;
      --shadow: 0 10px 30px rgba(2,8,23,.3);
      --radius: 16px;
      --radius-lg: 24px;
      --container: 1100px;
    }

    html[data-theme="light"] {
      --bg: #f7fafc;
      --bg-soft: #f1f5f9;
      --text: #0f172a;
      --muted: #475569;
      --primary: #0284c7;
      --primary-strong: #0369a1;
      --card: #ffffff;
      --card-border: #e2e8f0;
      --accent: #16a34a;
      --danger: #dc2626;
      --shadow: 0 10px 24px rgba(2,8,23,.08);
    }

    /* Base */
    * { box-sizing: border-box; }
    html { scroll-behavior: smooth; }
    body {
      margin: 0;
      font: 16px/1.6 system-ui, -apple-system, Segoe UI, Roboto, "Helvetica Neue", Arial, "Noto Sans", "Liberation Sans", sans-serif;
      background: radial-gradient(1200px 800px at 80% -10%, rgba(14,165,233,.15), transparent 60%), var(--bg);
      color: var(--text);
    }
    a { color: inherit; text-decoration: none; }
    img { max-width: 100%; display: block; }

    .container { width: min(100% - 32px, var(--container)); margin-inline: auto; }
    .tag { display:inline-block; padding:.25rem .6rem; border:1px solid var(--card-border); border-radius:999px; color:var(--muted); font-size:.8rem; }

    /* Header / Nav */
    header {
      position: sticky; top: 0; z-index: 50;
      backdrop-filter: saturate(140%) blur(10px);
      background: color-mix(in srgb, var(--bg), transparent 20%);
      border-bottom: 1px solid var(--card-border);
    }
    .nav { display:flex; align-items:center; justify-content:space-between; padding: .8rem 0; }
    .brand { font-weight: 800; letter-spacing: .3px; }
    .brand small { color: var(--muted); font-weight: 500; }
    .links { display:flex; gap:1rem; align-items:center; }
    .links a { padding:.5rem .8rem; border-radius:10px; border:1px solid transparent; }
    .links a:hover { border-color: var(--card-border); }
    .btn, button.btn { padding:.6rem .95rem; border-radius: 10px; border:1px solid var(--card-border); background: var(--card); color:var(--text); cursor:pointer; }
    .btn.primary { background: linear-gradient(180deg, var(--primary), var(--primary-strong)); border: 0; color: white; box-shadow: var(--shadow); }
    .btn.ghost { background: transparent; }

    /* Mobile menu */
    .menu-toggle { display:none; }
    @media (max-width: 768px) {
      .links { display:none; }
      .menu-toggle { display:block; }
      nav[data-open="true"] .links-mobile { display:block; }
    }
    .links-mobile { display:none; border-top:1px solid var(--card-border); padding:.5rem 0 .8rem; }
    .links-mobile a { display:block; padding:.6rem; border-radius:10px; }
    .links-mobile a:hover { background: color-mix(in srgb, var(--card), transparent 60%); }

    /* Hero */
    #hero { padding: 6rem 0 4rem; position: relative; }
    #hero .content { display:grid; grid-template-columns: 1.1fr .9fr; gap: 2rem; align-items: center; }
    #hero h1 { font-size: clamp(2rem, 3.4vw + .5rem, 3.2rem); line-height:1.15; margin:0 0 .6rem; }
    #hero p.big { color: var(--muted); font-size: 1.1rem; margin: 0 0 1.2rem; }
    .cta { display:flex; gap:.8rem; flex-wrap: wrap; }

    /* Hero visual placeholder */
    .visual { aspect-ratio: 4 / 3; border-radius: var(--radius-lg); overflow:hidden; border:1px solid var(--card-border);
      background: conic-gradient(from 160deg at 60% 40%, rgba(14,165,233,.45), transparent 35%),
                  radial-gradient(600px 400px at 10% 100%, rgba(34,197,94,.20), transparent 60%),
                  linear-gradient(135deg, color-mix(in srgb, var(--card), transparent 0%), color-mix(in srgb, var(--bg-soft), transparent 0%));
      box-shadow: var(--shadow);
      display:grid; place-items:center; color: #fff6; font-weight:600; letter-spacing:.3px;
    }

    /* Cards & Sections */
    section { padding: 4rem 0; }
    .section-head { display:flex; align-items:end; justify-content:space-between; margin-bottom:1.6rem; gap:1rem; }
    .section-head h2 { margin:0; font-size: clamp(1.4rem, 2.2vw + .4rem, 2.2rem); }
    .card {
      background: var(--card); border:1px solid var(--card-border); border-radius: var(--radius);
      padding: 1rem; box-shadow: var(--shadow);
    }

    /* Projects */
    .grid { display:grid; gap: 1rem; }
    .projects { grid-template-columns: repeat(3, 1fr); }
    @media (max-width: 992px) { .projects { grid-template-columns: repeat(2, 1fr); } }
    @media (max-width: 640px) { .projects { grid-template-columns: 1fr; } }
    .project-thumb { aspect-ratio: 16/10; border-radius:12px; overflow:hidden; border:1px solid var(--card-border); background:
        radial-gradient(400px 280px at 10% 10%, rgba(14,165,233,.25), transparent 40%),
        radial-gradient(300px 240px at 90% 90%, rgba(34,197,94,.2), transparent 50%),
        linear-gradient(145deg, color-mix(in srgb, var(--bg-soft), white 6%), var(--card));
    }
    .project h3 { margin:.8rem 0 .2rem; }
    .project p { color: var(--muted); margin:.2rem 0 .6rem; font-size:.95rem; }
    .project .meta { display:flex; gap:.5rem; flex-wrap:wrap; }

    /* Skills */
    .skills { grid-template-columns: repeat(2, 1fr); }
    @media (max-width: 640px) { .skills { grid-template-columns: 1fr; } }
    .skill { display:grid; gap:.4rem; }
    .bar { height: 10px; background: color-mix(in srgb, var(--card), white 8%); border:1px solid var(--card-border); border-radius: 999px; overflow:hidden; }
    .bar > i { display:block; height:100%; width: var(--w, 50%); background: linear-gradient(180deg, var(--primary), var(--primary-strong)); }

    /* Contact */
    form { display:grid; gap:.9rem; }
    input, textarea { width:100%; padding:.8rem .9rem; border-radius:10px; color:var(--text);
      background: var(--card); border:1px solid var(--card-border); }
    textarea { min-height: 140px; resize: vertical; }
    .field { display:grid; gap:.35rem; }
    .error { color: var(--danger); font-size:.9rem; display:none; }
    .success { color: var(--accent); }

    /* Footer */
    footer { border-top:1px solid var(--card-border); padding:2rem 0; color: var(--muted); }
    .socials { display:flex; gap:.8rem; flex-wrap: wrap; }

    /* Animations */
    .reveal { opacity: 0; transform: translateY(16px); transition: opacity .6s ease, transform .6s ease; }
    .reveal.in-view { opacity: 1; transform: none; }

    .sr-only { position:absolute; width:1px; height:1px; padding:0; margin:-1px; overflow:hidden; clip:rect(0,0,0,0); white-space:nowrap; border:0; }

    @media (max-width: 900px) {
      #hero .content { grid-template-columns: 1fr; }
    }

    @media (prefers-reduced-motion: reduce) {
      html { scroll-behavior: auto; }
      .reveal { opacity: 1 !important; transform: none !important; transition: none !important; }
    }

    :root {
  --bg: #1e1a17;
  --bg-soft: #282421;
  --text: #e8e3dc;
  --muted: #a69c92;
  --primary: #c98a5e;
  --primary-strong: #a86c47;
  --card: #2e2a27;
  --card-border: #443e38;
  --accent: #d8a83f;
  --danger: #d46a6a;
  --shadow: 0 10px 30px rgba(0,0,0,.3);
  --radius: 16px;
  --radius-lg: 24px;
  --container: 1100px;
}

  </style>
</head>
<body>
  <header>
    <nav class="container nav" aria-label="Primary">
      <div class="brand"><span aria-hidden>🧑🏻‍💻</span> Tean Chorn <small>• Web Developer</small></div>
      <div class="links" role="menubar">
        <a role="menuitem" href="#projects">Projects</a>
        <a role="menuitem" href="#skills">Skills</a>
        <a role="menuitem" href="#about">About</a>
        <a role="menuitem" href="#contact" class="btn">Contact</a>
        <button id="themeToggle" class="btn ghost" aria-label="Toggle color theme">🌙</button>
      </div>
      <button class="menu-toggle btn" aria-expanded="false" aria-controls="mobileMenu" id="menuBtn">☰</button>
    </nav>
    <div id="mobileMenu" class="container links-mobile" hidden>
      <a href="#projects">Projects</a>
      <a href="#skills">Skills</a>
      <a href="#about">About</a>
      <a href="#contact">Contact</a>
      <button id="themeToggleM" class="btn ghost" style="margin:.4rem 0 0;">🌙 Theme</button>
    </div>
  </header>

  <main>
    <!-- Hero -->
    <section id="hero" class="container">
      <div class="content">
        <div>
          <span class="tag">Open to Work</span>
          <h1 class="reveal">Hi, I'm <strong>Tean Chorn</strong> — I build clean, fast, accessible websites.</h1>
          <p class="big reveal" style="transition-delay:.08s">Frontend-focused developer with a love for minimal UI, performance, and great UX. Based in <em>Cambodia</em>. Available for freelance & full‑time roles.</p>
          <div class="cta reveal" style="transition-delay:.12s">
            <a href="#projects" class="btn primary">View Projects</a>
            <a href="#contact" class="btn">Contact Me</a>
            <a href="#" class="btn ghost" download>Download Résumé</a>
          </div>
        </div>
        <figure class="visual reveal" style="transition-delay:.16s" aria-label="Decorative cover">
          <figcaption class="sr-only">Abstract colorful gradient placeholder. Replace with your photo or a graphic if desired.</figcaption>
          <span><img src="/Imge/photo.jpg" alt=""></span>
        </figure>
      </div>

      <details class="card" style="margin-top:1.5rem">
        <summary><strong>How to use this template (Step by Step)</strong></summary>
        <ol>
          <li>Rename the title and text to your info.</li>
          <li>Add your projects below (title, description, tech tags, links).</li>
          <li>Adjust skills with your percentages.</li>
          <li>Set your email in the form handler (JS). <em>(front‑end demo only)</em></li>
          <li>Replace the resume link with a PDF.</li>
          <li>Deploy: host this <code>index.html</code> anywhere (GitHub Pages, Netlify, etc.).</li>
        </ol>
      </details>
    </section>

    <!-- Projects -->
    <section id="projects">
      <div class="container">
        <div class="section-head">
          <h2>Featured Projects</h2>
          <span class="tag">3 selected</span>
        </div>
        <div class="grid projects">
          <!-- Project 1 -->
          <article class="card project reveal">
            <div class="project-thumb"><img src="/Imge/photo.jpg" alt=""></div>
            <h3>ShopSmart – E‑commerce UI</h3>
            <p>Responsive storefront with product filtering, cart, and checkout flow. Focus on accessibility and performance.</p>
            <div class="meta">
              <span class="tag">HTML</span>
              <span class="tag">CSS Grid</span>
              <span class="tag">JavaScript</span>
            </div>
            <div style="margin-top:.8rem; display:flex; gap:.6rem; flex-wrap:wrap;">
              <a class="btn" href="#" target="_blank" rel="noopener">Live</a>
              <a class="btn ghost" href="#" target="_blank" rel="noopener">Code</a>
            </div>
          </article>

          <!-- Project 2 -->
          <article class="card project reveal" style="transition-delay:.06s">
            <div class="project-thumb"><img src="/Imge/photo.jpg" alt=""></div>
            <h3>DevNotes – Markdown Blog</h3>
            <p>Lightweight blog with client‑side search and tag filters. Instant nav and offline cache.</p>
            <div class="meta">
              <span class="tag">PWA</span>
              <span class="tag">Vanilla JS</span>
              <span class="tag">Service Worker</span>
            </div>
            <div style="margin-top:.8rem; display:flex; gap:.6rem; flex-wrap:wrap;">
              <a class="btn" href="#" target="_blank" rel="noopener">Live</a>
              <a class="btn ghost" href="#" target="_blank" rel="noopener">Code</a>
            </div>
          </article>

          <!-- Project 3 -->
          <article class="card project reveal" style="transition-delay:.12s">
            <div class="project-thumb"><img src="/Imge/photo.jpg" alt=""></div>
            <h3>Snapfolio – Photo Gallery</h3>
            <p>Masonry layout with lazy‑loaded images and keyboard navigation. Smooth and accessible.</p>
            <div class="meta">
              <span class="tag">Flexbox</span>
              <span class="tag">ARIA</span>
              <span class="tag">Lazy Load</span>
            </div>
            <div style="margin-top:.8rem; display:flex; gap:.6rem; flex-wrap:wrap;">
              <a class="btn" href="#" target="_blank" rel="noopener">Live</a>
              <a class="btn ghost" href="#" target="_blank" rel="noopener">Code</a>
            </div>
          </article>
        </div>
      </div>
    </section>

    <!-- Skills -->
    <section id="skills">
      <div class="container">
        <div class="section-head">
          <h2>Skills</h2>
          <span class="tag">Core stack</span>
        </div>
        <div class="grid skills">
          <div class="card skill reveal">
            <div style="display:flex; justify-content:space-between;">
              <strong>HTML</strong><span class="muted">90%</span>
            </div>
            <div class="bar"><i style="--w:90%"></i></div>
          </div>
          <div class="card skill reveal" style="transition-delay:.04s">
            <div style="display:flex; justify-content:space-between;">
              <strong>CSS</strong><span class="muted">85%</span>
            </div>
            <div class="bar"><i style="--w:85%"></i></div>
          </div>
          <div class="card skill reveal" style="transition-delay:.08s">
            <div style="display:flex; justify-content:space-between;">
              <strong>JavaScript</strong><span class="muted">80%</span>
            </div>
            <div class="bar"><i style="--w:80%"></i></div>
          </div>
          <div class="card skill reveal" style="transition-delay:.12s">
            <div style="display:flex; justify-content:space-between;">
              <strong>Accessibility (a11y)</strong><span class="muted">75%</span>
            </div>
            <div class="bar"><i style="--w:75%"></i></div>
          </div>
          <div class="card skill reveal" style="transition-delay:.12s">
            <div style="display:flex; justify-content:space-between;">
              <strong>JAVA</strong><span class="muted">50%</span>
            </div>
            <div class="bar"><i style="--w:50%"></i></div>
          </div>
          <div class="card skill reveal" style="transition-delay:.12s">
            <div style="display:flex; justify-content:space-between;">
              <strong>Databas</strong><span class="muted">70%</span>
            </div>
            <div class="bar"><i style="--w:70%"></i></div>
          </div>
        </div>
      </div>
    </section>

    <!-- About -->
    <section id="about">
      <div class="container">
        <div class="section-head">
          <h2>About</h2>
          <a class="tag" href="#contact">Hire me</a>
        </div>
        <div class="grid" style="grid-template-columns: 1.2fr .8fr; gap:1.2rem;">
          <div class="card reveal">
            <p>Hello! I'm <strong>Chorn</strong>, a frontend‑leaning web developer. I enjoy turning complex problems into simple, beautiful interfaces. When I'm not coding, I explore design systems and performance audits.</p>
            <p>I'm currently looking for roles where I can make an impact on user experience, accessibility, and component architecture.</p>
            <ul>
              <li>💼 Available for Freelance & Full‑time</li>
              <li>📍 Based in Your City (Remote‑friendly)</li>
              <li>🗂️ Résumé: <a href="#" class="tag">Download PDF</a></li>
            </ul>
          </div>
          <div class="card reveal" style="transition-delay:.06s">
            <h3 style="margin-top:0">Quick Facts</h3>
            <ul style="margin-top:.6rem; padding-left:1.1rem; line-height:1.9">
              <li>Built 10+ mini‑projects in JS</li>
              <li>Comfortable with Git/GitHub</li>
              <li>Loves clean semantics & a11y</li>
              <li>Learning: TypeScript, Node.js</li>
            </ul>
          </div>
        </div>
      </div>
    </section>

    <!-- Contact -->
    <section id="contact">
      <div class="container">
        <div class="section-head">
          <h2>Contact</h2>
          <span class="tag">Let's build something</span>
        </div>
        <div class="grid" style="grid-template-columns: 1fr 1fr; gap:1.2rem;">
          <form id="contactForm" class="card reveal" novalidate>
            <div class="field">
              <label for="name">Name</label>
              <input id="name" name="name" type="text" placeholder="Your name" required />
              <small class="error" id="err-name">Please enter your name.</small>
            </div>
            <div class="field">
              <label for="email">Email</label>
              <input id="email" name="email" type="email" placeholder="you@example.com" required />
              <small class="error" id="err-email">Please enter a valid email.</small>
            </div>
            <div class="field">
              <label for="message">Message</label>
              <textarea id="message" name="message" placeholder="What can we build together?" required></textarea>
              <small class="error" id="err-message">Please write a short message.</small>
            </div>
            <div style="display:flex; gap:.6rem; align-items:center;">
              <button type="submit" class="btn primary">Send Message</button>
              <span id="formStatus" aria-live="polite" class="success" hidden>Thanks! I'll reply soon.</span>
            </div>
          </form>
          <div class="card reveal" style="transition-delay:.06s">
            <h3 style="margin-top:0">Find me</h3>
            <p>Feel free to reach out via the form, or directly on these platforms:</p>
            <div class="socials" style="margin-top:.6rem">
              <a class="btn" href="#" target="_blank" rel="noopener">GitHub</a>
              <a class="btn" href="#" target="_blank" rel="noopener">LinkedIn</a>
              <a class="btn" href="#" target="_blank" rel="noopener">Twitter/X</a>
              <a class="btn ghost" href="mailto:your.email@example.com">Email</a>
            </div>
          </div>
        </div>
      </div>
    </section>
  </main>

  <footer>
    <div class="container" style="display:flex; justify-content:space-between; align-items:center; gap:1rem; flex-wrap:wrap;">
      <div>© <span id="year"></span> Tean Chorn. All rights reserved.</div>
      <div style="display:flex; gap:.5rem;">
        <a class="tag" href="#hero">Back to top ↑</a>
      </div>
    </div>
  </footer>

  <script>
    // ==========================
    //  THEME TOGGLE (localStorage)
    // ==========================
    const applyTheme = (t) => {
      if (t === 'auto') {
        document.documentElement.setAttribute('data-theme',
          matchMedia('(prefers-color-scheme: light)').matches ? 'light' : 'dark');
      } else {
        document.documentElement.setAttribute('data-theme', t);
      }
    }
    const getSavedTheme = () => localStorage.getItem('theme') || 'auto';
    const setSavedTheme = (t) => localStorage.setItem('theme', t);
    const cycleTheme = () => {
      const current = getSavedTheme();
      const next = current === 'auto' ? 'light' : current === 'light' ? 'dark' : 'auto';
      setSavedTheme(next); applyTheme(next); updateThemeButtons();
    }
    const updateThemeButtons = () => {
      const t = getSavedTheme();
      const label = t === 'auto' ? '🌗' : t === 'light' ? '🌞' : '🌙';
      document.getElementById('themeToggle').textContent = label;
      const m = document.getElementById('themeToggleM'); if (m) m.textContent = label + ' Theme';
    }
    document.getElementById('themeToggle').addEventListener('click', cycleTheme);
    document.getElementById('themeToggleM').addEventListener('click', cycleTheme);
    applyTheme(getSavedTheme()); updateThemeButtons();

    // Keep in sync with system when on 'auto'
    matchMedia('(prefers-color-scheme: light)').addEventListener('change', () => {
      if (getSavedTheme() === 'auto') applyTheme('auto');
    });

    // ==========================
    //  MOBILE MENU
    // ==========================
    const menuBtn = document.getElementById('menuBtn');
    const mobileMenu = document.getElementById('mobileMenu');
    const topNav = document.querySelector('header nav');
    menuBtn.addEventListener('click', () => {
      const open = menuBtn.getAttribute('aria-expanded') === 'true';
      menuBtn.setAttribute('aria-expanded', String(!open));
      topNav.setAttribute('data-open', String(!open));
      mobileMenu.hidden = open; // toggle
    });

    // Close on link click (mobile)
    mobileMenu.addEventListener('click', (e) => {
      if (e.target.tagName === 'A') { menuBtn.click(); }
    });

    // ==========================
    //  REVEAL ON SCROLL
    // ==========================
    const io = new IntersectionObserver((entries) => {
      for (const ent of entries) if (ent.isIntersecting) ent.target.classList.add('in-view');
    }, { threshold: 0.15 });
    document.querySelectorAll('.reveal').forEach(el => io.observe(el));

    // ==========================
    //  CONTACT FORM (FRONT-END ONLY)
    // ==========================
    const form = document.getElementById('contactForm');
    const statusEl = document.getElementById('formStatus');
    const show = (el) => el.style.display = 'block';
    const hide = (el) => el.style.display = 'none';

    form.addEventListener('submit', async (e) => {
      e.preventDefault();
      const name = form.name.value.trim();
      const email = form.email.value.trim();
      const message = form.message.value.trim();

      // Reset errors
      hide(document.getElementById('err-name'));
      hide(document.getElementById('err-email'));
      hide(document.getElementById('err-message'));

      let ok = true;
      if (!name) { show(document.getElementById('err-name')); ok = false; }
      if (!/.+@.+\..+/.test(email)) { show(document.getElementById('err-email')); ok = false; }
      if (message.length < 10) { show(document.getElementById('err-message')); ok = false; }
      if (!ok) return;

      // Demo submit: open mailto OR simulate success
      // TODO: Replace with your real endpoint or email service
      const mailto = `mailto:your.email@example.com?subject=Portfolio%20Inquiry%20from%20${encodeURIComponent(name)}&body=${encodeURIComponent(message + '\n\nFrom: ' + name + ' <' + email + '>')}`;
      window.open(mailto, '_blank');

      statusEl.hidden = false;
      form.reset();
    });

    // ==========================
    //  MISC
    // ==========================
    document.getElementById('year').textContent = new Date().getFullYear();
  </script>
</body>
</html>
