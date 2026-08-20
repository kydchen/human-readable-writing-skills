---
name: reader-first-writing
description: "Shape raw material into reader-followable long-form writing or structurally audit an existing draft. Use for articles, reports, essays, explainers, speeches, and manuscript sections before sentence-level polishing. Do not use for copyediting, translation, AI-tic cleanup, or conversation repair."
license: "MIT"
disable-model-invocation: true
---

# Reader-first writing

Build or repair the path a reader follows through a long-form document. Work at the level of claims, concepts, evidence, sections, and beats before polishing sentences.

Preserve the author's facts, judgments, uncertainty, technical terms, examples, and evidence boundaries. Never invent material to repair a structural gap. Name the gap and ask for material, or recommend cutting the unsupported move.

## Choose the mode

- **Shape mode:** The input is notes, fragments, a transcript, research material, or an early draft that may be reorganized freely.
- **Audit mode:** The input is an existing full draft. Diagnose and propose the structural change before rewriting it.

If the input could fit either mode, infer the mode from the request. Ask only when the choice would materially change the result.

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

A beat may be one sentence or several paragraphs. Split it when it performs more than one rhetorical job. A block may use prose, a list, a table, a quotation, or a code block; choose the format that serves the job.

### Source and file discipline

- Read all supplied material before shaping or auditing.
- Treat source material as a quarry, not as a sequence that must be preserved.
- Keep the source file read-only unless the user explicitly asks for in-place editing.
- When writing to a file, re-read the current file before every edit and preserve user changes.
- Write to a separate output file when the user has not authorized replacing the source.

## Shape mode

1. Establish the reader contract.
2. Draft two or three candidate openings. Each opening must imply a distinct angle or thesis and state what route it unlocks. Ask the user to choose when collaboration is expected. If the user requested an autonomous pass, choose one and label the assumption.
3. Build a provisional beat map. Keep each beat to one line and record its job, requires, grounds, and material. Include only beats needed to complete the reader's journey.
4. Check the map for ungrounded concepts, missing evidence, repeated jobs, unsupported pivots, and an ending that merely stops.
5. Draft in beat order. At ordinary transitions, choose the next reachable beat directly. Offer alternatives only at a real branch point such as the opening, a major pivot, or the ending.
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
   - Are any blocks repetitive, premature, orphaned, or overloaded?
   - Does the ending resolve the opening without introducing a new argument?
4. Propose a revised beat map and a concise change list. Show moves, merges, cuts, splits, and missing bridges explicitly.
5. Do not rewrite the full document before the user approves the structural plan, unless the user requested an autonomous rewrite. In an autonomous pass, present the plan and the rewritten document together so the changes remain auditable.
6. During the rewrite, preserve factual claims, evidence, quotations, numbers, uncertainty, and the author's stance. Flag any conflict that structure alone cannot resolve.

## Structure freeze and language handoff

When the author approves the structure, mark the document `STRUCTURE FROZEN` and provide this handoff:

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

- **Shape mode:** reader contract, proposed beat map, then the draft.
- **Audit mode:** overall structural judgment, structural ledger, revised beat map, and the rewritten draft only when authorized.

Keep diagnostic prose concise. The document is the deliverable.

## Attribution

This skill adapts the reader-grounding and beat concepts from Matt Pocock's MIT-licensed [`writing-shape`](https://github.com/mattpocock/skills/tree/main/skills/in-progress/writing-shape) and [`writing-beats`](https://github.com/mattpocock/skills/tree/main/skills/in-progress/writing-beats). Audit mode, structure freeze, and the downstream language handoff are local additions.
