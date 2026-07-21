# Videos

Demonstration media referenced from the README.

| File | Content |
|:---|:---|
| `system-walkthrough.mp4` | Guided tour of the deployed installation and enclosure |
| `diversion-event.mp4` | Live threshold breach triggering the valve transition |
| `mobile-app-demo.mp4` | End-to-end supervision and remote configuration |
| `field-commissioning.mp4` | Installation, sealing, and solar subsystem startup |

## Hosting

> [!IMPORTANT]
> **Do not commit large video files to this repository.** `.gitignore` blocks `*.mp4` by default.

Git handles binary media poorly — every revision is stored in full, and the repository grows permanently. Host demonstration video externally and link to it:

- Upload to YouTube (unlisted) or Vimeo (private) and link from the README table.
- Or drag the file into a GitHub issue or release to obtain a hosted URL, then reference that URL.

For short clips, an animated GIF under 5 MB placed in `images/` renders inline and needs no external host.

## Specification

| Property | Guideline |
|:---|:---|
| **Resolution** | 1080p |
| **Length** | 30–90 seconds — evaluators do not watch long clips |
| **Audio** | Optional; if narrated, keep it brief and technical |
| **Captions** | Recommended, since most viewers watch muted |

Apply the same disclosure check as for images: no visible wiring, component markings, network names, or credentials.
