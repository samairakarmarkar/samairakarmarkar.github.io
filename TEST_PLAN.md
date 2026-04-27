# Test Plan — Vintage Journal Redesign (PR #3)
 
## What changed (user-visible)
Full visual redesign to a "vintage journal / scrapbook" aesthetic. Beige/olive/brown/dusty-pink palette, paper-grain background, Caveat handwriting + Cormorant serif. Four pages got structural overhauls: home (journal cover), about (open notebook spread), projects (file-folder system), writing (lined-paper journal cards).
 
## Test environment
Local static server at `http://localhost:8765/` against the `devin/1777267522-scrapbook-journal` branch checked out at `/home/ubuntu/repos/samairakarmarkar.github.io`.
 
## Primary flow + adversarial assertions
 
Each test is designed so a broken implementation would produce a visibly different result.
 
### T1 — Home renders as a journal cover (not a sky+polaroid hero)
**Path:** open `http://localhost:8765/index.html`
**Pass criteria — ALL must hold:**
- Background of the main hero block is a **dark leather brown** (computed bg of `.cover` is rgb close to `#3b2c20`/`#2b1e14`), NOT light blue sky.
- A **stitched dashed border** (`.cover::before`) is visible inside the dark cover area.
- A horizontal **elastic band** (`.cover::after`) crosses the cover roughly in its lower third.
- Centered cream **title label** contains exact text: eyebrow `A Personal Journal`, h1 `Samaira's portfolio` (with `portfolio` italic in a different font), and a year line `2025 — 2026`.
- At least one **handwritten note** with text "Dear little me, everything will be alright. Ease your mind." is visible somewhere on the cover.
- A small CTA below the cover reads `open the journal — start with about me.` and the link goes to `about.html`.
 
**Distinguishes from broken:** if the redesign didn't apply, the home page would still render the old yellow-italic "samaira's portfolio" on a sky background. The dark leather background + the "Dear little me" note do not exist in any prior version.
 
### T2 — About is an open notebook spread with binder rings (CORE)
**Path:** click `about me` in the top nav.
**Pass criteria — ALL must hold:**
- The page contains a center `.spread` element with a **vertical column of 6 dark circular binder rings** running down the middle of the spread (computed: `.rings span` count = 6, each visually round and dark grey).
- The left page shows a **stack of polaroid-style cards** with at least 3 captions among `kelley, '25` / `studio.` / `paint days`.
- Below the photo stack, a tilted note card has the heading **`interests`** (NOT "fun facts") and the list contains the literal substring `linkedin games`.
- The right page begins with the date line `april 22, 2026 · bloomington` followed by the heading `Hi! I'm Samaira.` rendered in the Caveat handwriting font.
- The first paragraph on the right page has a **drop-cap first letter `I`** that is visibly larger than its paragraph text.
- Two buttons at the bottom: `view my resume` (links to `resume.html`) and `linkedin` (links to `linkedin.com/in/samairakarmarkar/`).
 
**Distinguishes from broken:** if the new CSS isn't loaded, there'll be no binder rings, no two-column spread, no drop cap, and the heading will be in Playfair (not Caveat). The "fun facts" → "interests" rename is a hard string check.
 
### T3 — Projects is a file-folder system that expands on click (CORE)
**Path:** click `projects` in the top nav.
**Pass criteria — ALL must hold:**
- The page shows a dark backdrop containing **6 stacked manila/colored folder elements**, each with a small upper-right tab.
- Each folder has a small uppercase tab label among the set: `brand & campaign`, `writing`, `painting`, `sewing & textile`, `cnc & fabrication`, `video`.
- Before any interaction, the folder bodies are collapsed — for the `painting` folder, the descriptive text starting with "An ongoing personal practice" is **NOT visible** in the rendered viewport (`.folder-body` height ~0).
- After **clicking** the `painting` folder, the folder lifts upward and the descriptive paragraph "An ongoing personal practice — small canvases, portrait studies…" becomes visible.
- After clicking it again, the folder collapses (description disappears).
- A handwritten hint at the bottom reads `click a folder to open it.`
 
**Distinguishes from broken:** if the JS toggle is broken, clicking the folder will do nothing — the body text will never appear (or will be visible permanently from the start). If the CSS transition is broken, all folder bodies will be visible at once.
 
### T4 — Writing books still navigate to the right essays (regression-ish, but the cards visually changed)
**Path:** click `writing` in the top nav.
**Pass criteria — ALL must hold:**
- At least 6 journal-card style links are visible, each with a tape strip on top and lined-paper background (NOT vertical book spines, NOT a wooden shelf).
- The card titled "Don't Blame the Player, Blame the Deck" navigates to `post1.html` and the post page renders the body paragraph starting `During any card game, there is always someone who loses…`.
- The card titled "Bananas, Balloons & the Price of Nothing" navigates to `post2.html` and the post page renders the body paragraph mentioning `$120,000`.
- On both post pages, the first paragraph has a **drop-cap first letter** and there is a tape strip visible at the top of the paper.
 
**Distinguishes from broken:** if `writing.html` lost its links during the rewrite, the books wouldn't navigate; if the post-paper styling didn't update, there'd be no drop cap or tape.
 
### T5 — Resume still serves the real PDF
**Path:** click `resume` in the top nav.
**Pass criteria — ALL must hold:**
- The page shows the embedded PDF `Karmarkar_Samaira_Resume.pdf` rendering with the name `Samaira Karmarkar` visible (or, if inline embed is blocked, the fallback link is present).
- A `download pdf` button links to `Karmarkar_Samaira_Resume.pdf` with HTTP 200 (verified via curl during setup).
- A `linkedin` button links to `https://www.linkedin.com/in/samairakarmarkar/`.
- The whole page is wrapped in a **kraft-colored folder frame** with a small tab labeled `RESUME / 2026` in the upper-right.
 
**Distinguishes from broken:** missing PDF would 404; missing folder frame would just show the PDF on plain background.
 
## Out of scope
- Mobile responsiveness beyond a quick visual sanity check (note: explicitly listed by user but won't be the focus of the recording)
- Keyboard accessibility of the folder buttons
- Browser compatibility beyond Chrome
- Photo content (still gradient placeholders — flagged in PR description)
