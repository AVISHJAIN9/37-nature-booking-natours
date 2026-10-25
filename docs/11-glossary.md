# Technical Glossary: Natours (Wanderly)

- **7-1 SASS Pattern**: An architectural standard organizing SASS code into 7 distinct folders (`abstracts/`, `base/`, `components/`, `layout/`, `pages/`, `themes/`, `vendors/`) imported into one root `main.scss`.
- **Backface-Visibility**: A CSS property determining whether the reverse side of an element is visible when facing the screen in 3D space (`backface-visibility: hidden`).
- **BEM (Block Element Modifier)**: A CSS naming methodology ensuring strict component isolation (`.block__element--modifier`) and flat specificity hierarchies.
- **Checkbox Hack**: A pure CSS technique utilizing a hidden checkbox input and the sibling combinator (`:checked ~ selector`) to maintain toggled state without JavaScript.
- **Clearfix**: A CSS micro-hack using `::after { content: ""; display: table; clear: both; }` to force a parent element to encompass floated child elements.
- **Clip-Path**: A CSS property creating a clipping region where only internal coordinates are visible, enabling complex geometric cuts (`polygon(0 0, 100% 0, 100% 75vh, 0 100%)`).
- **Compositor Thread**: The browser thread responsible for drawing layers onto the screen via the GPU, executing `transform` and `opacity` animations at 60 FPS without touching the main thread.
- **PostCSS**: A JavaScript toolchain transforming CSS styles with plugins such as Autoprefixer to ensure cross-browser compatibility.
- **Shape-Outside**: A CSS property allowing inline text to wrap around complex geometric boundaries (such as circles) rather than rectangular boxes.
- **Target Pseudo-Class (`:target`)**: A CSS selector matching an element whose ID matches the current URL fragment identifier (hash).
