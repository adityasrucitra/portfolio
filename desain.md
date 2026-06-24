# Design System Reference

**Portfolio Project - Neobrutalist Design System**

This document serves as the comprehensive style reference for all UI development in this portfolio project. Follow these conventions to maintain visual consistency across all pages.

---

## Table of Contents

1. [Design Philosophy](#design-philosophy)
2. [Color Palette](#color-palette)
3. [Typography](#typography)
4. [Layout System](#layout-system)
5. [Component Patterns](#component-patterns)
6. [Responsive Breakpoints](#responsive-breakpoints)
7. [Animation & Transitions](#animation--transitions)
8. [Accessibility](#accessibility)

---

## Design Philosophy

**Neobrutalism** - Bold, high-contrast design with thick borders, prominent shadows, and unapologetic use of color. Every element is intentionally visible and tactile.

### Core Principles

- **High Contrast**: Black borders on everything, strong color backgrounds
- **Bold Typography**: Heavy weights (700-900), uppercase text for emphasis
- **Tactile Shadows**: Offset box-shadows create depth (no blur)
- **Clear Hierarchy**: Visual weight through size, color, and position
- **Honest Design**: No gradients, no subtle effects - everything is explicit

---

## Color Palette

### Primary Colors

| Variable | Hex | Usage |
|----------|-----|-------|
| `--ink` | `#050505` | Text, borders, dark backgrounds |
| `--paper` | `#f7f0df` | Body background, warm neutral |
| `--white` | `#fffdf6` | Card backgrounds, light elements |
| `--yellow` | `#ffe14d` | Primary accent, highlights, CTAs |
| `--green` | `#62e889` | Secondary accent, success states |
| `--red` | `#ff6b6b` | Alerts, error states |
| `--blue` | `#73c7ff` | Information, links |
| `--purple` | `#b8a1ff` | Tertiary accent |
| `--muted` | `#3f3f3f` | Secondary text |

### Color Usage Examples

```css
/* Primary action */
.button {
  background: var(--yellow);
  border: 4px solid var(--ink);
  color: var(--ink);
}

/* Dark button variant */
.button.dark {
  background: var(--ink);
  color: var(--white);
}

/* Card background */
.card {
  background: var(--white);
  border: 4px solid var(--ink);
}
```

### Shadow System

**Standard shadow**: `10px 10px 0 var(--ink)`
**Medium shadow**: `8px 8px 0 var(--ink)`
**Small shadow**: `6px 6px 0 var(--ink)`
**Button shadow**: `5px 5px 0 var(--ink)`

```css
.neo {
  border: 4px solid var(--ink);
  box-shadow: var(--shadow); /* 10px 10px 0 var(--ink) */
}
```

---

## Typography

### Font Family

**Primary**: Inter (Google Fonts)
**Weights**: 500 (medium), 700 (bold), 800 (extra-bold), 900 (black)
**Fallback**: Arial, sans-serif

### Font Import

```html
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Inter:wght@500;700;800;900&display=swap" rel="stylesheet">
```

### Type Scale

| Element | Size | Weight | Transform | Line Height |
|---------|------|--------|-----------|-------------|
| `h1` (Hero) | `clamp(3.2rem, 8vw, 7.8rem)` | 900 | uppercase | 0.82 |
| `h2` (Title) | `clamp(2.2rem, 5vw, 4.6rem)` | 900 | uppercase | 0.9 |
| `h3` | `1.2rem - 1.5rem` | 900 | uppercase | 1.1 |
| Body (Lead) | `1.16rem` | 700 | none | 1.6 |
| Body (Regular) | `1rem - 1.1rem` | 700 | none | 1.6-1.9 |
| Small/Meta | `0.78rem - 0.84rem` | 900 | uppercase | 1.35 |

### Typography Examples

```css
/* Hero heading */
h1 {
  font-size: clamp(3.2rem, 8vw, 7.8rem);
  line-height: 0.82;
  letter-spacing: 0;
  font-weight: 900;
  text-transform: uppercase;
  max-width: 9ch;
}

/* Section title */
.title {
  font-size: clamp(2.2rem, 5vw, 4.6rem);
  line-height: 0.9;
  font-weight: 900;
  text-transform: uppercase;
}

/* Lead paragraph */
.lead {
  font-size: 1.16rem;
  font-weight: 700;
  color: #1b1b1b;
  line-height: 1.6;
}

/* Label/badge */
.label {
  font-size: 0.82rem;
  font-weight: 900;
  text-transform: uppercase;
  background: var(--ink);
  color: var(--white);
  padding: 7px 10px;
}
```

---

## Layout System

### Container

**Max width**: `1180px`
**Width**: `min(1180px, 92%)` (desktop) / `min(100% - 28px, 1180px)` (mobile)
**Centering**: `margin: auto`

```css
.container {
  width: min(1180px, 92%);
  margin: auto;
}

@media (max-width: 700px) {
  .container {
    width: min(100% - 28px, 1180px);
  }
}
```

### Spacing

**Section padding**: `100px 0` (desktop) → `70px 0` (mobile)
**Card padding**: `30px` (desktop) → `22px` (tablet) → `18px` (mobile)
**Gap between elements**: `24px - 30px` (standard)

### Grid Patterns

```css
/* 2-column grid */
.about-grid {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 24px;
}

/* 3-column responsive grid */
.grid {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 24px;
}

/* Auto-fit responsive grid */
.blog-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(350px, 1fr));
  gap: 30px;
}

/* Mobile: collapse to single column */
@media (max-width: 940px) {
  .about-grid,
  .grid {
    grid-template-columns: 1fr;
  }
}
```

---

## Component Patterns

### 1. Navigation Bar

Sticky navigation with logo, links, and locale selector.

```html
<nav class="nav" aria-label="Primary navigation">
  <div class="container">
    <a class="brand" href="index.html">Adityas Rucitra Pradipta</a>
    <div class="nav-actions">        
      <div class="nav-links">
        <a href="#impact">Impact</a>
        <a href="#about">About</a>
        <a href="#projects" class="active">Projects</a>
      </div>
    </div>
  </div>
</nav>
```

**Key styles**:
- Sticky positioning: `position: sticky; top: 0;`
- Yellow background: `background: var(--yellow);`
- Active state: `background: var(--yellow); border: 3px solid var(--ink); box-shadow: 4px 4px 0 var(--ink);`

### 2. Buttons

Bold, tactile buttons with shadow offset on hover.

```html
<a class="button" href="#section">View More</a>
<a class="button dark" href="#action">Primary Action</a>
```

**Key styles**:
```css
.button {
  display: inline-flex;
  align-items: center;
  justify-content: center;
  min-height: 48px;
  padding: 0 16px;
  background: var(--white);
  border: 4px solid var(--ink);
  box-shadow: 5px 5px 0 var(--ink);
  font-weight: 900;
  text-transform: uppercase;
  transition: transform 0.16s ease, box-shadow 0.16s ease;
}

.button:hover {
  transform: translate(3px, 3px);
  box-shadow: 2px 2px 0 var(--ink);
}

.button.dark {
  background: var(--ink);
  color: var(--white);
  box-shadow: 5px 5px 0 #666;
}
```

### 3. Cards (.neo class)

Neobrutalist cards with borders and shadows.

```html
<div class="card neo">
  <h3>Card Title</h3>
  <p>Card content goes here.</p>
</div>
```

**Key styles**:
```css
.neo {
  border: 4px solid var(--ink);
  box-shadow: var(--shadow); /* 10px 10px 0 var(--ink) */
}

.card {
  background: var(--white);
  padding: 30px;
}

/* Hover effect for interactive cards */
.card:hover {
  transform: translate(-4px, -4px);
  box-shadow: 14px 14px 0 var(--ink);
}
```

### 4. Hero Section

Large title with eyebrow label and lead text.

```html
<section class="hero">
  <div class="container">
    <div class="hero-main neo">
      <div>
        <p class="eyebrow">Category Label</p>
        <h1>Main Headline</h1>
        <p class="lead">Supporting description text.</p>
      </div>
    </div>
  </div>
</section>
```

**Key styles**:
```css
.eyebrow {
  display: inline-block;
  background: var(--ink);
  color: var(--white);
  padding: 8px 12px;
  font-size: 0.78rem;
  font-weight: 900;
  text-transform: uppercase;
}

.hero-main {
  background: var(--yellow);
  padding: 44px;
  min-height: 560px;
}
```

### 5. Tags/Badges

Small labeled elements for categories or metadata.

```html
<span class="tag">PHP</span>
<span class="category">SPRING BOOT</span>
<span class="label">Engineering Impact</span>
```

**Key styles**:
```css
.tag {
  background: var(--yellow);
  border: 3px solid var(--ink);
  padding: 8px 11px;
  font-weight: 900;
  text-transform: uppercase;
  font-size: 0.82rem;
}

.category {
  display: inline-block;
  background: var(--yellow);
  border: 3px solid var(--ink);
  padding: 6px 12px;
  font-weight: 900;
  text-transform: uppercase;
  font-size: 0.78rem;
}

.label {
  font-size: 0.82rem;
  font-weight: 900;
  text-transform: uppercase;
  background: var(--ink);
  color: var(--white);
  padding: 7px 10px;
}
```

### 6. Blog Components

#### Filter Buttons
```html
<div class="filter">
  <button class="active">ALL</button>
  <button>SPRING</button>
  <button>AWS</button>
</div>
```

#### Blog Grid
```html
<section class="blog-grid">
  <article class="card neo">
    <span class="category">SPRING BOOT</span>
    <h2>Article Title</h2>
    <div class="meta">June 2026 · 10 min read</div>
    <p>Article excerpt...</p>
    <a href="blog-detail.html" class="read-more">READ ARTICLE →</a>
  </article>
</section>
```

#### Article Header
```html
<header class="article-header neo">
  <h1>Article Title</h1>
  <div class="meta">Published June 2026 · 10 min read · Spring Boot</div>
</header>
```

#### Cover Section
```html
<div class="cover neo">
  SPRING BOOT<br/>
  @Bean<br/>
  Dependency Injection
</div>
```

#### Code Blocks
```html
<pre>
@Configuration
public class AppConfig {
    @Bean
    public PersonService personService() {
        return new PersonService();
    }
}
</pre>
```

**Key styles**:
```css
.content pre {
  background: var(--ink);
  color: var(--yellow);
  padding: 20px;
  overflow: auto;
  border: 4px solid var(--ink);
  font-family: monospace;
  font-size: 0.9rem;
  line-height: 1.6;
}
```

### 7. Timeline

Vertical timeline with marker dots.

```html
<div class="timeline">
  <article class="timeline-item neo">
    <div class="timeline-marker"></div>
    <div>
      <span class="timeline-meta">2023 - Present</span>
      <h3>Position Title</h3>
      <p>Description of role...</p>
    </div>
  </article>
</div>
```

---

## Responsive Breakpoints

### Breakpoint System

| Breakpoint | Width | Target |
|------------|-------|--------|
| Desktop | `> 1180px` | Large screens |
| Tablet | `940px - 1180px` | Medium screens |
| Mobile Large | `700px - 940px` | Small tablets, large phones |
| Mobile | `430px - 700px` | Standard phones |
| Mobile Small | `< 430px` | Small phones |

### Media Query Examples

```css
/* Tablet */
@media (max-width: 1180px) {
  .grid {
    grid-template-columns: repeat(2, 1fr);
  }
}

/* Mobile Large */
@media (max-width: 940px) {
  :root {
    --shadow: 8px 8px 0 var(--ink);
  }
  
  .hero-grid,
  .grid {
    grid-template-columns: 1fr;
  }
  
  section {
    padding: 70px 0;
  }
}

/* Mobile */
@media (max-width: 700px) {
  .container {
    width: min(100% - 28px, 1180px);
  }
  
  h1 {
    font-size: clamp(2.55rem, 17vw, 4.4rem);
  }
  
  .card {
    padding: 22px;
  }
}

/* Mobile Small */
@media (max-width: 430px) {
  :root {
    --shadow: 6px 6px 0 var(--ink);
  }
  
  .card {
    padding: 18px;
  }
}
```

### Responsive Font Scaling

Use `clamp()` for fluid typography:

```css
/* Hero title: 2.55rem minimum, 17vw fluid, 4.4rem maximum */
h1 {
  font-size: clamp(2.55rem, 17vw, 4.4rem);
}

/* Section title */
.title {
  font-size: clamp(2rem, 5vw, 4.6rem);
}
```

---

## Animation & Transitions

### Timing

**Standard**: `0.16s ease` (fast, tactile)
**Hover effects**: `0.2s ease` (slightly slower for visual feedback)

### Common Transitions

```css
/* Button press effect */
.button {
  transition: transform 0.16s ease, box-shadow 0.16s ease;
}
.button:hover {
  transform: translate(3px, 3px);
  box-shadow: 2px 2px 0 var(--ink);
}

/* Card lift effect */
.card {
  transition: transform 0.2s ease, box-shadow 0.2s ease;
}
.card:hover {
  transform: translate(-4px, -4px);
  box-shadow: 14px 14px 0 var(--ink);
}

/* Scale effect */
.read-more:hover {
  transform: scale(1.05);
}
```

### Smooth Scrolling

```css
html {
  scroll-behavior: smooth;
}

section {
  scroll-margin-top: 90px; /* Account for sticky nav */
}
```

---

## Accessibility

### Focus States

Always provide visible focus indicators:

```css
.button:focus-visible,
.nav-links a:focus-visible {
  outline: 3px solid var(--red);
  outline-offset: 3px;
}
```

### ARIA Labels

```html
<nav aria-label="Primary navigation">
  <!-- navigation content -->
</nav>

<button aria-label="Close modal">×</button>

<select aria-label="Select language">
  <option value="en">English</option>
</select>
```

### Semantic HTML

- Use `<main>` for primary content
- Use `<nav>` for navigation
- Use `<article>` for blog posts/cards
- Use `<section>` for thematic groupings
- Use proper heading hierarchy (h1 → h2 → h3)

### Touch Targets

Minimum touch target size: `44px × 44px` (mobile)

```css
.nav-links a {
  min-height: 44px;
  display: flex;
  align-items: center;
}

.button {
  min-height: 48px;
}
```

---

## Best Practices

### Do's ✅

- Use `.neo` class for all bordered/shadowed elements
- Apply `font-weight: 900` for headings and emphasis
- Use uppercase text for labels, buttons, and small text
- Maintain 4px border width consistently
- Use color from the defined palette
- Add hover states to interactive elements
- Test on mobile breakpoints (700px, 430px)

### Don'ts ❌

- Don't use gradients or blur effects
- Don't use thin borders (< 3px)
- Don't use subtle shadows (always offset, no blur)
- Don't use body text below 1rem on desktop
- Don't use font-weight below 700 for emphasis
- Don't forget `transition` on interactive elements
- Don't ignore focus states for keyboard navigation

---

## Quick Start Template

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Page Title</title>
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
  <link href="https://fonts.googleapis.com/css2?family=Inter:wght@500;700;800;900&display=swap" rel="stylesheet">
  <link rel="stylesheet" href="assets/css/styles.css">
</head>
<body>
  <nav class="nav">
    <div class="container">
      <a class="brand" href="index.html">Adityas Rucitra Pradipta</a>
      <div class="nav-actions">        
        <div class="nav-links">
          <a href="index.html#impact">Impact</a>
          <a href="index.html#about">About</a>
          <a href="index.html#projects">Projects</a>
        </div>
      </div>
    </div>
  </nav>

  <main>
    <section>
      <div class="container">
        <!-- Your content here -->
      </div>
    </section>
  </main>

  <footer>&copy; 2026 Adityas Rucitra Pradipta</footer>
</body>
</html>
```

---

## File Structure

```
portfolio.project/
├── index.html
├── blog-list.html
├── blog-detail.html
├── desain.md (this file)
└── assets/
    ├── css/
    │   └── styles.css
    ├── images/
    └── js/
```

---

## Version History

- **v1.0** (2026-06-24): Initial design system documentation
  - Neobrutalist design patterns established
  - Color palette defined
  - Typography scale documented
  - Component patterns catalogued
  - Responsive breakpoints standardized

---

## Future Enhancements

Considerations for future development:

1. **Interactive Component Library**: Create an HTML page showcasing all components with live examples
2. **Dark Mode Variant**: Explore dark mode color palette (preserve neobrutalist aesthetic)
3. **Animation Library**: Expand micro-interactions for enhanced user delight
4. **Icon System**: Establish icon style (outlined, bold, consistent with design language)
5. **Form Components**: Document input fields, checkboxes, radio buttons, textareas following neobrutalist style

---

**Last Updated**: 2026-06-24  
**Maintained By**: Adityas Rucitra Pradipta
