<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>DecodeLabs | Project 1 - Responsive Interface</title>
  <style>
    /* --------------------------------------------------
       1. VARIABLES & RESET (2025 Aesthetics & Palette)
       -------------------------------------------------- */
    :root {
      --color-mocha: #B93820;
      --color-ethereal: #FFC145;
      --color-moonlit: #DCEEFF;
      --color-dark: #15324B;
      --font-heading: 'Inter', system-ui, -apple-system, sans-serif;
      --font-body: 'Open Sans', system-ui, -apple-system, sans-serif;
    }

    * {
      box-sizing: border-box;
      margin: 0;
      padding: 0;
    }

    body {
      background-color: var(--color-moonlit);
      color: var(--color-dark);
      font-family: var(--font-body);
      line-height: 1.6;
      display: flex;
      flex-direction: column;
      min-height: 100vh;
    }

    /* --------------------------------------------------
       2. HEADER & NAVIGATION (Flexbox Micro-Component)
       -------------------------------------------------- */
    header {
      background-color: var(--color-moonlit);
      border-bottom: 1px solid rgba(165, 149, 111, 0.2);
      position: sticky;
      top: 0;
      z-index: 1000;
    }

    .nav-container {
      max-width: 1200px;
      margin: 0 auto;
      padding: 1rem 1.5rem;
      display: flex;
      justify-content: space-between;
      align-items: center;
    }

    .logo {
      font-family: var(--font-heading);
      font-weight: 700;
      font-size: 1.25rem;
      color: var(--color-dark);
      text-decoration: none;
    }

    .logo span {
      color: var(--color-mocha);
    }

    .nav-links {
      display: flex;
      gap: 1.5rem;
      list-style: none;
      align-items: center;
    }

    .nav-links a {
      text-decoration: none;
      color: var(--color-dark);
      font-weight: 5rem;
      font-family: var(--font-heading);
      font-size: 0.95rem;
      transition: color 0.2s ease;
    }

    .nav-links a:hover {
      color: var(--color-mocha);
    }

    .btn {
      background-color: var(--color-mocha);
      color: #ffffff;
      padding: 0.6rem 1.2rem;
      border: none;
      border-radius: 6px;
      font-family: var(--font-heading);
      font-weight: 600;
      cursor: pointer;
      text-decoration: none;
      display: inline-block;
      transition: opacity 0.2s ease;
    }

    .btn:hover {
      opacity: 0.9;
    }

    .btn-ethereal {
      background-color: var(--color-ethereal);
      color: var(--color-dark);
    }

    .menu-toggle {
      display: none;
      background: none;
      border: none;
      font-size: 1.5rem;
      cursor: pointer;
    }

    /* --------------------------------------------------
       3. HERO SECTION (Fluid Typography via clamp)
       -------------------------------------------------- */
    .hero {
      background-color: var(--color-moonlit);
      padding: 4rem 1.5rem;
      border-bottom: 1px solid rgba(165, 149, 111, 0.15);
    }

    .hero-container {
      max-width: 1200px;
      margin: 0 auto;
      display: flex;
      flex-direction: column;
      gap: 2rem;
      align-items: flex-start;
    }

    .hero-image {
      width: 100%;
      aspect-ratio: 16 / 9;
      object-fit: cover;
      border-radius: 8px;
    }

    .hero h1 {
      font-family: var(--font-heading);
      font-size: clamp(2rem, 5vw, 3.5rem);
      line-height: 1.15;
      color: var(--color-mocha);
      font-weight: 800;
      text-transform: uppercase;
      letter-spacing: -0.02em;
      max-width: 800px;
    }

    .hero p {
      font-size: clamp(1rem, 2vw, 1.2rem);
      max-width: 650px;
      color: #555550;
    }

    /* --------------------------------------------------
       4. MAIN MACRO LAYOUT (CSS Grid & Sidebar)
       -------------------------------------------------- */
    main {
      flex: 1;
      max-width: 1200px;
      width: 100%;
      margin: 2rem auto;
      padding: 0 1.5rem;
    }

    .layout-grid {
      display: grid;
      grid-template-columns: 1fr;
      gap: 2rem;
    }

    /* Step Cards Grid */
    .content-grid {
      display: grid;
      grid-template-columns: 1fr;
      gap: 1.5rem;
    }

    .card {
      background-color: #ffffff;
      border: 1px solid rgba(165, 149, 111, 0.3);
      border-radius: 8px;
      padding: 1.5rem;
      display: flex;
      flex-direction: column;
      gap: 0.75rem;
    }

    .card-image {
      width: 100%;
      aspect-ratio: 16 / 9;
      object-fit: cover;
      border-radius: 4px;
      margin-bottom: 0.25rem;
    }

    .card-step {
      display: inline-block;
      width: 28px;
      height: 28px;
      background-color: var(--color-mocha);
      color: #ffffff;
      font-family: var(--font-heading);
      font-weight: 700;
      border-radius: 4px;
      text-align: center;
      line-height: 28px;
      font-size: 0.85rem;
    }

    .card h3 {
      font-family: var(--font-heading);
      font-size: 1.15rem;
    }

    /* Side Panel */
    .side-panel {
      background-color: #ffffff;
      border: 1px solid rgba(165, 149, 111, 0.3);
      border-radius: 8px;
      padding: 1.5rem;
      height: fit-content;
    }

    .side-panel h3 {
      font-family: var(--font-heading);
      margin-bottom: 1rem;
      border-bottom: 2px solid var(--color-mocha);
      padding-bottom: 0.5rem;
    }

    .status-badge {
      display: inline-block;
      padding: 0.25rem 0.75rem;
      background-color: var(--color-moonlit);
      border-radius: 20px;
      font-size: 0.85rem;
      font-weight: 600;
      margin-top: 0.5rem;
    }

    /* --------------------------------------------------
       5. FOOTER CONTAINER
       -------------------------------------------------- */
    footer {
      background-color: var(--color-dark);
      color: var(--color-moonlit);
      padding: 2.5rem 1.5rem;
      margin-top: auto;
    }

    .footer-container {
      max-width: 1200px;
      margin: 0 auto;
      display: flex;
      flex-direction: column;
      gap: 1.5rem;
      justify-content: space-between;
      align-items: center;
      text-align: center;
    }

    .footer-container p {
      font-size: 0.9rem;
      opacity: 0.8;
    }

    /* 6. MEDIA QUERIES (Mobile-First Expansion)*/
    /* Tablet Breakpoint (768px) */
    @media (min-width: 768px) {
      .hero-container {
        display: grid;
        grid-template-columns: minmax(0, 1fr) minmax(280px, 0.85fr);
        align-items: center;
      }

      .content-grid {
        grid-template-columns: repeat(2, 1fr);
      }

      .footer-container {
        flex-direction: row;
        text-align: left;
      }
    }

    /* Desktop Breakpoint (1024px) */
    @media (min-width: 1024px) {
      .layout-grid {
        grid-template-columns: 2.5fr 1fr;
      }

      .menu-toggle {
        display: none;
      }
    }

    /* Mobile Nav Handling */
    @media (max-width: 767px) {
      .menu-toggle {
        display: block;
      }

      .nav-links {
        display: none;
        position: absolute;
        top: 100%;
        left: 0;
        right: 0;
        background-color: var(--color-moonlit);
        flex-direction: column;
        padding: 1.5rem;
        border-bottom: 1px solid rgba(165, 149, 111, 0.2);
        box-shadow: 0 4px 6px rgba(0,0,0,0.05);
      }

      .nav-links.active {
        display: flex;
      }
    }
  </style>
