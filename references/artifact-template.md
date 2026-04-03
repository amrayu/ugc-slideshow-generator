# React Artifact Template

Use this as the structural blueprint for the UGC slideshow artifact.

---

## Component Structure (in order)

1. `slides` data array
2. `export default function UGCSlideshow()`
3. State declarations
4. `defaultVibes` lookup + `vibes` definitions
5. Theme object `t`
6. Derived values (`activeVibeKey`, `activeVibe`, `slideColors`)
7. JSX: Header → Vibe Override Row → Script Selector → Main Content
8. `function PlatformTips({ t, dark })` — separate component at bottom

---

## Data Shape

```js
const slides = [
  {
    id: 1,
    title: "Script Title",
    emoji: "📖",
    color: "#FF6B6B",       // unique per script
    tags: ["Category", "Emotion: X → Y"],
    vibe: "cozy",           // "cozy" | "hype" | "raw" | "cinematic" | "educational"
    slides: [
      {
        type: "hook",       // "hook" | "problem" | "result" | "cta"
        label: "🎣 HOOK",
        text: "Script text.\nUse \\n for line breaks.",
        sub: "One-sentence visual note for preview bar.",
        visual: "Full 2–4 sentence shoot direction. Shot type, location, action, camera style, key detail.",
      },
      { type: "problem", label: "😤 PROBLEM", text: "...", sub: "...", visual: "..." },
      { type: "result",  label: "✨ RESULT",  text: "...", sub: "...", visual: "..." },
      { type: "cta",     label: "📲 CTA",     text: "...", sub: "...", visual: "..." },
    ],
  },
];
```

The `visual` field falls back to `sub` if empty, but always generate both. The `vibe` field on each script drives the Shoot Guide's Vibe Notes panel.

---

## State

```js
const [activeScript, setActiveScript] = useState(0);
const [activeSlide, setActiveSlide]   = useState(0);
const [copied, setCopied]             = useState(null);
const [dark, setDark]                 = useState(true);
const [vibeOverride, setVibeOverride] = useState(null); // null = auto
```

---

## Default Vibes Lookup

Assign per script ID. Use script's `vibe` field if available, otherwise fall back to this lookup:

```js
const defaultVibes = {
  // assign "cozy" | "hype" | "raw" | "cinematic" | "educational" per ID
};
const activeVibeKey = vibeOverride || defaultVibes[script.id] || script.vibe || "raw";
const activeVibe = vibes[activeVibeKey];
```

---

## Vibe Definitions

```js
const vibes = {
  cozy: {
    label: "Cozy", icon: "🛋️", color: "#C27B45",
    lighting:  "Warm tungsten or candlelight. Avoid harsh overheads.",
    pacing:    "Slow cuts — 3–5 sec each. Let moments breathe.",
    audio:     "Lo-fi hip hop, soft piano, or total silence.",
    editing:   "Soft fade transitions. No jump cuts.",
    textStyle: "Lowercase or sentence case. Rounded font if possible.",
    props:     "Blankets, steam rising from drinks, worn books, soft shadows, plants.",
  },
  hype: {
    label: "Hype", icon: "⚡", color: "#F59E0B",
    lighting:  "Bright, high contrast. Ring light or natural window light.",
    pacing:    "Fast cuts — 0.5–1.5 sec. Sync to beat drops.",
    audio:     "Trending audio. High energy. Beat-synced text reveals.",
    editing:   "Jump cuts, zoom punches, text animations timed to music.",
    textStyle: "ALL CAPS. Bold. Large. Flash on-screen fast.",
    props:     "Minimal — let the energy carry it. Motion is the prop.",
  },
  raw: {
    label: "Raw", icon: "🎙️", color: "#94A3B8",
    lighting:  "Natural daylight or a single soft source. Imperfect is fine.",
    pacing:    "One-take energy. Minimal cuts. Let pauses exist.",
    audio:     "No background music. Room ambiance only. Or one quiet track.",
    editing:   "As little as possible. A few cuts max. First takes preferred.",
    textStyle: "Minimal text overlays. Let the voice do the work.",
    props:     "Whatever is naturally around. Authenticity over staging.",
  },
  cinematic: {
    label: "Cinematic", icon: "🎬", color: "#818CF8",
    lighting:  "Golden hour, practical lights, or moody low-key setups.",
    pacing:    "Deliberate — 2–4 sec holds. Never rushed.",
    audio:     "Instrumental score, ambient soundscape, or emotional track.",
    editing:   "Color grade everything. Consistent LUT. Smooth transitions.",
    textStyle: "Elegant, small, lower-third placement. Serif if possible.",
    props:     "Carefully chosen. Every object in frame is intentional.",
  },
  educational: {
    label: "Educational", icon: "📚", color: "#34D399",
    lighting:  "Clean, even, bright. No drama — clarity over mood.",
    pacing:    "Measured — enough time to read every word on screen.",
    audio:     "Neutral background music or none. Never distracting.",
    editing:   "Text overlays, simple graphics, diagrams welcome.",
    textStyle: "Clear, readable, high contrast. Bullet points okay.",
    props:     "Books, notebooks, phone screens. Study-adjacent objects.",
  },
};
```

