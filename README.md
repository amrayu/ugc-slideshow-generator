# ugc-slideshow-generator

A Claude skill that generates emotional, conversion-focused UGC video scripts for short-form content — packaged as an interactive React slideshow with full visual shoot direction, vibe presets, and platform-specific production tips.

Designed for YouTube Shorts, TikTok, Instagram Reels, and X. Works for any product or audience.

---

## What It Does

Give Claude a product and a target audience. The skill generates a batch of 5–15 short video scripts, each built around a distinct emotional angle, and renders them as an interactive slideshow artifact with:

- Slide-by-slide preview (Hook → Problem → Result → CTA)
- One-click copy per slide or per full script
- **Two-layer visual guidance** — quick director's note + full shoot guide per slide
- **🎬 Shoot Guide panel** — per-script, color-coded visual directions for all 4 slides
- **Vibe system** — auto-matched per script, globally overridable
- **Platform tips** — tabbed TikTok / YouTube Shorts / Reels / X guidance
- Dark / light mode toggle
- Color-coded slide types

---

## Installation

1. Download `ugc-slideshow-generator.skill`
2. In Claude, go to **Settings → Skills → Install from file**
3. Upload the `.skill` file
4. Start a new conversation — the skill is now active

---

## How to Use

### Basic prompt
```
Make me UGC scripts for [product] targeting [audience].
```

### Examples
```
Make me UGC scripts for Dokkai, a Japanese reading app, targeting language learners who want to read novels.

Give me UGC ad scripts for a meal prep service targeting busy parents who want to eat healthy.

Create short video scripts for a freelance pricing tool targeting designers who undersell themselves.
```

If you don't include the product or audience, Claude will ask before generating.

---

## Script Structure

Every script is 4 slides:

| Slide | Purpose | Goal |
|-------|---------|------|
| 🎣 **Hook** | Stop the scroll | A confession, contrast, or specific failure the viewer recognizes in themselves |
| 😤 **Problem** | Build empathy | Reframe why they're stuck — not their fault, a broken system or bad advice |
| ✨ **Result** | Show the transformation | A specific, humble win — believable, not aspirational fluff |
| 📲 **CTA** | Drive action | Low-friction next step + 2–3 hashtags + optional comment question |

---

## Visual Guidance System

Every slide is generated with two levels of shoot direction:

### `sub` — Quick Director's Note
A single-sentence cue shown in the slide preview bar. Fast reference while reviewing scripts.

### `visual` — Full Shoot Guide
A 2–4 sentence production brief covering shot type, location, subject action, camera style, pacing, and the one key visual detail that makes the shot work. Shown in the **🎬 Shoot Guide** panel.

---

## Vibe System

Every script has a **default vibe** auto-matched to its emotional angle. A global override row lets you force all scripts to one vibe for a consistent batch look.

### The 5 Vibes

| Vibe | Visual Language | Best For |
|------|----------------|----------|
| 🛋️ **Cozy** | Warm tungsten light, slow cuts, blankets, steam, worn books | Novel Dream, Comfort Read, Photobook |
| ⚡ **Hype** | Bright contrast, fast cuts synced to beat drops, bold text | Speed Reader, Live Stream Gap, Drama Fan |
| 🎙️ **Raw** | Natural daylight, one-take energy, no music, room ambiance | Late Starter, Grammar Grind Lie, Quiet Flex |
| 🎬 **Cinematic** | Golden hour, color graded, deliberate pacing, emotional score | Murakami Effect, Interview Cry, Concert MC |
| 📚 **Educational** | Clean even light, text overlays, measured pace, diagrams | 3 Writing Systems, Immersion Myth, Lonely Dictionary |

### How It Works in the UI

- **AUTO** pill — each script uses its own default vibe (shown as `·auto` on the badge)
- **Override pills** — selecting a vibe forces all scripts to that style (shown as `·override`)
- **Vibe Notes panel** — appears at the top of the Shoot Guide with 6 production specs: Lighting, Pacing, Audio, Editing, Text Style, Props
- Clicking an active override pill deselects it, returning to AUTO

### Default Vibe Assignments

