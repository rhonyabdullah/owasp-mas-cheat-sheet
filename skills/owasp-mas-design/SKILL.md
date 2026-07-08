# OWASP MAS HTML Design System

> Version: 1.0.0  
> Scope: MASVS, MASWE, and future MASTG interactive HTML cheat sheets  
> Target: Single-file, self-contained HTML artifacts (no external dependencies)

---

## 1. Design Philosophy

- **Single-file artifact**: Everything — CSS, JS, HTML — lives in one file. No external CDN calls.
- **Self-contained**: Copy the file, open it in a browser. Done.
- **Engineer-first**: Dense information, minimal chrome. Collapsible sections for scanability.
- **OWASP brand alignment**: Colors derived from OWASP MAS project palette.
- **Mobile-friendly**: Responsive down to 360px width.

---

## 2. Color Palette

All colors are defined as CSS custom properties on `:root`.

| Token | Hex | Usage |
|---|---|---|
| `--owasp-blue` | `#1b7a8c` | Primary brand, group headers, active states |
| `--owasp-dark` | `#0d3b44` | Dark backgrounds, footer, hover states |
| `--owasp-accent` | `#f2a900` | CTAs, copy buttons, highlights, badges |
| `--owasp-light` | `#e8f4f6` | Subtle backgrounds, alternating rows |
| `--bg-page` | `#f4f7f9` | Page background |
| `--bg-card` | `#ffffff` | Card / content area background |
| `--text-primary` | `#1a1a2e` | Headings, primary text |
| `--text-secondary` | `#5e6c84` | Descriptions, metadata, placeholders |
| `--border-subtle` | `#e1e4e8` | Dividers, card borders |

### Profile Badge Colors (MASWE / MASTG)

| Profile | Hex | Background | Text |
|---|---|---|---|
| L1 | `#36B37E` | `rgba(54,179,126,0.12)` | `#36B37E` |
| L2 | `#0052CC` | `rgba(0,82,204,0.12)` | `#0052CC` |
| R (Resilience) | `#6554C0` | `rgba(101,84,192,0.12)` | `#6554C0` |
| P (Privacy) | `#FF5630` | `rgba(255,86,48,0.12)` | `#FF5630` |

### Status Badge Colors

| Status | Hex | Background | Text |
|---|---|---|---|
| current | `#36B37E` | `rgba(54,179,126,0.12)` | `#36B37E` |
| placeholder | `#FFAB00` | `rgba(255,171,0,0.12)` | `#b37600` |
| deprecated | `#FF5630` | `rgba(255,86,48,0.12)` | `#FF5630` |

---

## 3. Typography

| Element | Font | Size | Weight | Line Height | Color |
|---|---|---|---|---|---|
| Page Title | System sans | `2rem` | 700 | 1.2 | `--owasp-dark` |
| Group Header | System sans | `1.15rem` | 700 | 1.3 | `#ffffff` |
| Item Title | System sans | `1rem` | 600 | 1.4 | `--text-primary` |
| Description | System sans | `0.95rem` | 400 | 1.6 | `--text-secondary` |
| Metadata / Badges | System sans | `0.8rem` | 500 | 1.4 | varies |
| Prompt Text | Monospace | `0.85rem` | 400 | 1.5 | `#2d3748` |

**Font stack:** `-apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Helvetica, Arial, sans-serif`

**Monospace stack:** `"SFMono-Regular", Consolas, "Liberation Mono", Menlo, Courier, monospace`

---

## 4. Layout Structure

### 4.1 Page Shell

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>[Artifact Title]</title>
  <style>/* All CSS here */</style>
</head>
<body>
  <header class="page-header">
    <h1>[Title]</h1>
    <p class="subtitle">[Subtitle / description]</p>
  </header>

  <main class="container">
    <!-- Search / Filter Bar (MASWE/MASTG only) -->
    <!-- Group Sections -->
  </main>

  <footer class="page-footer">
    <!-- Timestamp, source links, disclaimers -->
  </footer>

  <script>/* All JS here */</script>
</body>
</html>
```

### 4.2 Container

- Max width: `1200px`
- Centered with `margin: 0 auto`
- Padding: `0 1.5rem` (desktop), `0 1rem` (mobile)

### 4.3 Group Section (Collapsible)

Each MASVS category or MASWE weakness group is a collapsible section.

```html
<section class="group" data-category="STORAGE">
  <button class="group-header" aria-expanded="true|false">
    <span class="group-title">MASVS-STORAGE</span>
    <span class="group-meta">[N controls / weaknesses]</span>
    <span class="group-toggle">▼</span>
  </button>
  <div class="group-content">
    <p class="group-description">[Group description]</p>
    <!-- Items -->
  </div>
