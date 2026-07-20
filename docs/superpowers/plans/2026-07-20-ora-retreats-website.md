# ora-retreats.com Website Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Build a static, single-page marketing site for ora-retreats.com (plus a separate moodboard page) matching the approved design spec, deployable as-is to easyhost.be shared hosting.

**Architecture:** Plain HTML/CSS/JS, no build step, no framework. One `index.html` (hero, retreat, about, contact sections via anchor nav) and one `moodboard.html` (photo mosaic), sharing `css/style.css` and `js/script.js`. Fonts via Google Fonts CDN. Images are stable placeholder photos downloaded from picsum.photos (seeded, so URLs are deterministic and reproducible).

**Tech Stack:** HTML5, CSS3 (flexbox/grid, no preprocessor), vanilla JS (no libraries), Google Fonts (Cormorant Garamond, Poppins, Jost).

## Global Constraints

- Spec source: `docs/superpowers/specs/2026-07-20-ora-retreats-website-design.md` — every task below implements a section of it.
- Colors: background `#E8E8E3`, text `#393939`, accent `#7a7268`, card background `#F4F4F1`. Use these exact hex values everywhere — no other colors.
- Fonts: logo = `'Cormorant Garamond', serif`; section titles/nav = `'Poppins', sans-serif`; body copy = `'Jost', sans-serif`.
- No backend, no build tooling, no npm dependencies. Everything must run by opening the HTML file directly or serving it as static files.
- "Join the waitlist" and Contact both use `mailto:hello@ora-retreats.com` — no form submission JS.
- Mobile-first responsive: nav collapses below 768px, all multi-column sections stack to one column.
- All images use descriptive filenames (`hero.jpg`, `retreat-program.jpg`, `about-portrait.jpg`, `moodboard-01.jpg`...`moodboard-08.jpg`) and `alt` text, so real photos can later replace them as a straight file swap.

---

### Task 1: Project scaffold

**Files:**
- Create: `index.html`
- Create: `moodboard.html`
- Create: `css/style.css`
- Create: `js/script.js`
- Create: `images/.gitkeep`

**Interfaces:**
- Produces: the CSS custom properties (`--color-bg`, `--color-text`, `--color-accent`, `--color-card`, `--font-logo`, `--font-heading`, `--font-body`) that every later CSS task relies on.
- Produces: base HTML documents that later tasks insert `<section>` markup into (index.html has an empty `<body>` with `<header>` and `<footer>` shells; moodboard.html has an empty `<body>` with a minimal header shell).

- [ ] **Step 1: Create the folder structure**

```bash
mkdir -p css js images
touch images/.gitkeep
```

- [ ] **Step 2: Write `css/style.css` reset and variables**

```css
/* ---- Reset ---- */
*, *::before, *::after {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}

html {
  scroll-behavior: smooth;
}

body {
  min-height: 100vh;
}

img {
  max-width: 100%;
  display: block;
}

a {
  color: inherit;
  text-decoration: none;
}

ul {
  list-style: none;
}

/* ---- Design tokens ---- */
:root {
  --color-bg: #E8E8E3;
  --color-text: #393939;
  --color-accent: #7a7268;
  --color-card: #F4F4F1;

  --font-logo: 'Cormorant Garamond', serif;
  --font-heading: 'Poppins', sans-serif;
  --font-body: 'Jost', sans-serif;

  --max-width: 1100px;
  --section-padding: 6rem 1.5rem;
}

body {
  background: var(--color-bg);
  color: var(--color-text);
  font-family: var(--font-body);
  line-height: 1.7;
  font-size: 1rem;
}

.container {
  max-width: var(--max-width);
  margin: 0 auto;
  padding: 0 1.5rem;
}

.eyebrow {
  font-family: var(--font-heading);
  text-transform: uppercase;
  letter-spacing: 0.2em;
  font-size: 0.75rem;
  color: var(--color-accent);
  display: block;
  margin-bottom: 1rem;
  text-align: center;
}

.section-title {
  font-family: var(--font-heading);
  text-transform: lowercase;
  letter-spacing: 0.05em;
  font-size: 1.75rem;
  font-weight: 500;
  text-align: center;
  margin-bottom: 2rem;
}

hr.divider {
  border: none;
  border-top: 1px solid var(--color-accent);
  opacity: 0.4;
  max-width: 120px;
  margin: 0 auto;
}

.btn {
  display: inline-block;
  font-family: var(--font-heading);
  text-transform: uppercase;
  letter-spacing: 0.1em;
  font-size: 0.75rem;
  padding: 0.9rem 2rem;
  border: 1px solid var(--color-text);
  border-radius: 999px;
  background: transparent;
  color: var(--color-text);
  transition: background 0.2s ease, color 0.2s ease;
}

.btn:hover {
  background: var(--color-text);
  color: var(--color-bg);
}

.btn-row {
  display: flex;
  gap: 1rem;
  justify-content: center;
  flex-wrap: wrap;
  margin-top: 2rem;
}
```

