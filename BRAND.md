# Haveaspot Brand Application Guide
### For Developers — Booking Platform UI

---

## AI Coding Assistant — Quick Context

If you are using Cursor, GitHub Copilot, Claude, or any AI coding assistant, paste this into your context window or `.cursorrules` file before generating UI:

> *This project uses the Haveaspot brand system. Font: Poppins (all weights). Primary text colour and borders: `#021300` (near-black). Accent and hover colour: `#0AAD0A` (brand green). Never use grey text — all text including subtext and metadata is `#021300` at the appropriate weight. H1/H2: weight 800. H3/H4 and card titles: weight 700. Nav active, footer headings: weight 600. Buttons, nav links, inputs: weight 500. Body: weight 400. Subtext, metadata, captions: weight 300. Buttons: 44px height, 6px radius, primary bg `#021300` hover bg `#0AAD0A`. Cards: 2px solid `#021300` border, 12px radius, lift on hover with green border. Do not use Tailwind colour utilities for text or borders — they are not brand-safe.*

---

## 1. Design Tokens

Paste this block at the top of your global stylesheet. Reference these variables throughout — do not hardcode hex values in component styles.

```css
:root {
  /* ── Brand Colours ── */
  --color-brand-dark:    #021300;   /* primary text, borders, button bg */
  --color-brand-green:   #0AAD0A;   /* hover, active, accent */
  --color-brand-hover:   #0E491F;   /* deep hover (use sparingly) */
  --color-white:         #FFFFFF;
  --color-surface:       #F9FAFB;   /* subtle section/card backgrounds */
  --color-border-light:  #E5E7EB;   /* dividers, non-featured card borders */

  /* ── Typography ── */
  --font-family:           'Poppins', system-ui, sans-serif;
  --font-weight-extrabold: 800;   /* H1, H2 */
  --font-weight-bold:      700;   /* H3, H4, card titles */
  --font-weight-semibold:  600;   /* nav active, footer headings */
  --font-weight-medium:    500;   /* nav links, buttons, inputs */
  --font-weight-regular:   400;   /* body copy */
  --font-weight-light:     300;   /* subtext, metadata, captions */

  /* ── Spacing ── */
  --spacing-section-sm:   4rem;   /* section padding, mobile */
  --spacing-section-lg:   6rem;   /* section padding, desktop */
  --spacing-header-gap:   3rem;   /* section header → content */
  --spacing-subtext-gap:  1.5rem; /* heading → subtext */

  /* ── Radii ── */
  --radius-card:    12px;
  --radius-button:   6px;
  --radius-input:    6px;
  --radius-pill:    20px;         /* filter/tag chips */

  /* ── Transitions ── */
  --transition-base: 0.2s ease;
}
```

---

## 2. Breakpoints

| Name | Range | CSS |
|---|---|---|
| Mobile | 0 – 639px | `@media (max-width: 639px)` |
| Tablet | 640px – 1023px | `@media (min-width: 640px) and (max-width: 1023px)` |
| Desktop | 1024px+ | `@media (min-width: 1024px)` |
| Max content width | 1536px | `max-width: 1536px; margin: 0 auto;` |

---

## 3. Tailwind Conflict Warning

**This project uses Tailwind. The following Tailwind colour utilities are not brand-safe and must not be used for text, headings, or borders:**

| Tailwind utility | Hex it produces | Problem |
|---|---|---|
| `text-gray-700` | `#374151` | Off-brand grey |
| `text-gray-900` | `#111827` | Too cold, no green undertone |
| `text-black` | `#000000` | Not brand dark |
| `border-gray-*` | various | Use `#021300` or `#E5E7EB` only |

**Always use the CSS variable or explicit hex instead of a Tailwind colour utility for brand-critical properties.**

---

## 4. Typography

### Loading Poppins

```html
<!-- Via Google Fonts (recommended for web) -->
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Poppins:wght@300;400;500;600;700;800&display=swap" rel="stylesheet">
```

