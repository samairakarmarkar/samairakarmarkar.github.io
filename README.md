# samairakarmarkar.github.io
# samairakarmarkar.github.io
 
Samaira Karmarkar's personal portfolio — a static site hosted on GitHub Pages.
 
**Live site:** https://samairakarmarkar.github.io
 
## Pages
 
- `index.html` — home / landing hero
- `about.html` — about me + fun facts
- `writing.html` — bookshelf of writing samples (each book clickable)
- `projects.html` — projects & work experience
- `resume.html` — resume with PDF download + LinkedIn
- `post1.html`, `post2.html`, `post3.html` — individual writing samples
- `style.css` — shared styling (sky/cloud background, polaroid collage, bookshelf)
- `Karmarkar_Samaira_Resume.pdf` — resume file linked from the Resume page
 
## Local preview
 
```bash
python3 -m http.server 8000
# then open http://localhost:8000
```
 
## Adding a new essay
 
1. Copy `post1.html` to `postN.html` and replace the title, meta, and body paragraphs.
2. In `writing.html`, add a new `<a>` book in the `.shelf` with a spine title:
 
```html
<a href="postN.html" class="book c-3 tall">
  <span class="spine">Your Title<span class="by">Samaira</span></span>
</a>
```
 
Available modifiers: `c-1` … `c-7` (colors), `short` / `tall`, `thick`, `tilt-l` / `tilt-r`.
 
## Swapping in real photos
 
The polaroid collage on the home page and project card covers currently use CSS gradient placeholders
(`.frame.ph-1` … `.ph-8`). To use real photos, replace each `<div class="frame ph-N"></div>`
with an `<img>` or set a `background-image` in `style.css`:
 
```css
.frame.ph-1 { background: url('images/your-photo.jpg') center/cover; }
```
