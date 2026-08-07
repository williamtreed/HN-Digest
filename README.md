# HN Onc Digest — Head & Neck Oncology Literature Digest

A recurring literature digest for a head & neck surgical oncologist, generated every ~2 weeks from PubMed and ClinicalTrials.gov. This repo contains the current state of the site — a small set of static, dependency-free HTML files.

## What's in here

- `HN_Onc_Digest_2026-08-06.html` — the current/live digest cycle. Interactive: each cited study is a collapsible `<details>` card with its own "Key conclusion" and "Counterpoint," section badges (Practice-changing / Hypothesis-generating / Background) are always visible, dark mode via `prefers-color-scheme`, and a print handler that force-expands everything for a clean tumor-board printout.
- `HN_Onc_Digest_2026-08-06.md` — the same content in plain markdown (no interactivity needed — this is the portable/fallback format).
- `HN_Onc_Digest_2026-08-03.html` — the first/baseline cycle (a ~12-month sweep), upgraded to the same interactive study-card and linked evidence-desk system as later cycles while preserving its original medical content and stable topic anchors.
- `index.html` — the archive hub. Lists every cycle newest-first with a short summary and links out. New cycles get prepended here.

Everything is self-contained: no build step, no external JS/CSS dependencies (safe to open directly in a browser or serve as-is from any static host).

## Design conventions to preserve

These are already baked into every digest's HTML/CSS and should be copied forward exactly for any new cycle, not reinvented:

- Each section (`<section id="...">`) uses a **stable topic-slug id** so links survive reordering across cycles: `perioperative-io`, `ctdna-mrd`, `neck-dissection`, `rt-deescalation`, `cutaneous-scc`, `systemic-pipeline`.
- "Last cycle" references in the prose are hyperlinked directly to the specific prior digest file + anchor (e.g. `HN_Onc_Digest_2026-08-03.html#neck-dissection`), not just re-cited by DOI — this lets the reader jump straight to what was said before.
- Every digest's `<body>` starts with a nav link back to `index.html`.
- CSS custom properties in `:root` (plus a `prefers-color-scheme: dark` override block) drive all theming — badge colors, links, callout borders, etc.

## What's done vs. what's still needed

**Done:** the digest content/format itself, the archive index, cross-cycle linking, and a recurring generation task (previously automated via a scheduled-task runner outside this repo — see "Recreating the automation" below).

**Not yet done — this is the reason for this export:** turning this into a real publicly-hosted website with a permanent URL (e.g. GitHub Pages). The original plan was:

1. Create a GitHub repo for this content.
2. Enable GitHub Pages (serve from the repo root or `/docs`, plain static HTML — no Jekyll processing needed, but Jekyll won't break anything either since none of these files use Liquid syntax).
3. Push these files.
4. Ideally, wire up the recurring digest generation (see below) to push new cycles to this repo automatically each time.

If you're picking this up in Codex: setting up the repo + Pages + pushing these files is the immediate task. A `git init` has already been done in this folder with one commit containing these files, so it's ready for `git remote add origin ...` and `git push`.

## Recreating the automation (optional, reference only)

The digest was generated on a recurring schedule by an agent with PubMed and ClinicalTrials.gov MCP tools. The exact task specification (search strategy, topic areas, voice/tone rules, required HTML structure, and a self-grading rubric) is included in `SCHEDULED_TASK_SPEC.md` in this folder, in case you want to reproduce equivalent automation (e.g. a GitHub Action, a cron job calling an LLM with search tools, etc.) in this new environment. It is not runnable code — it's a natural-language task prompt written for an LLM agent — but it documents every content/format requirement precisely.
