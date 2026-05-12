# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this project is

Static marketing site for **Targo Solutions** (ע.ש. תרגו פתרונות בע״מ) — a Hebrew B2B operations / supply-chain consultancy serving MedTech, Defense, HiTech, and Industry. The site is two pages: a Home and an About page. Both are hand-authored HTML with inline `<style>` and inline `<script>` — no build step, no framework, no package manager, no tests.

End goal: the static HTML will be **ported to basic Elementor widgets** on a WordPress site at targosolutions.com. Treat the HTML as the design source of truth; Elementor is the eventual delivery target.

## Source files

- The two source HTML pages were delivered by the founder via chat attachment (`targo-updated (1).html` = home, `targo-about-v2 (2).html` = about). They are the canonical content. **They are not yet committed to this repo as files** — the founder may resend updated versions. When working, reference them from the chat attachments.
- `DESIGN.md` is the extracted design system (palette, typography, components, do/don't, agent prompt guide). It follows the [awesome-design-md / Stitch DESIGN.md methodology](https://github.com/VoltAgent/awesome-design-md). **Read DESIGN.md before generating or modifying any UI.**

## Working rules specific to Targo

- **Language is Hebrew, direction is RTL.** All HTML must declare `lang="he" dir="rtl"`. Hairline accents anchor to the right edge (`border-right`, scaleX origin `right`), eyebrow `::before` lines flow right→left.
- **Brand is zero-radius.** Buttons, cards, inputs, badges all have sharp 90° corners. The two documented exceptions live in DESIGN.md §6.
- **Every section title contains exactly one italicized `<em>` word in `gold-light` at weight 300.** This is the brand's typographic signature. Headlines without it read as off-brand.
- **One filled CTA per section, max.** `.btn-gold` (or `.btn-white` on gold surfaces).
- **No gradients, no stock photos, no semantic-color states (red errors / green success).** State is communicated by copy weight and gold accents.
- **Section surfaces alternate** `dark` → `cream` → `warm` → `dark` ... Two adjacent sections never share a surface.
- **Heebo is the only typeface.** Weights 200/300/400/500/600/700/800 from Google Fonts.
- **Mobile breakpoint is a single threshold at 900px.** No tablet tier.

## Encoding gotcha

When the HTML source is pasted into a chat attachment, Hebrew may arrive as mojibake (UTF-8 bytes interpreted as Latin-1, e.g. `××××`). Do not copy the mojibake into a saved file — ask the founder to resend as an actual file or paste fresh Hebrew. The original site files are valid UTF-8.

## When generating new pages or sections

1. Read `DESIGN.md` end-to-end.
2. Pick a surface that contrasts with the previous section (`dark` ↔ `cream`/`warm`).
3. Open with an `.eyebrow` (gold, 0.3em letter-spacing, with the 1.5rem hairline `::before`).
4. Title uses the `<em>` italic-gold-light pattern.
5. Use the existing component vocabulary in DESIGN.md §7 — do not invent new patterns silently. If a new pattern is genuinely needed, document it in DESIGN.md before shipping.

## When porting to Elementor

See DESIGN.md §10 "When converting to Elementor widgets." Key points:
- Register the 8 palette colors as Elementor **Global Colors**.
- Register the type tokens as **Global Fonts**.
- The hover scaleX gold bar (DESIGN.md §5) requires per-widget Custom CSS — Elementor's built-in hover presets won't replicate it.
- Avoid Elementor's grow/shrink/float hover animations — they contradict the flat-sharp brand logic.

## No build / lint / test

There is no build, lint, type-check, or test command. Open the HTML in a browser to preview. If a dev server is needed for live reload while editing, any static server works (`python -m http.server`, VS Code Live Server, etc.).