---

## Vibe Override Row UI

Place between the header and script selector:

```jsx
<div style={{ display: "flex", alignItems: "center", justifyContent: "center", gap: 6, marginBottom: 20, flexWrap: "wrap" }}>
  <span style={{ fontSize: 10, color: t.textDim, letterSpacing: "0.12em", fontWeight: 700, marginRight: 4 }}>VIBE</span>
  {/* AUTO pill */}
  <button onClick={() => setVibeOverride(null)} style={{
    background: vibeOverride === null ? (dark ? "#2a2a2a" : "#E8E3DC") : "transparent",
    color: vibeOverride === null ? t.text : t.textDim,
    border: `1px solid ${vibeOverride === null ? t.label : t.inactiveBtnBorder}`,
    borderRadius: 20, padding: "3px 10px", fontSize: 10, cursor: "pointer",
    fontFamily: "'Courier New', monospace", fontWeight: 700, letterSpacing: "0.08em",
  }}>AUTO</button>
  {/* Vibe pills */}
  {Object.entries(vibes).map(([key, v]) => (
    <button key={key} onClick={() => setVibeOverride(key === vibeOverride ? null : key)} style={{
      background: vibeOverride === key ? `${v.color}22` : "transparent",
      color: vibeOverride === key ? v.color : t.textDim,
      border: `1px solid ${vibeOverride === key ? v.color : t.inactiveBtnBorder}`,
      borderRadius: 20, padding: "3px 10px", fontSize: 10, cursor: "pointer",
      fontFamily: "'Courier New', monospace", fontWeight: 700, letterSpacing: "0.08em",
    }}>{v.icon} {v.label}</button>
  ))}
</div>
```

---

## Vibe Badge (in Script Meta Bar)

```jsx
<span style={{
  fontSize: 10, background: `${activeVibe.color}22`, color: activeVibe.color,
  border: `1px solid ${activeVibe.color}55`, borderRadius: 20,
  padding: "2px 10px", letterSpacing: "0.08em", fontWeight: 700,
}}>
  {activeVibe.icon} {activeVibe.label}{vibeOverride === null ? " ·auto" : " ·override"}
</span>
```

---

## Shoot Guide Panel Structure

Inside the panel, in this order:

1. **Header** — "🎬 SHOOT GUIDE" label + "what to film for each slide"
2. **Vibe Notes row** — 6 specs grid (Lighting, Pacing, Audio, Editing, Text Style, Props)
3. **Slide-by-slide directions** — 4 rows, color-coded by type, showing `s.visual || s.sub`
4. **`<PlatformTips t={t} dark={dark} />`** — separate component

---

## Platform Tips Component

