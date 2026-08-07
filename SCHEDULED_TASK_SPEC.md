# Original recurring-task specification (reference only)

This is the exact natural-language task prompt that was run on a recurring schedule (every 14 days) by an LLM agent with PubMed and ClinicalTrials.gov MCP tools plus file read/write access to this folder. It's included verbatim as a reference for reproducing equivalent automation elsewhere — it is not executable code.

---

You are producing a recurring literature digest for a head & neck surgical oncologist who wants to stay current on emerging trends across surgical, medical, and radiation oncology literature in head & neck cancer (HNSCC, cutaneous SCC of the head/neck, HPV-associated disease).

## What this digest is for — read before each run

This is not a newsletter for its own sake. Its job is to let a busy surgeon spend 3-5 minutes scanning bottom lines, then optionally go deeper on exactly the studies that matter to a specific patient or tumor-board discussion, and trust that nothing practice-relevant was missed or overstated. Before presenting each cycle, self-grade against this rubric and fix anything that fails:

1. **Signal-to-noise** — every item earns its place by being genuinely new, genuinely HNSCC-relevant, and genuinely surgically-actionable-or-important. If a cycle is quiet, say so in Highlights rather than padding.
2. **Trust** — every claim has a real DOI/NCT link from an actual search result; every counterpoint is real (sample size, funding, study design, contradicting data), not manufactured; dosing/numeric claims are double-checked against the source abstract, not paraphrased from memory (a dosing-direction error was caught and fixed in the Aug 6 cycle — re-verify numbers like this every time).
3. **Frictionless depth** — the surgeon can get the bottom line without tapping anything, and can get the full study-level nuance (key conclusion + counterpoint) in one tap, per the Interactivity spec below.
4. **Continuity** — references to "last cycle's X" are live links to the exact prior digest section, not vague callbacks the reader has to hunt for.
5. **Durability under repetition** — the format, CSS, and interaction pattern are copied forward unchanged cycle to cycle (see "Design boilerplate" below) so the reader never has to re-learn how to use it, and so it doesn't require manual re-polishing every run.
6. **Portable fallback** — the .md file stands alone and is fully readable with zero interactivity, for anyone who can't/won't open the HTML.

Every HTML digest in the archive uses the same interactive standard, including the baseline cycle. Do not create or retain a simplified non-interactive HTML variant for an archived cycle.

## Output location — IMPORTANT

Write output files into a folder shared across the user's devices (originally: an `HN Onc Digest` subfolder inside the user's iCloud Drive, so it synced automatically to their iPhone's Files app). Also check that same folder for prior digest files (`HN_Onc_Digest_*.md` / `.html`) and `index.html` to avoid duplicating content already covered — read the most recent `.html` file first to copy its CSS/markup patterns exactly, and read `index.html` to see the full archive history.

## What to do

1. Search for literature published in roughly the last 14-21 days. Prioritize major journals: J Clin Oncol, JAMA Oncology, JAMA Otolaryngology-Head & Neck Surgery, Laryngoscope, Lancet, Lancet Oncology, NEJM, Int J Radiat Oncol Biol Phys, Head & Neck, Oral Oncology, Ann Surg Oncol, Clin Cancer Res, Annals of Oncology.

2. Cover these topic areas, running separate targeted searches for each:
   - Perioperative/adjuvant/neoadjuvant immunotherapy in resectable HNSCC (follow-on data, commentary, and rebuttals related to KEYNOTE-689 and NIVOPOST-OP/GORTEC 2018-01 specifically — these are the two landmark trials the user follows closely)
   - Cutaneous squamous cell carcinoma immunotherapy (cemiplimab, C-POST trial and related)
   - Circulating tumor DNA / molecular residual disease (ctDNA/MRD) in HNSCC — both biology/validation papers and ctDNA-adapted trial designs
   - Surgical de-escalation and technique advances (neck dissection extent, TORS, sentinel node, reconstruction)
   - Radiation de-escalation / dose de-intensification in HPV+ oropharyngeal cancer, and other radiation oncology advances
   - Novel systemic/targeted agents in recurrent-metastatic HNSCC (e.g., petosemtamab, ficerafusp alfa, other EGFR-directed or bispecific agents, therapeutic HPV vaccines)
   - Any other practice-changing phase III readouts in HNSCC

3. Also search ClinicalTrials.gov for newly registered or recently updated HNSCC trials involving ctDNA, novel immunotherapy combinations, or de-escalation, status RECRUITING/NOT_YET_RECRUITING/ACTIVE_NOT_RECRUITING.

