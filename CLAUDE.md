# CLAUDE.md - Portfolio Site Build Instructions

Build and maintain a single-file personal portfolio for Suraj Singh, ML Engineer
based in Stockholm, targeting permanent ML / MLOps roles. Hosted on GitHub Pages
at https://surajsingh108.github.io.

The reader is a recruiter or hiring manager who will spend 30 to 90 seconds on
the page before deciding to contact, forward, or close the tab. Every decision
below serves that reader. Build for the skim first, the deep read second.

---

## 0. Hard rules (never break these)

- Single `index.html` file only. All CSS and JS inline. No frameworks, no build
  step, no CDN dependencies. Everything must work opened straight from disk.
- Two external assets are allowed in the repo root and linked from the HTML:
  `cv.pdf` (the downloadable CV) and `se3-demo.gif` (the live demo recording).
  No other external files.
- No em dashes anywhere in copy. Use commas, periods, or restructure the
  sentence.
- No boastful or poetic language. No "passionate", "cutting-edge", "leveraging",
  "robust", "seamless", "journey", "delve", "elevate", "unlock", "empower",
  "world-class". Write like an engineer reporting facts.
- No AI tells: no triadic "X, Y, and Z" rhythm in every sentence, no "it's not
  just X, it's Y" constructions, no emoji in body copy, no exclamation marks.
- Mobile responsive. Test at 375px, 768px, and 1280px widths.
- Every claim must be true. If a metric is not yet known, leave the marked
  placeholder in place. Never invent numbers.

---

## 1. Design direction

Dark base, restrained. The impact metrics and the live demo do the talking, not
the styling.

- Background `#0d0d0d`. Text `#e8e8e8`. Muted text `#9a9a9a`. One accent color
  only, used sparingly for links, the primary button, and metric numbers.
  Suggested accent `#4ade80` (a calm green that reads as "live / healthy",
  fitting for an energy and systems engineer). Confirm with Suraj before
  changing.
- System font stack only (no web fonts to load): `-apple-system,
  BlinkMacSystemFont, "Segoe UI", Roboto, Helvetica, Arial, sans-serif`.
- Generous whitespace. Max content width around 820px so lines stay readable.
- Subtle only: a thin border or a slightly lighter card surface (`#161616`) to
  separate project cards. No gradients, no glassmorphism, no animated
  backgrounds, no parallax. One quiet fade-in on scroll is the maximum motion.
- Respect `prefers-reduced-motion` and `prefers-color-scheme` is not needed
  since the site is dark by intent.

---

## 2. Page structure (in this order)

### 2.1 Hero (above the fold, must render in one screen)

The single most important section. A recruiter decides here.

- Name: Suraj Singh.
- One-line value proposition. Concrete, role-aligned, no fluff. Template:
  "ML Engineer in Stockholm. I build and ship production ML systems, from
  forecasting models to deployed agents." Refine to match Suraj's voice, keep it
  under 20 words.
- A one-line availability tagline directly under it:
  "Open to permanent roles in Stockholm. No sponsorship required."
  This removes the biggest objection for a Swedish employer and must stay near
  the top.
- Primary actions, presented as a clear hierarchy so they do not compete:
  1. Primary button: "Download CV" linking to `cv.pdf`.
  2. Secondary button: "Email me" (mailto link, see Contact for address).
  3. Text link: "See the live SE3 demo" jumping to the SE3 card.
- Small inline row of links: GitHub, LinkedIn. Plain text links, not big icons.
- If a Calendly or booking link exists, add it as a third text action
  ("Book a call"). If not, omit it. Do not add a placeholder booking link.

### 2.2 Proof strip (immediately below hero)

A single horizontal row of three to four headline facts that a recruiter can
absorb in two seconds. These are the highest-signal claims you own. Example
slots, fill with real numbers:

- "Live ML system in production on GCP"
- "{{SE3_ACCURACY_CLAIM}}" e.g. "Forecasts 24h ahead, {{X}}% lower error than
  baseline"
- "{{YEARS}} yrs building production ML"
- "Stack: PyTorch, LightGBM, LangGraph, GCP"

Keep each to a few words. This strip is the safety net for the recruiter who
reads nothing else.

### 2.3 Projects

Three to five projects, quality over quantity. Each card must answer, in the
first two lines, what it does and what the result was, before any tech detail.

Card format for every project:
- Title.
- One sentence on the problem and the outcome, with a number where possible.
- Two or three sentences of how, written for a technical reader.
- A short tag row (the stack).
- Links: live demo and GitHub where they exist.

Ordering and content below.

#### Project 1: SE3 Electricity Price Forecast (FEATURED, full-width card)

This is the strongest asset because it is deployed and running. Give it the most
space and put the demo right inside the card.

- Live dashboard: https://tinyurl.com/se3-forecast
  (Replace with a clean custom domain or the real URL if available. A tinyurl is
  acceptable but a readable URL reads more credible. Optional improvement.)