| Vibe | Scripts |
|------|---------|
| 🛋️ Cozy | Novel Dream, 5 Min Reader, Hardcover Guilt, Comfort Read, Photobook |
| ⚡ Hype | Drama Fan, Speed Reader, Live Stream Gap, Subtitle Delay |
| 🎙️ Raw | Tokyo Tourist, JLPT Trap, Grammar Grind Lie, Late Starter, Quiet Flex |
| 🎬 Cinematic | Murakami Effect, Translation Betrayal, Midnight Epiphany, Rereader, First Sentence, Fan Letter, Interview Cry, Concert MC |
| 📚 Educational | 3 Writing Systems, Lonely Dictionary, Immersion Myth |

---

## Platform Tips

The bottom of the Shoot Guide has a tabbed platform selector with production guidance specific to each platform:

| Platform | Duration | Key Difference |
|----------|----------|----------------|
| 🎵 **TikTok** | 15–30 sec | Fast cuts, trending audio, beat-synced text, comment-bait CTA |
| ▶️ **YouTube Shorts** | 30–60 sec | Slightly longer setup okay, subtitles help, subscribe bug |
| 📸 **Instagram Reels** | 15–45 sec | Aesthetic transitions, save/share CTA, brand-forward |
| 𝕏 **X / Twitter** | Under 30 sec | Must read without sound, RT-bait CTA, fewer cuts |

Each tab shows 6 specs: Duration, Cuts, Audio, Text, CTA, and Loop guidance.

---

## Emotional Angles Library

The skill pulls from a built-in library of ~30 proven UGC angles, organized by category:

- **Identity & Self-Image** — The Confession, The Quiet Flex, The Late Starter, The Imposter
- **Frustration & Broken Systems** — The Grammar Grind Lie, The Immersion Myth, The Translation Betrayal, The Tool Overload
- **Time & Habit** — The 5 Min Reader, The Speed Reader, The Burnt Out, The Daily Habit
- **Dreams & Aspiration** — The Shelf Book, The Novel Dream, The Rereader, The Midnight Epiphany
- **Social & Community** — The Tourist Shame, The Train Reader, The Comment Bait
- **Mindset Shifts** — The Waiting Trap, The Permission Slip, The Reframe, The Anti-Grind

Each generation picks a fresh set — no two scripts in a batch share the same emotional entry point.

---

## Updating & Iteration

| You say | What happens |
|---------|-------------|
| "Add 10 more" | New scripts with unused angles, full visual + vibe guidance |
| "Now do this for [new product]" | Re-parameterizes everything, fresh generation |
| "Focus only on [audience segment]" | Filters angles and re-generates |
| "Add scripts for [niche]" | Audience-specific angles (e.g. oshikatsu fans, adult learners) |
| "Remove anything about [topic]" | Strips irrelevant references, regenerates cleanly |

---

## UI Features

| Feature | Description |
|---------|-------------|
| ☀ / ☾ Toggle | Dark mode (default) and light warm-parchment light mode |
| VIBE row | AUTO + 5 override pills — forces a global vibe or uses per-script defaults |
| Script tabs | One button per script, each with a unique accent color |
| Vibe badge | Shows active vibe on each script with `·auto` or `·override` indicator |
| Slide navigator | Color-coded tabs: Hook (yellow), Problem (red), Result (green), CTA (blue) |
| Slide preview | Large centered text, phone-style pane |
| Director's note bar | Quick `sub` note below preview + COPY button |
| View Full Script | Expandable grid — all 4 slides with copy buttons |
| 🎬 Shoot Guide | Vibe Notes panel + per-slide visual directions (color-coded by type) |
| Platform tabs | TikTok / YouTube Shorts / Reels / X — 6 production specs each |

---

## File Structure

```
ugc-slideshow-generator/
├── SKILL.md                          # Core instructions and workflow
└── references/
    ├── emotional-angles.md           # Full angle library with execution notes
    └── artifact-template.md          # React component blueprint, theme object,
                                      # vibe system, font weights, shoot guide spec
```

---

## Built With

This skill was developed by [MochiPixel LLC](https://mochipixel.io) to support UGC marketing for [Dokkai](https://mochipixel.io/dokkai), a Japanese reading companion app for iOS.

The emotional angle framework is adapted from UGC best practices for short-form video conversion content.

---

## License

For internal use. Not for redistribution without permission.
