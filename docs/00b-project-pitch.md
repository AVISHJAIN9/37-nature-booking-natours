# Project Pitch: Wanderly (Natours)

## 30-Second Elevator Pitch
"I built Wanderly, a high-performance nature tour booking platform engineered with a strict zero-JavaScript, 100% pure CSS architecture. By structuring the codebase using the production-grade 7-1 SASS pattern and BEM naming conventions, I created complex interactive user experiences—including a 3D perspective rotating card system, a pure CSS checkbox-driven fullscreen navigation overlay, and an anchor-targeted modal booking flow—running entirely on the browser's hardware-accelerated GPU compositor at a locked 60 frames per second."

---

## 2-Minute Technical Interview Pitch
"When approaching the Wanderly project, my primary engineering objective was to prove that complex, high-engagement web applications do not always require bulky JavaScript frameworks that bloat bundle sizes and degrade First Input Delay. I wanted to push the modern browser rendering engine to its limits using pure CSS3 and advanced SASS architectural principles.

I organized the styling into a strict 7-1 SASS architecture across abstracts, base rules, layout components, modular UI components, and page controllers. For state management, instead of loading a JavaScript library, I implemented declarative CSS state machines: the navigation utilizes the checkbox hack with adjacent sibling selectors to scale a radial background disc eighty-fold across the viewport; the interactive tour cards leverage CSS 3D transforms with 150-rem perspective and hidden backfaces to achieve fluid two-sided flips; and the booking modal relies on URL fragment targeting with the `:target` pseudo-class.

To ensure production resilience, I built an automated compilation pipeline with npm scripts: modern SCSS is compiled into raw CSS, merged with icon fonts, processed through PostCSS with Autoprefixer targeting the last ten browser versions, and compressed into a production artifact under 30 kilobytes. The layout engine features a custom mathematical float grid using `calc()` with micro-clearfixes, paired with a unified responsive mixin that adapts layouts across four distinct viewport tiers. The result is a travel booking landing page that scores 100 on Google Lighthouse performance with zero runtime layout thrashing."