```css
/* Or via @fontsource in JS/TS projects */
@import "@fontsource/poppins/300.css";
@import "@fontsource/poppins/400.css";
@import "@fontsource/poppins/500.css";
@import "@fontsource/poppins/600.css";
@import "@fontsource/poppins/700.css";
@import "@fontsource/poppins/800.css";
```

### Weight & size reference

| Element | Weight | Mobile size | Tablet size | Desktop size | Line height | Letter spacing |
|---|---|---|---|---|---|---|
| H1 / Hero heading | 800 | 2.5rem | 3.75rem | up to 4.75rem | 1.1 | -0.02em |
| H2 / Section heading | 800 | 2rem | 2.5rem | up to 3rem | 1.1 | -0.02em |
| H3 / Sub-heading | 700 | 1.35rem | 1.5rem | 1.6rem | 1.2 | default |
| H4 / Card title | 700 | 1.1rem | 1.2rem | 1.25rem | 1.2 | default |
| Body copy | 400 | 1rem | 1rem | 1rem | 1.625 | default |
| Subtext / section description | 300 | 0.95rem | 1rem | 1rem | 1.625 | default |
| Button label | 500 | 1rem | 1rem | 1rem | 1 | default |
| Nav link | 500 (inactive) / 600 (active) | — | — | 1rem | 1 | default |
| Metadata / date / caption | 300 | 13px | 14px | 14px | 1.4 | default |

### Base CSS

```css
body {
  font-family: var(--font-family);
  font-size: 1rem;
  font-weight: 400;
  line-height: 1.625;
  color: var(--color-brand-dark);
  background-color: var(--color-white);
}

h1, h2 { font-weight: 800; line-height: 1.1; letter-spacing: -0.02em; }
h3, h4 { font-weight: 700; line-height: 1.2; }
h5, h6 { font-weight: 600; line-height: 1.2; }

h1, h2, h3, h4, h5, h6 {
  color: var(--color-brand-dark);
  margin: 0 0 0.5rem 0;
}
```

---

## 5. Colour Application Rules

| Context | Colour | Weight | Notes |
|---|---|---|---|
| All headings | `#021300` | 800 or 700 | Never grey |
| Body copy | `#021300` | 400 | Never grey |
| Subtext / descriptions | `#021300` | 300 | Weight 300 gives visual lightness without changing colour |
| Metadata (dates, categories) | `#021300` | 300 | |
| Links at rest | `#021300` | inherited | |
| Links on hover | `#0AAD0A` | inherited | Green is hover-only for text links |
| Active nav link | `#0AAD0A` | 600 | |
| Primary button bg | `#021300` | — | |
| Primary button hover bg | `#0AAD0A` | — | |
| Card borders | `#021300` | — | 2px solid |
| Card hover border | `#0AAD0A` | — | |
| Dividers | `#E5E7EB` | — | Thin structural lines only |
| Page background | `#FFFFFF` | — | |
| Subtle surface | `#F9FAFB` | — | Search results, filter dropdowns |

**Green `#0AAD0A` is an action/hover colour — never a default text or background colour.**

---

## 6. Links

```css
a {
  color: var(--color-brand-dark);
  text-decoration: none;
  transition: color var(--transition-base);
}

a:hover {
  color: var(--color-brand-green);
  text-decoration: underline;
}

/* Heading links — keep dark at rest, green on hover */
a h1, a h2, a h3, a h4 {
  color: var(--color-brand-dark);
  transition: color var(--transition-base);
}
a:hover h1, a:hover h2, a:hover h3, a:hover h4 {
  color: var(--color-brand-green);
}
```

---

## 7. Buttons

### Primary button — complete component

