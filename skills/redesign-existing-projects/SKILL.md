---
name: redesign-existing-projects
description: "Audits and upgrades existing websites and apps to premium quality. Diagnoses generic AI design patterns, weak states, and sloppy code, then applies targeted fixes without breaking functionality. Use this skill whenever the user wants to improve, polish, upgrade, refine, audit, fix, or redesign an EXISTING site, page, app, or component, even when they only say it looks bad, cheap, generic, or AI made. Works with any CSS framework or vanilla CSS."
---

# Redesign Existing Projects

This skill is a **diagnostic**. It finds what is wrong with an existing interface and fixes it in place.

## Design values

All concrete values (fonts, background colors, spacing, radius, icon sets, motion timing) live in the **Design Values** section at the bottom of this file. That section is the single source of truth. The audit below tells you *what to look for*; Design Values tells you *what to replace it with*.

Never invent a font, hex value, spacing number, radius, or easing curve that is not in Design Values. If a situation is not covered there, ask rather than guessing.

To adapt this skill to a different design system, edit only the Design Values section. The entire audit follows it automatically.

## How this works

1. **Scan** — Read the codebase. Identify the framework, styling method (Tailwind, vanilla CSS, styled-components, CSS modules), and the current design patterns.
2. **Diagnose** — Run the full audit below. List every generic pattern, weak point, and missing state you find. Report before fixing.
3. **Fix** — Apply targeted upgrades inside the existing stack, in the Fix Priority order. Do not rewrite from scratch. Improve what is there.

---

# Design audit

## Typography

- **Browser default fonts, or Inter / Roboto / Arial / Open Sans / Helvetica.** Replace with an approved font from the Design Values section.
- **Two typefaces on one site.** Consolidate to one, unless the project brief explicitly calls for a pair.
- **Italic type anywhere.** Remove it. Use weight, size, or color for emphasis instead.
- **Ultra bold weights (800, 900, black).** Cap at semibold or bold.
- **Only Regular (400) and Bold (700) in use.** Introduce Medium (500) and SemiBold (600) for finer hierarchy.
- **Headlines lack presence.** Increase display size and tighten letter spacing so headlines feel heavy and intentional. Adjust tracking only within the line height the type scale already provides.
- **Body text too wide.** Cap paragraph measure at roughly 65 characters.
- **Numbers in a proportional font.** Enable `font-variant-numeric: tabular-nums` for data heavy interfaces.
- **Missing letter spacing adjustments.** Negative tracking on large headers, positive tracking on small labels and caps.
- **All caps subheaders everywhere.** Switch to sentence case or small caps. Do not switch to italics.
- **Orphaned words.** A single word alone on the last line. Fix with `text-wrap: balance` on headings and `text-wrap: pretty` on body.
- **Hyphens inside copy.** Do not use `-` in headings, body text, or labels. Rewrite the phrase.
- **Arbitrary or off scale font sizes.** Resolve every size to the Tailwind type scale. Never leave `text-[19px]`, `font-size: 22px`, or `1.4rem` in place. If a size does not land on a step, snap to the closest step below and take its paired line height. Do not combine this with independently set custom line heights from the two fixes above; adjust only within the matched step's value so the rules do not fight.
- **Buttons with off scale type.** Main buttons `text-base` semibold. Header buttons `text-sm` semibold.

## Color and surfaces

- **Background colors outside the approved palette.** Snap every dark surface to the approved dark values. Do not substitute `#0a0a0a`, `#121212`, or a tinted navy.
- **Gradient backgrounds of any kind.** Backgrounds are flat. Remove linear, radial, and mesh background gradients entirely. The only permitted gradient is on hero heading text.
- **Hero heading with flat text color.** Apply the approved left to right text gradient for the active theme.
- **The purple and blue "AI gradient" aesthetic.** The single most common AI fingerprint. Replace with a flat neutral base and one considered accent.
- **Oversaturated accent colors.** Keep saturation under 80% so accents sit with the neutrals instead of screaming.
- **More than one accent color.** Pick one. Remove the rest.
- **Mixing warm and cool grays.** Commit to one gray family and tint consistently.
- **Generic `box-shadow`.** Tint shadows toward the background hue instead of pure black at low opacity.
- **Flat surfaces with zero texture.** Add subtle noise or grain overlays. Do not reach for a gradient to solve flatness.
- **Inconsistent lighting direction.** Audit every shadow so they imply one light source.
- **A random dark section inside a light page, or the reverse.** This reads as a copy paste accident. Commit to one background tone, or step to a neighboring approved shade rather than jumping to `#111` in the middle of a cream page.
- **Empty sections with no depth.** Add high quality background imagery, masked or overlaid at low opacity, or a subtle pattern. Use `https://picsum.photos/seed/{name}/1920/1080` when real assets are unavailable. Never solve this with an ambient gradient.