</section>
```

**Behavior:**
- Clicking the header toggles `aria-expanded` and visibility of `.group-content`.
- Transition: `max-height` + `opacity` animation, `0.3s ease`.
- Chevron rotates 180° when collapsed.

**Default state:**
- **MASVS**: Groups expanded by default (only 8 groups, 24 items total).
- **MASWE**: Groups collapsed by default (99 items, too many to scroll).
- **MASTG Tests**: Groups collapsed by default (hundreds of items).

---

## 5. Components

### 5.1 Control / Weakness / Test Item Card

Each actionable item is a card inside a group.

```html
<div class="item-card" data-id="MASVS-STORAGE-1" data-profiles="L1 L2" data-status="current">
  <div class="item-header">
    <span class="item-id">MASVS-STORAGE-1</span>
    <span class="item-status status-current">current</span>
  </div>
  <h3 class="item-title">[Title]</h3>
  <p class="item-description">[Short description, 1-2 sentences]</p>

  <div class="item-badges">
    <span class="badge badge-l1">L1</span>
    <span class="badge badge-l2">L2</span>
  </div>

  <!-- Prompt section (collapsible) -->
  <button class="prompt-toggle">Show Prompt</button>
  <div class="prompt-content">
    <div class="prompt-box">
      <pre>[Prompt text]</pre>
      <button class="copy-btn" data-target="...">Copy</button>
    </div>
  </div>
</div>
```

**Card styling:**
- Background: `--bg-card`
- Border: `1px solid var(--border-subtle)`
- Border radius: `8px`
- Padding: `1rem 1.25rem`
- Margin bottom: `0.75rem`
- Box shadow: `0 1px 3px rgba(0,0,0,0.06)`

**Hover:**
- Border color shifts to `--owasp-blue`
- Subtle shadow increase: `0 4px 12px rgba(27,122,140,0.08)`
- Transition: `0.2s ease`

### 5.2 Badges

Badges are inline pills.

```css
.badge {
  display: inline-block;
  padding: 0.2rem 0.6rem;
  border-radius: 12px;
  font-size: 0.75rem;
  font-weight: 600;
  text-transform: uppercase;
  letter-spacing: 0.02em;
}
```

Profile badges use the colors defined in §2.
Status badges use the colors defined in §2.

### 5.3 Prompt Box

The prompt section is **collapsed by default** in all artifacts.

```css
.prompt-content {
  max-height: 0;
  overflow: hidden;
  opacity: 0;
  transition: max-height 0.3s ease, opacity 0.2s ease;
}
.prompt-content.open {
  max-height: 500px; /* or a large value */
  opacity: 1;
}
.prompt-box {
  background: #f8f9fa;
  border: 1px solid var(--border-subtle);
  border-radius: 6px;
  padding: 1rem;
  margin-top: 0.75rem;
  position: relative;
}
.prompt-box pre {
  margin: 0;
  white-space: pre-wrap;
  word-break: break-word;
}
```

**Copy button:**
- Position: absolute top-right inside `.prompt-box`
- Background: `--owasp-accent`
- Text: `#ffffff`, `0.75rem`, bold
- Padding: `0.3rem 0.7rem`
- Border radius: `4px`
- On click: text changes to "Copied!" for 1.5s, then reverts

### 5.4 Search & Filter Bar (MASWE / MASTG)

Placed at the top of `<main>`, before the first group.

```html
<div class="filter-bar">
  <input type="text" class="search-input" placeholder="Search by ID, title, or keyword...">
  <div class="filter-buttons">
    <button class="filter-btn active" data-filter="all">All</button>
    <button class="filter-btn" data-filter="STORAGE">Storage</button>
    <!-- ... -->
  </div>
  <div class="filter-buttons">
    <button class="filter-btn active" data-profile="all">All Profiles</button>
    <button class="filter-btn" data-profile="L1">L1</button>
    <button class="filter-btn" data-profile="L2">L2</button>
    <button class="filter-btn" data-profile="R">R</button>
    <button class="filter-btn" data-profile="P">P</button>
  </div>
</div>
```

**Styling:**
- `.filter-bar`: `display: flex; flex-wrap: wrap; gap: 0.75rem; margin-bottom: 1.5rem;`
- `.search-input`: `flex: 1; min-width: 260px; padding: 0.6rem 1rem; border: 1px solid var(--border-subtle); border-radius: 6px; font-size: 0.95rem;`
- `.filter-btn`: `padding: 0.4rem 0.9rem; border: 1px solid var(--border-subtle); background: #fff; border-radius: 20px; cursor: pointer; font-size: 0.85rem;`
- `.filter-btn.active`: `background: var(--owasp-blue); color: #fff; border-color: var(--owasp-blue);`

