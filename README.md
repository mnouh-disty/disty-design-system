[README.md](https://github.com/user-attachments/files/29406539/README.md)
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

---

## Animation

### Blur word reveal

Applied **only to h1, h2, h3**. Body text, subheadings, and all other elements are always static.

| Token | Value | Description |
|---|---|---|
| `--anim-blur-duration` | `1200ms` | How long each word takes to come into focus |
| `--anim-blur-stagger` | `80ms` | Delay between each word |
| `--anim-blur-amount` | `8px` | Starting blur, dissolves to 0px |
| `--anim-blur-easing` | `cubic-bezier(0.16, 1, 0.3, 1)` | Silky smooth ease-out |
| `--anim-blur-threshold` | `0.2` | 20% of element in viewport triggers it |

**Behavior:** On scroll into view, each word in the heading fades from blurry (`8px`) to sharp (`0px`), word by word with an 80ms stagger. Fires once — does not repeat on scroll out/in. No slide or movement — blur only.

**Never apply to:** body text, captions, nav links, buttons, badges, or any UI element other than h1/h2/h3.

### JS implementation (vanilla)

```js
(function () {
  const DURATION = 1200;
  const STAGGER  = 80;
  const BLUR     = 8;
  const EASING   = 'cubic-bezier(0.16, 1, 0.3, 1)';

  function wrapWords(el) {
    const words = el.innerText.split(' ');
    el.innerHTML = words.map((w, i) =>
      `<span style="display:inline-block;overflow:hidden;vertical-align:bottom;">` +
      `<span data-index="${i}" style="display:inline-block;opacity:0;filter:blur(${BLUR}px);
        transition:opacity ${DURATION}ms ${EASING},filter ${DURATION}ms ${EASING};">${w}</span>` +
      `</span>${i < words.length - 1 ? ' ' : ''}`
    ).join('');
  }

  function revealEl(el) {
    el.querySelectorAll('[data-index]').forEach(w => {
      setTimeout(() => {
        w.style.opacity = '1';
        w.style.filter  = 'blur(0px)';
      }, parseInt(w.dataset.index) * STAGGER);
    });
  }

  document.querySelectorAll('h1, h2, h3').forEach(el => {
    wrapWords(el);
    new IntersectionObserver((entries, obs) => {
      if (entries[0].isIntersecting) { revealEl(el); obs.unobserve(el); }
    }, { threshold: 0.2 }).observe(el);
  });
})();
```

### Framer Motion (React / HeroUI)

```jsx
import { motion } from 'framer-motion'

function BlurHeading({ children, as: Tag = 'h2' }) {
  const words = children.split(' ')
  return (
    <Tag>
      {words.map((word, i) => (
        <motion.span
          key={i}
          style={{ display: 'inline-block', marginRight: '0.25em' }}
          initial={{ opacity: 0, filter: 'blur(8px)' }}
          whileInView={{ opacity: 1, filter: 'blur(0px)' }}
          transition={{
            duration: 1.2,
            delay: i * 0.08,
            ease: [0.16, 1, 0.3, 1],
          }}
          viewport={{ once: true, amount: 0.2 }}
        >
          {word}
        </motion.span>
      ))}
    </Tag>
  )
}

// Usage
<BlurHeading as="h1">Build something that lasts.</BlurHeading>
<BlurHeading as="h2">Design with intention.</BlurHeading>
```
