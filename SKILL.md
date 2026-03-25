---
name: card-ui-design
description: "Generate production-ready card UI components for web applications. Use this skill whenever the user asks for card layouts, card grids, product cards, profile cards, dashboard cards, content cards, pricing cards, or any card-based UI component. Also trigger when the user mentions 'card design', 'card component', 'card grid', 'card list', 'tile layout', or requests UI for displaying collections of items (products, articles, team members, features, stats, testimonials, portfolios). Even if the user doesn't explicitly say 'card', trigger when they ask for a grid of items, a listing page, a product catalog view, a dashboard with stats boxes, a team page, a feature showcase, or any repeating content block layout. Covers HTML+CSS, React/JSX, and vanilla JS implementations with responsive grid systems, hover interactions, skeleton loading states, and accessibility compliance."
---

# Card UI Design Skill

Generate polished, accessible, production-ready card UI components. This skill produces real working code — not mockups or wireframes.

## When You Read This Skill

Before writing any code, read this file fully. For advanced patterns (accessibility deep-dive, animation recipes, responsive breakpoint tables), read the relevant file in `references/`.

## Core Philosophy

Cards are content containers that group related information into scannable, self-contained units. Every card should follow the **"One Card, One Topic"** rule — each card represents exactly one idea, product, or piece of content. This is the single most important principle; violating it makes the entire layout harder to scan.

Think of cards like physical playing cards or business cards: compact, consistent in shape, and focused on a single subject.

## Card Anatomy

A card is built from these structural layers (not all are required for every variant):

1. **Container** — the outer boundary (border, shadow, or background) that separates the card from its surroundings
2. **Media area** — image, video thumbnail, icon, or illustration (typically top or left)
3. **Header** — title and optional subtitle/metadata (author, date, tags)
4. **Body** — short supporting text, description, or data points
5. **Footer / Actions** — CTAs (buttons, links), secondary actions (share, like, bookmark)

The order matters: lead with the most visually impactful element (usually media), then title, then supporting info, then actions. This mirrors natural scanning patterns (F-pattern for western LTR layouts).

## Design Principles

### 1. Contrast the Card from the Background

Cards need clear visual separation from the page. Three common approaches:

- **Elevated** — `box-shadow` (e.g., `0 1px 3px rgba(0,0,0,0.12), 0 1px 2px rgba(0,0,0,0.08)`)
- **Outlined** — `border: 1px solid` with a subtle color (e.g., `#e2e8f0`)
- **Filled** — distinct background color from the page (e.g., white card on gray page)

Pick ONE approach per card set and apply it consistently. Mixing elevation styles within the same grid breaks visual rhythm.

### 2. Spacing System (8pt Grid)

Use an 8px base unit for all spacing:

- Card internal padding: `16px` (2×) or `24px` (3×)
- Gap between cards: `16px`, `24px`, or `32px`
- Text spacing within card: `8px` between elements, `16px` between sections

This creates consistent visual rhythm. All padding, margin, and gap values should be multiples of 8.

### 3. Typography Hierarchy

Inside each card, establish clear hierarchy:

- **Title**: bold, 16–20px, high contrast color
- **Subtitle/metadata**: regular or medium weight, 12–14px, muted color
- **Body text**: regular weight, 14–16px, standard text color
- **CTA text**: medium/bold, 14px, accent color or button style

Limit body text to 2–3 lines. If content varies in length, use `-webkit-line-clamp` to truncate consistently. This prevents card height misalignment in grids.

### 4. Image Handling

- Use `object-fit: cover` to prevent distortion
- Set a consistent `aspect-ratio` (e.g., `16/9`, `4/3`, `1/1`) across all cards in a grid
- Add `loading="lazy"` for images below the fold
- Always provide `alt` text for meaningful images
- Consider placeholder/skeleton for loading states

### 5. Interactive States

Cards that link to detail pages should feel clickable:

```
Hover:  box-shadow increase + slight translateY(-2px)
Focus:  visible outline (2px solid accent color, 2px offset)
Active: scale(0.98) or shadow decrease for "press" feel
```

