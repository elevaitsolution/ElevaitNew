# Elevait Homepage — Project Brief

## What this is

A rebuild of the homepage for Elevait, a B2B marketing agency based in Gurugram, India. Clients include Microsoft, Ingram Micro, Carrier, Faber Fränke (Italy), Nokia, Trilegal, Roadcast and SWIF. They serve India, the US, the UK and Europe.

The existing site (elevaitco.com) is a single long page with no navigation, built as a client-side rendered app. Two problems drive this rebuild: everything is crammed onto one page with no way to navigate, and the client-side rendering means AI crawlers see an empty shell.

This is currently a **design prototype for client approval**, not production.

## Stack — do not change this

- **One self-contained HTML file.** All CSS in a `<style>` block, all JS in a `<script>` block at the bottom.
- **No frameworks.** No React, no Tailwind, no build step, no npm.
- **No external dependencies** except the Google Fonts link.

This is deliberate. Elevait sells generative engine optimisation. Static HTML puts every word in the page source, so GPTBot and Perplexity can read all of it — which fixes the exact problem their current site has. Do not suggest converting this to a framework or splitting it into multiple files.

## Files

```
elevait/
  index.html          <- the site, single file
  index-backup.html   <- last known good version
  refs/               <- Figma exports for reference
  CLAUDE.md           <- this file
```

## Design system

All tokens live in `:root` at the top of the CSS. Change values there, never inline.

**Fonts — two only:**
- **Archivo** — all headings, buttons, client names, numbers
- **Manrope** — body copy, sub-lines, nav items, links, labels

Labels and eyebrows use Manrope at 12px, uppercase, 0.10em letter-spacing.

**Type scale:**
- Hero headline — CONFIRM IN FIGMA (screenshot suggests 64–72px; may be 48 if the export is 2x)
- Section headings — 48px
- Sub-headings — 28px
- Lead / sub-line — 20px
- Body — 16px
- Small — 14px
- Label — 12px

Nothing outside this scale.

**Colours** — exact values, do not substitute:

- `--bg` `#000724` page background
- `--surface` `#070B1C` alternating section bands
- `--surface2` `#0D1428` cards and image placeholders
- `--text` `#F9F9F9` primary text
- `--text-2` `#DEDEDE` secondary text, sub-lines, body
- `--text-3` `rgba(249,249,249,0.55)` labels, eyebrows, muted
- `--blue` `#273983` brand blue — fills and structural marks only, never text
- `--blue-text` `#E97A36` highlighted accent text on dark backgrounds
- `--cta` Primary Fill — see below
- `--cta-flat` `#FF8D28` small non-button orange marks (the Primary Fill start colour, flat)

### Primary Fill

Linear Gradient

- Start: `#FF8D28`
- End: `#BB5801`
- Usage: Primary CTA buttons, branded glyphs, interactive accents and selected decorative brand elements.
- Token: `--cta` — `linear-gradient(180deg, #FF8D28 0%, #BB5801 100%)`. Vector icons (`discovery`, `storytelling`, `growth`, `asterisk`, `quote`) carry the same two stops inside the SVG, since an `<img>` can't read CSS tokens.

> The Primary Fill gradient is the default orange treatment across Elevait. Do not use the previous red/orange gradient. Do not introduce alternate orange gradients unless explicitly specified.

**Colour rules:**

- `#273983` must never be used for text on the dark background — it fails WCAG contrast at 1.9:1. Any blue type uses `--blue-text`.
- The CTA gradient is for primary action buttons only.
- Primary CTA button labels are `#F9F9F9`. Dark labels fail contrast against the lower half of the gradient.
- Nothing outside this palette. No new colours, no additional opacity variants.

**Spacing scale:** 8, 16, 24, 32, 48, 64, 80, 96, 160. Never place a gap that isn't on this scale. Section padding is 150–160px top and bottom.

**Grid:** 1240px container, 12 columns, 24px gutters. Everything left-aligns to column one. Nothing is centred except the closing CTA block.

