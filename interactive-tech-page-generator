---
name: interactive-tech-page-generator
description: >
  Generate interactive, visually polished single-page frontends that explain AI model architectures,
  research papers, or technical systems. Produces React + Vite + TypeScript projects with scroll-triggered
  animations, interactive SVG architecture diagrams, benchmark charts, algorithm visualizations,
  and bilingual (Chinese/English) support. Use this skill whenever the user asks to build an
  interactive architecture explainer page, model introduction site, paper companion page, or technical
  system overview with dynamic visualizations — even if they don't explicitly name a framework.
  This skill is NOT for general landing pages, marketing sites, or e-commerce — it's specifically
  for technical/academic content explainers with data-rich visualizations.
---

# Interactive Tech Page Generator

A design pattern library for building interactive technical explainer pages for AI model architectures and research systems.

## Tech Stack

```
React 19 + Vite + TypeScript
Tailwind CSS v4 (with @tailwindcss/vite plugin)
Framer Motion (animations)
Recharts (charts)
lucide-react (icons, optional)
```

## Project Structure

```
project-root/
├── src/
│   ├── main.tsx              # Entry point
│   ├── App.tsx               # Layout: Navbar + scroll sections + Footer
│   ├── index.css             # Tailwind imports + theme variables + keyframes
│   ├── i18n.tsx              # Bilingual context provider
│   ├── data.ts               # Benchmarks, model specs, training curves
│   └── components/
│       ├── Hero.tsx
│       ├── ArchitectureSection.tsx
│       ├── AttentionSection.tsx
│       ├── MHCSection.tsx
│       ├── MuonSection.tsx
│       ├── BenchmarksSection.tsx
│       ├── TrainingPipeline.tsx
│       └── Footer.tsx
├── index.html                # Google Fonts (Playfair Display, Inter, JetBrains Mono)
├── vite.config.ts            # react() + tailwindcss() plugins
└── package.json
```

## Design System

### Theme (Light Academic)

Use Tailwind CSS v4 `@theme` directive to define a cohesive design token set:

```css
@theme {
  --color-paper: #f8f6f1;        /* warm off-white page background */
  --color-ink: #1e1e2e;          /* near-black text */
  --color-ink-light: #6b7280;    /* muted body text */
  --color-ink-lighter: #9ca3af;  /* hint text */
  --color-accent: #7c3aed;       /* primary accent (violet) */
  --color-teal: #0d9488;         /* secondary accent */
  --color-amber: #d97706;        /* tertiary accent */
  --color-rose: #e11d48;         /* quaternary accent */
  --color-border: #e5e1d9;       /* borders and dividers */
  --color-card: #ffffff;         /* card background */
  --font-sans: 'Inter', system-ui, sans-serif;
  --font-serif: 'Playfair Display', Georgia, serif;
  --font-mono: 'JetBrains Mono', monospace;
}
```

### Typography
- **Headings**: `font-serif` (Playfair Display) for section titles and hero text
- **Body**: `font-sans` (Inter) for paragraphs and labels
- **Code/Data**: `font-mono` (JetBrains Mono) for metrics, formulas, technical annotations
- **Section tag**: 12px uppercase tracking-widest in accent color above each title

### Layout Pattern
Each section follows a consistent rhythm:
1. `py-24 px-6` vertical padding
2. Centered max-w-7xl container
3. Animated tag + serif h2 + subtitle paragraph (centered, max-w-2xl)
4. Content grid (variable columns depending on content)
5. `section-divider` between sections (1px gradient border)

### Section Dividers
```css
.section-divider {
  height: 1px;
  background: linear-gradient(to right, transparent, var(--color-border), transparent);
}
```

## Component Patterns

### 1. Hero Section
- Full viewport height, flex column centered
- Subtle background blurs (accent/teal, 5% opacity, blur-3xl)
- Two-column grid: text left, visual right (radar chart)
- Framer Motion staggered entrance: `opacity: 0, y: 40` → `opacity: 1, y: 0`
- Badge pill (research preview indicator)
- CTA buttons + model spec summary strip

### 2. Interactive SVG Architecture Diagram
- Pure SVG with `<rect>`, `<text>`, `<line>` elements
- Each module is a clickable rect (toggle selected state)
- Connection lines between modules with hover highlighting
- Detail panel appears beside diagram on click (AnimatePresence for enter/exit)
- Dual-language text labels in SVG (check `t('nav.architecture')` to determine language)

### 3. Tab-Switched Content Sections
- Toggle group (pill-shaped buttons in a rounded bar)
- Content swaps with Framer Motion `key={activeId}` and AnimatePresence
- Used for: CSA vs HCA comparison, benchmark category switching, training stage details

### 4. Step Flow Pipelines
- Vertical numbered steps connected by vertical lines
- Hover highlights the step card and its number circle
- Each step has: number badge → label → description
- Used for: attention processing pipeline, optimizer steps