**Behavior:**
- Search filters in real-time (debounce 150ms optional).
- Category filter shows only groups matching the selected category.
- Profile filter shows only items matching the selected profile.
- If a group has zero visible items after filtering, hide the entire group.
- If search returns zero results, show a "No results" message.

---

## 6. Animations

### 6.1 Group Expand / Collapse

```css
.group-content {
  max-height: 2000px; /* sufficiently large */
  opacity: 1;
  overflow: hidden;
  transition: max-height 0.35s ease, opacity 0.25s ease;
}
.group-content.collapsed {
  max-height: 0;
  opacity: 0;
}
.group-toggle {
  transition: transform 0.3s ease;
}
.group-header[aria-expanded="false"] .group-toggle {
  transform: rotate(-90deg);
}
```

### 6.2 Item Card Hover

```css
.item-card {
  transition: border-color 0.2s ease, box-shadow 0.2s ease, transform 0.2s ease;
}
.item-card:hover {
  border-color: var(--owasp-blue);
  box-shadow: 0 4px 12px rgba(27,122,140,0.08);
  transform: translateY(-1px);
}
```

### 6.3 Copy Button Feedback

```css
.copy-btn {
  transition: background 0.2s ease;
}
.copy-btn.copied {
  background: #36B37E !important;
}
```

### 6.4 Page Load

```css
@keyframes fadeInUp {
  from { opacity: 0; transform: translateY(12px); }
  to   { opacity: 1; transform: translateY(0); }
}
.group {
  animation: fadeInUp 0.5s ease both;
}
/* Staggered delay via inline style or nth-child */
.group:nth-child(1) { animation-delay: 0.05s; }
.group:nth-child(2) { animation-delay: 0.10s; }
/* ... up to reasonable limit */
```

---

## 7. Responsive Breakpoints

| Breakpoint | Behavior |
|---|---|
| `>= 1024px` | Full layout, filter bar horizontal, groups in single column |
| `768px - 1023px` | Filter bar wraps, groups single column |
| `< 768px` | Reduced padding, smaller fonts, filter buttons scroll horizontally if needed, prompt box pre font-size `0.8rem` |

---

## 8. JavaScript Patterns

All JS is inline at the bottom of `<body>`. No external libraries.

### 8.1 Group Toggle

```javascript
document.querySelectorAll('.group-header').forEach(btn => {
  btn.addEventListener('click', () => {
    const expanded = btn.getAttribute('aria-expanded') === 'true';
    btn.setAttribute('aria-expanded', !expanded);
    btn.nextElementSibling.classList.toggle('collapsed', expanded);
  });
});
```

### 8.2 Prompt Toggle

```javascript
document.querySelectorAll('.prompt-toggle').forEach(btn => {
  btn.addEventListener('click', (e) => {
    e.stopPropagation();
    const content = btn.nextElementSibling;
    content.classList.toggle('open');
    btn.textContent = content.classList.contains('open') ? 'Hide Prompt' : 'Show Prompt';
  });
});
```

### 8.3 Copy to Clipboard

```javascript
document.querySelectorAll('.copy-btn').forEach(btn => {
  btn.addEventListener('click', async (e) => {
    e.stopPropagation();
    const pre = btn.parentElement.querySelector('pre');
    await navigator.clipboard.writeText(pre.innerText);
    btn.textContent = 'Copied!';
    btn.classList.add('copied');
    setTimeout(() => {
      btn.textContent = 'Copy';
      btn.classList.remove('copied');
    }, 1500);
  });
});
```

### 8.4 Search & Filter (MASWE / MASTG)