- [ ] **Step 3: Write `index.html` document shell**

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>ora — soulful retreats for women</title>
  <meta name="description" content="Empowering women to reconnect with their body, mind and soul through intentional movement and sacred spaces.">
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
  <link href="https://fonts.googleapis.com/css2?family=Cormorant+Garamond:wght@400;500;600&family=Poppins:wght@400;500&family=Jost:wght@300;400;500&display=swap" rel="stylesheet">
  <link rel="stylesheet" href="css/style.css">
</head>
<body>
  <header class="site-header">
    <!-- Task 3 fills this in -->
  </header>

  <main>
    <!-- Task 3: hero + intro -->
    <!-- Task 4: retreat section -->
    <!-- Task 5: about section -->
    <!-- Task 6: contact section -->
  </main>

  <footer class="site-footer">
    <!-- Task 6 fills this in -->
  </footer>

  <script src="js/script.js"></script>
</body>
</html>
```

- [ ] **Step 4: Write `moodboard.html` document shell**

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>ora — moodboard</title>
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
  <link href="https://fonts.googleapis.com/css2?family=Cormorant+Garamond:wght@400;500;600&family=Poppins:wght@400;500&family=Jost:wght@300;400;500&display=swap" rel="stylesheet">
  <link rel="stylesheet" href="css/style.css">
</head>
<body>
  <header class="moodboard-header">
    <a href="index.html" class="logo">ora</a>
  </header>

  <main>
    <!-- Task 7 fills this in -->
  </main>

  <footer class="site-footer">
    <!-- Task 6/7 fills this in -->
  </footer>
</body>
</html>
```

- [ ] **Step 5: Create empty `js/script.js` stub**

```js
// Interactivity added in Task 8
```

- [ ] **Step 6: Verify it loads with no console errors**

Run: open `index.html` directly in a browser (double-click or `start index.html` on Windows).
Expected: blank greige page (`#E8E8E3` background), no console errors, "ora — soulful retreats for women" in the browser tab title.

- [ ] **Step 7: Commit**

```bash
git add index.html moodboard.html css/style.css js/script.js images/.gitkeep
git commit -m "Scaffold static site structure with design tokens"
```

---

### Task 2: Placeholder images

**Files:**
- Create: `images/hero.jpg`
- Create: `images/retreat-program.jpg`
- Create: `images/about-portrait.jpg`
- Create: `images/moodboard-01.jpg` through `images/moodboard-08.jpg`

**Interfaces:**
- Produces: image files at fixed paths that Tasks 3, 4, 5, and 7 reference directly in `<img src="images/...">` tags.

- [ ] **Step 1: Download placeholder images from picsum.photos (seeded for reproducibility)**

```bash
curl -sL -o images/hero.jpg "https://picsum.photos/seed/ora-hero/1600/1000"
curl -sL -o images/retreat-program.jpg "https://picsum.photos/seed/ora-program/1000/1300"
curl -sL -o images/about-portrait.jpg "https://picsum.photos/seed/ora-portrait/800/1000"
curl -sL -o images/moodboard-01.jpg "https://picsum.photos/seed/ora-mood-01/800/800"
curl -sL -o images/moodboard-02.jpg "https://picsum.photos/seed/ora-mood-02/800/1000"
curl -sL -o images/moodboard-03.jpg "https://picsum.photos/seed/ora-mood-03/800/600"
curl -sL -o images/moodboard-04.jpg "https://picsum.photos/seed/ora-mood-04/800/1000"
curl -sL -o images/moodboard-05.jpg "https://picsum.photos/seed/ora-mood-05/800/800"
curl -sL -o images/moodboard-06.jpg "https://picsum.photos/seed/ora-mood-06/800/600"
curl -sL -o images/moodboard-07.jpg "https://picsum.photos/seed/ora-mood-07/800/1000"
curl -sL -o images/moodboard-08.jpg "https://picsum.photos/seed/ora-mood-08/800/800"
```

