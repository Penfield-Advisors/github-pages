# Style Guide

Brand assets and colour reference for the Penfield Advisors website.

The colours here are the source of truth and are declared once as CSS custom
properties at the top of [`assets/css/style.css`](../assets/css/style.css). Use
the token (`var(--navy)`) rather than pasting a hex value into new rules.

---

## Logos

All logo files live in [`assets/logos/`](../assets/logos/). Every variant is
drawn from the same two-leaf mark; they differ in what text is included and
whether the navy background is baked into the file.

### The two background families

| Suffix | Background | Wordmark colour | Use on |
| --- | --- | --- | --- |
| *(none)* — e.g. `main-logo.svg` | Opaque navy `#0b254b` | White / sky | Light surfaces, or anywhere a self-contained tile is needed |
| `-transparent` — e.g. `main-logo-transparent.svg` | None (alpha) | White / sky | **Dark surfaces only** |

The `-transparent` variants render their wordmark in **white**, so they
disappear on a light background. That is why the site header and footer are
navy. When placing a logo on a white or `--surface` panel, reach for the
non-transparent variant.

### Variants

| File | Canvas | Contents | Where it is used |
| --- | --- | --- | --- |
| `main-logo.svg` | 810 × 810 (1:1) | Leaf mark above "PENFIELD" / "ADVISORS" | Full lockup for light surfaces — not currently placed in the site |
| `main-logo-transparent.svg` | 810 × 810 (1:1) | Same, no background | Footer brand mark (`_includes/footer.html`), rendered at 170 px wide |
| `main-logo-wide.svg` | 1620 × 540 (3:1) | Leaf mark left, "PENFIELD" / "ADVISORS" right | Horizontal lockup for light surfaces |
| `main-logo-wide-transparent.svg` | 1620 × 540 (3:1) | Same, no background | Header lockup (`_includes/header.html`), rendered at 80 px tall (60 px under 560 px viewport) |
| `small-logo.svg` | 810 × 810 (1:1) | Leaf mark above the "PA" monogram | Square mark where the full name will not read |
| `small-logo-transparent.svg` | 810 × 810 (1:1) | Same, no background | Square mark on dark surfaces |
| `small-logo.png` | 180 × 180, RGB | Rasterised `small-logo.svg` | `apple-touch-icon` (`_includes/head.html`) |
| `small-logo-transparent.png` | 180 × 180, RGBA | Rasterised `small-logo-transparent.svg` | Raster fallback where alpha is wanted |
| `leaf-logo.svg` | 810 × 810 (1:1) | Leaf mark only, no text | Favicon (`_includes/head.html`) |
| `leaf-logo-transparent.svg` | 810 × 810 (1:1) | Leaf mark only, no background | Watermarks, mark-only placements on dark surfaces |

### Notes

- **`small-logo.png` must stay a PNG and must stay opaque.** iOS ignores SVG for
  `apple-touch-icon` and composites any transparency onto black.
- The wide lockup carries its own internal padding, which is why the header bar
  is only slightly taller than the image — no extra margin is needed around it.
- All logo files reference only the three brand colours below; there are no
  gradients or effects to match if a new variant is produced.

---

## Colours

### Brand

| Token | Hex | Use |
| --- | --- | --- |
| `--navy` | `#0b254b` | Primary. Header, CTA band, headings, solid buttons, `theme-color` meta |
| `--sky` | `#9bc6df` | Accent. Primary button fill, hero lead text, links on navy, focus ring |
| `--white` | `#ffffff` | Page background, text on navy, card surfaces |

> **Contrast:** `#9bc6df` does **not** meet WCAG minimums as text on white. Use
> it only as a fill, a rule, or as text on navy.

### Navy shades

| Token | Hex | Use |
| --- | --- | --- |
| `--navy-deep` | `#081b38` | Footer background, open mobile nav panel, hero gradient top stop |
| `--navy-soft` | `#16386e` | Link colour on light backgrounds, solid-button hover |

### Sky shades

| Token | Hex | Use |
| --- | --- | --- |
| `--sky-pale` | `#e8f2f8` | Tint fill (currently used by the placeholder portrait artwork) |

### Neutrals

| Token | Hex | Use |
| --- | --- | --- |
| `--ink` | `#16202e` | Body copy |
| `--muted` | `#55647a` | Secondary copy, eyebrows, captions, card body text |
| `--line` | `#dde5ee` | Borders, `<hr>`, card and image outlines |
| `--surface` | `#f5f8fb` | Alternating section background (`.section--surface`) |

### Derived values

These are expressed as `rgba()` rather than tokens, so they stay in sync with
the brand colours by construction.

| Value | Where |
| --- | --- |
| `rgba(11, 37, 75, .06)` / `rgba(11, 37, 75, .08)` | `--shadow` — navy-tinted card shadow |
| `rgba(8, 27, 56, .86)` → `rgba(11, 37, 75, .94)` | Hero and page-head gradient over the background artwork |
| `rgba(255, 255, 255, .82)` | Footer link and body text |
| `rgba(255, 255, 255, .62)` | Footer legal line |
| `rgba(255, 255, 255, .55)` / `.14` / `.12` / `.1` | Ghost-button border, footer rule, nav hover, mobile nav border |

---

## Typography

| Token | Stack | Use |
| --- | --- | --- |
| `--serif` | Georgia, "Iowan Old Style", "Times New Roman", Times, serif | Headings `h1`–`h4`, page titles |
| `--sans` | system UI stack (`-apple-system`, "Segoe UI", Roboto, …) | Body copy, navigation, buttons, eyebrows |

No web fonts are loaded — the site has no external font, script, or CDN
dependencies.

---

## Layout tokens

| Token | Value | Meaning |
| --- | --- | --- |
| `--wrap` | `1120px` | Max content width (`.wrap`) |
| `--gap` | `1.5rem` | Default grid gap |
| `--radius` | `10px` | Corner radius for cards, buttons, images |