```javascript
const searchInput = document.querySelector('.search-input');
const filterBtns = document.querySelectorAll('.filter-btn[data-filter]');
const profileBtns = document.querySelectorAll('.filter-btn[data-profile]');

function applyFilters() {
  const term = searchInput.value.toLowerCase().trim();
  const cat = document.querySelector('.filter-btn[data-filter].active')?.dataset.filter || 'all';
  const prof = document.querySelector('.filter-btn[data-profile].active')?.dataset.profile || 'all';

  document.querySelectorAll('.group').forEach(group => {
    const groupCat = group.dataset.category;
    let groupVisible = (cat === 'all' || groupCat === cat);
    let itemsVisible = 0;

    group.querySelectorAll('.item-card').forEach(card => {
      const text = card.innerText.toLowerCase();
      const profiles = card.dataset.profiles || '';
      const matchesSearch = !term || text.includes(term);
      const matchesProfile = prof === 'all' || profiles.includes(prof);
      const visible = matchesSearch && matchesProfile;
      card.style.display = visible ? '' : 'none';
      if (visible) itemsVisible++;
    });

    group.style.display = (groupVisible && itemsVisible > 0) ? '' : 'none';
  });
}

searchInput.addEventListener('input', applyFilters);
filterBtns.forEach(b => b.addEventListener('click', () => { setActive(b, filterBtns); applyFilters(); }));
profileBtns.forEach(b => b.addEventListener('click', () => { setActive(b, profileBtns); applyFilters(); }));
```

---

## 9. Data Attributes for Filtering

Every item card **must** expose these `data-*` attributes for JS filtering:

| Attribute | Example | Required For |
|---|---|---|
| `data-id` | `MASWE-0001` | All |
| `data-category` | `STORAGE` | All |
| `data-profiles` | `L1 L2` | MASWE, MASTG Tests |
| `data-status` | `current` | MASWE, MASTG Tests |
| `data-platform` | `android` | MASTG Tests, Tools |

Groups also expose `data-category` for category filtering.

---

## 10. Content Rules

### 10.1 Prompt Text Format

Each prompt must be:
- **Concise** (3-8 lines)
- **Specific**: mention platform, tool names, MASTG test references
- **Actionable**: ask for code examples in Kotlin / Swift where relevant
- **Context-aware**: include MASVS control or MASWE weakness ID

Example:
```
Explain MASVS-STORAGE-1 for Android. 
How should sensitive data be stored securely using Jetpack Security Crypto (EncryptedSharedPreferences / EncryptedFile)?
Include Kotlin code examples and mention MASTG-TEST-0001.
```

### 10.2 Description Length

- **MASVS controls**: 1-2 sentences, visible by default.
- **MASWE weaknesses**: 1-2 sentences, visible by default.
- **MASTG tests**: 1 sentence summary + metadata badges, visible by default.

### 10.3 Group Description

Each group header (when expanded) shows a short paragraph explaining the category. This is **visible by default** (not collapsed with items).

---

## 11. Footer Content

```html
<footer class="page-footer">
  <p>Generated: [ISO timestamp]</p>
  <p>Source: <a href="https://mas.owasp.org/MASVS">OWASP MASVS v2.1.0</a></p>
  <p class="disclaimer">
    This is an unofficial reference. Always consult the official OWASP documentation for authoritative guidance.
  </p>
</footer>
```

**Styling:**
- Background: `--owasp-dark`
- Text: `#ffffff` at 80% opacity
- Links: `--owasp-accent`
- Padding: `2rem 1.5rem`
- Font size: `0.85rem`
- Text align: center

---

## 12. Accessibility

- All interactive elements are `<button>` or `<a>`, not `<div onclick>`.
- `aria-expanded` on all toggles.
- Sufficient color contrast (WCAG AA) for all text/badges.
- Focus rings preserved: `outline: 2px solid var(--owasp-accent); outline-offset: 2px;` on `:focus-visible`.

---

## 13. File Naming Convention

| Artifact | Identifier | Filename hint |
|---|---|---|
| MASVS Summary | `owasp-masvs-summary` | `owasp-masvs-summary.html` |
| MASWE Summary | `owasp-maswe-summary-v3` | `owasp-maswe-summary.html` |
| MASTG Tests | `owasp-mastg-tests` | `owasp-mastg-tests.html` |
| MASTG Tools | `owasp-mastg-tools` | `owasp-mastg-tools.html` |

---

## 14. Checklist for Agent Implementation

Before declaring an artifact complete, verify:

- [ ] All CSS is inside `<style>` — no external stylesheet links.
- [ ] All JS is inside `<script>` at bottom of `<body>` — no external scripts.
- [ ] Color tokens use CSS custom properties on `:root`.
- [ ] Group headers are `<button>` with `aria-expanded`.
- [ ] Prompt sections are collapsed by default.
- [ ] Copy buttons work and show "Copied!" feedback.
- [ ] Search + filter logic handles empty results gracefully.
- [ ] All item cards have correct `data-*` attributes.
- [ ] Responsive down to 360px width.
- [ ] Footer contains timestamp, source URL, and disclaimer.
- [ ] No placeholder text — all content is real data.
- [ ] File size is reasonable (< 5MB for single artifact).

---

*End of DESIGN.md v1.0.0*