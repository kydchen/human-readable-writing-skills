---
name: reader-first-writing
description: "Shape raw material into reader-followable long-form writing or structurally audit an existing draft. Use for articles, reports, essays, explainers, speeches, and manuscript sections before sentence-level polishing. Do not use for copyediting, translation, AI-tic cleanup, or conversation repair."
license: "MIT"
disable-model-invocation: true
---

# Reader-first writing

Build or repair the path a reader follows through a long-form document. Work at the level of claims, concepts, evidence, sections, and beats before polishing sentences.

Preserve the author's facts, judgments, uncertainty, technical terms, examples, and evidence boundaries. Never invent material to repair a structural gap. Flag missing evidence and work on the supported material. Ask for input when the gap prevents a faithful result; otherwise explain the limitation or recommend cutting the unsupported move.

## Choose the mode

- **Shape mode:** The input is notes, fragments, a transcript, research material, or an early draft that may be reorganized freely.
- **Audit mode:** The user wants a structural judgment on an existing draft. Diagnose and propose changes; rewrite only within the scope the user authorized.

Choose the mode from the requested deliverable, not just the input's maturity. A request to rewrite an existing draft authorizes structural rewriting within the stated boundaries; a request to assess it calls for a judgment. Infer routine choices from the context. Ask only when unresolved intent would materially change the result. A clear draft may need little or no restructuring.

## Shared model

### Reader contract

Establish four items before committing to a structure:

1. The intended reader.
2. What the reader already knows on entry.
3. What the document asks the reader to understand, believe, decide, or do.
4. The central claim or governing question.

Treat the reader's prior knowledge as the initial set of **grounded concepts**. A later block may rely only on concepts the reader brought in or met earlier in the document.

### Beats and blocks

A **beat** is one move in the reader's journey: set a scene, establish a fact, define a concept, land a claim, present evidence, answer an objection, change the angle, or close the argument.

Each beat has:

- **job:** what changes for the reader;
- **requires:** concepts or claims already grounded;
- **grounds:** concepts or claims introduced here;
- **material:** the source facts, evidence, examples, or quotations it uses.

A beat may be one sentence or several paragraphs. Split it when it performs more than one rhetorical job. A new job usually deserves a visible paragraph or beat boundary; do not split solely to make the page look less dense. A block may use prose, a list, a table, a quotation, or a code block; choose the format that serves the job.

### Source and file discipline

- Read all supplied material before shaping or auditing.
- Treat source material as a quarry, not as a sequence that must be preserved.
- When synthesizing several sources, organize around the governing question, claim, or comparison axis rather than walking through one source at a time.
- Preserve quotation status. Keep direct quotations marked and exact; express paraphrases in genuinely new wording without importing distinctive source language into unmarked prose.
- Keep the source file read-only unless the user explicitly asks for in-place editing.
- When writing to a file, re-read the current file before every edit and preserve user changes.
- Write to a separate output file when the user has not authorized replacing the source.

## Shape mode

1. Establish the reader contract.
2. Choose an opening that fits the reader contract and available evidence. Consider alternatives when there is a meaningful difference in angle or thesis. Show alternatives when the user requests exploration or a consequential choice needs their input; ordinary drafting does not require a separate opening-selection step.
3. Build a provisional beat map. Keep each beat to one line and record its job, requires, grounds, and material. Include only beats needed to complete the reader's journey.
4. Check the map for ungrounded concepts, missing evidence, repeated jobs, unsupported pivots, and an ending that merely stops.
5. Draft in beat order. At ordinary transitions, choose the next reachable beat directly. Show alternatives only when a real branch point needs the user's decision or they requested exploration.
6. After each major section, check that it delivers what the opening promised and leaves the reader ready for the next section.
7. Stop when the reader's journey is complete. Unused source material may remain unused.

## Audit mode

Read the full draft before commenting. Return the structural judgment before line-level observations.