4. Skip anything not genuinely about head & neck cancer. It's fine to note follow-up developments on a prior story, but don't re-summarize the same finding from scratch — link back to it instead.

5. Double-check any specific numeric claim (dose levels, percentages, hazard ratios) against the actual abstract/source before writing it. Read your own draft once specifically hunting for numbers that could be backwards or mismatched before finalizing.

## Voice and audience

The reader is a **head & neck surgical oncologist**, not a medical oncologist or general researcher. Write every entry from that vantage point: does this change who you operate on, how much tissue/nodal basin you take, when you operate relative to systemic therapy, what you tell a patient in clinic, or what replaces a scan in surveillance. Data and stats support that bottom line — they don't lead it. Minimize medical-oncology-only minutiae unless directly relevant to a surgical decision. Organize sections around surgical decision points where possible.

## Required content structure

1. **Header block**: window covered, sources, PubMed attribution line, a one-line "how to read this" key, a tap-hint, and a note on cadence relative to the prior cycle.
2. **"Highlights — key takeaways"**: a short bulleted TL;DR (3-6 bullets) of the biggest things that happened this cycle, at the very top, each clickable to jump to its section. If nothing significant happened this cycle, say so plainly rather than padding it.
3. **Numbered topic sections**, each organized around a surgical decision point. Each section has:
   - A reference-count pill next to the heading (e.g. "4 studies").
   - A section-level badge (**Practice-changing**, **Hypothesis-generating**, or **Background**) plus one bolded **Bottom line** sentence written from the surgeon's vantage point, always visible.
   - A list of individual supporting references (1-3 sentences of data each, with DOI/NCT link) — see "Interactivity" below.
   - A section-level **Counterpoint** callout wherever the evidence is genuinely contested, underpowered, retrospective, or has a credible opposing interpretation.
   - A section-level **Go deeper** callout naming the single best review or most rigorous primary source.
4. **"Bottom line for tumor board"**: closing synthesis paragraph tying the cycle's findings together.

## Interactivity — the current standard format

- Each individual reference/finding within a section body-list is its own `<details class="ref">` accordion (collapsed by default): the `<summary>` shows the 1-3 sentence data summary, and expanding it reveals a `<div class="ref-detail">` containing:
  - `<span class="tag">Key conclusion —</span>` a synthesized 1-2 sentence takeaway specific to that study.
  - `<span class="tag warn">Counterpoint —</span>` a caveat specific to that study (sample size, retrospective design, single-center, funding source, methodological limitation) — omit only if the reference is a trial-registry note with nothing to critique yet.
  - A `<p class="ref-link">` with the DOI link (or ClinicalTrials.gov link for trials without a DOI).
- The section-level badge/bottom-line and section-level Counterpoint/Go-deeper callouts stay always-visible — only individual references collapse/expand.
- The Highlights bullets at the top are clickable (`onclick="openSection('topic-slug')"`) and scroll to the relevant stable topic-slug section id.
- A top-of-page pill nav (`.toc`) lists all sections for quick jumping, plus an "Expand all / Collapse all" toggle.
- At 1320px and above, the page progressively enhances into a two-pane reading workspace: an approximately 840px digest column and a 380-420px sticky **Study desk**. Below 1320px, hide the desk and use native inline `<details>` expansion with no horizontal squeeze.
- The Study desk opens on a generated **Cycle outline**, not an empty state. It must provide: per-section reviewed/total counts and mini progress bars; an overall progress bar; full-cycle search across summaries, conclusions, caveats, and source text; Next unread; and Reset progress. Search filters both the left-side findings/sections and the generated outline, but search text is intentionally not persisted.
- Selecting a reference marks it reviewed, visually marks its source card, and switches to the **Evidence** tab. The evidence view clones the reference summary and `.ref-detail`, adds the section bottom line for context, and keeps Previous, Next, Mark unread/reviewed, and Copy finding controls pinned below the scrollable evidence content. Next unread respects an active search filter.
- Persist only stable reviewed reference IDs in `localStorage`, keyed by digest title. Storage failures (including restrictive local-file contexts) must fail silently while retaining in-session behavior. Never store medical content, searches, browsing history, or user-authored notes.
- Do not maintain a second copy of study content in the HTML; the Study desk and outline must always derive from the existing sections and `<details class="ref">` nodes so the inline digest remains the single source of truth.
- Native `<details>` remains the required foundation and fallback. On wide screens, "Expand all" switches to inline-expanded mode. The Study desk is hidden on smaller screens and in print. Pressing `/` focuses cycle search; Escape clears an active search or returns to the outline.