```css
.btn-primary {
  display: inline-flex;
  align-items: center;
  justify-content: center;
  height: 44px;
  padding: 0 1.5rem;
  font-family: var(--font-family);
  font-size: 1rem;
  font-weight: 500;
  line-height: 1;
  color: #ffffff;
  background-color: var(--color-brand-dark);
  border: none;
  border-radius: var(--radius-button);
  text-decoration: none;
  cursor: pointer;
  transition: background-color var(--transition-base);
}

.btn-primary:hover         { background-color: var(--color-brand-green); }
.btn-primary:focus-visible { outline: 2px solid var(--color-brand-green); outline-offset: 2px; }
.btn-primary:active        { background-color: var(--color-brand-green); }
.btn-primary:disabled      { opacity: 0.4; cursor: not-allowed; pointer-events: none; }
```

### Secondary (outline) button — complete component

```css
.btn-secondary {
  display: inline-flex;
  align-items: center;
  justify-content: center;
  height: 44px;
  padding: 0 1.5rem;
  font-family: var(--font-family);
  font-size: 1rem;
  font-weight: 500;
  line-height: 1;
  color: var(--color-brand-dark);
  background-color: transparent;
  border: 1px solid var(--color-brand-dark);
  border-radius: var(--radius-button);
  text-decoration: none;
  cursor: pointer;
  transition: all var(--transition-base);
}

.btn-secondary:hover {
  background-color: var(--color-brand-green);
  color: #ffffff;
  border-color: var(--color-brand-green);
}
.btn-secondary:focus-visible { outline: 2px solid var(--color-brand-green); outline-offset: 2px; }
.btn-secondary:active        { background-color: var(--color-brand-green); color: #ffffff; border-color: var(--color-brand-green); }
.btn-secondary:disabled      { opacity: 0.4; cursor: not-allowed; pointer-events: none; }
```

### Button state summary

| State | Primary | Secondary |
|---|---|---|
| Default | bg `#021300`, text white | transparent, border + text `#021300` |
| Hover | bg `#0AAD0A` | bg `#0AAD0A`, text white, border `#0AAD0A` |
| Focus | `outline: 2px solid #0AAD0A` | same |
| Active | bg `#0AAD0A` | bg `#0AAD0A`, text white |
| Disabled | opacity 0.4, no pointer events | same |

---

## 8. Cards & Listing Items

### Venue / listing card — complete component

```css
.card {
  background-color: var(--color-white);
  border: 2px solid var(--color-brand-dark);
  border-radius: var(--radius-card);
  overflow: hidden;
  display: flex;
  flex-direction: column;
  transition: border-color var(--transition-base), transform var(--transition-base);
}

.card:hover {
  border-color: var(--color-brand-green);
  transform: translateY(-2px);
}

.card__image {
  width: 100%;
  height: 240px;
  object-fit: cover;
  display: block;
  margin-bottom: 1rem;
}

.card__body {
  padding: 0 1.25rem 1.25rem;
  display: flex;
  flex-direction: column;
  flex: 1;
}

.card__title {
  font-family: var(--font-family);
  font-size: 1.1rem;
  font-weight: 700;
  color: var(--color-brand-dark);
  line-height: 1.2;
  margin: 0 0 0.5rem 0;
}

.card__meta {
  font-family: var(--font-family);
  font-size: 14px;
  font-weight: 300;
  color: var(--color-brand-dark);
  margin: 0;
}
```

---

## 9. Search & Filter Inputs

### Search input — complete component

```css
.search-input {
  width: 100%;
  height: 44px;
  padding: 0 1rem 0 2.5rem;
  font-family: var(--font-family);
  font-size: 1rem;
  font-weight: 500;
  color: var(--color-brand-dark);
  background-color: var(--color-white);
  border: 1px solid var(--color-brand-dark);
  border-radius: var(--radius-input);
  outline: none;
  transition: border-color var(--transition-base), box-shadow var(--transition-base);
}

.search-input::placeholder {
  color: var(--color-brand-dark);
  opacity: 0.5;
  font-weight: 400;
}

.search-input:hover { border-color: var(--color-brand-green); }
.search-input:focus {
  border-color: var(--color-brand-green);
  box-shadow: 0 0 0 3px rgba(10, 173, 10, 0.08);
}
```