- [ ] **Step 2: Verify all files downloaded and are non-empty**

Run: `ls -la images/*.jpg | awk '{print $5, $9}'`
Expected: 11 lines listed, each with a file size greater than 1000 bytes (no zero-byte or missing files).

- [ ] **Step 3: Commit**

```bash
git add images/*.jpg
git commit -m "Add placeholder stock photos (picsum, seeded — swap with real assets later)"
```

---

### Task 3: Nav + Hero section

**Files:**
- Modify: `index.html` (`<header>` and first part of `<main>`)
- Modify: `css/style.css` (append nav + hero styles)

**Interfaces:**
- Consumes: `.container`, `.btn`, `.btn-row`, `--font-logo`, `--font-heading` from Task 1.
- Produces: `.site-header`, `.nav-links`, `#hero`, `.hero-overlay` CSS classes and the `#retreat`/`#about`/`#contact` anchor targets that Tasks 4–6 must use as their `<section id="...">` values.

- [ ] **Step 1: Replace the `<header>` block in `index.html`**

```html
<header class="site-header">
  <div class="container header-inner">
    <a href="#" class="logo">ora</a>
    <nav class="nav-links">
      <a href="#retreat">Retreat</a>
      <a href="#about">About</a>
      <a href="#contact">Contact</a>
      <a href="mailto:hello@ora-retreats.com" class="btn btn-small">Join the waitlist</a>
    </nav>
  </div>
</header>
```

- [ ] **Step 2: Add the hero + intro markup inside `<main>` (before the other section comments)**

```html
<section id="hero" class="hero">
  <img src="images/hero.jpg" alt="Woman practicing yoga on the beach at sunrise" class="hero-photo">
  <div class="hero-overlay">
    <h1 class="logo logo-large">ORA</h1>
    <p class="hero-tagline">Empowering women to reconnect with their body, mind and soul through intentional movement and sacred spaces.</p>
    <div class="btn-row">
      <a href="mailto:hello@ora-retreats.com" class="btn btn-light">Join the waitlist</a>
      <a href="#retreat" class="btn btn-light">Discover our retreats</a>
    </div>
  </div>
</section>

<section class="intro">
  <div class="container intro-inner">
    <p>At ora, we create soulful retreats for women who long to slow down, reconnect, and return to what truly matters.</p>
    <p>Through intentional movement, nourishing rituals, and meaningful connection, we offer a sanctuary where body, mind, and soul come home.</p>
  </div>
</section>
```

- [ ] **Step 3: Append nav + hero CSS to `css/style.css`**

```css
/* ---- Header / Nav ---- */
.site-header {
  position: sticky;
  top: 0;
  z-index: 10;
  background: rgba(232, 232, 227, 0.9);
  backdrop-filter: blur(6px);
}

.header-inner {
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 1.25rem 1.5rem;
}

.logo {
  font-family: var(--font-logo);
  font-size: 1.75rem;
  letter-spacing: 0.05em;
}

.logo-large {
  font-size: clamp(3rem, 10vw, 5rem);
  color: #fff;
}

.nav-links {
  display: flex;
  align-items: center;
  gap: 2rem;
  font-family: var(--font-heading);
  font-size: 0.85rem;
  text-transform: uppercase;
  letter-spacing: 0.08em;
}

.btn-small {
  padding: 0.6rem 1.25rem;
  font-size: 0.7rem;
}

/* ---- Hero ---- */
.hero {
  position: relative;
  height: 90vh;
  min-height: 500px;
  display: flex;
  align-items: center;
  justify-content: center;
  text-align: center;
  overflow: hidden;
}

.hero-photo {
  position: absolute;
  inset: 0;
  width: 100%;
  height: 100%;
  object-fit: cover;
}

.hero-overlay {
  position: relative;
  z-index: 1;
  color: #fff;
  padding: 2rem;
  max-width: 700px;
}

.hero-overlay::before {
  content: "";
  position: absolute;
  inset: -2rem;
  background: rgba(57, 57, 57, 0.35);
  z-index: -1;
  border-radius: 8px;
}

.hero-tagline {
  font-size: 1.1rem;
  margin-top: 1rem;
  line-height: 1.6;
}

.btn-light {
  border-color: #fff;
  color: #fff;
}

.btn-light:hover {
  background: #fff;
  color: var(--color-text);
}

/* ---- Intro ---- */
.intro {
  padding: var(--section-padding);
}

.intro-inner {
  max-width: 640px;
  text-align: center;
  font-size: 1.1rem;
}

.intro-inner p + p {
  margin-top: 1.25rem;
}

/* ---- Mobile nav (base: hide links, show toggle) ---- */
@media (max-width: 768px) {
  .nav-links {
    display: none;
    position: absolute;
    top: 100%;
    left: 0;
    right: 0;
    background: var(--color-bg);
    flex-direction: column;
    gap: 1.5rem;
    padding: 1.5rem;
  }

  .nav-links.open {
    display: flex;
  }

  .header-inner {
    position: relative;
  }
}
```