## Design boilerplate — copy forward exactly, don't reinvent each cycle

Read the most recent prior `HN_Onc_Digest_*.html` file first and copy its exact `<style>` block and structure, including:
- **Editorial/clinical-journal visual system**: dependency-free Charter/Bitstream Charter/Sitka Text/Cambria/Georgia fallback stack for the page title, section headings, bottom lines, and Study desk prose; system sans-serif for body text and UI chrome. Use the six-step type hierarchy already defined in the current file rather than inventing per-element sizes.
- **Layout**: page max-width 1500px with 40px desktop gutters; an up-to-840px primary reading column and a 380-420px Study desk separated by a 32-56px gap. At 1319px and below, collapse to one column with an 880px maximum reading width. At 640px and below, use 18px gutters and the compact mobile rhythm.
- **Palette/tokens**: copy all current `:root` variables exactly. Light mode uses ink `#17212b`, deep editorial blue `#174f78`, link blue `#155a87`, off-white canvas `#fcfcfb`, and cool gray surfaces/borders. Practice-changing uses the blue-tinted `--success-*` pair; hypothesis-generating uses muted amber `--warning-*`; background stays neutral. Section counterpoints use a restrained warm tint; Go deeper uses a cool blue tint.
- **Spacing and hierarchy**: base spacing is drawn from 4/8/12/16/24/32/48px. Sections use 48px vertical padding and a stronger divider; the bottom line is 17px semibold serif; badges and count pills are compact uppercase UI labels. Highlights and the Study desk use the shared restrained shadow token.
- **Reference cards**: 9px radius, quiet border/shadow, one-pixel lift on hover, blue active state, 15-16px internal padding, rotating chevron, and a short reveal animation. Key conclusion and Counterpoint paragraphs use distinct blue and amber left rules. Preserve `prefers-reduced-motion` handling.
- **Wide-screen Study desk**: include the `.reading-layout`, `.digest-content`, and `.evidence-pane` structure plus the complete current outline/evidence tab system. Copy the current JavaScript state model exactly: stable derived reference IDs, guarded persistence, search/filter restoration for print, progress rendering, next-unread behavior, evidence navigation, copy handling, and responsive fallback.
- **Dark mode**: `<meta name="color-scheme" content="light dark">` plus a `@media (prefers-color-scheme: dark)` block redefining the `:root` variables.
- **Print support**: `beforeprint`/`afterprint` listeners temporarily clear search filters, force all `details.ref` open, and then restore the prior search/open state; the `@media print` block hides the Study desk and other screen-only chrome.
- **Section-jump pill nav**: sticky and full-width on desktop, inline/non-sticky on mobile, with expand-all/collapse-all.
- **Reference-count pill** per section heading.
- The `openSection()` scroll helper.

## Cross-linking to prior cycles

Give each section a stable topic-slug id (see canonical list in README.md). Whenever the digest references a finding from a prior cycle, hyperlink that phrase directly to the specific prior digest file + anchor (e.g. `HN_Onc_Digest_2026-08-03.html#neck-dissection`) — never just re-cite the DOI again for these. Find the actual filename/anchor by reading the prior file(s) first; never guess.

## Archive

Every digest HTML file's `<body>` starts with: `<p class="archive-nav"><a href="index.html">← All digests (archive)</a></p>`. Maintain `index.html` as a running archive — read it first, prepend a new `.entry` card at the top (date, 2-4 sentence summary, links to the new `.html`/`.md`), leave prior entries untouched, match existing CSS exactly.

## Output — up to three files per run

1. `HN_Onc_Digest_YYYY-MM-DD.md` — plain markdown, portable fallback.
2. `HN_Onc_Digest_YYYY-MM-DD.html` — full interactive version per the sections above.
3. `index.html` — updated per "Archive" above.

Per PubMed's attribution requirement, note "According to PubMed" near the top of the .md and .html files and include DOI links for every cited article. If a cycle turns up very little new material, say so plainly rather than padding it.

## Verification before presenting

Confirm HTML tag balance (section/div/ul/li/details/summary open vs. close counts match), confirm every cross-cycle link points to a real anchor id actually seen in the target file, and re-scan numeric claims against source abstracts.
