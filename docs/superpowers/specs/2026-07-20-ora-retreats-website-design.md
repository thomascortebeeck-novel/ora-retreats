# ora-retreats.com — Website Design Spec

## Context

ora is a new women's wellness/yoga retreat brand run by Julie & Rilke. They already own the domain `ora-retreats.com`, hosted on easyhost.be (traditional shared hosting), and have written down site copy/structure and some visual identity decisions (color palette, logo font). No retreats are scheduled yet — the site's current job is to build a waitlist and establish the brand.

Competitor analyzed for inspiration: [sheshe-retreats.com](https://sheshe-retreats.com) — a quiet, editorial wellness-retreat site: serif wordmark, generous whitespace, greige/neutral palette, minimal nav (About / Newsletter / Contact), retreat listings with dates and "spots left," warm first-person About copy, Instagram + email in the footer, no heavy visual noise.

## Goals

- A calm, editorial, on-brand landing site that captures the ora tone ("slow down, reconnect, return to what matters").
- Waitlist capture and a simple way for visitors to reach out, with zero backend/server dependency.
- Deployable as-is to easyhost.be shared hosting via FTP upload.
- Easy for a non-developer to eventually swap in real photos/logo once the ZIP of assets is ready.

## Non-goals

- No CMS, no booking/payment system, no server-side code.
- No blog, no multi-retreat catalog (only one retreat program for now).
- No real photography/logo yet — placeholders are expected and clearly swappable.

## Site structure

- **Single-page scroll** for the main site: Hero → Retreat → About → Contact, all on `index.html`, with a sticky top nav linking to in-page anchors (`#retreat`, `#about`, `#contact`).
- **Separate page**: `moodboard.html` — a mosaic/masonry gallery of house & retreat photos, linked from the Retreat section and from the nav.
- Nav bar: `ORA` wordmark (left) · Retreat · About · Contact (right) · persistent "Join the waitlist" button.
- Footer (all pages): Instagram `@ora.retreats`, `hello@ora-retreats.com`, small copyright line.

## Visual system

**Colors** (from Julie & Rilke's palette doc):
- Background (greige): `#E8E8E3`
- Primary text: `#393939`
- Accent / muted taupe (eyebrow labels, dividers, secondary text): `#7a7268`
- Off-white card/section background: `#F4F4F1`

**Typography:**
- Logo "ORA": Cormorant Garamond, large, letter-spaced, matches their confirmed 63.3pt logo spec proportionally.
- Section titles ("retreat", "about", "contact", nav labels): Poppins — a free Google Fonts lookalike for the tentative "Gotham" pick, uppercase, letter-spaced, small size.
- Body copy: Jost — free geometric sans, regular weight, generous line-height (1.6+).
- All fonts loaded via Google Fonts CDN `<link>` (no local hosting/licensing needed).

**Components / styling rules:**
- Thin 1px hairline dividers between sections (echoing their `YOGA — RETREATS` sample), no drop shadows, no heavy borders.
- Buttons: text-links or thin-outline pill buttons only, staying within the greige/taupe palette — no bright accent colors.
- Layout stays close to the competitor's restraint: large whitespace margins, centered text blocks, full-bleed photography, small type for supporting copy.

## Page-by-page content

### Hero
Full-bleed placeholder photo (beach/yoga stock, similar mood to the "backbend on beach" reference photo). "ORA" wordmark + tagline ("Empowering women to reconnect with their body, mind and soul through intentional movement and sacred spaces.") overlaid centered. Two CTAs: "Join the waitlist" (mailto) and "Discover our retreats" (anchor-scrolls to `#retreat`).

Below the hero: the two-line intro paragraph from the brief ("At ora, we create soulful retreats...") on the plain greige background, no photo — mirrors the brief's "foto 1" treatment where the intro sits on its own after the full-photo hero.

### Retreat section (`#retreat`)
- Eyebrow "RETREAT" + title "designed with intention".
- Intro paragraph + second paragraph ("Expect slow mornings...").
- Two-column checklist of the 8 inclusions (yoga & movement, meditation & breathwork, nourishing meals, accommodation, nature & slow living, journaling, connection, rest).
- Closing paragraph ("More than a holiday...").
- Program image placeholder (stands in for the "full program PDF/image" asset, marked as swappable).
- Two buttons: "Book a shared room" / "Book a single room" — both scroll to `#contact`.
- Link/button to the Moodboard page ("See the house →").
- "Upcoming retreats coming soon" block: short copy + "Join the waitlist" mailto CTA (second placement, reinforces the primary conversion goal).

### About section (`#about`)
- Centered intro block: "More than a retreat." + the four short paragraphs from the brief (do the opposite / pause, breathe, listen / etc.), centered per the brief's `(centered)` note.
- Two-column layout below: left = "The souls behind ora — Meet Julie & Rilke" story copy (3 paragraphs from brief); right = portrait placeholder photo (stands in for "FOTO 3").

### Contact section (`#contact`)
- Short intro line ("We'd love to hear from you...").
- `hello@ora-retreats.com` as a mailto link.
- Instagram handle `@ora.retreats` linking out.
- Kept minimal and centered, matching the competitor's plain contact page.

### Moodboard page (`moodboard.html`)
- Masonry/mosaic grid of placeholder photos (nature, yoga, house, details) — mirrors the brief's "mozaïk achtig" request.
- Minimal header with just the ORA wordmark linking back to `index.html`, no full nav needed.

## Forms / interactivity

- "Join the waitlist" and the Contact section both use plain `mailto:hello@ora-retreats.com` links — no form backend, no JS submission handling. Confirmed with Julie & Rilke's preference for zero setup over a managed mailing list for now.
- No other JS-driven interactivity required beyond smooth-scroll for anchor nav links and a mobile nav toggle.

## Images

- All photos are temporary stock placeholders (free sources, e.g. Unsplash), chosen to match the intended mood (beach, yoga, nature, slow living) so the site looks presentable when shown to others.
- Every placeholder is easy to swap: consistent `<img>` tags with descriptive alt text and filenames (e.g. `hero.jpg`, `retreat-program.jpg`, `about-portrait.jpg`, `moodboard-01.jpg`...) so dropping in the real ZIP of assets later is a straight file replacement.

## Technical approach

- Plain HTML/CSS/JS, no build step, no framework, no dependencies beyond the Google Fonts CDN link.
- Files: `index.html`, `moodboard.html`, `style.css`, `script.js` (smooth scroll + mobile nav toggle only), `/images/` folder for placeholders.
- Mobile-first responsive design (nav collapses to a hamburger/simple stacked menu below ~768px; sections stack to single column).
- Deployable by uploading the folder as-is via FTP to easyhost.be — no server configuration needed.

## Open questions for later (not blocking this spec)

- Real logo file, photography, and program PDF — arriving later via ZIP, will replace placeholders.
- Whether to later add a proper mailing-list tool (Mailchimp etc.) once they want real newsletter functionality — explicitly deferred for now.
