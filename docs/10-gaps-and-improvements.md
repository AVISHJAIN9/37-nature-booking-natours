# Gaps, Hardening & Technical Debt

## Prioritized Improvement Roadmap

| Priority | Area | Current Implementation | Production Hardening Recommendation |
|---|---|---|---|
| **P1** | Modern Layout Engine | Float-based responsive grid using `calc()` | Migrate grid to native **CSS Grid** (`display: grid; grid-template-columns: repeat(auto-fit, minmax(30rem, 1fr)); gap: 6rem;`). |
| **P2** | Accessibility (a11y) | Checkbox hack navigation | Add ARIA attributes (`aria-expanded`, `aria-controls`) and focus trap management. |
| **P3** | Dialog Element | Pure CSS `:target` popup | Upgrade to native HTML5 `<dialog>` element with `showModal()` for accessible screen-reader focus handling. |
| **P4** | Next-Gen Images | JPG photographic assets in `img/` | Convert all images to **WebP / AVIF** with fallback `<picture>` elements for 60% bandwidth reduction. |
| **P5** | Asset Bundler | npm script chaining (`concat`, `sass`, `postcss`) | Migrate to **Vite** or **Lightning CSS** for sub-millisecond compilation and automated tree-shaking. |
