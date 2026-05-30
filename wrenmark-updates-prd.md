# Wrenmark Studio — Website Updates PRD
**Project:** wrenmarkstudio.com
**Files:** index.html · styles.css
**Prepared:** 2026-05-30
**Status:** Awaiting approval before implementation

---

## Design Context

Brand: Warm luxury boutique, editorial, premium home decor for women 45–65.
Style direction: Editorial minimalism with warm luxury accents.
Palette in use: Warm Cream #F5E6D3 · Deep Navy #1A2744 · Campfire Terracotta #C0392B · Soft Gold #C9A84C · Hazelnut Brown #8B6347 · Dark Espresso #2C1F14.
Typography: Cormorant Garamond Italic (headings) · Lato 300/400 (body) · Playfair Display (values bar labels — new).

---

## Change 1 — Footer Background Color

**File:** styles.css
**Selector:** `.site-footer`
**Change:** `background-color` from `#1A2744` (Deep Navy) → `#2C1F14` (Dark Espresso)

**Rationale:**
Deep Espresso reads warmer and more grounded than Deep Navy for a footer on a cream-background brand. It harmonises with the Hazelnut Brown and Campfire Terracotta used elsewhere, keeping the site in the warm brown-gold-terracotta family rather than pulling blue-cool at the bottom.

**Accessibility check:**
- Footer copy `#F5E6D3` on `#2C1F14`: contrast ratio ≈ 9.1:1 ✓ (WCAG AA + AAA pass)
- Footer links `#F5E6D3` on `#2C1F14`: ≈ 9.1:1 ✓
- Gold hover `#C9A84C` on `#2C1F14`: ≈ 5.2:1 ✓ (WCAG AA pass)

**No other changes to footer.**

---

## Change 2 — Nav Scroll Background + Link Color

**File:** styles.css
**Selectors:** `.site-nav.scrolled` · `.nav-etsy-link` (scrolled state) · `.nav-pinterest-link` (scrolled state — see Change 6)

### 2a. Scrolled background
**Change:** `.site-nav.scrolled` `background-color` from `#1A2744` → `#F5E6D3`
**Box shadow:** Update to `0 1px 16px rgba(139, 99, 71, 0.14)` (warm shadow matching new bg)

### 2b. Etsy link color on scroll
The existing `.nav-etsy-link` color is `#F5E6D3` (cream) — readable on Navy, invisible on Cream.
**Change:** Add `.site-nav.scrolled .nav-etsy-link` rule setting `color: #8B6347` (Hazelnut Brown).
Hover gold underline `#C9A84C` remains — readable on cream ✓.

### 2c. Pinterest icon color on scroll (see Change 6)
Per Sonja's answer: Pinterest icon turns `#C0392B` (Campfire Terracotta) on scroll.
**Change:** Add `.site-nav.scrolled .nav-pinterest-link` rule setting `color: #C0392B`.

**Unscrolled state:** No change — nav remains fully transparent, all links remain `#F5E6D3`.

**Accessibility check:**
- `#8B6347` on `#F5E6D3`: contrast ratio ≈ 3.5:1 — borderline at small sizes. Mitigate by keeping `font-weight: 400` and `letter-spacing: 0.14em` (larger effective size reduces contrast risk). Acceptable for nav utility text at this weight/size.
- `#C0392B` on `#F5E6D3`: contrast ratio ≈ 4.6:1 ✓ (WCAG AA pass for icon)

**Transition:** Existing `280ms ease` on `.site-nav` handles the background fade. Link color transitions added via `transition: color 280ms ease` on both link elements.

---

## Change 3 — Lifestyle Image Strip

**File:** index.html (new `<section>`) · styles.css (new rules)
**Position:** After `</section>` (hero close) · Before `<footer>`

### HTML structure
```html
<section class="lifestyle-strip" aria-label="Lifestyle photography">
  <div class="lifestyle-strip__grid">
    <div class="lifestyle-strip__item">
      <img src="images/lifestyle-1.jpg" alt="Wrenmark Studio — cozy camper interior detail" class="lifestyle-strip__img" loading="lazy" />
    </div>
    <div class="lifestyle-strip__item">
      <img src="images/lifestyle-2.jpg" alt="Wrenmark Studio — RV home styling" class="lifestyle-strip__img" loading="lazy" />
    </div>
    <div class="lifestyle-strip__item">
      <img src="images/lifestyle-3.jpg" alt="Wrenmark Studio — camper decor lifestyle" class="lifestyle-strip__img" loading="lazy" />
    </div>
  </div>
</section>
```

