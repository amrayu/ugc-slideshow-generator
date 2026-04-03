# React Artifact Template

Use this as the structural blueprint for the UGC slideshow artifact. Replace all placeholder values with real generated content.

## Component Structure

The component has 6 sections in order:
1. DATA — the `slides` array and `typeColors` object
2. HEADER — product name, title, subtitle with target demo
3. SCRIPT SELECTOR — tab buttons, one per script
4. SCRIPT META BAR — title, emoji, tag pills
5. SLIDE NAVIGATOR + PREVIEW — type tabs, phone-style preview, director note, copy button
6. FULL SCRIPT EXPAND + PRODUCTION TIPS

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

const typeColors = {
  hook:    { bg: "#0f0f0f", border: "#FFE66D", label: "#FFE66D" },
  problem: { bg: "#1a0a0a", border: "#FF6B6B", label: "#FF6B6B" },
  result:  { bg: "#0a1a0a", border: "#6EE7B7", label: "#6EE7B7" },
  cta:     { bg: "#0a0a1a", border: "#93C5FD", label: "#93C5FD" },
};
```

## Global Style Rules

- Background: `#080808`
- Font: `'Courier New', monospace`
- Header font: `'Georgia', serif`
- Avoid Inter, Roboto, system-ui
- Header label: `[PRODUCT] × [BRAND]`
- Subtitle: `[N] emotional hooks for [target demo]`
- Footer: `[BRAND] — FOR INTERNAL USE`

## Color Palette (rotate, never repeat in one batch)

#FF6B6B #4ECDC4 #A855F7 #F97316 #EC4899 #6366F1 #10B981 #F59E0B
#EF4444 #0EA5E9 #7C3AED #22C55E #92400E #6B7280 #BE185D #064E3B #1E3A5F #D97706
