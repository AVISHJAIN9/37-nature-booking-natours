# Architectural Decision Records (ADRs)

| ADR ID | Decision Title | Chosen Option | Alternatives Considered | Deciding Factors | Trade-Off Accepted | Revisit Trigger |
|---|---|---|---|---|---|---|
| **ADR-01** | SASS Architecture | 7-1 Pattern | Flat SASS, Single CSS, CSS Modules | Strict component isolation, BEM nesting, centralized tokens | Requires compilation step | Codebase migrates to Web Components |
| **ADR-02** | Menu Interaction Engine | CSS Checkbox Hack | Vanilla JS Event Listener, React State | Zero JS runtime overhead, instant responsiveness | Non-semantic input usage | Complex state requirements (search/cart) |
| **ADR-03** | Modal Dialog System | URL Hash `:target` | JS Dialog Modal, Bootstrap Modal | Native browser history integration (Back button closes modal) | URL fragment pollution | Form submission requires multi-step wizard |
| **ADR-04** | 3D Tour Card Interactions | CSS 3D Transforms | Three.js Canvas, JS Hover Listeners | Hardware-accelerated GPU 60 FPS performance | Requires mobile media query fallback | Interactive 3D terrain rendering required |
| **ADR-05** | Responsive Grid System | Mathematical Float Grid with `calc()` | CSS Flexbox, CSS Grid | Deep demonstration of layout mechanics & clearfixes | More verbose markup than CSS Grid | Standardizing on modern grid layouts |
