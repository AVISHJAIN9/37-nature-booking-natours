# Full Project Analysis: Natours (Wanderly)

## 0.1 What the Project Is

**Wanderly (Natours)** is an outdoor tour booking and expedition platform designed to showcase curated nature adventures (Forest Hiker, Ocean Explorer, Snow Adventurer). The application solves the problem of high-friction, slow-loading travel booking pages by implementing a zero-runtime-overhead, 100% pure CSS-driven user experience.

### Main User Journey

```mermaid
journey
    title Outdoor Explorer Booking Experience
    section Discovery
      Land on Hero Section: 5: Explorer
      Trigger Navigation Menu: 4: Explorer
      Smooth scroll to Top Tours: 5: Explorer
    section Evaluation
      Hover Tour Card for 3D Flip: 5: Explorer
      Inspect Pricing & Itinerary: 4: Explorer
      Click Book Now: 5: Explorer
    section Action
      Pure CSS Modal Popup opens: 5: Explorer
      Review Terms & Fill Booking: 4: Explorer
      Select Tour Group Radio: 4: Explorer
```

---

## 0.2 Master Feature Inventory & Traces

### System Overview Diagram

```mermaid
flowchart TD
    User([User Browser]) --> HTML[01_Natours/index.html]
    HTML --> CSS[01_Natours/css/style.css]
    subgraph BuildPipeline[SASS Build & PostCSS Pipeline]
        SassMain[sass/main.scss] --> SassComp[css/style.comp.css]
        SassComp --> Concat[css/style.concat.css]
        Concat --> PostCSS[PostCSS + Autoprefixer]
        PostCSS --> Minify[SASS Compressed Output]
        Minify --> CSS
    end
    HTML --> Nav[F2: Checkbox Navigation]
    HTML --> Hero[F1: Animated Hero & CTA]
    HTML --> Cards[F3: 3D Rotating Cards]
    HTML --> Popup[F4: Pure CSS Modal Popup]
    HTML --> Grid[F5: Float Grid System]
    HTML --> Stories[F6: Skewed Story Cards]
    HTML --> Video[F7: Ambient Background Video]
    HTML --> Form[F8: Floating Label Booking Form]
```

### F1: Hero Header & Animated Call-to-Action (CTA)
- **User Action**: Explorer loads landing page; hero text slides in smoothly from left and right; animated pill button appears from bottom and pulses on hover.
- **Trace**: `01_Natours/index.html` lines 14-29 (`.header`, `.heading-primary`, `.btn--animated`) -> `sass/layout/_header.scss` -> `sass/base/_animations.scss` (`@keyframes moveInLeft`, `@keyframes moveInRight`, `@keyframes moveInBottom`) -> `sass/components/_button.scss`.
- **CSS Engine**: Hardware-accelerated GPU transitions via `transform: translateX()` and `opacity`. Pseudo-element ripple via `::after` with `transition: all .4s`.

```mermaid
sequenceDiagram
    autonumber
    actor User as Site Visitor
    participant Browser as Rendering Engine (Blink/WebKit)
    participant Header as .header (_header.scss)
    participant Keyframes as @keyframes (_animations.scss)
    participant Button as .btn--animated (_button.scss)

    User->>Browser: Enters URL / Hits Refresh
    Browser->>Header: Evaluates background clip-path polygon
    Browser->>Keyframes: Triggers moveInLeft (0% -> 80% -> 100%)
    Browser->>Keyframes: Triggers moveInRight (0% -> 80% -> 100%)
    Browser->>Button: Delays moveInBottom by 0.75s with backwards fill-mode
    User->>Button: Hovers cursor over CTA
    Button-->>Browser: Spawns ::after pseudo-element scale(1.4) + opacity(0)
```

### F2: Pure CSS Fullscreen Navigation (Checkbox Hack)
- **User Action**: User clicks circular hamburger icon; background disc expands radial green gradient across viewport; nav links emerge smoothly.
- **Trace**: `01_Natours/sass/layout/_navigation.scss` lines 1-215. Leverages `<input type="checkbox" id="navi-toggle" class="navigation__checkbox">`.
- **CSS Engine**: Sibling selector `.navigation__checkbox:checked ~ .navigation__background` scales `transform: scale(80)`.
- **Failure State**: If HTML structure changes and `<label>` is separated from `<input>`, the hack fails. Fallback: Standard button with ARIA attributes.

```mermaid
stateDiagram-v2
    [*] --> Closed: Initial Page Load
    Closed --> Expanding: User Clicks Hamburger Label
    note right of Expanding: Checkbox:checked activates ~ .navigation__background transform scale(80)
    Expanding --> Open: Radial gradient covers 100vw/100vh
    Open --> Collapsing: User Clicks Nav Link or Label
    Collapsing --> Closed: Scale returns to 0, opacity 0, width 0
```

### F3: Interactive 3D Perspective Rotating Tour Cards
- **User Action**: User hovers over tour package card; card smoothly rotates 180 degrees in 3D space, revealing back side with price, duration, and booking CTA.
- **Trace**: `01_Natours/sass/components/_card.scss` lines 1-236.
- **CSS Engine**: Parent `.card` defines `perspective: 150rem`. Child `.card__side--front` rotates to `-180deg`, while `.card__side--back` rotates from `180deg` to `0deg`. Uses `backface-visibility: hidden`.
- **Failure Path**: On touch devices, `:hover` does not naturally persist. Handled via `@media only screen and (hover: none)` which collapses the card into a single continuous vertical block.