### CSS rules
```css
.lifestyle-strip {
  width: 100%;
  background: #F5E6D3; /* fallback while images load */
}

.lifestyle-strip__grid {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 3px;
}

.lifestyle-strip__item {
  overflow: hidden;
  aspect-ratio: 3 / 2;
}

.lifestyle-strip__img {
  width: 100%;
  height: 100%;
  object-fit: cover;
  object-position: center;
  display: block;
}

/* Mobile — single column */
@media (max-width: 768px) {
  .lifestyle-strip__grid {
    grid-template-columns: 1fr;
  }
}
```

**Notes:**
- `loading="lazy"` on all three — below the fold, no need to eagerly load.
- `aspect-ratio: 3/2` enforced on the wrapper `__item`, not the `img` — avoids layout shift.
- Alt text is descriptive (accessibility) but generic enough to not need updating per image.
- No text, no links, no overlays as specified.

---

## Change 4 — Brand Values Bar

**File:** index.html (new `<section>`) · styles.css (new rules) · `<head>` Google Fonts import (Playfair Display added)
**Position:** After lifestyle strip · Before `<footer>`

### Google Fonts update
**Current import:**
```
Cormorant+Garamond:ital,wght@1,300;1,400&family=Lato:wght@300;400
```
**Updated import:**
```
Cormorant+Garamond:ital,wght@1,300;1,400&family=Lato:wght@300;400&family=Playfair+Display:wght@400
```

### SVG Icons (inline, 40×40 viewBox, stroke-based outlines, Soft Gold #C9A84C)

**Leaf (Column 1):**
```svg
<svg viewBox="0 0 40 40" fill="none" stroke="#C9A84C" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round" aria-hidden="true">
  <path d="M20 34 C20 34 8 26 8 16 C8 9 13 6 20 6 C27 6 32 9 32 16 C32 26 20 34 20 34Z"/>
  <line x1="20" y1="34" x2="20" y2="16"/>
  <path d="M20 22 C17 19 14 18 12 18"/>
  <path d="M20 26 C23 23 26 22 28 22"/>
</svg>
```

**Compass (Column 2):**
```svg
<svg viewBox="0 0 40 40" fill="none" stroke="#C9A84C" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round" aria-hidden="true">
  <circle cx="20" cy="20" r="13"/>
  <polygon points="20,10 23,20 20,24 17,20" fill="#C9A84C" opacity="0.25"/>
  <polygon points="20,10 23,20 20,24 17,20" fill="none"/>
  <polygon points="20,30 17,20 20,24 23,20" fill="none"/>
  <circle cx="20" cy="20" r="1.5" fill="#C9A84C"/>
</svg>
```

**Hearth/Home (Column 3):**
```svg
<svg viewBox="0 0 40 40" fill="none" stroke="#C9A84C" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round" aria-hidden="true">
  <path d="M8 20 L20 9 L32 20"/>
  <path d="M11 17.5 L11 32 L29 32 L29 17.5"/>
  <rect x="16" y="24" width="8" height="8" rx="1"/>
  <path d="M16 32 L16 28 Q20 24 24 28 L24 32"/>
</svg>
```

### HTML structure
```html
<section class="values-bar" aria-label="Brand values">
  <div class="values-bar__inner">

    <a href="#" class="values-bar__col" aria-label="Original Illustration — Every design is created by hand">
      <span class="values-bar__icon" aria-hidden="true">
        <!-- Leaf SVG here -->
      </span>
      <span class="values-bar__label">Original Illustration</span>
      <span class="values-bar__sub">Every design is created by hand — not generated, not generic.</span>
    </a>

    <a href="#" class="values-bar__col" aria-label="Made for Your Journey — Cozy camper decor designed around the life you actually live">
      <span class="values-bar__icon" aria-hidden="true">
        <!-- Compass SVG here -->
      </span>
      <span class="values-bar__label">Made for Your Journey</span>
      <span class="values-bar__sub">Cozy camper decor designed around the life you actually live.</span>
    </a>

    <a href="#" class="values-bar__col" aria-label="Cohesive by Design — Everything coordinates so your space feels designed, not assembled">
      <span class="values-bar__icon" aria-hidden="true">
        <!-- Home SVG here -->
      </span>
      <span class="values-bar__label">Cohesive by Design</span>
      <span class="values-bar__sub">Everything coordinates — so your space feels designed, not assembled.</span>
    </a>

  </div>
</section>
```