- GitHub: https://github.com/surajsingh108/SE3-electricity-price-forecast
- Lead line, outcome first. Template:
  "End-to-end ML system that forecasts Swedish electricity prices (SE3 zone)
  24 hours ahead. {{SE3_HEADLINE_RESULT, e.g. p50 forecast beats the Ridge
  baseline by X% pinball loss; serves answers in under Y ms}}."
- How line: "LightGBM quantile model (p05/p50/p95) with 78 engineered features.
  Hourly ingestion from ENTSO-E and Open-Meteo via Cloud Run Jobs, DuckDB on
  GCS, weekly retraining via Cloud Scheduler, MLflow for versioning. A LangGraph
  agent answers plain-English questions over the live data with cited sources."
- Tags: LightGBM, GCP, Cloud Run, DuckDB, MLflow, Docker, LangGraph, Streamlit,
  Quantile Forecasting.
- Demo slot (critical): if `se3-demo.gif` exists in the repo root, render it in
  an `<img>` with `loading="lazy"`, a max-width matching the card, and caption
  "SE3 dashboard, live on GCP". If the file does not exist, render a visible
  placeholder box reading "Add se3-demo.gif to show the live dashboard" so it is
  obvious the slot is empty. The demo is the single best piece of evidence on the
  page. Treat its absence as a bug to flag, not hide.

#### Project 2: graph-rag-memory

- GitHub: https://github.com/surajsingh108/graph-rag-memory
- Lead line with outcome if measurable, e.g. retrieval quality or dedup rate.
  Template: "Graph-augmented RAG memory system. {{RESULT, e.g. cuts duplicate
  writes by X% via cosine plus residual novelty scoring}}."
- How: "Tiered source/derived memory on ChromaDB with decay-based compaction and
  write-time deduplication. NetworkX knowledge graph for multi-hop retrieval.
  Runs fully on a local LLM, no external APIs."
- Tags: LangChain, ChromaDB, NetworkX, RAG, Knowledge Graph, Local LLM.

#### Project 3: synthflow

- GitHub: https://github.com/surajsingh108/synthflow
- Lead line: "Synthetic time-series data generation toolkit built on TSGM."
- How: "Handles ingestion, imputation, generative modelling, and output
  validation. Claude API integration for guided synthesis."
- Tags: TSGM, Synthetic Data, Python, Claude API, Imputation.

#### Project 4: Physics-Informed Neural Networks, Dynamic Line Rating (ATO Energy)

Professional work, no public repo. This is real production ML and should be
framed as such, with a clear "proprietary, no public code" note so its absence
of a link is not read as a gap.

- No GitHub link (proprietary).
- Lead line, outcome first: "PINNs for real-time thermal modelling of
  high-voltage power lines. {{RESULT, e.g. models used operationally in grid
  management decisions; validated against digital-twin ground truth}}."
- How: "Live sensor data drives the thermal model. Digital twins of grid
  components validate ML predictions against simulated physical ground truth."
- Tags: PINNs, PyTorch, Digital Twins, Time Series, Grid Management,
  Production ML.
- Add a small label: "Industry work, code not public."

### 2.4 Skills / stack

Grouped, scannable, and ATS-friendly. Recruiters and automated screeners parse
this section for exact framework names. Use the real names verbatim.

- ML / DL: PyTorch, LightGBM, scikit-learn
- Agentic / GenAI: LangChain, LangGraph, RAG, ChromaDB
- Data: DuckDB, SQL, pandas
- Cloud / Infra: GCP, Cloud Run, Docker, MLflow

If Suraj uses other in-demand tools (Kubernetes, Terraform, BigQuery, Hugging
Face, W&B, FastAPI), add only the ones he can speak to in an interview. Do not
pad the list.

### 2.5 About (short, optional)

Three or four sentences maximum. Who he is, what he focuses on, what he is
looking for. Plain and factual. No life story. This is also where a recruiter
confirms fit (location, work authorization, domain interest in energy/grid ML).

### 2.6 Contact

- Email: ssingh.108@outlook.com (confirm this is the address Suraj wants on a
  public page; an alias is fine).
- LinkedIn: https://linkedin.com/in/surajsinghlinked/
- GitHub: https://github.com/surajsingh108
- Repeat the availability line here: "Open to permanent roles in Stockholm.
  No sponsorship required."
- Plain mailto and links. No contact form (a form needs a backend and adds
  friction; recruiters prefer to copy an address or click mailto).

---

## 3. Technical requirements

- Valid, semantic HTML5: one `<h1>` (the name), logical `<h2>` per section,
  `<section>` landmarks, `<nav>` if a nav exists.
- Accessibility: color contrast at least 4.5:1 for body text against `#0d0d0d`
  (verify the muted grey passes), `alt` text on the demo image, focus styles on
  all links and buttons, keyboard navigable.
