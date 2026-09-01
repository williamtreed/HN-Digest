# HN Onc Digest — Head & Neck Oncology Literature Digest

A recurring literature digest for a head & neck surgical oncologist, generated every two weeks from PubMed and ClinicalTrials.gov, with an off-cycle update reserved for a genuinely practice-changing phase III result, safety signal, regulatory action, or major guideline change. This repo contains the current state of the site — a small set of static, dependency-free HTML files.

## What's in here

- `HN_Onc_Digest_2026-08-31.html` — the current/live digest cycle. Its 17 findings are all new DOI/NCT records relative to the August 6 cycle. Each is a native `<details>` card with its own "Key conclusion," "Counterpoint," and article-specific digest covering scope, methods or argument, results, interpretation, limitations, and provenance. Wide screens turn that source into a dated evidence map and reader, with section/finding navigation, persistent reviewed state, next-unread navigation, and copy controls. A persistent `Aa` palette adds System, Light, Sepia, and Dark reading themes plus four text-size steps. Mobile inline expansion and a fully-expanded tumor-board printout remain built in.
- `HN_Onc_Digest_2026-08-31.md` — the same content in plain markdown (no interactivity needed — this is the portable/fallback format).
- `HN_Onc_Digest_2026-08-06.html` / `.md` — the prior incremental cycle, retained unchanged in the archive.
- `HN_Onc_Digest_2026-08-03.html` / `.md` — the first/baseline cycle (a ~12-month sweep), upgraded to the same article-specific evidence depth and interactive navigator/reader system as later cycles while preserving its stable topic anchors.
- `index.html` — the archive hub. Lists every cycle newest-first with a short summary and links out. New cycles get prepended here.

There is no build step and no external JavaScript or CSS dependency. The pages can be opened directly or served from any static host. A licensed article figure may load from its official source repository; the surrounding analysis and all interaction logic remain in the HTML.

## Design conventions to preserve

These are already baked into every digest's HTML/CSS and should be copied forward exactly for any new cycle, not reinvented:

- Each section (`<section id="...">`) uses a **stable topic-slug id** so links survive reordering across cycles: `perioperative-io`, `ctdna-mrd`, `neck-dissection`, `rt-deescalation`, `cutaneous-scc`, `systemic-pipeline`. These IDs are infrastructure only; visible section and navigator titles must describe that cycle's actual new evidence rather than repeat generic category names.
- "Last cycle" references in the prose are hyperlinked directly to the specific prior digest file + anchor (e.g. `HN_Onc_Digest_2026-08-03.html#neck-dissection`), not just re-cited by DOI — this lets the reader jump straight to what was said before.
- Every digest's `<body>` starts with a nav link back to `index.html`.
- CSS custom properties in `:root` drive all theming — badge colors, links, callout borders, reader type size, etc. The `Aa` palette sets the same variables for System, Light, Sepia, and Dark modes, with four text-size levels. Hyperlinks use a distinctly chromatic theme-specific color, medium weight, and a persistent 1.5px underline that strengthens on hover; do not revert to color-only link identification.
- At 1320px and above, every cycle uses the same master-detail workspace: a roughly one-third-width Digest navigator on the left and a two-thirds reader on the right. Both are generated at runtime from the hidden native digest source; mobile and print expose that original source directly. Local browser storage contains only stable reviewed-reference IDs and the reader's appearance choice; it never contains medical content, browsing history, or notes.
- Give every finding an `.evidence-brief` whose depth is proportional to the source. A primary study should expose design, population, endpoints, exact results, clinical interpretation, and limitations. A commentary, guideline, review, or registry-only item should instead explain its scope, argument or protocol, what it adds, and what it cannot establish. Label provenance honestly (`Full text`, `Structured abstract`, `Commentary`, `Consensus guideline`, or `Live registry`), distinguish digest-generated charts from publisher figures, and never imply paywalled content was reviewed in full. Reuse an article image only when its license explicitly permits it; link the original, preserve the figure unchanged, and put the article attribution and license in the caption. Otherwise summarize the data in an original table/chart and link out to the publisher's figure.

## What's done vs. what's still needed

**Done:** the interactive digest format, archive index, cross-cycle linking, GitHub repository, and public GitHub Pages deployment at `https://williamtreed.github.io/HN-Digest/`.

**Cadence:** every two weeks is the active default. This is frequent enough to catch time-sensitive papers and trial changes without becoming a general news feed, provided quiet cycles stay short instead of being padded. Search from the prior cycle's cutoff through the current run date; publish an off-cycle update only when waiting would delay a meaningful tumor-board or clinical decision. A rolling three-cycle coverage audit broadens the search across surgical oncology, reconstruction/function, surveillance, radiation, and systemic therapy without imposing artificial topic quotas.

**Automation:** an active local Codex scheduler runs every other Monday at 7:00 AM Eastern, researches the interval, creates both digest formats, updates the archive, validates the result, and publishes it to GitHub Pages. The current biweekly task specification is preserved below.

## Recreating the automation (optional, reference only)

The digest is generated on a recurring schedule by an agent with PubMed and ClinicalTrials.gov search access. The current task specification (biweekly search strategy, off-cycle threshold, topic areas, voice/tone rules, required HTML structure, and a self-grading rubric) is included in `SCHEDULED_TASK_SPEC.md` in this folder, in case you want to reproduce equivalent automation elsewhere. It is not runnable code — it's a natural-language task prompt written for an LLM agent — but it documents every content/format requirement precisely.