```mermaid
sequenceDiagram
    autonumber
    actor User as Explorer
    participant Front as .card__side--front
    participant Back as .card__side--back
    participant Compositor as GPU Compositor Layer

    User->>Front: Mouse enters .card container
    Front->>Compositor: transform: rotateY(-180deg) (cubic-bezier)
    Back->>Compositor: transform: rotateY(0deg) (cubic-bezier)
    Compositor-->>User: Backface hidden prevents mirroring; price details rendered
    User->>Front: Mouse leaves .card container
    Front->>Compositor: transform: rotateY(0deg)
    Back->>Compositor: transform: rotateY(180deg)
```

### F4: Pure CSS Modal Booking Popup (`:target` pseudo-class)
- **User Action**: Clicking "Book now!" with href `#popup` opens a full-screen blurred backdrop modal window with two-column content and terms.
- **Trace**: `01_Natours/sass/components/_popup.scss` lines 1-147.
- **CSS Engine**: URL hash updates to `#popup`. Selector `.popup:target` triggers `opacity: 1; visibility: visible;`. Modal content scales from `scale(.25)` to `scale(1)`. Close button points to anchor `#section-tours` or `#`, resetting target.

```mermaid
flowchart TD
    ClickCTA[Click 'Book Now' href='#popup'] --> URLChange[Browser URL Hash becomes #popup]
    URLChange --> CSSTarget{Is .popup :target?}
    CSSTarget -->|Yes| ModalVisible[Set opacity: 1, visibility: visible]
    ModalVisible --> InnerScale[Scale .popup__content from 0.25 to 1.0 with 0.5s ease]
    InnerScale --> UserCloses[Click 'X' href='#section-tours']
    UserCloses --> HashCleared[Hash cleared from URL]
    HashCleared --> CSSTarget
    CSSTarget -->|No| ModalHidden[Set opacity: 0, visibility: hidden, scale 0.25]
```

### F5: Custom Responsive Float Grid System
- **User Action**: Page smoothly renders 2, 3, and 4-column balanced layouts across mobile, tablet, and desktop screens.
- **Trace**: `01_Natours/sass/layout/_grid.scss` lines 1-110. Uses mathematical SASS variables `$grid-width`, `$gutter-horizontal`, `$gutter-vertical`.
- **CSS Engine**: Dynamic calculation via `calc((100% - #{$gutter-horizontal}) / 2)` and clearfix mixin `@include clearfix`. In tablet portrait (`$breakpoint == tab-port`), columns collapse to `width: 100% !important`.

```mermaid
flowchart LR
    Row[Container .row max-width: 114rem] --> Col1["col-1-of-2 (calc(100% - 6rem) / 2)"]
    Row --> Col2["col-1-of-2 (calc(100% - 6rem) / 2)"]
    Col1 --> Clearfix[Micro-clearfix ::after pseudo-element]
    Col2 --> Clearfix
    Clearfix --> ViewportCheck{Viewport < 900px?}
    ViewportCheck -->|Yes| FullWidth[width: 100% !important; margin-right: 0]
    ViewportCheck -->|No| FloatedLayout[float: left; margin-right: 6rem]
```

### F6: Skewed Story Cards with Circular Shape-Outside Avatar
- **User Action**: User scrolls to customer review stories; testimonial card is skewed by `-12deg`, but the inner text and circular image un-skew by `12deg` for perfect legibility, with text wrapping around a circular photo.
- **Trace**: `01_Natours/sass/components/_story.scss` lines 1-104.
- **CSS Engine**: `transform: skewX(-12deg)` on `.story`, `transform: skewX(12deg)` on `.story__shape`. Shape wrapping via `shape-outside: circle(50% at 50% 50%)` and `clip-path: circle(50% at 50% 50%)`.

### F7: Ambient Background Video
- **User Action**: Behind the customer stories, a muted scenic nature video loops continuously with low opacity to preserve text contrast.
- **Trace**: `01_Natours/sass/components/_bg-video.scss` lines 1-17.
- **CSS Engine**: Absolute positioning covering 100% width and height, `object-fit: cover`, `opacity: .15`, `z-index: -1`, with `overflow: hidden`.

### F8: Booking Form with Floating Label Transitions & Custom Radio Buttons
- **User Action**: User fills out reservation form; input placeholder smoothly disappears while a small label slides up; custom radio buttons display animated green inner dot.
- **Trace**: `01_Natours/sass/components/_form.scss` lines 1-124.
- **CSS Engine**: Sibling selector `:placeholder-shown + .form__label` applies `opacity: 0; visibility: hidden; transform: translateY(-4rem);`. When text is typed, placeholder is no longer shown, triggering smooth transition into view.

---

## 0.3 Final Inventory Counts

| Architectural Metric | Count | Code Verification Reference |
|---|---|---|
| **Total HTML Pages** | 1 | `01_Natours/index.html` |
| **SASS Source Files** | 21 | `01_Natours/sass/**/*.scss` |
| **SASS Architecture Pattern** | 7-1 | `abstracts/`, `base/`, `components/`, `layout/`, `pages/`, `main.scss` |
| **CSS Keyframe Animations** | 3 | `moveInLeft`, `moveInRight`, `moveInBottom` in `_animations.scss` |
| **Pure CSS State Machines** | 3 | Checkbox Hack (Nav), `:target` (Popup), `:hover` 3D (Cards) |
| **Responsive Breakpoints** | 4 | `phone` (600px), `tab-port` (900px), `tab-land` (1200px), `big-desktop` (1800px) |
| **Build & Toolchain Scripts** | 6 | `watch-sass`, `compile-sass`, `concat-css`, `prefix-css`, `compress-css`, `build-css` |
| **Dependencies / DevDependencies** | 5 | `sass`, `autoprefixer`, `concat`, `postcss-cli`, `npm-run-all` |