### 5. Algorithm Visualization (Canvas)
- HTML Canvas element for custom drawings
- Animatable via `useEffect` + `setInterval` (or `requestAnimationFrame`)
- "Run" button to start the animation, iteration counter display
- Used for: Sinkhorn-Knopp matrix convergence visualization

### 6. Charts (Recharts)
- **Radar chart**: Capability comparison across models (Hero section)
- **Bar chart**: Benchmark scores, efficiency comparison (grouped or stacked)
- **Line chart**: Training convergence curves
- Styling: minimal grid (`strokeDasharray="3 3"`), light gray axis ticks, rounded bar ends
- Legend at bottom with small font

### 7. Training Pipeline Flow
- Horizontal connected stages (cards with arrow connectors between them)
- Arrows: hidden on mobile, visible on `sm:` breakpoint
- Click to expand detail panel below
- Each stage has: tag (subtitle) + title

## i18n System (Bilingual)

### Architecture
- React Context-based: `LangProvider` wraps the app
- `useLang()` hook returns `{ lang, setLang, t }`
- `t(path)` resolves dot-separated keys from translation map
- All components call `t('section.key')` for every user-facing string

### Translation Map Structure
```typescript
type TranslationMap = {
  nav: { architecture: string; ... }
  hero: { badge: string; title: string; subtitle: string; ... }
  sectionName: {
    tag: string;
    title: string;
    subtitle: string;
    details: string | string[];
    ...
  }
}
```
- Support three value types: plain string, string array (for lists), nested Record (for complex objects like property cards)
- Each section has its own namespace under both `en` and `zh`

### Toggle Placement
- Top-right corner of navbar as a toggle button
- Button text: `"中文"` when in English, `"EN"` when in Chinese
- Style: small pill with border, matching nav link styling

### Language Detection in Components
For inline text that depends on language (e.g., chart axis labels, SVG labels), check:
```typescript
const isZh = t('nav.architecture') === '架构'
```
Or use the language-aware data fields pattern (each data item has `.en` and `.zh` variants).

## Animation Strategy

### Scroll-Triggered Entry
Every section wrap uses this Framer Motion pattern:
```tsx
<motion.div
  initial={{ opacity: 0, y: 30 }}
  whileInView={{ opacity: 1, y: 0 }}
  viewport={{ once: true, margin: '-100px' }}
  transition={{ duration: 0.6 }}
>
```

### Staggered Children
Use `transition={{ delay: index * 0.15 }}` with `whileInView` for staggered reveals.

### Interactive Feedback
- Hover: scale, border color, or background tint changes
- Selected/active state: thicker border, subtle shadow, colored background tint
- Use CSS transitions (`transition-all duration-300`) for SVG elements

## Content Architecture

### Data Layer
Centralize all numerical/benchmark data in `src/data.ts`:
- Model specs (params, activated params, context length, training tokens)
- Benchmark arrays (knowledge, reasoning, long-context)
- Efficiency comparison data
- Training convergence data
- Types should be exported for reuse in components

### Content Supply
- Primary source: PDF extraction via Python (pdfplumber/pypdf) → manual curation into i18n translation map
- Benchmark numbers from paper figures → hardcoded in data.ts
- Visual elements: inline SVG (no external assets needed)

## Key Architectural Decisions

1. **No routing library**: Single-page scroll with anchor links. Sections are `<section id="name">` elements, navbar uses `<a href="#name">`.
2. **No CSS modules**: Tailwind utilities throughout. Custom animations and theme in one `index.css`.
3. **No state management library**: React Context for i18n, local state for interactive components.
4. **No external fonts beyond Google Fonts**: Self-hosted alternatives can be used, but Google Fonts is the simplest path.
5. **PDF extraction**: Use Python virtual environment with pdfplumber for text extraction from academic PDFs.

## Section Checklist (for a complete page)

- [ ] Hero: tag + title + subtitle + radar chart
- [ ] Architecture Overview: interactive SVG diagram + detail panel
- [ ] Key Innovation 1 (e.g., Attention): tab-switched comparison + flow diagram
- [ ] Key Innovation 2 (e.g., μHC): canvas visualization + math + property cards
- [ ] Key Innovation 3 (e.g., Optimizer): convergence chart + steps + stat cards
- [ ] Benchmarks: category tabs + bar chart + efficiency chart + takeaways
- [ ] Training Pipeline: horizontal flow + expandable stages + infrastructure cards
- [ ] Footer: description + reference links + copyright

## Edge Cases to Handle
- Long Chinese text in SVG elements: use smaller font sizes (8-9px for SVG subtitles)
- Chart readability: ensure all tooltip styles and fonts are explicit (avoid theme-dependent defaults)
- Mobile: single-column layout at `lg:` breakpoint, hidden nav links
- Content overflow in detail panels: use `leading-relaxed` for paragraphs, `space-y-2` for lists