## Layout

- **Everything centered and symmetrical.** Break symmetry with offset margins, mixed aspect ratios, or a left aligned header over centered content.
- **Three equal card columns as the feature row.** The most generic AI layout. Three to five benefits is correct as *content*; the *layout* should be a two column zig zag, an asymmetric grid, horizontal scroll, or masonry.
- **`height: 100vh` on full screen sections.** Replace with `min-height: 100dvh` to stop layout jump on iOS Safari.
- **Complex flexbox percentage math.** Replace with CSS Grid.
- **No max width container.** Add a constraint around 1200 to 1440px with auto margins. Hero heading and subheading cap at 680px.
- **Cards forced to equal height by flexbox.** Allow variable heights, or use masonry when content length varies.
- **Radius chosen by feel.** Every radius comes from Tailwind's scale. When a shape sits inside another and the gap is under 32px, the inner radius equals the outer radius minus the gap, applied only when the result exceeds 2.
- **Spacing values invented ad hoc.** Every margin, padding, and gap resolves to the approved spacing scale.
- **No overlap or depth.** Elements sitting flat beside each other. Use negative margins to layer.
- **Symmetrical vertical padding.** Adjust optically. Bottom padding usually needs slightly more.
- **Dashboard always has a left sidebar.** Try top navigation, a floating command menu, or a collapsible panel.
- **Missing whitespace.** Step up one level on the spacing scale and let it breathe. Dense layouts suit data dashboards, not marketing pages.
- **Buttons not bottom aligned in card groups.** Pin CTAs to the bottom of each card so they form one clean horizontal line.
- **Feature lists starting at different vertical positions.** In pricing and comparison columns, lists must start at the same Y position. Use fixed height title and price blocks.
- **Inconsistent vertical rhythm across side by side elements.** Align titles, descriptions, prices, and buttons across all items. Misaligned baselines read as broken.
- **Mathematical alignment that looks optically wrong.** Icons beside text, play buttons in circles, and text in buttons often need one or two pixels of optical correction.

## Interactivity and states

- **Default easing curves.** `ease`, `linear`, and `ease-in-out` make motion feel mechanical. Switch to the base curve in Design Values, `duration-500` for movement and `duration-300` for color or opacity, never under 200ms.
- **Content that is simply there on scroll.** Sections should rise a short distance and fade in as they enter the viewport, once, over 600 to 800ms.
- **Scroll listeners driving animation.** Replace `window.addEventListener('scroll')` with `IntersectionObserver` or Framer Motion `whileInView`; per frame listeners cost real performance on mobile.
- **A nav bar welded to the top edge.** Let it float slightly off the edge, sized to its content, on a translucent blurred surface.
- **A menu icon that swaps instantly.** Animate the change between open and closed states on the base curve.
- **A cramped mobile dropdown.** Use a full height panel, with links arriving one after another in reading order (about 60ms apart, whole sequence under 400ms).
- **No reduced motion handling.** Under `prefers-reduced-motion`, swap movement for a plain fade.
- **No hover states on buttons.** Add a background shift, slight scale, or translate.
- **No active or pressed feedback.** Add `scale(0.98)` or `translateY(1px)` on press.
- **Missing focus ring.** Visible focus indicators are an accessibility requirement, not a style choice.
- **No loading states.** Replace circular spinners with skeleton loaders shaped like the real layout.
- **No empty states.** Design a composed "getting started" view instead of a blank panel.
- **No error states.** Inline, specific form errors. Never `window.alert()`.
- **Dead links.** Buttons pointing at `#`. Link them or visually disable them.
- **No current page indicator in navigation.** Style the active link distinctly.
- **Scroll jumping.** Add `scroll-behavior: smooth` for anchor navigation.
- **Animating `top`, `left`, `width`, or `height`.** Switch to `transform` and `opacity` for GPU acceleration.