## Hard rules

1. **Containment rule.** Containers only for things you click into — case study cards, process steps, FAQ rows. Everything you only read has no container. The Approach columns get a 3px top rule and nothing else. Never nest a card inside a card inside a panel.

2. **The CTA gradient does one job.** `--cta` marks the primary action and nothing else. If something is not a primary action button, it does not carry the gradient. One primary action per view.

3. **No gradients** as decoration. Two gradients are permitted, both functional: `--cta` on primary action buttons, and the directional scrim over the hero image, dark on the left falling to clear on the right, for text legibility. Nowhere else.

4. **Flat planes.** Sections separate by changing background one step, not by borders, shadows or rounded panels.

5. **Space is the design.** If a section feels too sparse, that is usually correct. Do not add elements to fill space.

6. **Never invent data.** Client names, metrics and case study numbers must come from the user. If a number is needed and not supplied, use a visible placeholder like `XX%`.

## Locked copy

**Nav:** What we do (dropdown) · Work · Insights · About · Contact (button)

**Dropdown items:** Brand story · Demand generation · Web assets · Brand advocacy · Learning

**Hero H1:**
> Build the brand.
> Shape the story.
> Create the growth.

**Hero sub-line:**
> Elevait is a **B2B marketing agency** bringing strategy, creativity, digital and demand together around the business outcome that matters.

"B2B marketing agency" is bold — use a `<strong>` tag. Do not use markdown asterisks; they render as literal characters.

**Hero buttons:** Explore Our Work (primary, orange) · Talk to Us (secondary, outline)

## Homepage structure

In scroll order:

1. **Nav** — logo left, four items centred, Contact button right. Transparent over the hero, solidifies to the dark field on scroll.
2. **Hero** — full-bleed image with directional scrim, three-line headline overlaid left, one supporting line, two CTAs.
3. **Client logo strip** — at the base of the hero viewport, small eyebrow label, no heading, clients only. *Not yet built.*
4. **Approach** — split header (eyebrow left, statement right), then three numbered columns: Clarity, Demand, Adoption. Each carries its service links beneath.
5. **Process** — split header, four steps as an accordion on the left, image panel on the right that changes with the active step.
6. **Work** — horizontally scrolling rail of case study cards. Result number leads, client name follows.
7. **Learning** — image left, text right. The differentiator block.
8. **FAQ** — split layout, accordion.
9. **Closing CTA** — centred, one clear action.
10. **Footer** — four link columns, then a full-bleed wordmark.

## Technical copy rules

- Spell out "Generative Engine Optimization" in full at least once before using "GEO" — it collides with geography.
- One `<h1>` per page, in the hero. Every section heading is `<h2>`.
- Client logo images need alt text carrying the client name.

## How to work on this

- **One section at a time.** Always scope the request to a named section and leave everything else untouched.
- **Top to bottom.** Spacing reads against the section above it, so work in scroll order.
- **Within a section:** structure, then spacing, then type, then colour, then interaction. Do not tune hover states before the layout is settled.
- Do not refactor, reorganise or "tidy" code that wasn't part of the request.
- Do not split this file into multiple files.
- Do not introduce a CSS framework or a build step.

## Open decisions

Do not resolve these by guessing.

- **Hero headline size** — confirm in Figma.
- **CTA wording** — the nav says Contact, the hero primary says Explore Our Work, the secondary says Talk to Us. Three different labels, and the primary orange button currently routes to a portfolio rather than converting. Under review.
- **Client logo strip** — specced but not built. Decide whether it goes in.
- The three pillar names (Clarity / Demand / Adoption) are a recommendation, not approved.
- Case study metrics for Trilegal, Roadcast and SWIF are unverified and must be confirmed before use.
- Whether Microsoft and Carrier were direct engagements or partner work — affects whether they can appear in the client strip.
- Elevait's stated verticals (industrial, renewable tech, SaaS) do not match the documented case studies (telecom, healthtech, B2B tech, legal, logistics). Positioning decision pending.
