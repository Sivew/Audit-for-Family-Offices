---
file: visual_prompts
purpose: AI image generator prompts for every visual asset the audit project needs
style_system: SynexumLabs navy + cyan — same as deck, case studies, and setter script
---

# Visual Prompts

Every visual asset the audit project needs — landing page hero, OG share image, email headers, report cover, and quiz section backgrounds. Each prompt is paste-ready for Midjourney, DALL-E, Ideogram, or Adobe Firefly.

Shared brand constraints apply to every prompt:
- **Primary colour:** dark navy (#031B4E to #0B1220 gradient)
- **Accent:** bright cyan (#35D1FF)
- **Supporting:** light cyan tint (#ECF5FB), soft grey (#64748B)
- **No photorealistic faces or hands**
- **No real company logos**
- **No stock-photo aesthetic**

---

## V01 — Landing page hero image

**Purpose:** Dominant visual at the top of the audit landing page. Signals institutional seriousness.

```
A minimalist editorial illustration of an institutional-grade digital workspace,
rendered in a dark navy palette with bright cyan accents. Centre: an abstract
representation of a locked, sovereign data vault — a geometric shield motif
intersected by subtle data-flow lines in cyan. The vault sits inside a soft
glowing perimeter that reads as "protected environment." Behind it, faint
grid lines and abstract document silhouettes suggest the volume of family office
data being governed. Clean Swiss-design composition. Negative space on the right
third for text overlay. Minimal, institutional, premium — Monocle magazine
aesthetic meets high-end fintech brand. Dark navy #031B4E background,
cyan #35D1FF accents, no photorealistic elements, no text in the image.

Style tags: editorial illustration, Swiss design, minimal, premium fintech,
Monocle magazine aesthetic, flat vector, 4K
```

**Aspect ratio:** 16:9 (desktop) + 4:5 crop (mobile)
**Where it appears:** Hero section of `02_Landing_Page.md`

---

## V02 — OG / social share image

**Purpose:** Image shown when the audit URL is shared on LinkedIn, email, Slack, etc. Must be legible at 1200×630.

```
A clean, bold editorial card for a professional service announcement. Dark navy
background with a subtle cyan accent line across the top. Centre composition:
large white serif-sans typography reading "The Family Office Operational
Readiness Audit" (this text should be rendered in the image, large and clean).
Beneath it, smaller cyan text reads "A private 10-minute diagnostic — SynexumLabs."
On the right third, a subtle geometric vault/shield motif in cyan. Clean margins,
premium feel, no stock imagery. 1200×630 for OG share use.

Style tags: OG card, LinkedIn preview, editorial, premium fintech, clean typography,
Swiss design
```

**Aspect ratio:** 1200×630 (fixed — this is the OG spec)
**Where it appears:** HTML `<meta property="og:image">` tag

**Tool note:** Ideogram handles the text rendering best for this one.

---

## V03 — Quiz section background (subtle)

**Purpose:** Faint background pattern inside the quiz UI — not a hero, just enough to signal brand continuity.

```
A very subtle, barely-visible background pattern for an institutional web form.
Dark navy base (#031B4E), with faint geometric grid lines in a slightly
lighter navy (#0B2A5B) — only 10–15% opacity against the base. One or two
tiny cyan accent dots placed as compositional anchors. The pattern must feel
quiet, not decorative. Nothing eye-catching — the respondent's attention
should stay on the question. 100% tileable or seamless at 1920×1080.

Style tags: subtle background, barely visible pattern, institutional,
geometric minimal, dark navy, Swiss design
```

**Aspect ratio:** 1920×1080, seamless tile
**Where it appears:** Background behind all question screens

---

## V04 — Report cover illustration

**Purpose:** The visual element on Page 1 of the audit PDF report. Signals that the respondent is holding something crafted, not auto-generated.

```
A refined editorial illustration for the cover of a confidential institutional
audit report. Dark navy page background. Centre-right: an abstract composition
of a sovereign data perimeter — a geometric shield motif enclosing stylised
document icons, data-flow lines, and a small subtle vault icon. The entire
composition is enclosed in a hairline cyan border that reads as "sealed envelope"
without being literal. On the left third of the composition, generous negative
space where the report title and recipient name will be overlaid in editing.
Visual quality: Economist cover meets high-end financial-services brand.
Clean lines, no texture, no photo-realism, no human figures.

Style tags: editorial cover illustration, confidential document, premium
institutional, Economist cover aesthetic, Swiss design, flat vector, 4K
```

**Aspect ratio:** 8.5×11 portrait (US Letter cover)
**Where it appears:** Page 1 of generated audit PDFs

---

## V05 — Email header banner

**Purpose:** Banner at the top of each email in the three-step sequence. Subtle enough that it doesn't dominate the inbox preview, strong enough to carry brand recognition.

```
A horizontal brand banner for a professional email header, 600 pixels wide,
120 pixels tall. Dark navy background (#031B4E) with a single bright cyan
accent line (#35D1FF) spanning the bottom edge. Centred vertically: the text
"SYNEXUM LABS" in clean sans-serif, white, uppercase, with letter-spacing.
To its right, in cyan italic, a single line reading "Strategy That Ships."
Maximum restraint. No illustrations, no icons, just the typography and the
cyan accent line. Must look identical on light-mode and dark-mode email clients.

Style tags: email header banner, clean typography, brand bar, minimal,
professional, no illustration
```

**Aspect ratio:** 600×120 pixels (fixed — email standard)
**Where it appears:** Top of all three sequence emails

---

## V06 — Priority matrix background (Page 4 of report)

**Purpose:** The 2×2 grid behind the priority-matrix findings. Must be visually anchored but not visually noisy — the respondent's three dots are what matter.

```
A clean 2x2 strategic matrix grid for a business report. Two perpendicular
axes, light cyan lines, intersecting at the centre. Four quadrants defined by
soft background tints: upper-left quadrant has a very subtle cyan-tinted
background (#ECF5FB at 50% opacity) to indicate "start here"; the other three
quadrants are neutral white or very light grey. Axis labels in small uppercase
grey text at the extremes: "HIGH IMPACT" / "LOW IMPACT" vertically,
"LOW EFFORT" / "HIGH EFFORT" horizontally. No decoration beyond the lines
and the quadrant tint. Clean, functional, premium business report aesthetic.
Transparent background outside the grid area so it can overlay cleanly.

Style tags: 2x2 matrix, strategic framework, business report, clean minimal,
Swiss design, functional illustration
```

**Aspect ratio:** Square, 1000×1000
**Where it appears:** Page 4 of the generated report PDF

---

## V07 — "Thank you" page illustration

**Purpose:** Companion visual on the post-submission screen. Reassures the respondent that something is actually happening behind the scenes.

```
A quiet editorial illustration representing "your request is being prepared."
Dark navy background. Centre: a subtle animated-looking (but static) composition
of three concentric circles in cyan, suggesting activity without being
cartoonish. Inside the innermost circle, a small abstract document icon. Light
cyan particles or dots arranged around the composition to suggest motion /
processing. Highly restrained, premium feel. No cartoon elements, no human
figures, no literal clocks or spinners. Must read as "institutional-grade work
is happening" rather than "loading."

Style tags: processing visualisation, premium, institutional, Swiss design,
restrained motion, flat vector
```

**Aspect ratio:** 16:9 or square, flexible — 1200×1200 is a safe default
**Where it appears:** Post-submission confirmation screen

---

## V08 — Finding block icons (set of 6)

**Purpose:** A small icon for each of the six pain findings, used in the report's Priority Findings section.

Generate as a single set so the icons feel consistent — same stroke weight, same colour, same visual grammar.

```
A set of six matching icons for an institutional audit report, each representing
one of these concepts, in order:
  1. Data fragmentation — fragmented puzzle pieces with cyan highlight
  2. Reporting lag — a clock face with a cyan arc indicating delay
  3. Structural complexity — nested entity boxes connected by thin lines
  4. Shadow AI — a locked vault with a subtle warning badge
  5. Portfolio blindspots — a magnifying glass over a bar chart
  6. Deal flow drag — a funnel with stylised document icons flowing through

All six rendered as flat vector icons, single-weight strokes, cyan #35D1FF on
transparent background. Each icon sized identically at 128×128. Clean line-art
style with subtle fill accents in a lighter cyan #ECF5FB. No shadows, no gradients,
no decorative embellishment. Must feel like a cohesive icon set from an
institutional brand toolkit.

Style tags: icon set, flat vector, line art, SF Symbols style, minimal, cyan
monochrome, 128px grid
```

**Aspect ratio:** 128×128 each, delivered as a 6-up grid for review, then exported individually
**Where it appears:** Beside each finding block in `Finding_Blocks.md`

---

## V09 — Partner card background (report Page 6)

**Purpose:** Subtle treatment behind the "Named founding partners" block on the final page of the report.

```
A quiet horizontal banner for a professional biography block. Dark navy
background (#031B4E) with a subtle vertical cyan accent on the left edge
(3 pixels wide, full height). Soft gradient wash on the navy, barely visible,
to give the banner subtle depth without decoration. No illustration, no
icons — this is a container for text and headshots that will overlay. Clean
institutional feel.

Style tags: banner container, subtle gradient, minimal, premium institutional
```

**Aspect ratio:** Full page width, approximately 7×2 inches
**Where it appears:** Behind the partner names block on Page 6 of the report

---

## V10 — Favicon + small-size brand marks

**Purpose:** The 16×16, 32×32, 48×48 favicon versions for the audit URL — must survive extreme downsizing.

```
A simple geometric mark for a technology brand favicon. A stylised "S" or a
small vault/shield shape, rendered in bright cyan (#35D1FF) on a dark navy
(#031B4E) square background. Must remain legible at 16×16 pixels. Single-weight,
no gradients, no complex detail. Reminiscent of institutional fintech favicons
like Stripe, Plaid, or Mercury.

Style tags: favicon, brand mark, extreme simplicity, legible at 16px, fintech brand
```

**Sizes:** 16×16, 32×32, 48×48, 180×180 (Apple touch), 512×512 (PWA)
**Where it appears:** Browser tab, bookmark, Apple home-screen icon

---

## Tool-specific notes

| Tool | Best for | Tweaks |
|---|---|---|
| **Midjourney** | V01, V04, V07 (editorial illustrations) | Append `--ar 16:9 --style raw --v 6.1 --stylize 300` for premium feel |
| **DALL-E 3 / GPT Image** | V02, V05 (banner typography) | Repeat the exact text 3× in the prompt — DALL-E's text rendering benefits |
| **Ideogram** | V02, V05 (text-in-image) | Only tool that reliably renders long text strings correctly |
| **Adobe Firefly** | V08, V10 (icon sets, favicons) | Firefly's icon-generation mode is cleanest for flat vector output |

---

## Generation sequence recommendation

Generate in this order:

1. **V02 (OG card)** — needed before the landing page can be shared
2. **V01 (hero)** — needed for the landing page to feel finished
3. **V05 (email header)** — needed before Email 01 can go live
4. **V04 (report cover)** — needed before the first audit report ships
5. **V06 (priority matrix)** — needed for Page 4 of the report
6. **V08 (finding icons)** — needed for Page 3 of the report
7. **V03, V07, V09, V10** — nice-to-haves, generate during polish pass

---

## Approval loop

Every visual generated against these prompts goes to a founding partner for a 30-second check before it goes live. The brand consistency across the audit, deck, case studies, and setter script is one of the trust signals this project depends on — a single off-brand visual undermines all of it.
