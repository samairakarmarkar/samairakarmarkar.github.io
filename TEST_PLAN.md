# Test Plan — Portfolio rebuild (PR #1)

Testing the rebuilt `samairakarmarkar.github.io` site against the local preview at `http://localhost:8765`. Single recording covering the primary flow.

## What changed
Old site: 4 minimal text-only pages. New site: 5-page portfolio with styled hero, polaroid collage, clickable bookshelf of writing samples, resume page with PDF, and full essay reading pages.

## Primary flow — "Visitor explores the portfolio"

### Test 1: Home page renders the Canva-style hero
- Navigate to `/index.html`.
- **Assertions:**
  - Nav pills visible: `home`, `about me`, `writing samples`, `projects`, `resume` (5 total). `home` pill is black-filled (active state).
  - `h1` text reads `samaira's` on line one and `portfolio` on line two.
  - The word `portfolio` renders in **italic** serif with a **yellow highlight background** (not plain black text).
  - At least 3 polaroid cards are visible in the hero area with "Details.jpg" / "slay.png" captions.
  - Subtitle text matches: "an insight into my professional and creative works."
- **Broken-state check:** If styling didn't load, `portfolio` would be plain black serif with no yellow box — visually obvious fail.

### Test 2: Bookshelf — each book is clickable and opens the right essay
Most-important test (user explicitly called this out).
- Click the `writing samples` pill.
- **Assertions on /writing.html:**
  - A brown wooden shelf is visible with **at least 7 book spines** leaning on it.
  - Spine text is readable vertically and includes:
    - `Don't Blame the Player, Blame the Deck`
    - `Bananas, Balloons & the Price of Nothing`
    - `More on Medium →`
  - Click book #1 (leftmost red book titled "Don't Blame the Player").
    - URL becomes `/post1.html`.
    - Page shows an `<h1>` reading **"Don't Blame the Player, Blame the Deck"**.
    - First paragraph starts with: "During any card game, there is always someone who loses…"
    - Footer has a black button **"read on medium"** pointing to the matching Medium URL.
  - Click "back to the shelf" and click book #2 (tall blue "Bananas, Balloons…").
    - URL becomes `/post2.html`.
    - `<h1>` reads **"Bananas, Balloons, and the Price of Nothing"**.
    - Paragraph contains "In 2019, a banana taped to a wall was sold for $120,000".
- **Broken-state check:** If the bookshelf feature were broken, either (a) books wouldn't be links (clicking does nothing), (b) they'd all go to the same page, or (c) essay pages would show the stub "Essay Title / Your writing goes here…" that was in the old repo.

### Test 3: About page shows the adapted Canva quote + fun facts
- Click `about me`.
- **Assertions:**
  - Page title `about me` with `me` in yellow italic highlight.
  - Quote card starts with "Hi! My name is Samaira…" and mentions "Kelley School of Business".
  - A separate "fun facts about me" list has **7 bullets** with ✦ glyphs (e.g. "confidence is a practice, not a personality trait").
  - Two buttons visible: black `view resume` and outlined `my linkedin`; the LinkedIn button `href` is exactly `https://www.linkedin.com/in/samairakarmarkar/`.
- **Broken-state check:** Old about page had 3 plain `<p>` tags with no card, no quote mark, no fun facts — visually very different.

### Test 4: Projects page shows 6 cards
- Click `projects`.
- **Assertions:**
  - **6** project cards visible, each with a tape strip at top.
  - Card titles include exactly these strings: "Designers & Business", "PA Young Ambassadors", "Multicultural Resource Center", "Bitcoding Academy", "Essays on Medium", "Sewing, Painting & Video".
- **Broken-state check:** Old projects page read "Currently building new work—check back soon." — one sentence, no cards. If CSS or content regressed we'd see that instead.

### Test 5: Resume — PDF download link is real, not a 404
- Click `resume`.
- **Assertions:**
  - Click `download pdf` — a PDF opens in a new tab and **renders page 1 with the name "Samaira Karmarkar"** (not a 404 page).
  - `linkedin` button opens `https://www.linkedin.com/in/samairakarmarkar/` in a new tab.
  - Resume body includes sections **Education**, **Experience**, **Activities**, **Skills & Interests**, and mentions "Indiana University, Kelley School of Business".
- **Broken-state check:** Old resume page linked to the same PDF filename, but the file wasn't actually in the repo — the link would 404. This test catches that regression.

## Recording
One continuous recording following Tests 1 → 5 in order, with `record_annotate` markers at each test boundary.

## Out of scope
- Mobile responsive (spot-check in summary only)
- Real photos (placeholders are intentional until user provides images)
- Post3.html "coming soon" page (trivial placeholder)
- Cross-browser (Chrome only)

## Preview URL
Local only: `http://localhost:8765/`. GitHub Pages won't update until the PR is merged into `main`.
