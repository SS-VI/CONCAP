# Assets

Brand and design assets for the CONCAP documentation.

| File | Purpose |
|:---|:---|
| `logo.svg` | Primary mark, centered in the README header |

## Design system

Applying these consistently is what makes the documentation read as a product rather than a collection of files.

### Palette

| Role | Hex | Use |
|:---|:---|:---|
| **Primary** | `#0A66C2` | Water, primary accents, links |
| **Accent** | `#38BDF8` | Highlights, telemetry indicators |
| **Deep** | `#0B3B66` | Depth, secondary structure |
| **Safe** | `#2EA44F` | Normal service state, success |
| **Alarm** | `#E7352C` | Diversion state, faults |
| **Energy** | `#F2A900` | Solar and power subsystem |
| **Surface** | `#0D1117` | GitHub dark mode background |
| **Border** | `#30363D` | Dividers, diagram strokes |

### Rules

- **Dark mode first.** GitHub's dark theme is the default for most viewers. Assets must not assume a white background.
- **SVG wherever possible.** Vector marks stay sharp at every scale and cost almost nothing in repository size.
- **Mermaid diagrams use the palette above** via `classDef`, so diagrams and images share one visual language.
- **Emoji sparingly** — as section wayfinding and state indicators, never decoration.
- **Tables over prose** for anything enumerable. Recruiters scan; they do not read.
