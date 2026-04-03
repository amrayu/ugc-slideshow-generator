---
name: ugc-slideshow-generator
description: >
  Generate UGC (user-generated content) marketing slideshow scripts for short-form video (YouTube Shorts, TikTok, Instagram Reels, X/Twitter). Each script follows a Hook → Problem → Result → CTA structure designed to trigger emotion and drive conversions. Use this skill whenever the user asks for UGC scripts, short video content, marketing slideshows, social media ad copy, or emotional storytelling for a product or app. Also trigger when the user says things like "make me UGC content", "write short video scripts", "give me hooks for [product]", "create ad scripts", or "marketing content for [audience]". This skill produces an interactive React artifact with copyable slides, a vibe system, per-slide shoot guides, and platform-specific production tips — fully parameterized for any product and target demographic.
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
- `visual` — full shoot direction (shown in the Shoot Guide panel). 2–4 sentences: shot type, location, subject action, camera style, key visual detail. Write like a director briefing a UGC creator who has never made a video. Be specific.

### Vibe assignment
Every script must include a `vibe` field. Assign one of these based on the script's emotional angle:

| Vibe | Key traits | Best for |
|------|-----------|----------|
| `cozy` | Warm light, slow cuts, intimate, lo-fi | Comfort, aspiration, lifestyle |
| `hype` | Fast cuts, beat-synced, high energy, bold | Progress, urgency, excitement |
| `raw` | One-take, no music, talking head, authentic | Confessions, reframes, adult learners |
| `cinematic` | Color graded, deliberate pacing, emotional score | Literary, emotional peaks, fan content |
| `educational` | Clean light, text overlays, measured pace | Explainers, methodology, how-it-works |

---

## Step 3: Output as Interactive React Artifact

Render the scripts as a `.jsx` artifact with all of the following:

### Required UI components:
- **Dark/light toggle** — top-right of header
- **Vibe override row** — AUTO pill + 5 vibe pills (🛋️ Cozy / ⚡ Hype / 🎙️ Raw / 🎬 Cinematic / 📚 Educational), positioned between header and script selector
- **Script selector tabs** — one per script, each with unique accent color
- **Vibe badge** on script meta bar — shows active vibe with `·auto` or `·override`
- **Slide navigator** — Hook / Problem / Result / CTA tabs, color-coded
- **Phone-style preview pane** — large centered text
- **Director's note bar** — `sub` field + COPY button
- **View Full Script** — expandable grid, all 4 slides
- **🎬 Shoot Guide panel** — contains in order:
  1. Panel header
  2. **Vibe Notes row** — 6 specs for the active vibe: Lighting, Pacing, Audio, Editing, Text Style, Props
  3. Slide-by-slide visual directions (color-coded by slide type)
  4. **Platform Tips footer** — tabbed TikTok / YouTube Shorts / Reels / X

### Vibe system implementation:
```js
// Default vibe lookup by script ID
const defaultVibes = { 1: "hype", 2: "raw", ... }; // assign per script

// State
const [vibeOverride, setVibeOverride] = useState(null);

// Active vibe
const activeVibeKey = vibeOverride || defaultVibes[script.id] || "raw";
const activeVibe = vibes[activeVibeKey];
```

The `vibes` object defines each vibe's 6 production specs. See `references/artifact-template.md` for the full definitions.

### Platform tips:
Four tabs — TikTok, YouTube Shorts, Instagram Reels, X/Twitter — each with 6 specs: Duration, Cuts, Audio, Text, CTA, Loop.

**X/Twitter color fix:** X uses `#000000` which is invisible on dark backgrounds. Use adaptive colors:
- Dark mode: `#cccccc`
- Light mode: `#333333`

Apply this to both the tab button and the tips grid label color.

### Visual design rules:
- Dark terminal aesthetic by default (`#0a0a0a` bg, monospace font) + light warm-parchment mode (`#F4F1ED`)
- **NEVER use webkit gradient text on the H1** — use plain `color: dark ? "#ffffff" : "#0D0B0A"`
- All colors through theme object `t` — no hardcoded hex values in JSX
- Each script has a unique accent color — vary widely, no purple gradients
- Font: `'Courier New'` or serif for headers — avoid Inter/Roboto
- Body text `fontWeight: 700` min, supporting text `600`+
- Header: `[PRODUCT] × [BRAND]`
- Footer: `[BRAND] — FOR INTERNAL USE`

See `references/artifact-template.md` for theme object, vibe definitions, font weight table, and H1 fix.

---

## Step 4: Summary After the Artifact

- Table: Script name | Angle | Vibe | Core Emotion
- 2–3 sentences on which scripts to test first and why
- Any notes on angles especially strong for this product/audience combo

---

## Updating Scripts

- **Add more** — fresh angles, full `sub` + `visual` + `vibe` on every slide, append to artifact
- **Change product/demo** — re-parameterize all scripts, regenerate
- **Add platform variants** — platform tips are in the UI; no new scripts needed
- **Change vibe defaults** — update `defaultVibes` lookup in the artifact
- **Remove/filter content** — strip irrelevant references, regenerate

Always regenerate the full artifact on updates — don't describe changes in prose.
