# F6: Skewed Story Cards with Circular Shape-Outside Avatar

## Overview & Architecture
Testimonial cards with a parallelogram slant using `transform: skewX(-12deg)` while counter-skewing child elements by `12deg` for legibility.

```mermaid
flowchart TD
    StoryCard[.story: transform skewX(-12deg)] --> ShapeContainer[.story__shape: transform skewX(12deg)]
    ShapeContainer --> ShapeOutside[shape-outside: circle 50%]
    ShapeOutside --> ClipPath[clip-path: circle 50%]
    ClipPath --> Caption[Caption text wraps naturally around circular profile image]
```

## Say It Out Loud
> "In `_story.scss`, I created the customer testimonial stories with an angled modern editorial aesthetic. The parent `.story` card is skewed horizontally by negative twelve degrees. To ensure readability, I counter-skewed the internal content by positive twelve degrees. For the customer profile photograph, I used `shape-outside: circle()` and `clip-path: circle()` so the accompanying testimonial paragraphs organically flow and wrap around the circular image contour rather than hitting an awkward rectangular boundary."