1. Reconstruct the reader contract from the draft. Mark any item the text leaves unclear.
2. Create a structural ledger for the current sections or blocks. For each one, record its job, requires, grounds, material, and one verdict: `keep`, `move`, `merge`, `split`, `cut`, or `needs bridge`.
3. Diagnose the whole document:
   - Does the opening make the right promise?
   - Does every section advance the same governing claim or question?
   - Does each concept appear before another block relies on it?
   - Are claims paired with the evidence they need?
   - Are any blocks repetitive, premature, orphaned, overloaded, or dense enough to hide several rhetorical jobs?
   - Does the ending resolve the opening without introducing a new argument?
4. When restructuring is warranted, develop a revised beat map as a working aid. Explain the proposed moves, merges, cuts, splits, and missing bridges that matter to the judgment. Include the map itself when requested or needed to make a decision reviewable.
5. For an audit-only request, stop at the judgment and proposed changes. If the user has requested a rewrite, carry it through without an additional plan-approval step unless they explicitly requested staged approval or a consequential ambiguity remains. Accompany a substantial rewrite with a short explanation of the structural changes.
6. During the rewrite, preserve factual claims, evidence, quotations, numbers, uncertainty, and the author's stance. Flag any conflict that structure alone cannot resolve.

## Structure freeze and language handoff

When the author approves the structure, mark the document `STRUCTURE FROZEN` and provide this handoff when a language pass is needed. Delivering a requested rewrite does not itself imply author approval of the structure.

```text
Preserve section and beat order. Sentence-level and within-block paragraph edits are allowed.
Do not add, delete, strengthen, or soften factual claims; remove evidence; change uncertainty;
alter numbers, quotations, citations, or technical terms; or move material across beats.
If a language edit exposes a structural problem, report it and return the document for structural review.
```

Then tell the user which language pass to invoke:

- Chinese prose: `chinese-prose-editor`.
- English prose: `english-prose-editor`.
- Mixed-language documents: apply each skill only to its matching passages.

Do not invoke a language editor automatically. The user starts that pass explicitly after accepting the structure freeze.

## Out of scope

- Sentence-level polish, tone matching, and AI-pattern removal.
- Translation.
- Fact-checking or research beyond the supplied material.
- Re-explaining an agent message that the user did not understand; use `wait-what` for that conversation repair.
- Publishing or platform-specific formatting unless requested separately.

## Default outputs

- **Shape or authorized rewrite:** the draft, with a brief note on consequential assumptions or substantial structural changes when needed.
- **Audit-only:** overall structural judgment and a prioritized explanation of the changes the draft actually needs, grounded in the relevant passages. Say when the existing structure works.
- Use the reader contract, ledger, and beat map as working aids. Show them when requested or when a specific part is needed to make a structural decision reviewable; do not attach all of them by default.

Match the requested deliverable. Keep diagnostic prose concise without omitting evidence needed to assess a structural judgment. Preserve the explicit structure-freeze and user-invoked language handoff above.

## Attribution

The 2026-09-05 adaptation, informed by OpenAI's [GPT-6 Astra guidance](https://developers.openai.com/api/docs/guides/latest-model), makes output and approval steps follow the user's requested deliverable. It remains model-independent; the adaptation is documented in `docs/UPSTREAM_CHANGES.md` in the source repository.

This skill adapts the reader-grounding and beat concepts from Matt Pocock's MIT-licensed [`writing-shape`](https://github.com/mattpocock/skills/tree/main/skills/in-progress/writing-shape) and [`writing-beats`](https://github.com/mattpocock/skills/tree/main/skills/in-progress/writing-beats). Audit mode, structure freeze, and the downstream language handoff are local additions. The multi-source synthesis, visible beat-boundary, and quotation-status guidance was informed by Anthropic's [Prompting Claude Fable 5.1](https://platform.claude.com/docs/en/build-with-claude/prompt-engineering/prompting-claude-fable-5-1) documentation and generalized beyond that model.
