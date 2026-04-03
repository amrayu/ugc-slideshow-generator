---
name: ugc-slideshow-generator
description: >
  Generate UGC (user-generated content) marketing slideshow scripts for short-form video (YouTube Shorts, TikTok, Instagram Reels). Each script follows a Hook → Problem → Result → CTA structure designed to trigger emotion and drive conversions. Use this skill whenever the user asks for UGC scripts, short video content, marketing slideshows, social media ad copy, or emotional storytelling for a product or app. Also trigger when the user says things like "make me UGC content", "write short video scripts", "give me hooks for [product]", "create ad scripts", or "marketing content for [audience]". This skill produces an interactive React artifact with copyable slides, director's notes, and production tips — and is fully parameterized for any product and target demographic.
---

# UGC Slideshow Generator

You generate emotional, conversion-focused UGC video scripts packaged as an interactive React slideshow artifact. Each script is a 4-slide sequence: Hook → Problem → Result → CTA.

## Step 1: Gather Parameters

Before generating, collect these two required inputs. If either is missing from the user's message, ask for them:

1. **Product** — What app, tool, or service is being marketed? Collect:
   - Product name
   - What it does (one sentence)
   - Key differentiator or feature worth highlighting (e.g. "tap-to-lookup", "offline mode", "AI tutor")

2. **Target Demo** — Who is the audience? Collect:
   - Primary identity (e.g. "Japanese language learners", "busy parents", "freelance designers")
   - Their core desire or dream (e.g. "read Japanese novels", "lose weight without a gym", "land their first client")
   - Their current frustration or blocker (e.g. "can't read kanji", "no time to cook healthy", "don't know how to price themselves")

If the user has already provided these, extract them from context and proceed directly.

---

## Step 2: Generate 5–15 Scripts

Each script targets a distinct **emotional angle**. Use the reference file `references/emotional-angles.md` for the full menu of proven angles. Select angles that fit the product and audience — don't use all of them every time.

### Script structure (4 slides each):

```
HOOK     — A confession, contrast, or provocative fact that stops the scroll.
           1–2 punchy lines. Specific and personal. Aim for "that's me" recognition.

PROBLEM  — Reframe why they're stuck. Not their fault — a broken system, bad advice,
           or wrong approach. 2–4 lines. Make them feel understood, not blamed.

RESULT   — A specific, believable win. Not "I became fluent" — "I read one chapter."
           Humble and real. 2–3 lines. Show the transformation, not the perfection.

CTA      — A low-friction next step. Usually "link in bio" or a question for comments.
           Include 2–3 relevant hashtags. Optionally end with a comment-bait question.
```

### Director's notes
Every slide must include two visual guidance fields:

- `sub` — one-sentence visual note (shown in the slide preview bar)
- `visual` — full shoot direction (shown in the Shoot Guide panel). This should be 2–4 sentences describing exactly what to film or photograph: shot type, location, subject action, camera style, what's on screen, and any key visual contrast or detail. Write it like a director briefing a UGC creator who has never made a video before. Be specific — "close-up on a dense kanji menu, creator's face just visible in background looking overwhelmed" beats "show a menu."

---

## Step 3: Output as Interactive React Artifact

Render the scripts as a `.jsx` artifact with:

- **Script selector tabs** — one button per script, colored distinctly
- **Slide navigator** — Hook / Problem / Result / CTA tabs with color-coded types:
  - Hook → yellow `#FFE66D`
  - Problem → red `#FF6B6B`
  - Result → green `#6EE7B7`
  - CTA → blue `#93C5FD`
- **Phone-style preview pane** — large centered text, dark background
- **Director's note bar** — italic, below the preview
- **Copy button** — per slide and per full script
- **"View Full Script" expandable section** — all 4 slides in a grid
- **Production Tips panel** — pacing, audio, format, branding guidelines

### Visual design rules:
- Dark terminal aesthetic by default (`#0a0a0a` bg, monospace font) with a light warm-parchment mode (`#F4F1ED`)
- **Dark/light toggle button** is required — positioned top-right of header
- **NEVER use webkit gradient text on the H1** — it breaks on React state toggle. Use plain `color: dark ? "#ffffff" : "#0D0B0A"`
- All colors must route through the theme object `t` — no hardcoded hex values in JSX
- Each script has a unique accent color (not purple gradients — vary widely)
- Use `'Courier New'` or a serif for headers — avoid Inter/Roboto/system fonts
- High contrast required: slide body text `fontWeight: 700` min, supporting text `600`+
- Labeled `[PRODUCT NAME] × [STUDIO/BRAND]` in the header
- Footer: `[BRAND] — FOR INTERNAL USE`

See `references/artifact-template.md` for the full theme object, font weight table, toggle button code, and H1 rendering fix.

---

## Step 4: Summary After the Artifact

After the artifact, write a brief plain-text summary:

- A table: Script name | Angle | Core Emotion
- 2–3 sentences on which scripts to **test first** and why
- Any notes on angles especially strong for this product/audience combo

---

## Updating Scripts

If the user asks to:
- **Add more scripts** — generate new ones with fresh emotional angles not already used, append to the existing artifact
- **Change the product** — re-parameterize all scripts and regenerate
- **Change the demo** — re-skin the emotional language, keep the angles, regenerate
- **Remove manga/gaming/etc.** — filter out irrelevant references and regenerate cleanly

Always regenerate the full artifact on updates — don't describe changes in prose.
