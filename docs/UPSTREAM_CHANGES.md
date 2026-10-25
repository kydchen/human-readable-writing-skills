# Upstream changes

This file records where each skill came from, which upstream snapshot was reviewed, and what changed in this repository. Commit hashes make the comparison reproducible even if an upstream project changes later.

## 2026-10-25 reader-effort update

Source reviewed: Thomas Hikaru Clark, Matias B. Martin, and Kyle Mahowald, [Why is AI-generated language so hard to understand?](https://arxiv.org/abs/2610.29162v1), v1, submitted 2026-10-21, accessed 2026-10-25. Relevant sections: 3, 4, 7, and Appendices B and C.

The paper compares English linguistic features across model outputs, human corpora, and round-trip translations. It does not directly test readers' comprehension of the sampled outputs or these editing rules. Effects vary by model and setting. A length-penalty experiment with Qwen2.5-1.5B-Instruct provides a possible mechanism, not a causal account of frontier-model training.

Our editorial decisions:

- Inspect compressed syntax and unclear relationships before cosmetic pattern changes. A revision may add useful words.
- Unpack ambiguous noun chains, reduce disruptive nesting, and restore omitted grammatical cues when needed.
- Preserve clear long sentences, established terms, accurate passives, and literal nonhuman subjects. Retain conditions, attribution, uncertainty, and the author's voice.
- Adapt these checks to Chinese without claiming that the paper tested Chinese. Preserve natural subject omission when the reference is clear.

Round-trip translation remains a research comparison, not a required editing workflow. No detector targets, word-count thresholds, or automatic replacement rules were added. Validation covers packaging, instruction consistency, and source/installed-copy agreement. No model A/B evaluation or reader study was performed.

## 2026-09-05 GPT-6 Astra adaptation

Source reviewed: OpenAI, [Using GPT-6 Astra](https://developers.openai.com/api/docs/guides/latest-model), accessed 2026-09-05, especially instruction following and personality and writing style.

The guide motivates auditing conflicting skill instructions and making the desired output explicit. The following are this repository's editorial decisions in response, not model-performance findings or a copied system prompt:

- English editing now defaults to the revised text, permits unchanged passages, and uses a focused fidelity/readability check. The mandatory draft/self-critique/final bundle, numerical self-rating, and score-triggered rewrite loop were removed. Rules and examples no longer encourage inventing a named actor, a second-person scene, or an author's feelings to make text vivid.
- Chinese pattern lists now trigger contextual inspection rather than unconditional string replacement. Meaningful corrections, inferences, clear references, technical terms, direct quotations, and explicit user preferences take precedence over generic pattern matching. Diagnosis has no minimum finding count.
- Structural editing selects its workflow from the requested deliverable. A requested rewrite does not require an extra routine plan approval. Audit-only requests remain diagnostic, and author-approved structure freeze and user-invoked language editing are preserved. Contracts, ledgers, and beat maps remain working aids and are shown selectively.

The skills remain model-independent. Reasoning effort, model routing, runtime permissions, tool orchestration, and Personalization are outside this update. Validation checks instruction consistency, packaging, and installed-copy synchronization; no model-level A/B evaluation has been performed.

## 2026-09-02 cross-model editorial update

Source reviewed: Anthropic, [Prompting Claude Fable 5.1](https://platform.claude.com/docs/en/build-with-claude/prompt-engineering/prompting-claude-fable-5-1), accessed 2026-09-02.

The source is model-specific. This repository adopts only three writing mechanisms that remain useful across models, restated in original language rather than copied as a prompt block:

- identify mannered prose that substitutes display for precise statement;
- choose headings, lists, punctuation, and paragraphing according to the material instead of treating a format as an automatic AI tell;
- keep direct quotations marked and exact while rewriting paraphrases in the editor's own words.

Agent-runtime advice about effort, tool batching, conversation history, compaction, search triggering, subagents, and task completion remains outside these writing skills.

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
- multi-source synthesis organized by the governing question or comparison axis;
- visible beat and paragraph boundaries for changes in rhetorical job;
- quotation-status preservation;
- a `STRUCTURE FROZEN` handoff;
- routing to separate Chinese and English language editors.

## `chinese-prose-editor`

Source: Pluviobyte, [`ra-人话`](https://github.com/Pluviobyte/rnskill/tree/main/skills/ra-%E4%BA%BA%E8%AF%9D), snapshot [`d450948`](https://github.com/Pluviobyte/rnskill/commit/d4509487ad4585033b3be92b577c2c98c4255c0a).

The initial public version changed the packaging boundary:

- renames the machine identifier from `ra-人话` to `chinese-prose-editor`;
- quotes and rewrites the frontmatter description for portability and discovery;
- states that the skill handles Chinese while `english-prose-editor` handles English;
- adds license and attribution metadata.

The initial public version kept the editing rules from the locally modified `ra-renhua` version. The 2026-09-02 update adds a Chinese-specific mannered-prose rule, density and paragraph checks, context-sensitive formatting, and explicit quotation/paraphrase boundaries.

## `english-prose-editor`

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
- a precision-over-performance rule for mannered prose;
- context-sensitive punctuation, formatting, paragraphing, and quotation boundaries;
- a focused fidelity and readability check with revised-text-only default output;
- contextual pattern inspection and permission to leave already-clear prose unchanged;
- an explicit ban on inventing facts, names, dates, citations, examples, or experiences.

The current upstream Humanizer was substantially rewritten after this fork's base. Its present pattern numbering therefore does not map one-to-one to this repository. We document the lineage instead of claiming that this file is a patch against current upstream.

## `wait-what`

Source: Matt Pocock, [`wait-what`](https://github.com/mattpocock/skills/blob/main/skills/productivity/wait-what/SKILL.md), repository snapshot [`885e2ca`](https://github.com/mattpocock/skills/commit/885e2ca4d842d139e9aef4e48d366c63cb1b8013).

The local version has the same one-action purpose. It changes two lines:

- replaces the short description punctuation;
- reads the active workspace's `CONTEXT.md` directly instead of following `CONTEXT-MAP.md` when several context files exist.

The public package also adds license and attribution metadata.