- [ ] **Step 4: Verify in browser**

Run: open `index.html` in a browser.
Expected: sticky nav with "ora" logo left, Retreat/About/Contact/Join the waitlist links right; full-bleed hero photo with "ORA" title and tagline centered, two pill buttons; below the hero, the two-paragraph intro centered on the greige background. No console errors.

- [ ] **Step 5: Commit**

```bash
git add index.html css/style.css
git commit -m "Add nav and hero section"
```

---

### Task 4: Retreat section

**Files:**
- Modify: `index.html` (insert `<section id="retreat">` into `<main>`, replacing the `<!-- Task 4: retreat section -->` comment)
- Modify: `css/style.css` (append retreat section styles)

**Interfaces:**
- Consumes: `.container`, `.eyebrow`, `.section-title`, `hr.divider`, `.btn`, `.btn-row` from Task 1; `#contact` anchor target defined by Task 6 (link ahead is fine — anchors resolve at runtime regardless of task order).
- Produces: `.checklist` grid class, `.retreat-cta` block — no later task depends on these directly.

- [ ] **Step 1: Insert the retreat section markup**

```html
<section id="retreat" class="section retreat">
  <div class="container">
    <span class="eyebrow">Retreat</span>
    <h2 class="section-title">designed with intention</h2>
    <hr class="divider">

    <p class="section-lead">Our retreats are intimate experiences where every element has been thoughtfully curated.</p>
    <p class="section-lead">Expect slow mornings, grounding yoga practices, nourishing meals, inspiring workshops, meaningful conversations, and time to simply exist, without the pressure to be anywhere else.</p>

    <h3 class="includes-title">Each retreat includes:</h3>
    <ul class="checklist">
      <li>Daily yoga &amp; mindful movement</li>
      <li>Meditation &amp; breathwork</li>
      <li>Nourishing meals</li>
      <li>Beautiful accommodation</li>
      <li>Nature &amp; slow living</li>
      <li>Journaling &amp; self-reflection</li>
      <li>Connection with like-minded women</li>
      <li>Plenty of space to rest</li>
    </ul>

    <p class="section-lead">More than a holiday, our retreats are an opportunity to reconnect with the person you've always been beneath the noise.</p>

    <img src="images/retreat-program.jpg" alt="Full retreat program overview" class="program-image">

    <div class="btn-row">
      <a href="#contact" class="btn">Book a shared room</a>
      <a href="#contact" class="btn">Book a single room</a>
    </div>

    <p class="moodboard-link"><a href="moodboard.html">See the house &rarr;</a></p>

    <div class="waitlist-card">
      <p>Upcoming retreats coming soon.</p>
      <p>Join our waitlist to be the first to hear about new retreats and receive early access.</p>
      <a href="mailto:hello@ora-retreats.com" class="btn">Join the waitlist</a>
    </div>
  </div>
</section>
```

- [ ] **Step 2: Append retreat section CSS**

