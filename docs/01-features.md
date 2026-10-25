# Master Feature Inventory: Natours (Wanderly)

## Subsystem Matrix

| Feature ID | Feature Name | Core Source Files | Primary Architectural Mechanism |
|---|---|---|---|
| **F1** | Slanted Hero & Keyframe CTA | `sass/layout/_header.scss`, `sass/base/_animations.scss`, `sass/components/_button.scss` | CSS `clip-path: polygon()`, `@keyframes moveInLeft/Right/Bottom`, GPU hardware acceleration. |
| **F2** | Pure CSS Navigation Hack | `sass/layout/_navigation.scss` | Checkbox hack (`input:checked ~ .navigation__background`), radial gradient scale(80). |
| **F3** | 3D Rotating Tour Cards | `sass/components/_card.scss` | `perspective: 150rem`, `rotateY(180deg)`, `backface-visibility: hidden`. |
| **F4** | Pure CSS Modal Booking Popup | `sass/components/_popup.scss` | CSS `:target` pseudo-class, URL hash activation, backdrop filter blur. |
| **F5** | Mathematical Float Grid | `sass/layout/_grid.scss`, `sass/abstracts/_mixins.scss` | Dynamic `calc()` formulas, micro-clearfix, responsive breakpoint collapsing. |
| **F6** | Skewed Testimonial Stories | `sass/components/_story.scss` | Inverse `skewX(-12deg)` container with `shape-outside: circle()` image wrap. |
| **F7** | Fullscreen Ambient Background Video | `sass/components/_bg-video.scss` | HTML5 `<video>` tag with `object-fit: cover` and low-opacity overlay. |
| **F8** | Floating Label Booking Form | `sass/components/_form.scss` | `:placeholder-shown` pseudo-class sibling selector, custom animated radio buttons. |

---

## Detailed Feature Specifications

### F1: Slanted Hero & Keyframe CTA
- **Description**: Visual entry point featuring an angled polygonal bottom edge (`clip-path: polygon(0 0, 100% 0, 100% 75vh, 0 100%)`) and typography entrance animations.
- **Functions & Mixins**: `@mixin respond(phone)` in `_mixins.scss:L39` adapts polygon angle on mobile devices to prevent excessive content cropping.
- **Edge Cases**: Older browsers lacking `clip-path` support display standard rectangular box via graceful degradation.
- **Say It Out Loud**:
> "I built the hero section in `_header.scss` to deliver an immediate premium visual impact without any external animation libraries. I used CSS `clip-path: polygon()` to cut the bottom edge of the hero into a dynamic 75-vh angled slope. For the typography, I wrote custom CSS `@keyframes` in `_animations.scss` that animate both horizontal translation and opacity, timed with a cubic-bezier easing curve. The CTA button includes an animated pseudo-element ripple that expands and fades on hover. Because everything is handled by CSS transforms and opacity, the animation runs exclusively on the GPU compositor thread with zero layout reflows."

---

### F2: Pure CSS Navigation Hack
- **Description**: Fullscreen mobile-friendly navigation overlay triggered completely by native HTML checkbox state without a single line of JavaScript.
- **Trace**: Checkbox `<input type="checkbox" id="navi-toggle">` followed by `<label for="navi-toggle">` and `<div class="navigation__background">`.
- **Say It Out Loud**:
> "To achieve an interactive fullscreen menu without JavaScript, I implemented the CSS checkbox hack in `_navigation.scss`. An invisible native checkbox is bound to an accessible circular button label. When the user clicks the hamburger icon, the checkbox toggles to `:checked`, which triggers the adjacent sibling combinator to scale an underlying green radial gradient circle from 6rem to eighty times its size. This instantly floods the viewport with color while the navigation links fade into view with cubic-bezier timing. If a user clicks outside or on a link, the checkbox state resets, collapsing the overlay smoothly back into the circular icon."

---

### F3: 3D Rotating Tour Cards
- **Description**: Three-dimensional interactive cards showcasing nature tour packages. Hovering rotates the card 180 degrees along the Y-axis to reveal pricing and booking details.
- **Trace**: `sass/components/_card.scss`.
- **Say It Out Loud**:
> "In `_card.scss`, I engineered the 3D rotating tour cards using native CSS 3D transforms. The parent container sets a `perspective: 150rem` to establish realistic visual depth. Inside, I created two mirrored card sides—front and back—positioned absolutely on top of each other with `backface-visibility: hidden`. When hovered, the front face rotates from 0 to negative 180 degrees, while the back face rotates from positive 180 degrees to 0. For mobile touchscreens where hover states don't exist, I added a media query for `hover: none` that automatically flattens the card into a single vertical card layout with the price immediately visible."

---

### F4: Pure CSS Modal Booking Popup
- **Description**: Fullscreen booking modal dialog triggered when a user clicks any "Book now!" button.
- **Trace**: `sass/components/_popup.scss`. Anchor links set window hash `#popup`.
- **Say It Out Loud**:
> "For the booking modal in `_popup.scss`, I eliminated the need for modal management JavaScript by utilizing the native CSS `:target` pseudo-class. When an explorer clicks 'Book now', the URL hash updates to `#popup`. The CSS selector `.popup:target` immediately activates, transitioning the backdrop from opacity zero to one and scaling the modal dialog box from 0.25 to full scale with a smooth bounce. Clicking the close button or anywhere outside the modal routes the anchor back to the tours section, immediately dismissing the target state and hiding the modal."
