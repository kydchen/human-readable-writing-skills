# Upstream changes

This file records where each skill came from, which upstream snapshot was reviewed, and what changed in this repository. Commit hashes make the comparison reproducible even if an upstream project changes later.

## `reader-first-writing`

Sources:

- Matt Pocock, [`writing-shape`](https://github.com/mattpocock/skills/tree/main/skills/in-progress/writing-shape)
- Matt Pocock, [`writing-beats`](https://github.com/mattpocock/skills/tree/main/skills/in-progress/writing-beats)
- Repository snapshot: [`885e2ca`](https://github.com/mattpocock/skills/commit/885e2ca4d842d139e9aef4e48d366c63cb1b8013)

This is a synthesis, not a renamed copy. It keeps the idea that a reader can rely only on concepts already grounded, and uses beats as the units of a reader's journey. It adds:

- separate shape and audit modes;
- a four-part reader contract;
- a structural ledger with explicit edit verdicts;
- evidence-preservation rules;
- a `STRUCTURE FROZEN` handoff;
- routing to separate Chinese and English language editors.

## `chinese-prose-editor`

Source: Pluviobyte, [`ra-人话`](https://github.com/Pluviobyte/rnskill/tree/main/skills/ra-%E4%BA%BA%E8%AF%9D), snapshot [`d450948`](https://github.com/Pluviobyte/rnskill/commit/d4509487ad4585033b3be92b577c2c98c4255c0a).

The public version changes only the packaging boundary:

- renames the machine identifier from `ra-人话` to `chinese-prose-editor`;
- quotes and rewrites the frontmatter description for portability and discovery;
- states that the skill handles Chinese while `humanizer` handles English;
- adds license and attribution metadata.

The editing rules themselves are unchanged from the locally modified `ra-renhua` version. Compared with the upstream file, that local version added six lines and removed two: the portable identifier, quoted description, and four-line language-scope section account for the behavioral diff.

## `humanizer`

Sources:

- [`blader/humanizer`](https://github.com/blader/humanizer), snapshot [`e2e92e7`](https://github.com/blader/humanizer/commit/e2e92e7b4b8229253ed5c8e81dc65463fdeddda5)
- [`hardikpandya/stop-slop`](https://github.com/hardikpandya/stop-slop), snapshot [`8da1f03`](https://github.com/hardikpandya/stop-slop/commit/8da1f030185bdfe8471220585162991eaeb970e9)

This fork retains the older 33-pattern Humanizer structure and adds six craft patterns from stop-slop:

34. False agency
35. Narrator from a distance
36. Business jargon
37. Repeated `wh-` sentence starters
38. Vague declaratives
39. Empty-emphasis adverbs

It also adds:

- explicit English and Chinese routing;
- optional voice calibration from an author's sample;
- guidance against false positives;
- a draft, audit, and final rewrite loop;
- a five-dimension, 50-point final check;
- an explicit ban on inventing facts, names, dates, citations, examples, or experiences.

The current upstream Humanizer was substantially rewritten after this fork's base. Its present pattern numbering therefore does not map one-to-one to this repository. We document the lineage instead of claiming that this file is a patch against current upstream.

## `wait-what`

Source: Matt Pocock, [`wait-what`](https://github.com/mattpocock/skills/blob/main/skills/productivity/wait-what/SKILL.md), repository snapshot [`885e2ca`](https://github.com/mattpocock/skills/commit/885e2ca4d842d139e9aef4e48d366c63cb1b8013).

The local version has the same one-action purpose. It changes two lines:

- replaces the short description punctuation;
- reads the active workspace's `CONTEXT.md` directly instead of following `CONTEXT-MAP.md` when several context files exist.

The public package also adds license and attribution metadata.
