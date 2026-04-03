# ugc-slideshow-generator

A Claude skill that generates emotional, conversion-focused UGC video scripts for short-form content — packaged as an interactive React slideshow with full visual shoot direction for every slide.

Designed for YouTube Shorts, TikTok, and Instagram Reels. Works for any product or audience.

---

## What It Does

Give Claude a product and a target audience. The skill generates a batch of 5–15 short video scripts, each built around a distinct emotional angle, and renders them as an interactive slideshow artifact with:

- Slide-by-slide preview (Hook → Problem → Result → CTA)
- One-click copy per slide or per full script
- **Two-layer visual guidance on every slide** — a quick director's note and a full shoot guide
- **🎬 Shoot Guide panel** — per-script, color-coded visual directions for all 4 slides
- Dark / light mode toggle
- Color-coded slide types
- Universal production tips (format, pacing, audio, branding)

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

```
🎬 Close-up on a dense kanji menu, no pictures. Creator's face just visible in background.
```

### `visual` — Full Shoot Guide
A 2–4 sentence production brief shown in the **🎬 Shoot Guide** panel at the bottom of each script. Written like a director briefing a UGC creator who has never made a video. Covers:

- **Shot type** — close-up, talking head, screen record, POV, montage, flat lay
- **Location & props** — what physical objects or environments to use
- **Subject action** — what the creator does on screen, moment by moment
- **Camera style** — handheld, static, slow zoom, screen record overlay
- **Pacing & feel** — how fast to cut, whether to use music or silence
- **Key visual detail** — the one thing that makes the shot work

### Example (Script: The Murakami Effect)

| Slide | Shoot Guide |
|-------|-------------|
| 🎣 Hook | Close-up on a Japanese copy of Norwegian Wood on a shelf, slightly dusty. Creator's hand reaches in, picks it up, blows dust off the cover. Look at the camera with a sheepish expression. Warm, slightly dim shelf lighting. The dust is the story — don't skip it. |
| 😤 Problem | Creator opens the book, starts reading, hits a word, picks up phone to search it, loses their place, scrolls back, loses focus, closes the book with a soft thud. Repeat this cycle fast — 3 seconds total. No words needed. Every learner will recognize this loop immediately. |
| ✨ Result | Screen record: Dokkai open to a Japanese text. Tap a kanji — definition slides in from bottom instantly. Dismiss, continue reading. Tap another — same speed. The rhythm is unbroken. Overlay a subtle timer in corner showing 10 pages read in one session. Speed and flow are the product. |
| 📲 CTA | Return to the same shelf from the hook — same book, same angle, but now a bookmark is sticking out partway through. Creator pulls it off the shelf again, this time with purpose. Holds it up. Nods. End frame: book in one hand, phone with Dokkai open in the other. |

The Shoot Guide is **per-script** — it updates automatically when you switch between scripts in the artifact.

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
| "Add 10 more" | Generates new scripts with unused angles, full visual guidance included |
| "Now do this for [new product]" | Re-parameterizes everything, fresh generation |
| "Focus only on [audience segment]" | Filters angles and re-generates |
| "Remove anything about [topic]" | Strips irrelevant references, regenerates cleanly |
| "Add scripts for [niche audience]" | Generates angles specific to that community (e.g. oshikatsu fans, adult learners) |

---

## UI Features

| Feature | Description |
|---------|-------------|
| ☀ / ☾ Toggle | Dark mode (default) and light mode — warm parchment palette |
| Script tabs | One button per script, each with a unique accent color |
| Slide navigator | Color-coded tabs: Hook (yellow), Problem (red), Result (green), CTA (blue) |
| Slide preview | Large centered text in a phone-style pane |
| Director's note bar | Quick `sub` note below the preview, with a COPY button |
| View Full Script | Expandable grid showing all 4 slides with copy buttons |
| 🎬 Shoot Guide | Per-script panel with full visual direction for all 4 slide types |
| Production tips | Universal format/pacing/branding reference in the footer of the Shoot Guide |

---

## File Structure

```
ugc-slideshow-generator/
├── SKILL.md                          # Core instructions and workflow
└── references/
    ├── emotional-angles.md           # Full angle library with execution notes
    └── artifact-template.md          # React component blueprint, theme object,
                                      # font weight standards, and shoot guide spec
```

---

## Output Example

```
┌─────────────────────────────────────────────────────┐
│  ☀ LIGHT          DOKKAI × MOCHIPIXEL               │
│                   UGC Script Generator              │
│                   20 emotional hooks                │
├─────────────────────────────────────────────────────┤
│  [📖 Novel Dream] [🌙 Murakami] [💌 Fan Letter] …  │
├─────────────────────────────────────────────────────┤
│  🌙 The Murakami Effect   [Novels] [Aspiration→Reality] │
├─────────────────────────────────────────────────────┤
│  🎣  😤  ✨  📲                           2/4       │
├─────────────────────────────────────────────────────┤
│                                                     │
│   Every time I tried to read,                       │
│   I'd hit a kanji I didn't know.                    │
│   I'd lose my place, lose my flow.                  │
│   And just… give up.                                │
│                                                     │
├─────────────────────────────────────────────────────┤
│  🎬 Recreate the frustration: dictionary open…     │
│                                          [COPY]     │
├─────────────────────────────────────────────────────┤
│  🎬 SHOOT GUIDE              what to film for each slide │
├──────────────────────────────────────────────────────┤
│ 🎣 HOOK    Close-up on Norwegian Wood on shelf,      │
│            slightly dusty. Creator blows dust off,  │
│            looks at camera: sheepish expression...  │
├──────────────────────────────────────────────────────┤
│ 😤 PROBLEM  Creator opens book, hits unknown word,   │
│            picks up phone, loses place, closes book. │
│            Repeat 3x fast. No words needed...       │
├──────────────────────────────────────────────────────┤
│ ✨ RESULT   Screen record: Dokkai open, tap kanji,   │
│            definition appears instantly, continue.  │
│            Timer overlay: 10 pages in one session.. │
├──────────────────────────────────────────────────────┤
│ 📲 CTA     Return to shelf — same book, bookmark    │
│            now inside. Creator pulls it with purpose.│
│            Book + phone with Dokkai. End frame.     │
├──────────────────────────────────────────────────────┤
│  ⏱ 2–4s/slide  📱 9:16  🎵 Lo-fi  ✍️ Bold text     │
└─────────────────────────────────────────────────────┘
```

---

## Built With

This skill was developed by [MochiPixel LLC](https://mochipixel.io) to support UGC marketing for [Dokkai](https://mochipixel.io/dokkai), a Japanese reading companion app for iOS.

The emotional angle framework is adapted from UGC best practices for short-form video conversion content.

---

## License

For internal use. Not for redistribution without permission.
