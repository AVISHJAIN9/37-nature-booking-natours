# F2: Pure CSS Fullscreen Navigation (Checkbox Hack)

## Overview & Architecture
A zero-JavaScript fullscreen modal navigation drawer activated entirely by the native HTML checkbox state machine.

```mermaid
sequenceDiagram
    autonumber
    actor User as Explorer
    participant Toggle as #navi-toggle (checkbox)
    participant Bg as .navigation__background (radial disk)
    participant Nav as .navigation__nav (nav list)

    User->>Toggle: Clicks hamburger label
    Toggle->>Bg: Checked state triggers ~ .navigation__background scale(80)
    Bg-->>User: Radial gradient expands to cover entire viewport
    Toggle->>Nav: Checked state sets width 100%, opacity 1
    Nav-->>User: Displays navigation links with cubic-bezier transition
```

## Say It Out Loud
> "To achieve an interactive fullscreen menu without JavaScript, I implemented the CSS checkbox hack in `_navigation.scss`. An invisible native checkbox is bound to an accessible circular button label. When the user clicks the hamburger icon, the checkbox toggles to `:checked`, which triggers the adjacent sibling combinator to scale an underlying green radial gradient circle from 6rem to eighty times its size. This instantly floods the viewport with color while the navigation links fade into view with cubic-bezier timing. If a user clicks outside or on a link, the checkbox state resets, collapsing the overlay smoothly back into the circular icon."