CSS state order matters: `:hover` → `:focus` → `:active`. Writing them out of order causes specificity issues where states override each other.

Make the **entire card** the click target (not just the title or a small button). Use a wrapping `<a>` or a pseudo-element overlay technique. This benefits touch users and motor-impaired users with larger tap targets.

### 6. Responsive Grid

Cards are inherently responsive. Use CSS Grid with `auto-fill` / `auto-fit` for fluid layouts:

```css
.card-grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(280px, 1fr));
  gap: 24px;
}
```

This automatically reflows from 3+ columns on desktop to 1 column on mobile without media queries. Adjust the `minmax` first value based on card content density:

- Content-heavy cards: `300px–350px`
- Compact/product cards: `240px–280px`
- Minimal/stat cards: `180px–220px`

For more controlled breakpoints, see `references/responsive-patterns.md`.

### 7. Loading / Skeleton State

Always provide a skeleton state that mirrors the card layout. The skeleton should match the shape and approximate size of each content block within the card:

```css
.skeleton {
  background: linear-gradient(90deg, #f0f0f0 25%, #e0e0e0 50%, #f0f0f0 75%);
  background-size: 200% 100%;
  animation: shimmer 1.5s infinite;
  border-radius: 4px;
}
@keyframes shimmer {
  0% { background-position: 200% 0; }
  100% { background-position: -200% 0; }
}
```

This tells the user what type of content to expect, reducing perceived loading time.

## Card Variants

Choose the right variant for the use case:

| Variant | Use Case | Key Elements |
|---------|----------|-------------|
| **Product Card** | E-commerce, marketplace | Image, title, price, rating, CTA button |
| **Article/Blog Card** | News, magazine, blog | Thumbnail, title, excerpt, author, date, read time |
| **Profile Card** | Team pages, social | Avatar, name, role, bio, social links |
| **Stat/Metric Card** | Dashboards, analytics | Icon, number, label, trend indicator |
| **Pricing Card** | SaaS, plans comparison | Plan name, price, feature list, CTA |
| **Testimonial Card** | Landing pages | Quote, avatar, name, company |
| **Feature Card** | Product pages, landing | Icon/illustration, heading, description |
| **Media Card** | Gallery, portfolio | Full-bleed image, overlay text on hover |
| **Notification Card** | Feeds, activity logs | Icon, message, timestamp, action |
| **Horizontal Card** | Lists, search results | Side-by-side image + text layout |

For detailed code templates of each variant, see `references/card-variants.md`.

## Accessibility Checklist

These are not optional polish — they are requirements:

