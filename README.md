# GSAP Scroll Horizontal — Before & After Effect

> A scroll-driven image reveal animation built with **GSAP** and **ScrollTrigger**.  
> Smooth, performant, and zero dependencies beyond the GSAP CDN.

<!-- Replace with an actual GIF/screenshot of the animation -->
<!-- ![Demo](./IMG/demo.gif) -->

## 🔗 Live Demo

👉 [View on GitHub Pages](https://olaigv.github.io/GSAP-ScrollHorizontal/)

---

## What it does

As the user scrolls down, a "before" image is progressively revealed by a sliding "after" image — creating a cinematic before/after comparison effect. The section is **pinned** while the animation plays, then scroll resumes normally.

---

## Tech stack

| Technology | Purpose |
|---|---|
| HTML5 / CSS3 | Structure and layout |
| [GSAP 3](https://gsap.com/) | Animation engine |
| [ScrollTrigger](https://gsap.com/docs/v3/Plugins/ScrollTrigger/) | Scroll-linked animation + pinning |
| Google Fonts | Typography (`Luckiest Guy`) |

---

## Key GSAP concepts demonstrated

- **`ScrollTrigger`** — pinning a section and scrubbing animation to scroll position
- **`gsap.timeline()`** — chaining two coordinated tweens (container slide + counter-slide image)
- **`xPercent`** — percentage-based transforms for fluid, resolution-independent animations
- **`scrub: true`** — real-time playback tied to the scrollbar, not a one-shot trigger
- **`anticipatePin`** — eliminates the visual jump when a section becomes pinned

---

## How it works

```js
gsap.utils.toArray(".comparisonSection").forEach((section) => {
  let tl = gsap.timeline({
    scrollTrigger: {
      trigger: section,
      start: "50% center",
      end: () => "+=" + section.offsetWidth,
      scrub: true,
      pin: true,
      anticipatePin: 1,
    },
  });

  // Slide the after-image container in from the right
  tl.fromTo(section.querySelector(".afterImage"), { xPercent: 100 }, { xPercent: 0 })
  // Counter-translate the image so it appears to stay in place
    .fromTo(section.querySelector(".afterImage img"), { xPercent: -100 }, { xPercent: 0 }, 0);
});
```

The trick is the **counter-translation**: the outer container slides right→left while the inner `<img>` slides left→right at the same rate, so the image appears to be revealed rather than pushed in.

---

## Getting started

No build tools required. Just open `index.html` in a browser.

```bash
git clone https://github.com/OlaiGV/GSAP-ScrollHorizontal.git
cd GSAP-ScrollHorizontal
# Open index.html in your browser
```

> **Note:** Add your own images to `./IMG/` named `imagen1.jpg` (before) and `imagen2.jpg` (after).

---

## Project structure

```
GSAP-ScrollHorizontal/
├── index.html
├── CSS/
│   ├── reset.css       # Meyer reset
│   └── styles.css      # Layout + animation styles
├── IMG/
│   ├── imagen1.jpg     # "Before" image
│   └── imagen2.jpg     # "After" image
└── JS/
    └── script.js       # GSAP + ScrollTrigger logic
```

---

## Author

**Olai García** — [GitHub](https://github.com/OlaiGV)
