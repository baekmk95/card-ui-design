# Card Variant Code Templates

Complete, copy-paste-ready code templates for each card variant. Each template includes HTML structure, CSS styling, and notes on customization.

## Table of Contents

1. [Product Card](#product-card)
2. [Article / Blog Card](#article-blog-card)
3. [Profile / Team Card](#profile-team-card)
4. [Stat / Metric Card](#stat-metric-card)
5. [Pricing Card](#pricing-card)
6. [Testimonial Card](#testimonial-card)
7. [Feature Card](#feature-card)
8. [Media / Portfolio Card](#media-portfolio-card)
9. [Horizontal Card](#horizontal-card)
10. [Notification / Activity Card](#notification-activity-card)

---

## Product Card

E-commerce product listing with image, price, rating, and add-to-cart action.

```html
<li class="product-card">
  <a href="/product/1" class="product-card__link">
    <div class="product-card__media">
      <img src="product.jpg" alt="Product name - brief description" loading="lazy">
      <span class="product-card__badge">Sale</span>
    </div>
    <div class="product-card__content">
      <span class="product-card__category">Category</span>
      <h3 class="product-card__title">Product Name</h3>
      <div class="product-card__rating" aria-label="4.5 out of 5 stars">
        ★★★★☆ <span class="product-card__reviews">(128)</span>
      </div>
      <div class="product-card__pricing">
        <span class="product-card__price">$49.99</span>
        <span class="product-card__price--original">$79.99</span>
      </div>
    </div>
  </a>
  <button class="product-card__cta" aria-label="Add Product Name to cart">
    Add to Cart
  </button>
</li>
```

```css
.product-card {
  background: var(--card-bg);
  border-radius: var(--card-radius);
  box-shadow: var(--card-shadow);
  overflow: hidden;
  display: flex;
  flex-direction: column;
  transition: box-shadow var(--card-transition), transform var(--card-transition);
}
.product-card:hover {
  box-shadow: var(--card-shadow-hover);
  transform: translateY(-2px);
}
.product-card__link {
  text-decoration: none;
  color: inherit;
  display: flex;
  flex-direction: column;
  flex: 1;
}
.product-card__media {
  position: relative;
  aspect-ratio: 4/3;
  overflow: hidden;
}
.product-card__media img {
  width: 100%;
  height: 100%;
  object-fit: cover;
  transition: transform 0.3s ease;
}
.product-card:hover .product-card__media img {
  transform: scale(1.05);
}
.product-card__badge {
  position: absolute;
  top: 12px;
  left: 12px;
  background: #e53e3e;
  color: white;
  font-size: 12px;
  font-weight: 600;
  padding: 4px 8px;
  border-radius: 4px;
}
.product-card__content {
  padding: var(--card-padding);
  flex: 1;
  display: flex;
  flex-direction: column;
  gap: 4px;
}
.product-card__category {
  font-size: 12px;
  color: var(--text-secondary);
  text-transform: uppercase;
  letter-spacing: 0.05em;
}
.product-card__title {
  font-size: 16px;
  font-weight: 600;
  color: var(--text-primary);
  margin: 0;
  display: -webkit-box;
  -webkit-line-clamp: 2;
  -webkit-box-orient: vertical;
  overflow: hidden;
}
.product-card__rating {
  font-size: 14px;
  color: #ecc94b;
}
.product-card__reviews {
  color: var(--text-secondary);
  font-size: 12px;
}
.product-card__pricing {
  display: flex;
  align-items: center;
  gap: 8px;
  margin-top: auto;
}
.product-card__price {
  font-size: 18px;
  font-weight: 700;
  color: var(--text-primary);
}
.product-card__price--original {
  font-size: 14px;
  color: var(--text-secondary);
  text-decoration: line-through;
}
.product-card__cta {
  display: block;
  width: calc(100% - var(--card-padding) * 2);
  margin: 0 var(--card-padding) var(--card-padding);
  padding: 10px 16px;
  background: var(--accent);
  color: white;
  border: none;
  border-radius: 8px;
  font-size: 14px;
  font-weight: 600;
  cursor: pointer;
  transition: background 0.2s ease;
}
.product-card__cta:hover {
  background: color-mix(in srgb, var(--accent) 85%, black);
}
```

**Customization notes:**
- Badge: change color/text for "New", "Best Seller", "Out of Stock" etc.
- Rating: replace text stars with SVG icons for pixel-perfect rendering
- For wishlists, add a heart icon button positioned absolute on the media area

---

## Article / Blog Card

News or blog post preview with thumbnail, title, excerpt, and metadata.

```html
<li class="article-card">
  <a href="/post/slug" class="article-card__link">
    <div class="article-card__media">
      <img src="article-thumb.jpg" alt="Article topic visual" loading="lazy">
    </div>
    <div class="article-card__content">
      <div class="article-card__meta">
        <span class="article-card__tag">Design</span>
        <span class="article-card__dot">·</span>
        <time datetime="2025-03-15">Mar 15, 2025</time>
      </div>
      <h3 class="article-card__title">Article Headline Goes Here</h3>
      <p class="article-card__excerpt">
        Brief preview text that gives readers a reason to click through and read the full article...
      </p>
      <div class="article-card__footer">
        <img src="avatar.jpg" alt="" class="article-card__avatar">
        <span class="article-card__author">Author Name</span>
        <span class="article-card__read-time">5 min read</span>
      </div>
    </div>
  </a>
</li>
```

```css
.article-card {
  background: var(--card-bg);
  border-radius: var(--card-radius);
  box-shadow: var(--card-shadow);
  overflow: hidden;
  transition: box-shadow var(--card-transition), transform var(--card-transition);
}
.article-card:hover {
  box-shadow: var(--card-shadow-hover);
  transform: translateY(-2px);
}
.article-card__link {
  text-decoration: none;
  color: inherit;
  display: flex;
  flex-direction: column;
  height: 100%;
}
.article-card__media {
  aspect-ratio: 16/9;
  overflow: hidden;
}
.article-card__media img {
  width: 100%;
  height: 100%;
  object-fit: cover;
}
.article-card__content {
  padding: var(--card-padding);
  display: flex;
  flex-direction: column;
  gap: 8px;
  flex: 1;
}
.article-card__meta {
  font-size: 13px;
  color: var(--text-secondary);
  display: flex;
  align-items: center;
  gap: 6px;
}
.article-card__tag {
  color: var(--accent);
  font-weight: 600;
}
.article-card__title {
  font-size: 18px;
  font-weight: 700;
  color: var(--text-primary);
  margin: 0;
  line-height: 1.3;
  display: -webkit-box;
  -webkit-line-clamp: 2;
  -webkit-box-orient: vertical;
  overflow: hidden;
}
.article-card__excerpt {
  font-size: 14px;
  color: var(--text-secondary);
  line-height: 1.5;
  margin: 0;
  display: -webkit-box;
  -webkit-line-clamp: 3;
  -webkit-box-orient: vertical;
  overflow: hidden;
}
.article-card__footer {
  display: flex;
  align-items: center;
  gap: 8px;
  margin-top: auto;
  padding-top: 12px;
  border-top: 1px solid var(--card-border);
  font-size: 13px;
  color: var(--text-secondary);
}
.article-card__avatar {
  width: 24px;
  height: 24px;
  border-radius: 50%;
  object-fit: cover;
}
.article-card__read-time {
  margin-left: auto;
}
```

---

## Profile / Team Card

Team member or user profile display.

```html
<li class="profile-card">
  <div class="profile-card__avatar-wrap">
    <img src="person.jpg" alt="Full Name" class="profile-card__avatar">
  </div>
  <div class="profile-card__info">
    <h3 class="profile-card__name">Full Name</h3>
    <p class="profile-card__role">Job Title / Role</p>
    <p class="profile-card__bio">
      Short bio text describing expertise or responsibilities...
    </p>
  </div>
  <div class="profile-card__socials">
    <a href="#" aria-label="LinkedIn profile">
      <svg><!-- LinkedIn icon --></svg>
    </a>
    <a href="#" aria-label="Twitter profile">
      <svg><!-- Twitter icon --></svg>
    </a>
    <a href="#" aria-label="Email">
      <svg><!-- Email icon --></svg>
    </a>
  </div>
</li>
```

```css
.profile-card {
  background: var(--card-bg);
  border-radius: var(--card-radius);
  box-shadow: var(--card-shadow);
  padding: var(--card-padding);
  display: flex;
  flex-direction: column;
  align-items: center;
  text-align: center;
  gap: 12px;
}
.profile-card__avatar-wrap {
  width: 80px;
  height: 80px;
  border-radius: 50%;
  overflow: hidden;
  border: 3px solid var(--accent);
}
.profile-card__avatar {
  width: 100%;
  height: 100%;
  object-fit: cover;
}
.profile-card__info {
  display: flex;
  flex-direction: column;
  gap: 4px;
}
.profile-card__name {
  font-size: 18px;
  font-weight: 700;
  color: var(--text-primary);
  margin: 0;
}
.profile-card__role {
  font-size: 14px;
  color: var(--accent);
  margin: 0;
}
.profile-card__bio {
  font-size: 14px;
  color: var(--text-secondary);
  margin: 0;
  line-height: 1.5;
  display: -webkit-box;
  -webkit-line-clamp: 3;
  -webkit-box-orient: vertical;
  overflow: hidden;
}
.profile-card__socials {
  display: flex;
  gap: 12px;
  margin-top: auto;
  padding-top: 12px;
}
.profile-card__socials a {
  width: 36px;
  height: 36px;
  display: flex;
  align-items: center;
  justify-content: center;
  border-radius: 50%;
  background: #f7fafc;
  color: var(--text-secondary);
  transition: background 0.2s, color 0.2s;
}
.profile-card__socials a:hover {
  background: var(--accent);
  color: white;
}
```

---

## Stat / Metric Card

Dashboard KPI display with trend indicator.

```html
<div class="stat-card">
  <div class="stat-card__icon" aria-hidden="true">
    <svg><!-- metric icon --></svg>
  </div>
  <div class="stat-card__body">
    <span class="stat-card__label">Active Users</span>
    <span class="stat-card__value">2,847</span>
  </div>
  <div class="stat-card__trend stat-card__trend--up" aria-label="Increased by 12.5 percent">
    <svg viewBox="0 0 16 16" width="14" height="14" aria-hidden="true">
      <path d="M8 4l4 4H4z" fill="currentColor"/>
    </svg>
    +12.5%
  </div>
</div>
```

```css
.stat-card {
  background: var(--card-bg);
  border-radius: var(--card-radius);
  box-shadow: var(--card-shadow);
  padding: 20px;
  display: flex;
  align-items: flex-start;
  gap: 16px;
}
.stat-card__icon {
  width: 44px;
  height: 44px;
  border-radius: 10px;
  background: color-mix(in srgb, var(--accent) 12%, transparent);
  color: var(--accent);
  display: flex;
  align-items: center;
  justify-content: center;
  flex-shrink: 0;
}
.stat-card__body {
  display: flex;
  flex-direction: column;
  gap: 2px;
  flex: 1;
}
.stat-card__label {
  font-size: 13px;
  color: var(--text-secondary);
}
.stat-card__value {
  font-size: 28px;
  font-weight: 700;
  color: var(--text-primary);
  line-height: 1.1;
}
.stat-card__trend {
  font-size: 13px;
  font-weight: 600;
  display: flex;
  align-items: center;
  gap: 2px;
  padding: 4px 8px;
  border-radius: 6px;
}
.stat-card__trend--up {
  color: #38a169;
  background: #f0fff4;
}
.stat-card__trend--down {
  color: #e53e3e;
  background: #fff5f5;
}
```

---

## Pricing Card

SaaS/subscription plan comparison.

```html
<li class="pricing-card pricing-card--featured">
  <div class="pricing-card__header">
    <span class="pricing-card__badge">Most Popular</span>
    <h3 class="pricing-card__plan">Pro</h3>
    <div class="pricing-card__price">
      <span class="pricing-card__amount">$29</span>
      <span class="pricing-card__period">/month</span>
    </div>
    <p class="pricing-card__desc">Best for growing teams</p>
  </div>
  <ul class="pricing-card__features" role="list">
    <li>✓ Unlimited projects</li>
    <li>✓ 50GB storage</li>
    <li>✓ Priority support</li>
    <li>✓ Advanced analytics</li>
    <li class="pricing-card__feature--disabled">✗ Custom domain</li>
  </ul>
  <button class="pricing-card__cta">Get Started</button>
</li>
```

```css
.pricing-card {
  background: var(--card-bg);
  border-radius: var(--card-radius);
  border: 1px solid var(--card-border);
  padding: 32px 24px;
  display: flex;
  flex-direction: column;
  gap: 24px;
  position: relative;
}
.pricing-card--featured {
  border-color: var(--accent);
  box-shadow: 0 0 0 1px var(--accent), var(--card-shadow-hover);
  transform: scale(1.03);
}
.pricing-card__badge {
  position: absolute;
  top: -12px;
  left: 50%;
  transform: translateX(-50%);
  background: var(--accent);
  color: white;
  font-size: 12px;
  font-weight: 600;
  padding: 4px 12px;
  border-radius: 12px;
}
.pricing-card__header {
  text-align: center;
}
.pricing-card__plan {
  font-size: 20px;
  font-weight: 700;
  color: var(--text-primary);
  margin: 0 0 8px;
}
.pricing-card__amount {
  font-size: 48px;
  font-weight: 800;
  color: var(--text-primary);
}
.pricing-card__period {
  font-size: 16px;
  color: var(--text-secondary);
}
.pricing-card__desc {
  font-size: 14px;
  color: var(--text-secondary);
  margin: 8px 0 0;
}
.pricing-card__features {
  list-style: none;
  padding: 0;
  margin: 0;
  display: flex;
  flex-direction: column;
  gap: 10px;
  font-size: 14px;
  color: var(--text-primary);
  flex: 1;
}
.pricing-card__feature--disabled {
  color: var(--text-secondary);
  opacity: 0.5;
}
.pricing-card__cta {
  display: block;
  width: 100%;
  padding: 12px;
  border-radius: 8px;
  font-size: 15px;
  font-weight: 600;
  cursor: pointer;
  border: 2px solid var(--accent);
  background: transparent;
  color: var(--accent);
  transition: background 0.2s, color 0.2s;
}
.pricing-card--featured .pricing-card__cta {
  background: var(--accent);
  color: white;
}
.pricing-card__cta:hover {
  background: var(--accent);
  color: white;
}
```

---

## Testimonial Card

Customer quote or review.

```html
<li class="testimonial-card">
  <blockquote class="testimonial-card__quote">
    <p>"Customer feedback text goes here. Keep it concise and impactful — 2–3 sentences maximum."</p>
  </blockquote>
  <div class="testimonial-card__author">
    <img src="customer.jpg" alt="" class="testimonial-card__avatar">
    <div>
      <cite class="testimonial-card__name">Customer Name</cite>
      <span class="testimonial-card__company">Company, Title</span>
    </div>
  </div>
</li>
```

---

## Feature Card

Product feature or service highlight with icon.

```html
<li class="feature-card">
  <div class="feature-card__icon" aria-hidden="true">
    <svg><!-- feature icon --></svg>
  </div>
  <h3 class="feature-card__title">Feature Name</h3>
  <p class="feature-card__desc">
    Brief explanation of what this feature does and why it matters to the user.
  </p>
  <a href="/features/detail" class="feature-card__link">
    Learn more →
  </a>
</li>
```

---

## Media / Portfolio Card

Full-bleed image card with overlay text on hover. Great for galleries, portfolios, and visual-first content.

```html
<li class="media-card">
  <a href="/project/1" class="media-card__link">
    <img src="project.jpg" alt="Project name description" loading="lazy">
    <div class="media-card__overlay">
      <h3 class="media-card__title">Project Title</h3>
      <span class="media-card__category">Category</span>
    </div>
  </a>
</li>
```

```css
.media-card {
  border-radius: var(--card-radius);
  overflow: hidden;
  position: relative;
}
.media-card__link {
  display: block;
  aspect-ratio: 4/3;
}
.media-card__link img {
  width: 100%;
  height: 100%;
  object-fit: cover;
  transition: transform 0.4s ease;
}
.media-card:hover img {
  transform: scale(1.08);
}
.media-card__overlay {
  position: absolute;
  inset: 0;
  background: linear-gradient(to top, rgba(0,0,0,0.7) 0%, transparent 60%);
  display: flex;
  flex-direction: column;
  justify-content: flex-end;
  padding: 20px;
  opacity: 0;
  transition: opacity 0.3s ease;
}
.media-card:hover .media-card__overlay,
.media-card:focus-within .media-card__overlay {
  opacity: 1;
}
.media-card__title {
  color: white;
  font-size: 18px;
  font-weight: 700;
  margin: 0;
}
.media-card__category {
  color: rgba(255,255,255,0.8);
  font-size: 13px;
}
```

---

## Horizontal Card

Side-by-side layout for search results, article lists, or any context where vertical space is limited.

```html
<li class="h-card">
  <a href="/item/1" class="h-card__link">
    <div class="h-card__media">
      <img src="thumb.jpg" alt="Item description" loading="lazy">
    </div>
    <div class="h-card__content">
      <span class="h-card__meta">Category · Mar 15</span>
      <h3 class="h-card__title">Item Title Goes Here</h3>
      <p class="h-card__desc">Brief description for context...</p>
    </div>
  </a>
</li>
```

```css
.h-card {
  background: var(--card-bg);
  border-radius: var(--card-radius);
  box-shadow: var(--card-shadow);
  overflow: hidden;
  transition: box-shadow var(--card-transition);
}
.h-card:hover {
  box-shadow: var(--card-shadow-hover);
}
.h-card__link {
  display: flex;
  text-decoration: none;
  color: inherit;
}
.h-card__media {
  width: 200px;
  flex-shrink: 0;
}
.h-card__media img {
  width: 100%;
  height: 100%;
  object-fit: cover;
}
.h-card__content {
  padding: var(--card-padding);
  display: flex;
  flex-direction: column;
  gap: 6px;
  justify-content: center;
}
.h-card__meta {
  font-size: 12px;
  color: var(--text-secondary);
}
.h-card__title {
  font-size: 16px;
  font-weight: 600;
  color: var(--text-primary);
  margin: 0;
}
.h-card__desc {
  font-size: 14px;
  color: var(--text-secondary);
  margin: 0;
  display: -webkit-box;
  -webkit-line-clamp: 2;
  -webkit-box-orient: vertical;
  overflow: hidden;
}

/* Stack vertically on small screens */
@media (max-width: 480px) {
  .h-card__link {
    flex-direction: column;
  }
  .h-card__media {
    width: 100%;
    aspect-ratio: 16/9;
  }
}
```

---

## Notification / Activity Card

Compact card for feeds, activity logs, and notification lists.

```html
<li class="notif-card notif-card--unread">
  <div class="notif-card__icon">
    <svg><!-- notification type icon --></svg>
  </div>
  <div class="notif-card__body">
    <p class="notif-card__message">
      <strong>User Name</strong> commented on your post
    </p>
    <time class="notif-card__time" datetime="2025-03-15T14:30">2 hours ago</time>
  </div>
  <button class="notif-card__action" aria-label="Mark as read">
    <svg><!-- dot or checkmark --></svg>
  </button>
</li>
```

```css
.notif-card {
  display: flex;
  align-items: center;
  gap: 12px;
  padding: 12px 16px;
  background: var(--card-bg);
  border-bottom: 1px solid var(--card-border);
  transition: background 0.15s ease;
}
.notif-card:hover {
  background: #f7fafc;
}
.notif-card--unread {
  border-left: 3px solid var(--accent);
}
.notif-card__icon {
  width: 36px;
  height: 36px;
  border-radius: 50%;
  background: color-mix(in srgb, var(--accent) 12%, transparent);
  color: var(--accent);
  display: flex;
  align-items: center;
  justify-content: center;
  flex-shrink: 0;
}
.notif-card__body {
  flex: 1;
  min-width: 0;
}
.notif-card__message {
  font-size: 14px;
  color: var(--text-primary);
  margin: 0;
  white-space: nowrap;
  overflow: hidden;
  text-overflow: ellipsis;
}
.notif-card__time {
  font-size: 12px;
  color: var(--text-secondary);
}
.notif-card__action {
  background: none;
  border: none;
  cursor: pointer;
  padding: 8px;
  color: var(--text-secondary);
  border-radius: 50%;
}
.notif-card__action:hover {
  background: #edf2f7;
}
```