## Content

- **Placeholder people.** Stock names and repeated faces read as fake. Use full, specific names that fit the audience, and a different face for every person.
- **Suspiciously round numbers.** Real metrics carry decimals and odd final digits; real prices look like real pricing. Vary dates across lists.
- **Generic brand names.** Customer logos and company names should sound like they belong to the product's industry.
- **Filler marketing words.** Cut "revolutionize", "supercharge", "cutting edge", "effortless", "transform your workflow", "take it to the next level", "harness the power", "world class". Say what the product actually does.
- **Vague value propositions.** "Streamline" and "optimize" say nothing. Replace with a measurable outcome: "Cut weekly reporting from 4 hours to 15 minutes".
- **Features listed with no outcome.** Every feature line should state what it means for the user.
- **Weak CTAs.** Never "Learn more" or "Submit". Use a verb plus what they get: "Start free trial", "Book a demo".
- **Competing CTAs above the fold.** One primary action per page.
- **Proof buried at the bottom.** Move testimonials, logos, and numbers next to the claims they support.
- **No risk reversal.** Add at least one of free trial, free plan, no credit card, cancel anytime, money back guarantee.
- **Loud or cute system messages.** Confirmations should be calm and specific ("Invoice sent to Dana"). Errors should name what failed and the next step ("Upload failed. The file is over 20 MB."). No exclamation marks, no interjections.
- **Passive voice.** Name who did what: "We couldn't save your draft."
- **Placeholder text.** Any "Your headline here" or Latin filler is a blocker. Write real draft copy.
- **Title Case everywhere.** Use sentence case for headings and buttons.

## Component patterns

- **Generic card look: border plus shadow plus white background.** Drop to background color alone, or spacing alone. Cards should exist only where elevation communicates hierarchy.
- **Border on a single side of a card.** Never. Borders go all the way around or not at all.
- **Always one filled button plus one ghost button.** Introduce text links or tertiary styles to cut visual noise.
- **Pill shaped "New" and "Beta" badges.** Try square badges, flags, or plain text labels.
- **Accordion FAQ.** The FAQ section itself should stay, six to twelve questions. Change the pattern: a side by side list, searchable help, or inline progressive disclosure reads better than a stack of chevrons.
- **Three card carousel testimonials with dots.** Replace with a masonry wall, embedded social posts, or one rotating quote.
- **Pricing table with three towers.** Emphasize the recommended tier with color and weight, not extra height.
- **Modals for everything.** Use inline editing, slide over panels, or expandable sections for simple actions.
- **Avatar circles exclusively.** Try squircles or rounded squares.
- **Light and dark toggle as a sun and moon switch.** Use a dropdown, system preference detection, or a settings entry.
- **Four column footer link farm.** Simplify to main paths plus legally required links.

## Iconography and imagery

- **Lucide, Feather, Material Icons, or Material Symbols.** These are the default AI choices. Replace with an approved set from the Design Values section.
- **Rocketship for "Launch", shield for "Security".** Replace cliche metaphors with bolt, fingerprint, spark, vault.
- **Inconsistent stroke widths.** Standardize every icon to one stroke weight.
- **Missing favicon.** Always ship a branded one.
- **Stock "diverse team" photos.** Use real photos, candid shots, or one consistent illustration style.

## Code quality

- **Div soup.** Use `<nav>`, `<main>`, `<article>`, `<aside>`, `<section>`.
- **Inline styles mixed with classes.** Move everything into the project's styling system.
- **Hardcoded pixel widths.** Use `%`, `rem`, `em`, and `max-width`.
- **Missing alt text.** Describe the content. Never leave `alt="image"` on a meaningful image.
- **Arbitrary z index like `9999`.** Establish a scale in the theme.
- **Commented out dead code.** Remove all debug artifacts.
- **Import hallucinations.** Verify every import exists in the project dependencies.
- **Missing meta tags.** Add `<title>`, description, `og:image`, and social sharing tags.