```css
/* ---- Section shared ---- */
.section {
  padding: var(--section-padding);
  text-align: center;
}

.section-lead {
  max-width: 640px;
  margin: 1.5rem auto 0;
  font-size: 1.05rem;
}

/* ---- Retreat ---- */
.includes-title {
  font-family: var(--font-heading);
  font-size: 1rem;
  text-transform: uppercase;
  letter-spacing: 0.08em;
  margin-top: 3rem;
  margin-bottom: 1.5rem;
}

.checklist {
  display: grid;
  grid-template-columns: repeat(2, minmax(0, 260px));
  justify-content: center;
  gap: 0.75rem 3rem;
  max-width: 640px;
  margin: 0 auto;
  text-align: left;
}

.checklist li {
  position: relative;
  padding-left: 1.25rem;
}

.checklist li::before {
  content: "—";
  position: absolute;
  left: 0;
  color: var(--color-accent);
}

.program-image {
  max-width: 480px;
  margin: 3rem auto 0;
  border-radius: 4px;
}

.moodboard-link {
  margin-top: 2rem;
  font-family: var(--font-heading);
  font-size: 0.85rem;
  letter-spacing: 0.05em;
  text-decoration: underline;
}

.waitlist-card {
  margin: 4rem auto 0;
  max-width: 480px;
  background: var(--color-card);
  padding: 3rem 2rem;
  border-radius: 8px;
}

.waitlist-card p {
  margin-bottom: 0.75rem;
}

.waitlist-card .btn {
  margin-top: 1rem;
}

@media (max-width: 600px) {
  .checklist {
    grid-template-columns: 1fr;
    max-width: 280px;
  }
}
```

- [ ] **Step 3: Verify in browser**

Run: open `index.html`, scroll to (or click "Retreat" in nav to jump to) the retreat section.
Expected: eyebrow "RETREAT" + title "designed with intention", intro paragraphs, two-column checklist of 8 items (single column on narrow viewport), program image, two booking buttons, "See the house →" link, and the waitlist card at the bottom.

- [ ] **Step 4: Commit**

```bash
git add index.html css/style.css
git commit -m "Add retreat section"
```

---

### Task 5: About section

**Files:**
- Modify: `index.html` (insert `<section id="about">` into `<main>`, replacing the `<!-- Task 5: about section -->` comment)
- Modify: `css/style.css` (append about section styles)

**Interfaces:**
- Consumes: `.container`, `.eyebrow`, `.section-title`, `hr.divider`, `.section` from Task 1/4.
- Produces: `.about-columns` grid class — no later task depends on it.

- [ ] **Step 1: Insert the about section markup**

```html
<section id="about" class="section about">
  <div class="container">
    <span class="eyebrow">About</span>
    <h2 class="section-title">more than a retreat.</h2>
    <hr class="divider">

    <div class="about-intro">
      <p>In a world that constantly asks us to do more, move faster, and give endlessly, ora invites you to do the opposite.</p>
      <p>To pause. To breathe. To listen.</p>
      <p>We believe every woman deserves moments of stillness. Moments to reconnect with herself beyond expectations, responsibilities, and routines.</p>
      <p>Whether you arrive seeking rest, clarity, healing, or simply space to breathe, you'll leave feeling lighter, grounded, and deeply connected to yourself.</p>
    </div>

    <div class="about-columns">
      <div class="about-story">
        <h3>The souls behind ora</h3>
        <p class="about-story-subtitle">Meet Julie &amp; Rilke</p>
        <p>ora was born from a shared passion for creating spaces where women feel seen, supported, and free to simply be.</p>
        <p>Rooted in movement, wellbeing, and conscious living, we believe that true transformation begins with slowing down and reconnecting with yourself.</p>
        <p>Our purpose is to create retreats that feel deeply personal — where every detail, from the yoga practice to the shared meals and meaningful conversations, is designed with care.</p>
        <p>We can't wait to welcome you.</p>
      </div>
      <div class="about-photo">
        <img src="images/about-portrait.jpg" alt="Julie and Rilke, founders of ora">
      </div>
    </div>
  </div>
</section>
```

- [ ] **Step 2: Append about section CSS**

```css
/* ---- About ---- */
.about-intro {
  max-width: 560px;
  margin: 0 auto;
}

.about-intro p + p {
  margin-top: 1.25rem;
}

.about-columns {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 3rem;
  align-items: center;
  margin-top: 4rem;
  text-align: left;
}

.about-story h3 {
  font-family: var(--font-heading);
  font-size: 1.1rem;
  text-transform: uppercase;
  letter-spacing: 0.05em;
}

.about-story-subtitle {
  font-family: var(--font-logo);
  font-size: 1.5rem;
  color: var(--color-accent);
  margin: 0.5rem 0 1.5rem;
}

.about-story p + p {
  margin-top: 1rem;
}

.about-photo img {
  border-radius: 4px;
}

@media (max-width: 768px) {
  .about-columns {
    grid-template-columns: 1fr;
  }

  .about-photo {
    order: -1;
  }
}
```

