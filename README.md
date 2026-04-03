# ugc-slideshow-generator

A Claude skill that generates emotional, conversion-focused UGC video scripts for short-form content — packaged as an interactive React slideshow you can use, copy, and hand off to creators.

Designed for YouTube Shorts, TikTok, and Instagram Reels. Works for any product or audience.

---

## What It Does

Give Claude a product and a target audience. The skill generates a batch of 5–15 short video scripts, each built around a distinct emotional angle, and renders them as an interactive slideshow artifact with:

- Slide-by-slide preview (Hook → Problem → Result → CTA)
- One-click copy per slide or full script
- Director's notes on every slide (what to show on screen)
- Color-coded slide types
- Production tips panel (format, pacing, audio, branding)

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
| "Add 10 more" | Generates new scripts with unused angles, appends to artifact |
| "Now do this for [new product]" | Re-parameterizes everything, fresh generation |
| "Focus only on [audience segment]" | Filters angles and re-generates |
| "Remove anything about [topic]" | Strips irrelevant references, regenerates cleanly |

---

## File Structure

```
ugc-slideshow-generator/
├── SKILL.md                          # Core instructions and workflow
└── references/
    ├── emotional-angles.md           # Full angle library with execution notes
    └── artifact-template.md          # React component blueprint and color palette
```

---

## Output Example

After one prompt, you get a fully interactive React artifact like this:

```
┌─────────────────────────────────────────────┐
│  DOKKAI × MOCHIPIXEL                        │
│  UGC Script Generator                       │
│  14 emotional hooks for novel readers       │
├─────────────────────────────────────────────┤
│  [📖 Novel Dream] [🌙 Murakami] [🔀 Trans…] │
├─────────────────────────────────────────────┤
│  🎣  PROBLEM  ✨  📲              2/4        │
├─────────────────────────────────────────────┤
│                                             │
│   Every time I tried to read,               │
│   I'd hit a kanji I didn't know.            │
│   I'd lose my place, lose my flow.          │
│   And just… give up.                        │
│                                             │
├─────────────────────────────────────────────┤
│  🎬 Re-enact the frustration: close book…  │
│                                    [COPY]   │
└─────────────────────────────────────────────┘
```

---

## Built With

This skill was developed by [MochiPixel LLC](https://mochipixel.io) to support UGC marketing for [Dokkai](https://mochipixel.io/dokkai), a Japanese reading companion app for iOS.

The emotional angle framework is adapted from UGC best practices for short-form video conversion content.

---

## License

For internal use. Not for redistribution without permission.