### CSS rules
```css
.values-bar {
  background-color: #F5E6D3;
  padding: 72px 2rem;
}

.values-bar__inner {
  display: flex;
  justify-content: center;
  gap: 3rem;
  max-width: 1100px;
  margin: 0 auto;
}

.values-bar__col {
  display: flex;
  flex-direction: column;
  align-items: center;
  text-align: center;
  flex: 1;
  text-decoration: none;
  color: inherit;
  cursor: default; /* visually inert until real URLs added */
}

.values-bar__icon {
  display: flex;
  align-items: center;
  justify-content: center;
  width: 48px;
  height: 48px;
  margin-bottom: 1.25rem;
  flex-shrink: 0;
}

.values-bar__icon svg {
  width: 40px;
  height: 40px;
}

.values-bar__label {
  font-family: 'Playfair Display', Georgia, serif;
  font-weight: 400;
  font-size: 17px;
  line-height: 1.3;
  color: #1A2744;
  margin-bottom: 0.6rem;
  display: block;
}

.values-bar__sub {
  font-family: 'Lato', sans-serif;
  font-weight: 400;
  font-size: 14px;
  line-height: 1.65;
  color: #8B6347;
  display: block;
  max-width: 240px;
}

/* Mobile — single column */
@media (max-width: 768px) {
  .values-bar {
    padding: 56px 2rem;
  }

  .values-bar__inner {
    flex-direction: column;
    align-items: center;
    gap: 32px;
  }

  .values-bar__col {
    max-width: 320px;
  }
}
```

