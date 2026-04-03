# React Artifact Template

Use this as the structural blueprint for the UGC slideshow artifact. Replace all placeholder values with real generated content.

---

## Component Structure

The component has 6 sections in order:
1. DATA — the `slides` array
2. HEADER — dark/light toggle button, product name, title, subtitle with target demo
3. SCRIPT SELECTOR — tab buttons, one per script
4. SCRIPT META BAR — title, emoji, tag pills
5. SLIDE NAVIGATOR + PREVIEW — type tabs, phone-style preview, director note, copy button
6. FULL SCRIPT EXPAND + PRODUCTION TIPS

---

## Data Shape

```js
const slides = [
  {
    id: 1,
    title: "Script Title",
    emoji: "📖",
    color: "#FF6B6B",       // unique per script, see color palette below
    tags: ["Category", "Emotion: X → Y"],
    slides: [
      { type: "hook",    label: "🎣 HOOK",    text: "...", sub: "Director note" },
      { type: "problem", label: "😤 PROBLEM", text: "...", sub: "Director note" },
      { type: "result",  label: "✨ RESULT",  text: "...", sub: "Director note" },
      { type: "cta",     label: "📲 CTA",     text: "...", sub: "Director note" },
    ],
  },
];
```

There is NO standalone `typeColors` object. Slide type colors are defined inside the theme object `t` (see below).

---

## State

```js
const [activeScript, setActiveScript] = useState(0);
const [activeSlide, setActiveSlide]   = useState(0);
const [copied, setCopied]             = useState(null);
const [dark, setDark]                 = useState(true);  // dark mode on by default
```

---

## Theme Object

All colors must route through `t`. Define `t` based on the `dark` boolean. Never hardcode dark/light colors directly into JSX — always use `t.*`.

```js
const t = dark ? {
  // DARK THEME
  bg: "#0a0a0a", surface: "#141414", surfaceAlt: "#1a1a1a",
  border: "#2e2e2e", borderFaint: "#222",
  text: "#ffffff", textStrong: "#ffffff", textMuted: "#a0a0a0", textDim: "#777",
  label: "#cccccc", labelDim: "#999", counter: "#666",
  summaryColor: "#aaaaaa", footerColor: "#555",
  slideTypeBg:     { hook: "#1a1800",  problem: "#1a0a0a",  result: "#071a0e",  cta: "#080d1a"  },
  slideTypeLabel:  { hook: "#FFE14D",  problem: "#FF5252",  result: "#4DFFAA",  cta: "#6EB5FF"  },
  slideTypeBorder: { hook: "#FFE14D",  problem: "#FF5252",  result: "#4DFFAA",  cta: "#6EB5FF"  },
  toggleBg: "#1e1e1e", toggleBorder: "#3a3a3a", toggleText: "#cccccc",
  inactiveBtnBorder: "#3a3a3a",
} : {
  // LIGHT THEME
  bg: "#F4F1ED", surface: "#FFFFFF", surfaceAlt: "#EDE9E3",
  border: "#C8C0B5", borderFaint: "#DDD8D0",
  text: "#1A1614", textStrong: "#0D0B0A", textMuted: "#5A4F47", textDim: "#7A6E67",
  label: "#3D3530", labelDim: "#6B5F58", counter: "#7A6E67",
  summaryColor: "#5A4F47", footerColor: "#A89E97",
  slideTypeBg:     { hook: "#FFFBEA",  problem: "#FFF0EE",  result: "#EDFFF5",  cta: "#EEF4FF"  },
  slideTypeLabel:  { hook: "#7A5C00",  problem: "#A01010",  result: "#0A5C30",  cta: "#0A2E7A"  },
  slideTypeBorder: { hook: "#C49A00",  problem: "#CC3333",  result: "#1A9955",  cta: "#2255BB"  },
  toggleBg: "#E8E3DC", toggleBorder: "#BFB8B0", toggleText: "#3D3530",
  inactiveBtnBorder: "#BFB8B0",
};
```

---

## Critical Rendering Rules

### ❌ NEVER use webkit gradient text on the H1
This pattern breaks on React state toggles — the background swaps but the clip doesn't re-apply, turning the title into a colored block:
```js
// BROKEN — do not use
background: "linear-gradient(...)",
WebkitBackgroundClip: "text",
WebkitTextFillColor: "transparent",
```

### ✅ ALWAYS use solid color for the H1
```js
<h1 style={{
  fontSize: "clamp(20px, 5vw, 32px)",
  fontWeight: 900,
  fontFamily: "'Georgia', serif",
  letterSpacing: "-0.02em",
  margin: 0,
  color: dark ? "#ffffff" : "#0D0B0A",   // plain solid color, toggles cleanly
}}>
  UGC Script Generator
</h1>
```

---

## Font Weight Standards

High contrast and legibility are required. Use these minimum weights:

| Element | Min Weight |
|---------|------------|
| H1 title | 900 |
| Script title in meta bar | 800 |
| Slide body text (main preview) | 700 |
| Production tips keys | 800 |
| Production tips values | 600 |
| Director's note | 600 |
| Full script card text | 600 |
| Slide type label (HOOK / PROBLEM etc.) | 700 |
| Header eyebrow (PRODUCT × BRAND) | 700 |
| Subtitle | 600 |

---

## Toggle Button

Place in the header `div`, `position: absolute, right: 0, top: 0`:

```jsx
<button
  onClick={() => setDark(!dark)}
  style={{
    position: "absolute", right: 0, top: 0,
    background: t.toggleBg, border: `1px solid ${t.toggleBorder}`,
    color: t.toggleText, borderRadius: 4, padding: "5px 12px",
    fontSize: 11, cursor: "pointer", fontFamily: "'Courier New', monospace",
    letterSpacing: "0.1em", transition: "all 0.2s",
  }}
>
  {dark ? "☀ LIGHT" : "☾ DARK"}
</button>
```

---

## Global Style Rules

- Root background: `t.bg`
- Font: `'Courier New', monospace`
- Header font: `'Georgia', serif`
- Avoid Inter, Roboto, system-ui
- Header eyebrow: `[PRODUCT] × [BRAND]`
- Subtitle: `[N] emotional hooks for [target demo]`
- Footer: `[BRAND] — FOR INTERNAL USE`
- Add `transition: "background 0.2s, color 0.2s"` to the root div for smooth toggling

---

## Color Palette for Script Accent Colors (rotate, never repeat in one batch)

#FF6B6B #4ECDC4 #A855F7 #F97316 #EC4899 #6366F1 #10B981 #F59E0B
#EF4444 #0EA5E9 #7C3AED #22C55E #92400E #6B7280 #BE185D #064E3B #1E3A5F #D97706
