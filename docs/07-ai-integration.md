# AI Integration Analysis: Natours (Wanderly)

## Current Status: No AI Integration

The repository currently contains **No AI integration**. Wanderly is intentionally implemented as an ultra-lean, pure CSS and HTML frontend to showcase master-level web development fundamentals.

---

## Architectural Blueprint: Client-Side Edge AI Integration

To augment Wanderly with modern intelligent capabilities without introducing heavy server backends, the following client-side AI architecture is proposed:

```mermaid
sequenceDiagram
    autonumber
    actor Explorer as Outdoor Adventurer
    participant UI as Tour Booking View
    participant TFJS as TensorFlow.js (MobileNet / Universal Sentence Encoder)
    participant Model as Local Vector Embeddings (IndexedDB)
    participant Engine as Client-Side Cosine Recommender

    Explorer->>UI: Types: "Chilly high-altitude mountaineering with local guide"
    UI->>TFJS: Computes 512-dimensional text embedding in browser WebGL worker
    TFJS->>Model: Queries pre-computed tour catalog embeddings
    Model->>Engine: Returns top-3 matching tour items (Snow Adventurer: 94% similarity)
    Engine-->>UI: Highlights Tour Card #3 and auto-rotates card to reveal booking CTA
```

### Proposed AI Capabilities
1. **Semantic Tour Matcher**: Natural language search matching adventurer preferences against tour itineraries using client-side embeddings via TensorFlow.js.
2. **Visual Landmark Search**: Explorer uploads vacation photo; on-device MobileNet model extracts visual features and suggests corresponding mountain or coastal tours.
