# Redesign Skill

**A design audit for AI coding tools.** Point it at an existing site and it finds the generic patterns, the missing states, and the sloppy code, then fixes them in place without rewriting your project.

Works with Claude Code, Cursor, Codex, Windsurf, and anything else that reads a markdown rules file.

<!-- Replace with your before/after screenshot -->
![Before and after](./assets/before-after.png)

---

## Install

<details open>
<summary><b>Claude Code</b></summary>

```bash
mkdir -p .claude/skills
git clone https://github.com/elayadesign/redesign-skill.git /tmp/redesign-skill
cp -r /tmp/redesign-skill/skills/redesign-existing-projects .claude/skills/
```

Then just ask: *"audit this project and upgrade the design"*
</details>

<details>
<summary><b>Cursor</b></summary>

```bash
mkdir -p .cursor/rules
curl -o .cursor/rules/redesign.md \
  https://raw.githubusercontent.com/elayadesign/redesign-skill/main/skills/redesign-existing-projects/SKILL.md
```

Or paste the file into **Settings → Rules for AI**.
</details>

<details>
<summary><b>Codex / Windsurf / other</b></summary>

Copy `SKILL.md` into whatever your tool uses for project rules:

| Tool | Path |
|---|---|
| Codex | `AGENTS.md` |
| Windsurf | `.windsurfrules` |
| Cline | `.clinerules` |
| Generic | paste into your system prompt |
</details>

<details>
<summary><b>Claude.ai (no terminal)</b></summary>

Download `SKILL.md` and upload it to a Project, or attach it to a chat and say *"follow this when reviewing my site."*
</details>

---

## What it enforces

| Area | Rule |
|---|---|
| **Type** | Approved fonts only, no Inter or Roboto, no italics, no black weights, every size snapped to the Tailwind scale |
| **Color** | Fixed dark palette, zero background gradients, one accent, tinted shadows |
| **Spacing** | A closed token scale. No invented values. |
| **Radius** | Nested shapes use `inner = outer − gap`, so corners actually sit concentric |
| **Layout** | Breaks the three-equal-columns default, aligns baselines across cards, optical padding |
| **Motion** | Custom easing curves, `IntersectionObserver` reveals, no scroll listeners |
| **Copy** | No Lorem Ipsum, no "Acme Corp", no "Elevate" or "Seamless", no round fake numbers |
| **States** | Hover, active, focus, loading, empty, error — all required |
| **Ship** | 404, legal links, validation, favicon, meta tags, alt text |

Full list in [`SKILL.md`](./skills/redesign-existing-projects/SKILL.md).

---

## Try it

Paste this at any AI tool with the skill installed:

```
Audit this project and upgrade the design. Report what you find before changing anything.
```

It will come back with a diagnosis first. You approve, then it fixes in priority order — fonts, then color, then states, then layout, then motion.

---

## The one rule people ask about

**Nested corner radius.** When a shape sits inside another and the gap is under 32px:

```
inner radius = outer radius − gap
```

Applied only when the result is greater than 2.

A card at `rounded-2xl` (16px) with 8px of padding gives inner elements an 8px radius. Do it any other way and the corners look subtly wrong without anyone being able to say why.

---

## Make it yours

The design values are opinions. Fork it and swap them.

Everything lives in the **Design Values** section at the bottom of `SKILL.md` — fonts, hex values, spacing scale, icon sets, easing curve. Change those and the entire audit follows your system instead of mine.

---

## License

MIT. Use it, fork it, ship it, sell what you build with it. No attribution needed.