- [ ] **Step 3: Verify in browser**

Run: open `index.html`, click "About" in nav.
Expected: centered intro block, then two columns below (story left, portrait photo right on desktop; photo stacks above story text on narrow viewports).

- [ ] **Step 4: Commit**

```bash
git add index.html css/style.css
git commit -m "Add about section"
```

---

### Task 6: Contact section + footer

**Files:**
- Modify: `index.html` (insert `<section id="contact">` into `<main>`, replacing the `<!-- Task 6: contact section -->` comment; replace the `<footer class="site-footer">` comment)
- Modify: `css/style.css` (append contact + footer styles)

**Interfaces:**
- Consumes: `.container`, `.eyebrow`, `.section-title`, `hr.divider`, `.section` from Task 1/4.
- Produces: `.site-footer` CSS class, reused verbatim (same markup) inside `moodboard.html` by Task 7.

- [ ] **Step 1: Insert the contact section markup**

```html
<section id="contact" class="section contact">
  <div class="container">
    <span class="eyebrow">Contact</span>
    <h2 class="section-title">we'd love to hear from you</h2>
    <hr class="divider">

    <p class="section-lead">Whether you have a question, an idea for a collaboration, or simply want to say hello — we're here.</p>

    <div class="contact-links">
      <a href="mailto:hello@ora-retreats.com">hello@ora-retreats.com</a>
      <a href="https://www.instagram.com/ora.retreats" target="_blank" rel="noopener">@ora.retreats on Instagram</a>
    </div>
  </div>
</section>
```

- [ ] **Step 2: Insert the footer markup**

```html
<footer class="site-footer">
  <div class="container footer-inner">
    <a href="index.html" class="logo">ora</a>
    <div class="footer-links">
      <a href="mailto:hello@ora-retreats.com">hello@ora-retreats.com</a>
      <a href="https://www.instagram.com/ora.retreats" target="_blank" rel="noopener">Instagram</a>
    </div>
    <p class="footer-copyright">&copy; 2026 ora retreats. All rights reserved.</p>
  </div>
</footer>
```

- [ ] **Step 3: Append contact + footer CSS**

```css
/* ---- Contact ---- */
.contact-links {
  margin-top: 2rem;
  display: flex;
  flex-direction: column;
  gap: 0.75rem;
  font-family: var(--font-heading);
  font-size: 0.95rem;
  letter-spacing: 0.03em;
}

.contact-links a {
  text-decoration: underline;
}

/* ---- Footer ---- */
.site-footer {
  border-top: 1px solid var(--color-accent);
  padding: 3rem 1.5rem;
}

.footer-inner {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 1rem;
  text-align: center;
}

.footer-links {
  display: flex;
  gap: 1.5rem;
  font-family: var(--font-heading);
  font-size: 0.8rem;
  text-transform: uppercase;
  letter-spacing: 0.05em;
}

.footer-copyright {
  font-size: 0.75rem;
  color: var(--color-accent);
}
```

- [ ] **Step 4: Verify in browser**

Run: open `index.html`, click "Contact" in nav, scroll to the bottom.
Expected: centered contact section with mailto link and Instagram link; footer with logo, email/Instagram links, and copyright line.

- [ ] **Step 5: Commit**

```bash
git add index.html css/style.css
git commit -m "Add contact section and footer"
```

---

### Task 7: Moodboard page

**Files:**
- Modify: `moodboard.html` (insert gallery markup into `<main>`, replace footer comment with the same footer markup Task 6 produced)
- Modify: `css/style.css` (append moodboard styles)

**Interfaces:**
- Consumes: `.logo`, `.site-footer`, `.footer-inner`, `.footer-links`, `.footer-copyright` from Tasks 3/6.

- [ ] **Step 1: Insert the moodboard gallery markup**

