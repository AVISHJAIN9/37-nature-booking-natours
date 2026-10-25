# Technology Choice Comparisons & Trade-Off Analysis

## 1. CSS Architecture: 7-1 SASS vs Alternatives

| Comparison Metric | Chosen: 7-1 SASS Pattern | CSS Modules | Tailwind CSS | Styled Components (CSS-in-JS) | Vanilla CSS |
|---|---|---|---|---|---|
| **File Organization** | 7 dedicated folders (abstracts, base, components, layout, pages, themes, vendors) | 1 file per component (`Button.module.css`) | Utility classes in markup (`p-4 text-center`) | Scoped template literals inside JS files | Single monolithic or split files |
| **Runtime Overhead** | **0 ms (Zero runtime)** | 0 ms (Zero runtime) | 0 ms (Zero runtime) | High (JS parsing, CSS injection, memory footprint) | **0 ms** |
| **BEM Compliance** | Native & seamless (`&__element--modifier`) | Scoped classes; BEM redundant | Anti-BEM; atomic utilities | Component-centric; BEM redundant | Manual string maintenance |
| **Global Design Tokens** | First-class SCSS variables & maps | Requires CSS variables (`var(--color)`) | Config file (`tailwind.config.js`) | JS ThemeProvider context | CSS custom properties |
| **Fit with Wanderly** | **Optimal** (Demonstrates master-level CSS engineering) | Overkill (No JS framework) | Avoided (Encapsulates CSS fundamentals) | Inapplicable (No React/Vue runtime) | Lacks nesting & mixin modularity |

- **Why I Used 7-1 SASS**: The 7-1 pattern enforces strict separation of concerns between global configurations (`abstracts/`), base resets (`base/`), and reusable UI building blocks (`components/`), while SCSS nesting enables clean BEM notation without repetitive class typing.
- **Why I Did NOT Use Alternatives**:
  - *Tailwind CSS*: Bypasses core CSS cascade and specificity fundamentals that an advanced CSS showcase is intended to prove.
  - *Styled Components*: Requires a heavyweight JavaScript runtime (React) to output basic styles, adding unnecessary bundle weight.
  - *Vanilla CSS*: Lacks mathematical mixins, functions, and automated vendor prefixing pipelines.
- **30-Second Interview Answer**: "I chose the 7-1 SASS architecture because it provides an enterprise-grade file structure that cleanly decouples global design tokens and responsive mixins from modular BEM components, generating a lean, zero-runtime production stylesheet."

---

## 2. Layout Engine: Float Grid vs Flexbox vs CSS Grid

| Comparison Metric | Chosen: Float Grid with `calc()` | CSS Flexbox (`display: flex`) | CSS Grid (`display: grid`) |
|---|---|---|---|
| **Dimensional Model** | 1-Dimensional horizontal columns with clearing | 1-Dimensional flex container (row or column) | 2-Dimensional grid (rows and columns simultaneously) |
| **Browser Compatibility** | **100% (Backwards compatible to IE8)** | High (IE11 partial) | Modern browsers (IE lacks modern syntax) |
| **Gutter Management** | Manual `margin-right` subtraction via `calc()` | `gap` property (modern) or margin hacks | Native `grid-gap` / `gap` |
| **Clearance Requirements** | Mandatory Micro-Clearfix (`::after` pseudo) | Self-clearing | Self-clearing |
| **Pedagogical Rigor** | **Maximum** (Demonstrates deep layout mechanics) | Moderate | Moderate |

- **Why Float Grid Was Used**: To demonstrate deep understanding of the CSS box model, browser flow, micro-clearfixes, and mathematical `calc()` dynamic sizing formulas.
- **When I Would Switch**: For modern commercial production applications, I would migrate to CSS Grid for page layouts and Flexbox for component-level alignment due to native `gap` support and elimination of clearfix hacks.