## Strategic omissions

What AI builds typically forget entirely:

- **No legal links.** Privacy policy and terms in the footer.
- **No back navigation.** Every page needs a way out.
- **No custom 404.** Design a branded, helpful one.
- **No form validation.** Client side checks for email format and required fields.
- **No skip to content link.** Essential for keyboard users.
- **No cookie consent.** Add a compliant banner where the jurisdiction requires it.
- **Landing page indexing not considered.** Ad only and time bound offers should be `noindex`. Evergreen pages need a real title, meta description, internal links, and a plain question and answer FAQ for AEO.

---

# Fix priority

Maximum visual impact, minimum risk, in this order:

1. **Font swap** — biggest instant improvement, lowest risk
2. **Color and surface cleanup** — snap to the approved palette, remove background gradients
3. **Hover, active, and focus states** — makes the interface feel alive
4. **Layout and spacing** — grid, max width, spacing scale, nested radius formula
5. **Motion pass** — base easing curve, scroll reveals via IntersectionObserver, floating nav and mobile menu
6. **Replace generic components** — swap cliche patterns for the alternatives above
7. **Loading, empty, and error states** — makes it feel finished
8. **Copy pass** — remove cliches, add specificity, fix CTAs
9. **Type scale polish** — the premium final touch

---

# Rules

- Work with the existing tech stack. Do not migrate frameworks or styling libraries.
- Do not break existing functionality. Test after every change.
- Report the diagnosis before applying fixes. Let the user veto items.
- Check the project's dependency file before importing any new library.
- If the project uses Tailwind, check the version, v3 or v4, before touching config.
- If there is no framework, use vanilla CSS.
- Keep changes reviewable and focused. Small targeted improvements over big rewrites.
- Never invent a design value. If it is not in Design Values, ask.

---

# Design values

The single source of truth for this skill. Edit this section to adapt it to your own design system.

**Fonts:** Geist, Manrope, Geist Mono, Poppins. Never Inter, Roboto, Arial, Open Sans, Helvetica. No italics. No weights above bold.

**Dark backgrounds:** `#000000` · `#181818` · `#1F1F1F` · `#272727` · `#313131` · `#131209`

**Hero heading gradient:** dark theme `#FFFFFF` → `#9B9B9B`; light theme `#000000` → `#666666`. Left to right, text only.

**Spacing:** 0, 2, 4, 8, 12, 16, 24, 32, 40, 48, 64, 80, 96px. Main buttons 8px vertical, 12px horizontal.

**Radius:** Tailwind values only. Nested shapes under a 32px gap use `inner = outer − gap`, applied only when the result exceeds 2.

**Icons:** Phosphor, Solar, Iconamoon.

**Motion:** base curve `ease-[cubic-bezier(0.22,1,0.36,1)]`, `duration-500` for movement, `duration-300` for color and opacity. Scroll reveals 600 to 800ms via `IntersectionObserver`. Respect `prefers-reduced-motion`.

**Type scale:** Tailwind default.

| Class | Size | Line height |
|---|---|---|
| `text-xs` | 12px | 16px |
| `text-sm` | 14px | 20px |
| `text-base` | 16px | 24px |
| `text-lg` | 18px | 28px |
| `text-xl` | 20px | 28px |
| `text-2xl` | 24px | 32px |
| `text-3xl` | 30px | 36px |
| `text-4xl` | 36px | 40px |
| `text-5xl` | 48px | 1 |
| `text-6xl` | 60px | 1 |
| `text-7xl` | 72px | 1 |
| `text-8xl` | 96px | 1 |
| `text-9xl` | 128px | 1 |

---

## Credits

Parts of this skill were adapted from [taste-skill](https://github.com/Leonxlnx/taste-skill) by Leon Lin ([@LexnLin](https://x.com/LexnLin)), MIT licensed. Its redesign audit structure, content realism checks, and motion and navigation ideas informed the matching sections here, which have since been rewritten.

<details>
<summary>taste-skill license</summary>

```
MIT License

Copyright (c) 2026 Leonxlnx

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
```
</details>