- [ ] Cards wrapped in `<ul>` + `<li>` when part of a collection (provides count and boundaries to screen readers)
- [ ] Heading level used for card title (`<h2>` or `<h3>`, matching page hierarchy)
- [ ] Images have descriptive `alt` text (or `alt=""` if purely decorative)
- [ ] Minimum 44×44px touch target for any interactive element
- [ ] Color contrast: 4.5:1 for body text, 3:1 for large text and UI elements
- [ ] Focus indicator visible on keyboard navigation (never `outline: none` without replacement)
- [ ] If the entire card is a link, avoid redundant links inside it (don't have both a card-level link and a separate title link pointing to the same destination)
- [ ] DOM order matches visual order (use CSS `order` for visual rearrangement, not HTML reordering)

## Implementation Patterns

### Pattern A: Vanilla HTML + CSS (Recommended Default)

Use this when the user's stack is vanilla HTML/JS or when building static pages. No framework dependencies.

```html
<ul class="card-grid" role="list">
  <li class="card">
    <a href="/detail/1" class="card-link">
      <div class="card-media">
        <img src="..." alt="Description" loading="lazy">
      </div>
      <div class="card-content">
        <h3 class="card-title">Title</h3>
        <p class="card-desc">Short description text...</p>
      </div>
      <div class="card-footer">
        <span class="card-meta">Meta info</span>
        <span class="card-action">View →</span>
      </div>
    </a>
  </li>
  <!-- more cards -->
</ul>
```

CSS variables for theming:

```css
:root {
  --card-bg: #ffffff;
  --card-border: #e2e8f0;
  --card-shadow: 0 1px 3px rgba(0,0,0,0.1);
  --card-shadow-hover: 0 4px 12px rgba(0,0,0,0.15);
  --card-radius: 12px;
  --card-padding: 16px;
  --card-gap: 24px;
  --card-transition: 0.2s ease;
  --text-primary: #1a202c;
  --text-secondary: #718096;
  --accent: #3182ce;
}
```

### Pattern B: React / JSX

Use when the user works with React. Use Tailwind utility classes when the user's project uses Tailwind; otherwise, use CSS Modules or styled-components.

```jsx
function Card({ title, description, image, href, meta }) {
  return (
    <li className="card">
      <a href={href} className="card-link">
        {image && (
          <div className="card-media">
            <img src={image} alt={title} loading="lazy" />
          </div>
        )}
        <div className="card-content">
          <h3 className="card-title">{title}</h3>
          {description && <p className="card-desc">{description}</p>}
        </div>
        {meta && (
          <div className="card-footer">
            <span className="card-meta">{meta}</span>
          </div>
        )}
      </a>
    </li>
  );
}
```

### Pattern C: Dashboard / Stat Cards

Stat cards have a different anatomy — no media area, emphasis on a big number:

```html
<div class="stat-card">
  <div class="stat-icon"><!-- SVG icon --></div>
  <div class="stat-body">
    <span class="stat-value">2,847</span>
    <span class="stat-label">Active Users</span>
  </div>
  <div class="stat-trend positive">+12.5%</div>
</div>
```

## Anti-Patterns to Avoid

- **Overloading**: cramming too many actions, text blocks, or data points into one card. If it needs a scroll bar, it's not a card anymore.
- **Inconsistent heights**: mixing cards with different heights in the same row. Use fixed heights with text clamping, or use `grid-auto-rows: 1fr` for equal-height rows.
- **Click target ambiguity**: having multiple competing link targets inside one card. Users shouldn't have to guess what happens when they click.
- **Missing hover/focus states**: if a card links somewhere, it must look interactive. A flat rectangle with no state changes feels broken.
- **Decorative-only shadows**: shadows should serve the purpose of visual separation from background. Don't add shadows inside cards or use them as decoration.
- **Infinite scroll without pagination**: for large card collections, paginate or use "load more". Endless scrolling causes scroll fatigue and hurts accessibility.

## Dark Mode Considerations

When implementing dark mode for cards:

- Reverse the elevation model: in light mode, shadows push cards forward; in dark mode, use lighter background tints instead of shadows (shadows are invisible on dark backgrounds)
- Card background should be slightly lighter than page background (e.g., page `#121212`, card `#1e1e1e`)
- Reduce image opacity slightly (e.g., `opacity: 0.9`) to prevent images from "glaring" against dark surroundings
- Maintain contrast ratios — check with tools, don't eyeball it

```css
@media (prefers-color-scheme: dark) {
  :root {
    --card-bg: #1e1e1e;
    --card-border: #2d3748;
    --card-shadow: 0 1px 3px rgba(0,0,0,0.3);
    --text-primary: #e2e8f0;
    --text-secondary: #a0aec0;
  }
}
```

## Output Expectations

When generating card UI code, always deliver:

1. **Complete, runnable HTML file** (or React component) — no pseudo-code or partial snippets
2. **CSS variables** at the root for easy theming
3. **Responsive grid** that works from mobile to desktop without breakpoints when possible
4. **Hover and focus states** for all interactive cards
5. **Semantic HTML** with proper heading levels, lists, and alt text
6. **At least 3–6 example cards** with realistic placeholder content (not "Lorem ipsum" — use contextually appropriate placeholder text)
7. **Skeleton loading state** if the user's use case involves dynamic data

If the user provides a specific design or screenshot, match the visual as closely as possible while maintaining accessibility standards.

## Reference Files

For deeper implementation details, read these as needed:

- `references/card-variants.md` — Full code templates for each card variant (product, article, profile, stat, pricing, testimonial, feature, media, horizontal)
- `references/responsive-patterns.md` — Breakpoint strategies, container queries, and layout shift prevention