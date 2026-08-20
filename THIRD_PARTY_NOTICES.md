# Third-party notices

This repository contains adaptations and a synthesis of the following projects.

## Pluviobyte `ra-人话`

- Source: https://github.com/Pluviobyte/rnskill/tree/main/skills/ra-%E4%BA%BA%E8%AF%9D
- Copyright: 2024-2026 雪踏乌云 (Pluviobyte)
- License: Creative Commons Attribution-NonCommercial 4.0 International
- Used in: `skills/chinese-prose-editor/`
- Changes: renamed for portable public use, with language routing and attribution metadata added. Editing rules are otherwise preserved.

## blader `humanizer`

- Source: https://github.com/blader/humanizer
- Copyright: 2025 Siqi Chen
- License: MIT
- Used in: `skills/english-prose-editor/`
- Changes: combined with stop-slop guidance and extended with language routing, voice calibration, false-positive guidance, and a revision loop.

## Hardik Pandya `stop-slop`

- Source: https://github.com/hardikpandya/stop-slop
- Copyright: 2025 Hardik Pandya
- License: MIT
- Used in: `skills/english-prose-editor/`
- Changes: selected craft patterns and the scoring approach were incorporated into the Humanizer workflow.

## Matt Pocock `skills`

- Source: https://github.com/mattpocock/skills
- Copyright: 2026 Matt Pocock
- License: MIT
- Used in: `skills/reader-first-writing/` and `skills/wait-what/`
- Changes: `writing-shape` and `writing-beats` were synthesized into a structural writing skill; `wait-what` was adapted to read the active workspace's `CONTEXT.md` directly.

See [`docs/UPSTREAM_CHANGES.md`](docs/UPSTREAM_CHANGES.md) for source snapshots and a fuller change record.