Separate `function PlatformTips({ t, dark })` at the bottom of the file. Contains:
- 4 platform tabs: TikTok, YouTube Shorts, Instagram Reels, X/Twitter
- 6 specs per tab: Duration, Cuts, Audio, Text, CTA, Loop

### X/Twitter Color Fix

X uses `#000000` which is invisible on dark backgrounds. Define adaptive colors:

```js
x: {
  label: "X / Twitter", icon: "𝕏",
  color: "#888888",       // fallback
  darkColor: "#cccccc",   // used in dark mode
  lightColor: "#333333",  // used in light mode
  tips: [...],
}
```

Apply in rendering:
```js
const pColor = key === "x" ? (dark ? val.darkColor : val.lightColor) : val.color;
```

Use `pColor` for the tab button color, border, background tint, and tips grid label color.

---

## Theme Object

```js
const t = dark ? {
  bg: "#0a0a0a", surface: "#141414", surfaceAlt: "#1a1a1a",
  border: "#2e2e2e", borderFaint: "#222",
  text: "#ffffff", textStrong: "#ffffff", textMuted: "#a0a0a0", textDim: "#777",
  label: "#cccccc", labelDim: "#999", counter: "#666",
  summaryColor: "#aaaaaa", footerColor: "#555",
  slideTypeBg:     { hook: "#1a1800", problem: "#1a0a0a", result: "#071a0e", cta: "#080d1a" },
  slideTypeLabel:  { hook: "#FFE14D", problem: "#FF5252", result: "#4DFFAA", cta: "#6EB5FF" },
  slideTypeBorder: { hook: "#FFE14D", problem: "#FF5252", result: "#4DFFAA", cta: "#6EB5FF" },
  toggleBg: "#1e1e1e", toggleBorder: "#3a3a3a", toggleText: "#cccccc",
  inactiveBtnBorder: "#3a3a3a",
} : {
  bg: "#F4F1ED", surface: "#FFFFFF", surfaceAlt: "#EDE9E3",
  border: "#C8C0B5", borderFaint: "#DDD8D0",
  text: "#1A1614", textStrong: "#0D0B0A", textMuted: "#5A4F47", textDim: "#7A6E67",
  label: "#3D3530", labelDim: "#6B5F58", counter: "#7A6E67",
  summaryColor: "#5A4F47", footerColor: "#A89E97",
  slideTypeBg:     { hook: "#FFFBEA", problem: "#FFF0EE", result: "#EDFFF5", cta: "#EEF4FF" },
  slideTypeLabel:  { hook: "#7A5C00", problem: "#A01010", result: "#0A5C30", cta: "#0A2E7A" },
  slideTypeBorder: { hook: "#C49A00", problem: "#CC3333", result: "#1A9955", cta: "#2255BB" },
  toggleBg: "#E8E3DC", toggleBorder: "#BFB8B0", toggleText: "#3D3530",
  inactiveBtnBorder: "#BFB8B0",
};
```

---

## Critical Rendering Rules

### ❌ NEVER webkit gradient text on H1
```js
// BROKEN on state toggle — do not use
background: "linear-gradient(...)",
WebkitBackgroundClip: "text",
WebkitTextFillColor: "transparent",
```

### ✅ Always use solid color for H1
```js
color: dark ? "#ffffff" : "#0D0B0A"
```

---

## Font Weight Standards

| Element | Min Weight |
|---------|------------|
| H1 title | 900 |
| Script title in meta bar | 800 |
| Slide body text | 700 |
| Vibe notes keys | 800 |
| Vibe notes values | 600 |
| Director's note | 600 |
| Full script card text | 600 |
| Platform tips keys | 800 |
| Platform tips values | 600 |

---

## Color Palette for Script Accent Colors

Rotate — never repeat in one batch:

```
#FF6B6B #4ECDC4 #A855F7 #F97316 #EC4899 #6366F1 #10B981 #F59E0B
#EF4444 #0EA5E9 #7C3AED #22C55E #92400E #6B7280 #BE185D #064E3B #1E3A5F #D97706
```
