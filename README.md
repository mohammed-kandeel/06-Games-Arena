<div align="center">

# 🎮 GameArena — Gaming Landing Page

**The Ultimate Gaming Experience**

[![Live Demo](https://img.shields.io/badge/🌐_Live_Demo-View_Project-cbfe1c?style=for-the-badge&labelColor=0b0e13)](https://mohammed-kandeel.github.io/06-Games-Arena/)
[![GitHub](https://img.shields.io/badge/GitHub-Source_Code-181717?style=for-the-badge&logo=github)](https://github.com/mohammed-kandeel/06-Games-Arena)
![HTML5](https://img.shields.io/badge/HTML5-E34F26?style=for-the-badge&logo=html5&logoColor=white)
![CSS3](https://img.shields.io/badge/CSS3-1572B6?style=for-the-badge&logo=css3&logoColor=white)
![Bootstrap](https://img.shields.io/badge/Bootstrap_5-7952B3?style=for-the-badge&logo=bootstrap&logoColor=white)

</div>

---

## 📌 About

**GameArena** is a fully responsive gaming landing page built as a real-world client brief simulation — **Assignment 6** of my Frontend learning journey. The goal was to implement a pixel-perfect mockup using **Bootstrap 5** as the primary layout system, layered with custom CSS for animations, effects, and a complete design system.

---

## ✨ Technical Highlights

### 1. Bootstrap 5 as the Layout Foundation

The entire page structure is built on Bootstrap's grid system (`container-xxl`, `row`, `col-*`) alongside utility classes for spacing, typography, and display — while deliberately **extending** Bootstrap where it falls short.

A custom utilities file (`utilities.css`) extends Bootstrap with a complete token set: font sizes, colors, and weights that mirror the design system exactly but integrate seamlessly with Bootstrap's class naming conventions.

```html
<!-- Bootstrap grid + custom utilities working together -->
<div class="row row-cols-1 row-cols-lg-2 gy-4 gy-lg-0 gx-lg-4 align-items-center">
  <div class="col">...</div>
  <div class="col ps-lg-3">...</div>
</div>
```

---

### 2. Responsive Carousel — 3 Separate Instances

One of the trickier Bootstrap challenges: the Games section needed to show **1 card on mobile, 2 on tablet, and 3 on desktop** — each paginating differently. The solution was three separate carousel instances, shown/hidden with Bootstrap's display utilities.

```html
<div class="d-md-none">                    <!-- 1-up carousel (mobile) -->
<div class="d-none d-md-block d-lg-none">  <!-- 2-up carousel (tablet) -->
<div class="d-none d-md-none d-lg-block">  <!-- 3-up carousel (desktop) -->
```

Each carousel has its own `id` so the prev/next controls target the correct instance per viewport.

---

### 3. CSS Grid for Section Layouts

While Bootstrap handles the macro layout, CSS Grid handles the inner layouts of complex sections — giving precise control that Bootstrap's 12-column system can't offer cleanly.

```css
/* "More Than Games" bento-style grid */
.items {
  display: grid;
  grid-template-columns: repeat(2, 1fr);
  grid-auto-rows: 1fr;
  gap: 1rem;
}
@media (min-width: 992px) {
  .items {
    grid-template-columns: repeat(4, minmax(0, 290px));
  }
}
```

---

### 4. CSS Custom Properties Design System

A full token layer in `:root` drives the entire visual identity — brand color, dark backgrounds, typography scale, and transition curves. This means the "lime green" accent (`#cbfe1c`) only lives in one place.

```css
:root {
  --color-main: #cbfe1c;
  --color-dark: #0b0e13;
  --font-Days-One: 'Days One', sans-serif;
  --font-Chakra-Petch: 'Chakra Petch', sans-serif;
  --default-transition-duration: 0.15s;
  --default-transition-timing-function: cubic-bezier(0.4, 0, 0.2, 1);
}
```

---

### 5. Button Shimmer Effect — Pure CSS

Every CTA button has a light shimmer that sweeps across on hover, built with a `::after` pseudo-element and a CSS transition — no JavaScript, no libraries.

```css
.btn::after {
  content: '';
  position: absolute;
  left: -100%;
  background-image: linear-gradient(90deg, transparent, rgba(255,255,255,0.4), transparent);
  transition: left 0.6s;
}
.btn:hover::after {
  left: 100%;
}
```

---

### 6. Team Cards — `backdrop-filter` Grayscale Reveal (Bonus)

The "Our Team" section uses `backdrop-filter: grayscale(100%)` as an overlay that slides away on hover, revealing the full-color photo underneath — the Bonus feature of this assignment.

```css
figure::before {
  content: '';
  position: absolute;
  inset: 0;
  backdrop-filter: grayscale(100%) brightness(0.9);
  transition: transform 0.8s cubic-bezier(0.4, 0, 0.2, 1);
}
figure:hover::before {
  transform: translateY(-100%);
}
```

---

### 7. Infinite Scroll Animation — CSS Keyframes

The brand logos section has two rows scrolling in opposite directions using a single `@keyframes` animation — reversed on the second row via `animation-direction: reverse`.

```css
@keyframes scroll-animate {
  0%   { transform: translateX(-60%); }
  100% { transform: translateX(0); }
}
.animate-1 { animation: scroll-animate 20s linear infinite; }
.animate-2 { animation: scroll-animate 20s linear infinite reverse; }
```

The logos are duplicated in HTML to create a seamless loop.

---

### 8. Parallax Hero Background

The hero section uses `background-attachment: fixed` for a subtle parallax effect — the background image stays in place as the user scrolls, creating depth without JavaScript.

```css
#hero {
  background-image: linear-gradient(rgba(0,0,0,0.88) 0% 100%), url(../images/hero-bg.webp);
  background-attachment: fixed;
  background-size: cover;
}
```

---

### 9. Scroll Spy Navigation

Bootstrap's built-in ScrollSpy is wired to the navbar, automatically highlighting the active nav link as the user scrolls through sections.

```html
<body data-bs-spy="scroll" data-bs-target="#navbar-game-arena">
```

---

### 10. Interactive Contact Form

The contact section features a fully styled form (inputs, select, textarea, checkbox) with custom focus states that replace Bootstrap's default ring with a 4-sided highlight using the brand color.

```css
input:focus, select:focus, textarea:focus {
  box-shadow:
    0 2px 0 var(--color-main),
    2px 0 0 var(--color-main),
    0 -2px 0 var(--color-main),
    -2px 0 0 var(--color-main);
}
```

---

## 🧩 Sections

| Section | Description |
|---|---|
| **Navbar** | Fixed responsive navbar with ScrollSpy, collapse on mobile, Sign In CTA |
| **Hero** | Full-viewport parallax header with CTA buttons and stats badge |
| **Latest Games** | Responsive carousel — 1/2/3 cards per viewport breakpoint |
| **More Than We Do** | Bento-grid service cards with corner accent hover effects |
| **Brand Logos** | Infinite auto-scrolling logo marquee, two rows in opposite directions |
| **Team Members** | Photo grid with `backdrop-filter` grayscale reveal on hover |
| **Get In Touch** | Contact info + fully styled form with custom focus states |
| **Footer** | 4-column grid with social links, nav lists, legal links |

---

## 🛠️ Built With

- **HTML5** — Semantic markup, accessibility attributes
- **CSS3** — Custom Properties · Grid · Keyframe Animations · `backdrop-filter` · Transitions
- **Bootstrap 5** — Grid · Carousel · Navbar · ScrollSpy · Collapse · Utility classes
- **Font Awesome 6** — Icon library
- **Days One + Chakra Petch** — Google Fonts pairing

---

## 🚀 Getting Started

```bash
git clone https://github.com/mohammed-kandeel/06-Games-Arena.git
cd 06-Games-Arena
# Open index.html in your browser
```

Or visit the [Live Demo](https://mohammed-kandeel.github.io/06-Games-Arena/) directly.

---

<div align="center">
  Built with ❤️ by <strong>Mohammed Kandeel</strong>
</div>
