# Disty Design System

A production-ready design system for Disty's marketing website. Built with HeroUI conventions, TT Commons Pro, and a custom purple palette.

---

## Stack

| Layer | Choice |
|---|---|
| Framework | React + Next.js |
| Component library | HeroUI (formerly NextUI) |
| Styling | Tailwind CSS |
| Font | TT Commons Pro (Adobe Typekit — `fcz0pyr`) |
| Mode | Light only |

---

## Font setup

Add this to your `<head>` before any stylesheets:

```html
<link rel="stylesheet" href="https://use.typekit.net/fcz0pyr.css">
```

Then in CSS or Tailwind config:

```css
font-family: "tt-commons-pro", sans-serif;
```

---

## Color palette

### Primary
| Name | Hex | Usage |
|---|---|---|
| Purple | `#511DCE` | Primary CTAs, links, accents |
| Black | `#000000` | Body text, dark surfaces |
| White | `#FFFFFF` | Backgrounds, text on dark |

### Secondary
| Name | Hex | Usage |
|---|---|---|
| Purple hover | `#7B6DE8` | Hover state for primary purple |
| Lavender | `#AB9FFF` | Secondary accents |
| Lilac | `#D4CEFF` | Borders on tint backgrounds |
| Purple tint | `#EDE9FF` | Badge backgrounds, tint surfaces |

### Grey scale (purple-tinted)
| Token | Hex | Usage |
|---|---|---|
| Grey 50 | `#F7F6FA` | Page backgrounds, footer |
| Grey 100 | `#EEEDF4` | Subtle section backgrounds |
| Grey 200 | `#DDDCE8` | Default borders, dividers |
| Grey 300 | `#C4C3D0` | Strong borders |
| Grey 400 | `#9896A8` | Muted text, placeholders |
| Grey 500 | `#6B6978` | Secondary text |
| Grey 600 | `#4A4856` | Secondary text (stronger) |
| Grey 700 | `#2E2C38` | Body text on grey backgrounds |
| Grey 800 | `#1A1820` | Near-black, dark surfaces |

---

## Typography

Font: **TT Commons Pro** across all weights (100–900), normal and italic.

| Role | Size | Weight |
|---|---|---|
| Display | 64px | 700 |
| Heading 1 | 48px | 700 |
| Heading 2 | 36px | 600 |
| Heading 3 | 28px | 600 |
| Heading 4 | 22px | 500 |
| Body large | 18px | 400 |
| Body | 16px | 400 |
| Body small | 14px | 400 |
| Caption | 12px | 400 |

Letter spacing on headings: `-0.02em` to `-0.03em` for large display sizes.

---

## Spacing scale

| Token | Value |
|---|---|
| `--space-1` | 4px |
| `--space-2` | 8px |
| `--space-3` | 12px |
| `--space-4` | 16px |
| `--space-5` | 20px |
| `--space-6` | 24px |
| `--space-8` | 32px |
| `--space-10` | 40px |
| `--space-12` | 48px |
| `--space-16` | 64px |

---

## Border radius

| Token | Value | Usage |
|---|---|---|
| `--radius-sm` | 6px | Badges, small tags |
| `--radius-md` | 10px | Buttons, inputs |
| `--radius-lg` | 14px | Cards, modals |
| `--radius-xl` | 20px | Large cards |
| `--radius-full` | 999px | Pills, avatars |

---

## HeroUI theme config

```js
// tailwind.config.js
const { heroui } = require("@heroui/react");

module.exports = {
  plugins: [
    heroui({
      themes: {
        light: {
          colors: {
            primary:    "#511DCE",
            secondary:  "#AB9FFF",
            background: "#FFFFFF",
            foreground: "#000000",
          },
        },
      },
    }),
  ],
  theme: {
    extend: {
      fontFamily: {
        sans: ['"tt-commons-pro"', "sans-serif"],
      },
      colors: {
        purple: {
          DEFAULT: "#511DCE",
          hover:   "#7B6DE8",
          mid:     "#AB9FFF",
          light:   "#D4CEFF",
          tint:    "#EDE9FF",
        },
        grey: {
          50:  "#F7F6FA",
          100: "#EEEDF4",
          200: "#DDDCE8",
          300: "#C4C3D0",
          400: "#9896A8",
          500: "#6B6978",
          600: "#4A4856",
          700: "#2E2C38",
          800: "#1A1820",
        },
      },
    },
  },
};
```

---

## Files

| File | Description |
|---|---|
| `design-system-starter.html` | Full visual design system — all components and marketing patterns |
| `tokens.css` | CSS custom properties — import into any project |
| `README.md` | This file |

---

## Components included

**Base components:** Buttons (6 variants, 3 sizes), Cards (5 types), Form inputs, Badges, Avatars

**Marketing patterns:** Navbar (default + frosted), Hero (2 variants), Pricing (3-tier), FAQ accordion, Toast notifications, Footer

---

## Design rules

- Light mode only
- Text on white: `#000000`
- Text on purple backgrounds: `#FFFFFF`
- Muted / secondary text: `#4A4856` or `#6B6978`
- Primary CTA hover: `#7B6DE8`
- Never use pure grey — always use the purple-tinted grey scale
- Heading letter spacing: `-0.02em`
