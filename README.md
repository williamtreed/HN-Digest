# HN Onc Digest — Head & Neck Oncology Literature Digest

A recurring literature digest for a head & neck surgical oncologist, generated every ~2 weeks from PubMed and ClinicalTrials.gov. This repo contains the current state of the site — a small set of static, dependency-free HTML files.

## What's in here

- `HN_Onc_Digest_2026-08-06.html` — the current/live digest cycle. Each cited study is a native `<details>` card with its own "Key conclusion" and "Counterpoint." Wide screens add a full Study desk with cycle search, section progress, persistent reviewed state, next-unread navigation, focused evidence reading, and copy controls. Dark mode, mobile inline expansion, and a fully-expanded tumor-board printout remain built in.
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
- At 1320px and above, every cycle uses the same two-pane reading workspace. The wider left-side Study desk is derived from the native reference cards, while the digest remains visible on the right for context. It stores only reviewed reference IDs in local browser storage and never duplicates or alters medical content.

## What's done vs. what's still needed

**Done:** the interactive digest format, archive index, cross-cycle linking, GitHub repository, and public GitHub Pages deployment at `https://williamtreed.github.io/HN-Digest/`.

**Still optional:** recreate the recurring generation task so each new cycle is researched, generated, committed, and published automatically. The exact prior task specification is preserved below.

## Recreating the automation (optional, reference only)

The digest was generated on a recurring schedule by an agent with PubMed and ClinicalTrials.gov MCP tools. The exact task specification (search strategy, topic areas, voice/tone rules, required HTML structure, and a self-grading rubric) is included in `SCHEDULED_TASK_SPEC.md` in this folder, in case you want to reproduce equivalent automation (e.g. a GitHub Action, a cron job calling an LLM with search tools, etc.) in this new environment. It is not runnable code — it's a natural-language task prompt written for an LLM agent — but it documents every content/format requirement precisely.