```html
<section class="section moodboard-page">
  <div class="container">
    <span class="eyebrow">Moodboard</span>
    <h2 class="section-title">a place to slow down</h2>
    <hr class="divider">

    <div class="mosaic">
      <img src="images/moodboard-01.jpg" alt="Retreat house detail" class="mosaic-item mosaic-tall">
      <img src="images/moodboard-02.jpg" alt="Nature surrounding the retreat" class="mosaic-item mosaic-tall">
      <img src="images/moodboard-03.jpg" alt="Yoga space at the retreat house" class="mosaic-item">
      <img src="images/moodboard-04.jpg" alt="Retreat house exterior" class="mosaic-item mosaic-tall">
      <img src="images/moodboard-05.jpg" alt="Shared living space" class="mosaic-item">
      <img src="images/moodboard-06.jpg" alt="Outdoor lounge area" class="mosaic-item">
      <img src="images/moodboard-07.jpg" alt="Bedroom at the retreat house" class="mosaic-item mosaic-tall">
      <img src="images/moodboard-08.jpg" alt="Morning light in the retreat house" class="mosaic-item">
    </div>
  </div>
</section>
```

- [ ] **Step 2: Replace the footer comment in `moodboard.html` with the same footer markup from Task 6**

```html
<footer class="site-footer">
  <div class="container footer-inner">
    <a href="index.html" class="logo">ora</a>
    <div class="footer-links">
      <a href="mailto:hello@ora-retreats.com">hello@ora-retreats.com</a>
      <a href="https://www.instagram.com/ora.retreats" target="_blank" rel="noopener">Instagram</a>
    </div>
    <p class="footer-copyright">&copy; 2026 ora retreats. All rights reserved.</p>
  </div>
</footer>
```

- [ ] **Step 3: Append moodboard CSS**

```css
/* ---- Moodboard header (standalone page) ---- */
.moodboard-header {
  padding: 1.5rem;
  text-align: center;
}

/* ---- Moodboard mosaic ---- */
.mosaic {
  columns: 3 220px;
  column-gap: 1rem;
  margin-top: 3rem;
}

.mosaic-item {
  width: 100%;
  margin-bottom: 1rem;
  border-radius: 4px;
  break-inside: avoid;
}

.mosaic-tall {
  aspect-ratio: 4 / 5;
  object-fit: cover;
}

@media (max-width: 600px) {
  .mosaic {
    columns: 2 160px;
  }
}
```

- [ ] **Step 4: Verify in browser**

Run: open `moodboard.html`.
Expected: centered "ora" logo linking back to `index.html`; "MOODBOARD" eyebrow + title; a masonry-style photo grid (3 columns desktop, 2 columns mobile) with no gaps or overlapping images; footer matching `index.html`'s footer.

- [ ] **Step 5: Commit**

```bash
git add moodboard.html css/style.css
git commit -m "Add moodboard page"
```

---

### Task 8: JS interactivity (mobile nav toggle)

**Files:**
- Modify: `index.html` (add a hamburger button inside `.header-inner`, before `.nav-links`)
- Modify: `js/script.js` (replace the stub comment with real logic)
- Modify: `css/style.css` (append hamburger button styles)

**Interfaces:**
- Consumes: `.nav-links` and its `.open` modifier class from Task 3.
- Produces: nothing consumed by later tasks.

- [ ] **Step 1: Add the hamburger button markup**

```html
<a href="#" class="logo">ora</a>
<button class="nav-toggle" aria-label="Toggle navigation" aria-expanded="false">
  <span></span>
  <span></span>
  <span></span>
</button>
<nav class="nav-links">
```

(This replaces the existing `<a href="#" class="logo">ora</a>` line inside `.header-inner`, inserting the button immediately after it and before the existing `<nav class="nav-links">` line.)

- [ ] **Step 2: Write `js/script.js`**

```js
const navToggle = document.querySelector('.nav-toggle');
const navLinks = document.querySelector('.nav-links');

if (navToggle && navLinks) {
  navToggle.addEventListener('click', () => {
    const isOpen = navLinks.classList.toggle('open');
    navToggle.setAttribute('aria-expanded', String(isOpen));
  });

  navLinks.querySelectorAll('a').forEach((link) => {
    link.addEventListener('click', () => {
      navLinks.classList.remove('open');
      navToggle.setAttribute('aria-expanded', 'false');
    });
  });
}
```

- [ ] **Step 3: Append hamburger CSS**

```css
/* ---- Mobile nav toggle ---- */
.nav-toggle {
  display: none;
  flex-direction: column;
  gap: 5px;
  background: none;
  border: none;
  cursor: pointer;
  padding: 0.5rem;
}

.nav-toggle span {
  width: 22px;
  height: 2px;
  background: var(--color-text);
}

@media (max-width: 768px) {
  .nav-toggle {
    display: flex;
  }
}
```

- [ ] **Step 4: Verify in browser at a narrow viewport**