</head>
<body>

  <!-- SEMANTIC HEADER & NAV -->
  <header>
    <div class="nav-container">
      <a href="#" class="logo">Decode<span>Labs</span></a>
      <button class="menu-toggle" id="menuToggle" aria-label="Toggle Navigation">☰</button>
      <ul class="nav-links" id="navLinks">
        <li><a href="#discovery">Discovery</a></li>
        <li><a href="#semantics">Semantics</a></li>
        <li><a href="#grid">Grid & Flex</a></li>
        <li><a href="#" class="btn">Earn Your Badge</a></li>
      </ul>
    </div>
  </header>

  <!-- HERO SECTION -->
  <section class="hero">
    <div class="hero-container">
      <h1>Architecting the Future of the Mobile Web</h1>
      <p>Step into the role of a Full Stack Developer. Build flexible, accessible, and adaptive frontends using pure HTML, CSS, and basic JavaScript.</p>
      <a href="#roadmap" class="btn btn-ethereal">Get Started</a>
      <img class="hero-image" src="https://images.unsplash.com/photo-1498050108023-c5249f4df085?auto=format&fit=crop&w=1200&q=85" alt="Laptop and workspace set up for web development">
    </div>
  </section>

  <!-- MAIN CONTENT AREA -->
  <main id="roadmap">
    <div class="layout-grid">
      
      <!-- MAIN CONTENT GRID (CSS Grid) -->
      <section class="content-grid">
        
        <article class="card">
          <img class="card-image" src="https://images.unsplash.com/photo-1521737711867-e3b97375f902?auto=format&fit=crop&w=800&q=80" alt="Developers collaborating around a laptop">
          <span class="card-step">01</span>
          <h3>Research & Empathy Maps</h3>
          <p>Uncover user pain points through structured empathy research before writing a single line of code.</p>
        </article>

        <article class="card">
          <img class="card-image" src="https://images.unsplash.com/photo-1581291518857-4e27b48ff24e?auto=format&fit=crop&w=800&q=80" alt="Designer arranging interface sketches on a desk">
          <span class="card-step">02</span>
          <h3>Low-Fidelity Wireframing</h3>
          <p>Establish structural hierarchy in grayscale. If layout flow fails without color, styling won't fix it.</p>
        </article>

        <article class="card">
          <img class="card-image" src="https://images.unsplash.com/photo-1555949963-ff9fe0c870eb?auto=format&fit=crop&w=800&q=80" alt="Code displayed on a computer screen">
          <span class="card-step">03</span>
          <h3>Semantic HTML5</h3>
          <p>Utilize proper landmarks (&lt;header&gt;, &lt;main&gt;, &lt;footer&gt;) to guarantee screen reader and AI accessibility.</p>
        </article>

        <article class="card">
          <img class="card-image" src="https://images.unsplash.com/photo-1512941937669-90a1b58e7e9c?auto=format&fit=crop&w=800&q=80" alt="Smartphone showing a mobile app interface">
          <span class="card-step">04</span>
          <h3>Mobile-First Layouts</h3>
          <p>Design single-column micro-components with Flexbox and macro-page structures with 2D CSS Grid.</p>
        </article>

        <article class="card">
          <img class="card-image" src="https://images.unsplash.com/photo-1555066931-4365d14bab8c?auto=format&fit=crop&w=800&q=80" alt="Developer typing code on a laptop">
          <span class="card-step">05</span>
          <h3>JavaScript State</h3>
          <p>Implement clean, lightweight state management for interactive UI components and toggles.</p>
        </article>

        <article class="card">
          <img class="card-image" src="https://images.unsplash.com/photo-1454165804606-c3d57bc86b40?auto=format&fit=crop&w=800&q=80" alt="Team reviewing project metrics and documents">
          <span class="card-step">06</span>
          <h3>Audit & Compliance</h3>
          <p>Measure Core Web Vitals (LCP/CLS) and enforce strict WCAG accessibility compliance.</p>
        </article>

      </section>

      <!-- SIDE PANEL (Flexbox & Semantic Aside) -->
      <aside class="side-panel">
        <h3>Project Stats</h3>
        <p><strong>Batch:</strong> 2026</p>
        <p><strong>Track:</strong> Industrial Training</p>
        <p><strong>Status:</strong> <span class="status-badge" id="statusBadge">Phase 1: Active</span></p>
        <br>
        <button class="btn" style="width: 100%; text-align: center;" onclick="toggleStatus()">Toggle Progress</button>
      </aside>

    </div>
  </main>

  <!-- SEMANTIC FOOTER -->
  <footer>
    <div class="footer-container">
      <p>DecodeLabs &copy; 2026 | Build the Future</p>
      <p>Project 1: The Responsive Architecture</p>
    </div>
  </footer>

  <!-- JAVASCRIPT FOR LOGIC & INTERACTIVITY -->
  <script>
    // Mobile Navigation Toggle
    const menuToggle = document.getElementById('menuToggle');
    const navLinks = document.getElementById('navLinks');

    menuToggle.addEventListener('click', () => {
      navLinks.classList.toggle('active');
    });

    // Basic State Management Demo
    function toggleStatus() {
      const badge = document.getElementById('statusBadge');
      if (badge.innerText === 'Phase 1: Active') {
        badge.innerText = 'Phase 1: Completed';
        badge.style.backgroundColor = 'var(--color-ethereal)';
      } else {
        badge.innerText = 'Phase 1: Active';
        badge.style.backgroundColor = 'var(--color-moonlit)';
      }
    }
  </script>

</body>
</html>
