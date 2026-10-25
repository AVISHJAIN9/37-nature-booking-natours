# Codebase Anatomy & Project Map

## Directory Tree

```
43-nature-booking-natours/
├── 01_Natours/
│   ├── index.html                   # Master semantic HTML5 markup
│   ├── package.json                 # Build pipeline dependencies and npm scripts
│   ├── package-lock.json            # Deterministic dependency lockfile
│   ├── README.md                    # Project overview & quickstart instructions
│   ├── css/
│   │   ├── style.css                # Final compressed production CSS bundle
│   │   ├── style.comp.css           # Raw uncompressed compiled SCSS
│   │   ├── style.concat.css         # Merged stylesheet with icon fonts
│   │   ├── style.prefix.css         # Vendor-prefixed stylesheet (Autoprefixer)
│   │   ├── icon-font.css            # Linea icon font definitions
│   │   └── fonts/                   # Linea icon font binary files (eot, ttf, woff, svg)
│   ├── img/                         # Optimized photographic assets & SVGs
│   │   ├── hero.jpg                 # Desktop hero background
│   │   ├── hero-small.jpg           # Responsive mobile hero background
│   │   ├── nat-1.jpg to nat-10.jpg  # Tour gallery and card images
│   │   ├── logo-wanderly-white.svg  # White vector branding logo
│   │   └── logo-wanderly-color.svg  # Multi-color vector branding logo
│   └── sass/                        # 7-1 SASS Architecture Root
│       ├── main.scss                # Primary SCSS orchestrator / entry manifest
│       ├── abstracts/               # Global variables, mixins, and functions
│       │   ├── _variables.scss      # Colors, typography scales, grid gutters
│       │   ├── _mixins.scss         # Responsive breakpoint & clearfix mixins
│       │   └── _functions.scss      # Utility calculations
│       ├── base/                    # Foundational reset, base styles, and animations
│       │   ├── _base.scss           # Box-sizing reset, html font-size root definition
│       │   ├── _typography.scss     # Font family, heading hierarchies, letter spacing
│       │   ├── _animations.scss     # Keyframe definitions (moveInLeft, moveInRight, moveInBottom)
│       │   └── _utilities.scss      # Atomic utility helper classes (u-center-text, etc.)
│       ├── components/              # Modular, reusable UI components
│       │   ├── _button.scss         # Animated CTA button & ripple effects
│       │   ├── _card.scss           # 3D perspective rotating tour cards
│       │   ├── _popup.scss          # Pure CSS modal popup via :target
│       │   ├── _composition.scss    # Overlapping image gallery with hover lift
│       │   ├── _feature-box.scss    # Feature highlight box with perspective hover
│       │   ├── _form.scss           # Floating labels and custom radio buttons
│       │   ├── _story.scss          # Skewed testimonial cards with circular avatars
│       │   └── _bg-video.scss       # Fullscreen ambient video container
│       ├── layout/                  # Structural page layout components
│       │   ├── _header.scss         # Slanted hero container with clip-path
│       │   ├── _navigation.scss     # Checkbox-hack fullscreen menu overlay
│       │   ├── _grid.scss           # Mathematical float-based responsive grid
│       │   └── _footer.scss         # Multi-column footer with logo and navigation
│       └── pages/                   # Page-specific styling rules
│           └── _home.scss           # Section padding and background transitions
└── docs/                            # Interview-Ready Documentation Portal
```

---

## Dependency & Toolchain Directory

| Package Name | Exact Version | Type | Architectural Purpose in Wanderly |
|---|---|---|---|
| `sass` | `^1.53.0` | `devDependency` | Dart Sass compiler converting modular SCSS syntax into native CSS. |
| `concat` | `^1.0.3` | `devDependency` | Command-line utility concatenating `icon-font.css` and compiled SCSS into a single bundle. |
| `autoprefixer` | `^10.4.7` | `devDependency` | PostCSS plugin parsing CSS and appending vendor prefixes (`-webkit-`, `-moz-`) via Can I Use. |
| `postcss-cli` | `^10.0.0` | `devDependency` | CLI runner executing PostCSS transformations in the npm build pipeline. |
| `npm-run-all` | `^4.1.5` | `devDependency` | Orchestration utility running build tasks sequentially (`npm-run-all compile-sass concat-css prefix-css compress-css`). |

---

## Environment Variables & Keys
- **Status**: **No environment variables required**.
- **Reason**: The project is a client-side static presentation platform with zero external third-party API dependencies or cloud secret requirements.
