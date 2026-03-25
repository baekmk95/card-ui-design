# Responsive Card Layout Patterns

Strategies for making card grids work across all screen sizes without breaking layouts.

## Table of Contents

1. [CSS Grid Auto-Fill (Recommended Default)](#css-grid-auto-fill)
2. [Fixed Column Breakpoints](#fixed-column-breakpoints)
3. [Container Queries](#container-queries)
4. [Masonry Layout](#masonry-layout)
5. [Horizontal Scroll (Mobile)](#horizontal-scroll)
6. [Layout Shift Prevention](#layout-shift-prevention)

---

## CSS Grid Auto-Fill

The simplest and most robust approach. No media queries needed for basic reflow.

```css
.card-grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(280px, 1fr));
  gap: 24px;
  padding: 0;
  list-style: none;
}
```

**How `minmax` values map to column counts:**

| minmax value | 1440px screen | 1024px screen | 768px screen | 375px screen |
|-------------|---------------|---------------|-------------|-------------|
| `180px`     | ~6 cols       | ~4 cols       | ~3 cols     | 2 cols      |
| `240px`     | ~5 cols       | ~3 cols       | ~2 cols     | 1 col       |
| `280px`     | ~4 cols       | ~3 cols       | ~2 cols     | 1 col       |
| `320px`     | ~4 cols       | ~3 cols       | ~2 cols     | 1 col       |
| `360px`     | ~3 cols       | ~2 cols       | ~2 cols     | 1 col       |

**`auto-fill` vs `auto-fit`:**
- `auto-fill`: keeps empty column tracks (cards stay at min width even if grid has space). Better when you want consistent card sizes.
- `auto-fit`: collapses empty tracks (cards stretch to fill available space). Better when you have few cards and want them to fill the row.

For most card grids, `auto-fill` is the safer choice.

---

## Fixed Column Breakpoints

When you need exact control over column counts per breakpoint.

```css
.card-grid {
  display: grid;
  gap: 24px;
  grid-template-columns: 1fr;
}

@media (min-width: 640px) {
  .card-grid { grid-template-columns: repeat(2, 1fr); }
}

@media (min-width: 1024px) {
  .card-grid { grid-template-columns: repeat(3, 1fr); }
}

@media (min-width: 1440px) {
  .card-grid { grid-template-columns: repeat(4, 1fr); }
}
```

**Common breakpoint patterns:**

| Pattern | Mobile | Tablet | Desktop | Wide |
|---------|--------|--------|---------|------|
| Standard | 1 col | 2 col | 3 col | 4 col |
| E-commerce | 2 col | 3 col | 4 col | 5 col |
| Dashboard | 1 col | 2 col | 3 col | 4 col |
| Blog/News | 1 col | 2 col | 3 col | 3 col |

---

## Container Queries

Modern approach where cards respond to their container width, not the viewport. Ideal when cards appear in sidebars, modals, or varying-width panels.

```css
.card-grid-wrapper {
  container-type: inline-size;
  container-name: card-area;
}

.card-grid {
  display: grid;
  gap: 24px;
  grid-template-columns: 1fr;
}

@container card-area (min-width: 500px) {
  .card-grid { grid-template-columns: repeat(2, 1fr); }
}

@container card-area (min-width: 800px) {
  .card-grid { grid-template-columns: repeat(3, 1fr); }
}
```

**Browser support:** Container queries are supported in all modern browsers (Chrome 105+, Firefox 110+, Safari 16+). No polyfill needed for 2024+ projects.

---

## Masonry Layout

For Pinterest-style variable-height cards. Two approaches:

### A. CSS Columns (Simple, Works Now)

```css
.card-masonry {
  columns: 3 280px;
  column-gap: 24px;
}

.card-masonry .card {
  break-inside: avoid;
  margin-bottom: 24px;
}
```

**Limitation:** items flow top-to-bottom per column, not left-to-right. Users may find this order confusing for sequential content.

### B. CSS Grid Masonry (Experimental)

```css
.card-masonry {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(280px, 1fr));
  grid-template-rows: masonry;
  gap: 24px;
}
```

**Note:** `grid-template-rows: masonry` is only available in Firefox (behind a flag) and Safari Technology Preview as of early 2025. Use CSS Columns as the stable fallback.

---

## Horizontal Scroll (Mobile)

For mobile, sometimes a horizontal scroll is better than stacking — especially for category browsing or featured items.

```css
.card-scroll {
  display: flex;
  gap: 16px;
  overflow-x: auto;
  scroll-snap-type: x mandatory;
  -webkit-overflow-scrolling: touch;
  padding: 8px 0;
  scrollbar-width: none; /* Firefox */
}

.card-scroll::-webkit-scrollbar {
  display: none; /* Chrome, Safari */
}

.card-scroll .card {
  flex: 0 0 280px;
  scroll-snap-align: start;
}
```

**Accessibility consideration:** horizontal scrolling is less discoverable than vertical scrolling. Always show a partial next card peeking from the edge to signal that more content exists. Consider adding left/right arrow buttons for keyboard and mouse users.

```css
/* Show a peek of the next card */
.card-scroll {
  padding-right: 40px; /* ensures partial card is visible */
}
```

---

## Layout Shift Prevention

Cards loading with dynamic content (images, async data) can cause layout shifts (CLS). Prevent this:

### Fixed Aspect Ratio for Images

```css
.card-media {
  aspect-ratio: 16/9;
  overflow: hidden;
  background: #f0f0f0; /* placeholder color while loading */
}

.card-media img {
  width: 100%;
  height: 100%;
  object-fit: cover;
}
```

### Equal-Height Cards in Grid

```css
.card-grid {
  grid-auto-rows: 1fr; /* all rows same height */
}
```

Or if card content varies significantly, let cards be their natural height and accept uneven rows — this is preferable to either truncating content or adding excessive whitespace.

### Skeleton Placeholder

```css
.card-skeleton {
  background: var(--card-bg);
  border-radius: var(--card-radius);
  overflow: hidden;
}

.skeleton-block {
  background: linear-gradient(90deg, #f0f0f0 25%, #e0e0e0 50%, #f0f0f0 75%);
  background-size: 200% 100%;
  animation: shimmer 1.5s ease-in-out infinite;
  border-radius: 4px;
}

.skeleton-block--media {
  aspect-ratio: 16/9;
  border-radius: 0;
}

.skeleton-block--title {
  height: 20px;
  width: 70%;
}

.skeleton-block--text {
  height: 14px;
  width: 100%;
}

.skeleton-block--text-short {
  height: 14px;
  width: 50%;
}

@keyframes shimmer {
  0% { background-position: 200% 0; }
  100% { background-position: -200% 0; }
}
```

### Explicit Width/Height on Images

Always set dimensions on images to reserve layout space:

```html
<img src="..." alt="..." width="400" height="225" loading="lazy">
```

The browser uses these to calculate the aspect ratio before the image loads, preventing layout shifts.