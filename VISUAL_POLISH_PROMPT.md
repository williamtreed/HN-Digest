# Visual polish pass — prompt for iteration

Use this as the brief for a coding agent (Codex, Claude, etc.) doing a visual refinement pass on the HN Onc Digest site. Paste it in as-is, or edit the bracketed assumptions first.

---

## Brief

This is a recurring literature digest built as static, dependency-free HTML files (see `README.md` in this repo for full context). The content, information architecture, and interactivity are final and should not change. This pass is purely visual: typography, spacing, color, hierarchy, and polish.

**Direction: editorial / clinical-journal.** Think the digital reading experience of NEJM, JAMA, or a well-typeset Stripe docs page — restrained, confident, trustworthy. Not flashy, not "startup dashboard." The reader is a physician scanning this in a spare few minutes; it should feel calm and authoritative, not busy.

**Scope: refinement, not redesign.** Keep the existing structure exactly as-is: header block, clickable Highlights list, numbered sections with badge + bottom-line + expandable per-study reference cards + section callouts, closing synthesis, footer. Do not change the interaction model (the `<details>`-based expand/collapse, the section-jump nav, dark mode, print handling, cross-cycle linking) — only how it looks.

**Primary viewing context: desktop browser.** Optimize the layout for a comfortable desktop reading width first — the current `max-width: 760px` container was tuned for mobile-first and may feel cramped or under-designed on a larger screen. It still needs to degrade gracefully on mobile (this is also opened via iPhone Files app / Safari), but desktop polish is the priority for this pass.

## Specific things to improve

1. **Typography.** The current version uses a plain system sans-serif stack throughout, which reads as functional but generic. Try a considered pairing — e.g. a serif or high-quality slab for headings/section titles (something in the Source Serif / Charter / Georgia / STIX family, or a Google Fonts equivalent loaded via a single self-hosted `@font-face` or system-safe fallback stack — no external CDN calls, this file must stay dependency-free) paired with a clean sans for body text and UI chrome. Tighten up type scale, line-height, and measure (character-per-line) for the prose paragraphs — right now everything shares one font at similar weights with not much hierarchy beyond size.

2. **Color.** The current palette is a neutral warm-gray with a single blue link/badge color, functional but flat. Consider a slightly more considered, muted palette — a refined accent color (deep blue, forest, oxblood, or similar "journal" tone) used sparingly for links and the "Practice-changing" badge, with the other two badge states (Hypothesis-generating, Background) staying muted/desaturated so the eye is drawn to what matters. Preserve full dark-mode parity — every new color needs a dark-mode counterpart in the existing `@media (prefers-color-scheme: dark)` block.

3. **Hierarchy and rhythm.** Increase visual distinction between: page title vs. section titles vs. study-reference summaries vs. body prose. Section dividers, spacing before/after callouts, and the badge/bottom-line pairing at the top of each section could all be tightened into a clearer visual rhythm — right now sections are somewhat visually flat (similar weight throughout).

4. **The expandable reference cards** (`details.ref`) are the core interaction — give them a bit more visual craft: refined hover/focus states, a slightly more elegant expand transition (currently instant), better visual separation between the "Key conclusion" and "Counterpoint" lines inside an expanded card (right now they're both just bold-tagged paragraphs — consider distinct treatment, e.g. a subtle left-border accent or icon per tag type).

5. **Callouts** (section Counterpoint / Go deeper) currently use a plain left-border block. Consider a more refined treatment — subtle background tint, better icon/label treatment — while keeping them clearly secondary to the main bottom-line.

6. **Desktop layout.** Consider whether a wider reading column (e.g. ~820-900px) with slightly larger type serves desktop better than the current mobile-tuned 760px, and whether the section-jump pill nav could become a lightweight sticky sidebar or top bar on wide viewports (progressive enhancement — mobile keeps the current inline pill row).

7. **Micro-details:** badge shape/weight, the chevron rotation on expand, the count-pill styling, footer treatment — these are all currently serviceable but not refined. Sweat them.

## Hard constraints — do not break these

- Must remain a single self-contained HTML file per digest: inline `<style>`, no external JS/CSS/font CDN dependencies (must open correctly from the iPhone Files app / offline).
- Must preserve: dark mode (`prefers-color-scheme`), the print handler (`beforeprint`/`afterprint` force-expand), the section-jump nav + expand-all/collapse-all control, all stable section anchor IDs (`perioperative-io`, `ctdna-mrd`, `neck-dissection`, `rt-deescalation`, `cutaneous-scc`, `systemic-pipeline`), and every existing cross-file link (`href="HN_Onc_Digest_2026-08-03.html#..."` etc.) — don't rename anchors or break links between files.
- Apply the new design system consistently to `HN_Onc_Digest_2026-08-06.html` and `index.html`. Leave `HN_Onc_Digest_2026-08-03.html` (the archived first cycle) untouched — it's a deliberate historical snapshot, not upgraded to newer visual patterns.
- Once finalized, update `SCHEDULED_TASK_SPEC.md`'s "Design boilerplate" section to describe the new visual system precisely enough that future digest cycles can copy it forward exactly, the same way the current one documents the existing system.

## Process

Iterate — don't try to nail it in one shot. Propose one direction, show it (screenshot or describe the rendered result), and take feedback before expanding it across every section. Sweat the details that compound: type scale, spacing scale, and color usage should all come from a small consistent system (e.g. a spacing scale of 4/8/12/16/24/32/48px, a type scale of maybe 5-6 sizes) rather than one-off values per element.

---

## Assumptions made / fill in if you want a tighter brief

- **Accent color:** not specified — the agent should propose 2-3 options rather than guess. If you have a color in mind (or a hex code), state it.
- **Font pairing:** described directionally (serif headline + sans body) but not prescribed — if you have fonts in mind, name them.
- **Reference sites/screenshots:** none provided. If there's a specific site or app whose typography/spacing you want mimicked, link it or attach a screenshot — this is the single highest-leverage thing you could add to this brief.
- **Current pain points:** not specified beyond "not refined" — if particular elements bother you right now (e.g. "the badges look cheap," "too much whitespace," "hard to scan"), naming them directly will save iteration cycles.
- **Logo/branding:** none assumed. If this should carry any personal or institutional branding (name, initials, a small mark in the header), say so.