- SEO and link previews, all inline in `<head>`:
  - `<title>Suraj Singh, ML Engineer, Stockholm</title>`
  - meta description, one factual sentence with key terms (ML Engineer,
    Stockholm, production ML, MLOps).
  - Open Graph and Twitter Card tags (title, description, and an image if an OG
    image is added later). These control how the link looks when pasted into
    LinkedIn or Slack, which is exactly how recruiters share it.
  - `<html lang="en">`.
  - JSON-LD `Person` schema with name, jobTitle, address (Stockholm, SE), and
    sameAs links to GitHub and LinkedIn. Helps machine parsing.
- Performance: no render-blocking external requests, total page under 200KB
  excluding the demo GIF, GIF lazy-loaded. Should reach a near-perfect
  Lighthouse score by default because it is one static file.
- Favicon: a small inline SVG favicon (data URI) so there are no extra requests
  and no broken favicon icon.

---

## 4. Copy guidelines (how to write every line)

- Outcome before method, always. "Forecasts prices 24h ahead at X accuracy" then
  "using a LightGBM quantile model", not the reverse.
- Quantify wherever a true number exists: error reduction, latency, uptime, data
  volume, retraining cadence, cost. A real number stops the skim.
- Active voice, short sentences. Cut any word that can be removed without losing
  meaning.
- No filler adjectives. "Production ML system" not "powerful, scalable,
  production-grade ML system".
- Consistency: pick one capitalization for "ML Engineer" and one spelling per
  tool, and use it everywhere.

---

## 5. Metric placeholders to fill before publishing

The site is recruiter-ready only once these are real. Each is marked in the HTML
with a `{{...}}` token and an HTML comment. Build the page with the tokens
visible so the gaps are obvious, then Suraj replaces them.

- `{{SE3_HEADLINE_RESULT}}`: the one number that proves the SE3 model works
  (e.g. pinball loss vs baseline, MAE, or hit rate).
- `{{SE3_LATENCY}}`: response time of the agent or dashboard.
- `{{YEARS}}`: years of production ML experience.
- `{{GRAPHRAG_RESULT}}`: a measurable result for graph-rag-memory.
- `{{PINN_RESULT}}`: the operational impact statement for the ATO Energy work,
  cleared of anything confidential.

Do not publish with any `{{...}}` token still present. Add a build check (a quick
grep for `{{`) before deploy.

---

## 6. Assets

### CV (cv.pdf)
Place `cv.pdf` in the repo root. Keep it in sync with the site: same projects,
same numbers, same availability line. The "Download CV" button links to it
directly. If `cv.pdf` is missing, the button should still render but Claude
Code must flag that the file is absent.

### Demo GIF (se3-demo.gif)
1. Screen-record the live SE3 dashboard for 30 to 60 seconds.
2. Convert: `ffmpeg -i recording.mp4 -vf "fps=10,scale=900:-1" -loop 0 se3-demo.gif`
3. Keep it under ~5MB so the page stays fast. Drop it in the repo root.

---

## 7. Updating the site

Tell Claude Code the change in plain language, for example:
- "Add a project card for X with this result."
- "Update the SE3 headline number to Y."
- "Swap the accent color to Z."
- "Add a short writing/blog section."

Claude Code edits `index.html` directly, keeps all rules above, then commits.

---

## 8. Pre-deploy checklist (run every time before pushing)

1. No `{{...}}` tokens remain.
2. No em dashes in the file.
3. No banned filler words (section 0).
4. All links resolve: GitHub repos, LinkedIn, live demo, mailto, cv.pdf.
5. `cv.pdf` and `se3-demo.gif` exist, or their absence is flagged.
6. Renders correctly at 375px, 768px, 1280px.
7. Hero fits in one viewport on a laptop.
8. Page weight under 200KB excluding the GIF.

---

## 9. Deploy

```bash
git add index.html cv.pdf se3-demo.gif
git commit -m "update portfolio"
git push
```

Live at https://surajsingh108.github.io within about 60 seconds.

---

## Why these choices (research basis, June 2026)

- Recruiters spend 30 to 90 seconds on a portfolio and screen for deployed
  services, quantified impact, and clear architecture. Hence the hero, the proof
  strip, and outcome-first copy.
- Over 70% of open ML Engineer roles now require end-to-end and MLOps experience.
  SE3 is exactly that and is featured first with its pipeline made explicit.
- Stockholm holds about 64% of Sweden's AI roles, demand for senior ML/MLOps
  outstrips supply, and mid-to-senior is 57% of the market. The availability and
  "no sponsorship" lines target that demand directly.
- Generic, template-feeling, feature-listing copy makes recruiters close the tab.
  Hence the banned-words list and the outcome-first rule.
- Many recruiters browse on phones and share links in LinkedIn/Slack. Hence
  mobile-first testing and Open Graph tags.