Run: open `index.html`, resize the browser window (or use devtools device toolbar) to under 768px wide.
Expected: nav links are hidden, a 3-line hamburger button appears top-right; clicking it reveals the stacked nav links below the header; clicking any nav link closes the menu again and scrolls to the target section.

- [ ] **Step 5: Commit**

```bash
git add index.html js/script.js css/style.css
git commit -m "Add mobile nav toggle"
```

---

### Task 9: Responsive polish pass

**Files:**
- Modify: `css/style.css` (add/adjust media query rules only — no new HTML)

**Interfaces:**
- Consumes: all classes from Tasks 1–8.

- [ ] **Step 1: Add hero and typography scaling for small screens**

Append to `css/style.css`:

```css
@media (max-width: 480px) {
  .hero {
    height: 100vh;
  }

  .section-title {
    font-size: 1.4rem;
  }

  .section {
    padding: 4rem 1.25rem;
  }

  .waitlist-card {
    padding: 2rem 1.5rem;
  }

  .btn-row {
    flex-direction: column;
    align-items: stretch;
  }

  .btn-row .btn {
    width: 100%;
    text-align: center;
  }
}
```

- [ ] **Step 2: Verify at three widths in browser devtools**

Run: open `index.html` with devtools responsive mode set to 1440px, 768px, and 375px widths in turn.
Expected at every width: no horizontal scrollbar, no overlapping text/images, hero text remains readable over the photo, checklist and about-columns stack correctly below 768px, buttons stack full-width below 480px.

- [ ] **Step 3: Verify `moodboard.html` at the same three widths**

Run: open `moodboard.html` with the same three devtools widths.
Expected: mosaic grid re-flows from 3 to 2 columns at the 600px breakpoint, no horizontal scrollbar at any width.

- [ ] **Step 4: Commit**

```bash
git add css/style.css
git commit -m "Responsive polish for small screens"
```

---

### Task 10: Deploy notes + final review

**Files:**
- Create: `README.md`

**Interfaces:**
- None — final documentation task.

- [ ] **Step 1: Write `README.md`**

```markdown
# ora-retreats.com

Static marketing site for ora retreats. No build step required.

## Local preview

Open `index.html` directly in a browser, or serve the folder with any static
file server (e.g. `python -m http.server` from this directory).

## Deploying to easyhost.be

1. Log in to the easyhost.be control panel.
2. Open the file manager (or connect via FTP) for the `ora-retreats.com` hosting product.
3. Upload the entire contents of this folder (`index.html`, `moodboard.html`,
   `css/`, `js/`, `images/`) to the web root.
4. Visit ora-retreats.com to confirm it's live.

## Swapping in real assets

- Replace files in `images/` with the real photos, keeping the same filenames
  (`hero.jpg`, `retreat-program.jpg`, `about-portrait.jpg`,
  `moodboard-01.jpg`...`moodboard-08.jpg`) — no HTML changes required.
- Replace the Google Fonts `<link>` in both HTML files if the real logo font
  or title font changes.
```

- [ ] **Step 2: Full click-through verification**

Run: open `index.html`, click every nav link (Retreat, About, Contact), both booking buttons, the "See the house →" link, both "Join the waitlist" links, the footer Instagram/email links, and the moodboard page's logo link back home.
Expected: every anchor link scrolls to the correct section; both waitlist/contact mailto links open a mail compose window addressed to `hello@ora-retreats.com`; the Instagram link opens `instagram.com/ora.retreats` in a new tab; "See the house →" navigates to `moodboard.html`; the moodboard logo link returns to `index.html`.

- [ ] **Step 3: Commit**

```bash
git add README.md
git commit -m "Add deployment README"
```

---

## Self-review notes

- Spec coverage confirmed: nav/hero (Task 3), retreat section incl. checklist/program image/booking buttons/moodboard link/waitlist card (Task 4), about section incl. centered intro + two-column founder story (Task 5), contact section + footer (Task 6), moodboard page (Task 7), mailto-only forms (Tasks 3/4/6, no JS submission handling), mobile nav (Task 8), responsive stacking (Task 9), deploy instructions (Task 10).
- All image references use the exact filenames declared in Task 2 — checked against every `<img src="images/...">` in Tasks 3, 4, 5, 7.
- Color/font tokens defined once in Task 1 and referenced by `var(...)` everywhere else — no hardcoded hex values in later tasks.