### Filter chip / tag — complete component

```css
.filter-chip {
  display: inline-flex;
  align-items: center;
  height: 32px;
  padding: 0 1rem;
  font-family: var(--font-family);
  font-size: 13px;
  font-weight: 500;
  color: var(--color-brand-dark);
  background-color: var(--color-surface);
  border: 1px solid transparent;
  border-radius: var(--radius-pill);
  cursor: pointer;
  white-space: nowrap;
  transition: all var(--transition-base);
}

.filter-chip:hover         { color: var(--color-brand-green); }
.filter-chip.is-active     { background-color: var(--color-brand-dark); color: #ffffff; }
.filter-chip:focus-visible { outline: 2px solid var(--color-brand-green); outline-offset: 2px; }
```

---

## 10. Navigation

```css
.nav {
  height: 64px;
  width: 100%;
  max-width: 1536px;
  margin: 0 auto;
  display: flex;
  align-items: center;
  background-color: var(--color-white);
}

.nav__link {
  font-family: var(--font-family);
  font-size: 1rem;
  font-weight: 500;
  color: var(--color-brand-dark);
  text-decoration: none;
  transition: color var(--transition-base);
}

.nav__link:hover     { color: var(--color-brand-green); }
.nav__link.is-active { font-weight: 600; color: var(--color-brand-green); }
```

---

## 11. Section Layout Pattern

Every section on the platform must follow this structure:

```
┌─────────────────────────────────────────────┐
│  [H2 — 800 ExtraBold, #021300]              │
│  [Subtext — 300 Light, #021300, 1rem]       │
│  ↕ 3rem gap                                  │
│  [Content — cards / grid / list]            │
└─────────────────────────────────────────────┘
```

```css
.section {
  padding: var(--spacing-section-sm) 1.5rem;
}

@media (min-width: 1024px) {
  .section { padding: var(--spacing-section-lg) 2rem; }
}

.section__header {
  margin-bottom: var(--spacing-header-gap);
}

.section__heading {
  font-size: clamp(2rem, 3vw, 3rem);
  font-weight: 800;
  color: var(--color-brand-dark);
  margin-bottom: var(--spacing-subtext-gap);
}

.section__subtext {
  font-size: 1rem;
  font-weight: 300;
  color: var(--color-brand-dark);
  line-height: 1.625;
  max-width: 36rem;
}
```

---

## 12. Focus & Accessibility

```css
/* Brand focus ring — keyboard navigation only */
a:focus-visible,
button:focus-visible,
input:focus-visible,
select:focus-visible {
  outline: 2px solid var(--color-brand-green);
  outline-offset: 2px;
}

/* Suppress focus ring on mouse click */
a:focus:not(:focus-visible),
button:focus:not(:focus-visible),
input:focus:not(:focus-visible) {
  outline: none;
  box-shadow: none;
}
```

---

## 13. Do / Don't Reference

| Do | Don't |
|---|---|
| Use `#021300` for all body text, headings, and subtext | Substitute `#374151`, `#333333`, or `#000000` — they are off-brand |
| Use Poppins 300 for subtext and metadata | Use weight 400 for subtext — it reads as too heavy |
| Use Poppins 800 for H1 and H2 | Use the same weight for all headings |
| Use `#0AAD0A` for hover and active states only | Use green as a default text or background colour |
| Use 2px `#021300` borders on featured cards and images | Use shadow-only card styles with no border |
| Use 44px height for all buttons | Use smaller touch targets |
| Use `translateY(-2px)` on card hover | Use a shadow lift alone — the border + lift together is the brand pattern |
| Use `0.2s ease` for all transitions | Use instant state changes or long easing curves |
| Use CSS variables from the tokens block | Hardcode hex values in component styles |
| Use `#E5E7EB` for dividers and non-featured borders | Use brand dark `#021300` for all borders — reserve it for featured/card borders |
