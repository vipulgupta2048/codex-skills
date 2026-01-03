# Implementation Patterns

Use these patterns to move quickly while keeping the aesthetic sharp. Load only sections you need.

## Vanilla HTML/CSS/JS Workflow
- Start with semantic structure: `header`, `main`, `section`, `article`, `footer`. Keep nav skip-links (`a.skip-nav` to `#main`).
- Define theme tokens up top:
  ```css
  :root { --bg: #0b0c10; --fg: #f7f2e9; --accent: #ff6b4a; --muted: #9aa1b5; --radius: 18px; --shadow: 0 18px 40px rgba(0,0,0,0.35); }
  ```
- Load fonts via `<link>` or `@import`; set base styles on `body` (smooth scrolling, background texture, max width handling).
- Layout: use CSS Grid for macro layout, Flexbox for inline clusters. Mix asymmetry: stagger column widths (e.g., `grid-template-columns: 1.1fr 0.9fr`).
- Motion: prefer CSS keyframes and `transition: transform 320ms var(--ease)`; orchestrate with delays on child elements. Use `prefers-reduced-motion` guards.
- Interactivity: lean on small JS to toggle classes, e.g., IntersectionObserver for reveal animations.

## React Patterns
- Create a `Theme` object for tokens and pass via context or props. Keep components focused (Hero, FeatureList, TestimonialRail).
- Use CSS Modules, styled-components, or Tailwind? If Tailwind is mandated, extend the config with custom fonts, gradients, and shadows; avoid defaults-only look.
- Animations: prefer Framer Motion for page-load + hover effects; stagger `variants` and keep durations <0.5s.
- Data-driven UI: define arrays for cards, metrics, timelines; map to components to keep markup DRY and easily themeable.
- Accessibility: forward refs for focusable elements; use `aria-live` for status, `aria-pressed` for toggles, and proper `alt` text for imagery.

## Layout & Spacing
- Hero patterns: split-screen with oversized headline and vertical nav stripe; magazine stack with overlapping cards; timeline rail with labeled markers.
- Micro-layout: use 4/8 spacing scale; keep heading-to-body ratio ~1.6–1.8; limit max-width of prose to 68–76ch.
- Negative space vs density: if maximalist, constrain chaos inside frames; if minimal, increase margins and align to a visible grid.

## Color, Texture, and Backgrounds
- Always define CSS variables for palette. Keep 1–2 primary + 1 accent. Add noise overlays to avoid sterile flatness:
  ```css
  .grain { position: fixed; inset: 0; pointer-events: none; background: radial-gradient(circle at 20% 20%, rgba(255,255,255,.04), transparent 40%), repeating-linear-gradient(90deg, rgba(255,255,255,.018), rgba(255,255,255,.018) 1px, transparent 1px, transparent 3px); mix-blend-mode: soft-light; opacity: 0.7; }
  ```
- Gradient mesh idea: layer multiple radial gradients with different sizes and opacities; rotate a pseudo-element slowly.
- Borders: try 1.5–2px strokes with `border-image` gradients for subtle sheen.

## Motion Recipes
- Staggered reveal: apply `transform: translateY(20px); opacity: 0;` then add `.visible` to animate to neutral.
- Magnetic hover: on buttons/cards, use `transition: transform 220ms ease, box-shadow 220ms ease;` and slightly rotate/translate toward cursor.
- Hero load: fade-in background first, then text with 80ms steps, then accent lines sliding in from edges.

## Responsive Guidance
- Collapse grids to single column below 900px; center align key text; maintain comfortable padding (min 18–22px).
- Replace hover-dependent cues with clear focus/active styles. Increase tap targets to 44px minimum.
- Test with viewport meta tag, clamp() for font sizes, and avoid fixed heights; use `minmax` grids.

## QA Checklist
- Color contrast passes WCAG AA for text/background. Verify focus order and skip link.
- Assets load with sensible fallbacks (system font stack declared after customs).
- Animations respect `prefers-reduced-motion: reduce`.
- Verify semantics: one `h1`, landmarks defined, inputs labeled, buttons not masquerading as links.