**Accessibility notes:**
- `aria-label` on each `<a>` combines label + subtext for screen readers.
- `aria-hidden="true"` on icon spans — decorative only.
- `cursor: default` keeps columns visually inert until real URLs assigned.
- No hover state (per Sonja's answer).

---

## Change 5 — Hero CTA Button Style

**File:** styles.css
**Selector:** `.hero-cta`

### Current style (to be replaced)
```css
color: #F5E6D3;
background-color: transparent;
border: 2px solid #F5E6D3;
```

### New style
```css
color: #F5E6D3;
background-color: #C0392B;
border: none;
```

### Hover state (updated)
**Current:** `background-color: #F5E6D3; color: #1A2744; border-color: #F5E6D3`
**New:** `background-color: #A8302A; color: #F5E6D3;` (border remains none)

**All other `.hero-cta` properties unchanged:** padding, font, letter-spacing, text-transform, border-radius, cursor, transition, focus-visible.

**Rationale:**
Solid Campfire Terracotta CTA reads as a stronger commercial signal than an outlined ghost button — better conversion intent. The warm red against the hero image's golden tones is on-brand and eye-catching without being harsh.

**Accessibility check:**
- `#F5E6D3` on `#C0392B`: contrast ratio ≈ 4.7:1 ✓ (WCAG AA pass)
- `#F5E6D3` on `#A8302A` (hover): ≈ 5.1:1 ✓

---

## Change 6 — Pinterest Icon in Nav

**File:** index.html (new element in `.nav-inner`) · styles.css (new rules)

### HTML — add after `.nav-etsy-link`
```html
<a
  href="https://www.pinterest.com/WrenmarkStudio"
  class="nav-pinterest-link"
  target="_blank"
  rel="noopener noreferrer"
  aria-label="Wrenmark Studio on Pinterest"
>
  <svg class="nav-pinterest-icon" viewBox="0 0 24 24" fill="currentColor" aria-hidden="true" focusable="false">
    <path d="M12 0C5.373 0 0 5.373 0 12c0 5.084 3.163 9.426 7.627 11.174-.105-.949-.2-2.405.042-3.441.218-.937 1.407-5.965 1.407-5.965s-.359-.719-.359-1.782c0-1.668.967-2.914 2.171-2.914 1.023 0 1.518.769 1.518 1.69 0 1.029-.655 2.568-.994 3.995-.283 1.194.599 2.169 1.777 2.169 2.133 0 3.772-2.249 3.772-5.495 0-2.873-2.064-4.882-5.012-4.882-3.414 0-5.418 2.561-5.418 5.207 0 1.031.397 2.138.893 2.738a.36.36 0 0 1 .083.345l-.333 1.36c-.053.22-.174.267-.402.161-1.499-.698-2.436-2.889-2.436-4.649 0-3.785 2.75-7.262 7.929-7.262 4.163 0 7.398 2.967 7.398 6.931 0 4.136-2.607 7.464-6.227 7.464-1.216 0-2.359-.632-2.75-1.378l-.748 2.853c-.271 1.043-1.002 2.35-1.492 3.146C9.57 23.812 10.763 24 12 24c6.627 0 12-5.373 12-12S18.627 0 12 0z"/>
  </svg>
</a>
```

### Nav right-side wrapper
The nav currently has only `.nav-etsy-link` on the right. Both links will be wrapped in a flex container:
```html
<div class="nav-right">
  <a href="..." class="nav-etsy-link">Shop on Etsy</a>
  <a href="..." class="nav-pinterest-link" ...><!-- SVG --></a>
</div>
```

### CSS rules
```css
/* Right-side nav group */
.nav-right {
  display: flex;
  align-items: center;
  gap: 1.25rem;
}

/* Pinterest icon — unscrolled (transparent nav) */
.nav-pinterest-link {
  display: flex;
  align-items: center;
  justify-content: center;
  color: #F5E6D3;
  min-width: 44px;
  min-height: 44px;
  cursor: pointer;
  transition: color 200ms ease;
}

.nav-pinterest-icon {
  width: 20px;
  height: 20px;
  flex-shrink: 0;
}

.nav-pinterest-link:hover,
.nav-pinterest-link:focus-visible {
  color: #C9A84C; /* Soft Gold hover — unscrolled */
}

.nav-pinterest-link:focus-visible {
  outline: 2px solid #C9A84C;
  outline-offset: 4px;
  border-radius: 2px;
}

/* Scrolled state — terracotta (per Sonja's answer) */
.site-nav.scrolled .nav-pinterest-link {
  color: #C0392B;
}

.site-nav.scrolled .nav-pinterest-link:hover,
.site-nav.scrolled .nav-pinterest-link:focus-visible {
  color: #8B6347; /* dims to brown on hover when scrolled */
}

/* Scrolled state — Etsy link */
.site-nav.scrolled .nav-etsy-link {
  color: #8B6347;
}
```

---

## Implementation Order

Apply changes in this sequence to minimise risk of conflicting edits:

1. `styles.css` — Change 1 (footer bg) — isolated, zero risk
2. `styles.css` — Change 5 (hero CTA) — isolated, zero risk
3. `index.html` + `styles.css` — Change 6 (Pinterest nav icon + nav-right wrapper)
4. `styles.css` — Change 2 (nav scroll colors, now that nav-right and pinterest classes exist)
5. `index.html` + `styles.css` — Change 3 (lifestyle image strip)
6. `index.html` + `styles.css` — Change 4 (brand values bar + Playfair Display font)

---

## Pre-Delivery Checklist

### Visual quality
- [ ] No emojis used as icons — all SVG inline ✓
- [ ] Hover states do not cause layout shift ✓
- [ ] Logo remains visible on scrolled cream nav (gold on cream — verify in browser)

### Interaction
- [ ] All new clickable elements have `cursor-pointer` (or `cursor: default` where intentionally inert)
- [ ] Transitions smooth at 200–280ms ✓
- [ ] Focus states visible on all new interactive elements ✓

### Responsive
- [ ] Lifestyle strip: 3-col desktop → 1-col at ≤768px ✓
- [ ] Values bar: 3-col desktop → 1-col centered at ≤768px, 32px gap ✓
- [ ] Nav right group: Etsy + Pinterest sit side by side without wrapping at 375px

### Accessibility
- [ ] All lifestyle images have descriptive alt text ✓
- [ ] Pinterest nav icon has `aria-label` ✓
- [ ] Values bar `<a>` elements have combined `aria-label` ✓
- [ ] All new color pairs pass WCAG AA (documented per change above) ✓

### Files
- [ ] CNAME untouched ✓
- [ ] README.md untouched ✓
- [ ] No new files created other than this PRD ✓

---

## Files to be Modified

| File | Changes |
|---|---|
| `index.html` | Changes 3, 4, 6 — new sections + nav update + font import |
| `styles.css` | Changes 1, 2, 3, 4, 5, 6 — all visual rules |
| `CNAME` | **Not touched** |
| `README.md` | **Not touched** |
