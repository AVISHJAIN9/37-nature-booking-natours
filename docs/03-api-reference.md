# API Reference: Natours (Wanderly)

## Backend Endpoints Matrix
- **Status**: **Not applicable for this project type (Frontend Only / CSS Architecture)**.
- **Reason**: Wanderly is a pure client-side static presentation platform. All state transitions (menu toggle, card flip, modal popup, form labels) are executed natively within the browser rendering engine via CSS pseudo-classes and selectors.

---

## Client-Side Document & DOM Interaction Reference

| Trigger Element | Selector / Identifier | Activated CSS State / Pseudo-Class | Visual Result |
|---|---|---|---|
| Hamburger Checkbox | `#navi-toggle` | `:checked ~ .navigation__background` | Expands radial green background disc by `scale(80)`. |
| Navigation Link | `.navigation__link` | `href="#section-..."` | Performs native browser smooth scroll to target anchor section. |
| Tour Card Container | `.card:hover` | `.card__side--front`, `.card__side--back` | Applies `transform: rotateY(-180deg)` front and `rotateY(0deg)` back. |
| "Book Now" Anchor | `<a href="#popup">` | `.popup:target` | Renders modal overlay (`opacity: 1; visibility: visible;`). |
| Modal Close Anchor | `<a href="#section-tours">` | Clears URL hash | Unsets `:target`, collapsing modal dialog back to hidden state. |
| Form Input Field | `.form__input:placeholder-shown` | `+ .form__label` | Keeps label hidden while placeholder is visible; slides up when typed. |
| Custom Radio Button | `.form__radio-input:checked` | `~ .form__radio-label .form__radio-button::after` | Activates opacity 1 on custom green radial dot indicator. |

---

## External APIs & SDKs Called
- **Status**: **No external third-party APIs called**.
- **Self-Contained Assets**: All SVG icons and typography are bundled locally in `css/fonts/` and `img/`.
