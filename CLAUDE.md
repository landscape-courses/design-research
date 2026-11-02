# Design Research — course site

Repo in the `landscape-courses` org. Served by GitHub Pages at
`https://landscape-courses.github.io/design-research/` from `main` / root (`.nojekyll`).
Hand-authored static HTML, no build step. Keep it that way.

## Working rules (all instructors, all Claude sessions)
- **Never push to `main`.** Work on a branch, open a PR, the other instructor reviews.
- **Every internal path starts with `/design-research/`** (the Pages subpath). A bare `/assets/...`
  breaks on Pages. If a custom domain is added later, sed the prefix away in one pass.
- **Self-contained.** CSS, JS, deck system and images all live in this repo. Do not link assets
  from zihaozhang.cc or other course repos; copy them in.
- Links to Zihao's talks (`https://zihaozhang.cc/talks/...`) are external references, which is fine.
- Shared chrome (head, side-panel nav) is duplicated per page by design. Propagate nav edits with sed.
- Images: AVIF, long edge ≤1920. Declare `width`/`height` on every `<img>`, `loading="lazy"` below the fold.
- Find-and-replace across HTML: sed via Bash, not PowerShell (it double-encodes UTF-8).
- Nothing private here: the repo is public. Grades, rubrics with student names, student work stay out.

## Layout
- `index.html` — syllabus. `lectures/` — deck pages. `assets/img/what-is-research/` — shared plate pool for both research lectures.
- `assets/deck/` — slide-deck system; `deck-spec.md` is its spec. Read it before touching a deck.
- `assets/css/` — `tokens.css` (every font and color as a variable; write `var(--…)`, never a hex),
  `main.css`, `workflow-shared.css`, `footer.css`. `assets/js/` — `nav.js`, `wf-progress.js`.
- `assets/img/<lecture-slug>/` — lecture images.

## Origin
Migrated Nov 2026 from `zihaoooo/zihao-site` `teaching/laar64150/`. The notes below are that
folder's teaching context, kept as written. Where they mention `../laar61400/` or the factory
(`course-prep`), read: those live outside this repo now; borrowed assets are copied in, and this
repo is the source of truth.

---


Listed: a course card in `teaching/index.html` points here, and the pages are indexable.
The page serves as the lecture home for the course while the seminar is redeveloped.

Factory output of `../../../course-prep/laar64150/`; same authoring rules as laar61400
(see `../laar61400/CLAUDE.md`, "Factory output").

- `index.html` carries a course header, an Overview written from the three lectures, a
  Where to Find Information source list (the general lecture links to it), and the lecture
  table — no weekly schedule, by choice. The Fall 2025 syllabus was combined with the
  studio (studio–research seminar pair); this course is being redeveloped as a standalone seminar.
- Styles and nav script borrow laar61400's `assets/css/` and `assets/js/nav.js`.
- `lectures/` holds reusable research lectures, named by topic (no week prefix) so other courses
  can link them:
  - `what-is-research.html` (30 slides, seven parts) — the **general** version, for students from
    any discipline. Parts: what is research · asking the question · methods and evidence · why
    theory matters · paradigms and incommensurability · disciplines and working across · research
    is never neutral (one slide, Haraway's situated knowledges).
    - **Brief by design** (cut from 68 slides / 5,800 words to 41 / 2,300, then to 30 in 2026-09). The rule
      is ~90 words and ~5 bullets a slide; **detail lives in `data-notes`, not on the slide.**
      When adding to this deck, put the elaboration in the speaker notes and keep the card short.
    - No images: it is text-only by choice. The six plates it used to carry are still in
      `assets/img/what-is-research/` and still used by the designers lecture.
    - Part II's argument is **ask a *how* question**: a why needs a cause isolated from its
      rivals, a what stops at description, a how names a process with parts you can go look at.
    - Part V is two slides: normal science / anomaly / paradigm, and incommensurability
      (what it does and does not mean, the five values). Part VI has no trading-zones slide.
    - **No Part VIII.** Finding sources and making it public were cut (2026-09); the source
      list lives only in `index.html`'s **Where to Find Information** section, and the
      proposal skeleton stays in `grant-writing-101.html`. The deck ends on "Before next week".
  - `what-is-research-for-designers.html` (42 slides) — the original lecture, renamed 2026-09.
    Making and theorizing as methods, with graphic references.
  - `grant-writing-101.html` (15 slides). Rebuilt, with the designer lecture, from the Dropbox
    sources in `/Zihao Zhang/03_Lectures/` (What is Research.pdf, Grant Writing 101.pptx) —
    text became typeset cards, images were extracted and encoded to AVIF.
- `assets/img/what-is-research/` is a **shared pool for both** What is Research lectures — the
  folder keeps the old name after the rename so no paths broke. The general lecture reuses six
  of its plates (05-a, 10-a/b, 12-a, 13-a, 17-a); the rest are designer-only.
- Nav: all four pages carry the same three-link `.panel-section`, generic lecture first.
  Propagate nav edits across them together (sed, or a regex replace of the whole
  `.panel-section-label` block).
- Text cards are now **shared, in `/assets/deck/deck.css`**: `.txt-card` (heading + bullets),
  `.stmt` (one sentence carried large) and `.cmp` (comparison table, added 2026-09 for the
  question-stem, paradigm and discipline slides in Parts II, IV and VI). Promoted out of these pages once the third lecture needed
  them, with `.pv-deck` mirrors in deck.js — so Presenter View renders them properly now, which
  it did not before. Spec: `/assets/deck/deck-spec.md`. Each page keeps only the 3-line
  `.slide .embed` rule inline, same as the laar61400 lectures.
- Speaker notes are written for this material, not carried over: the .pptx notes were one
  repeated line.
