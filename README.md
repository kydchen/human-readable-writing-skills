# Human-readable writing skills

[中文说明](README_CN.md)

Four small skills for turning AI-assisted writing into something a reader can actually follow.

Hard-to-read writing does not have one cause. A reply may be missing context. A full article may introduce ideas in the wrong order. The structure may be sound while the sentences still sound formulaic. This repository separates those jobs so each edit happens at the right layer.

## Four skills, three layers

| Layer | Skill | Use it when | What it changes |
| --- | --- | --- | --- |
| Conversation | [`wait-what`](skills/wait-what/) | The last AI reply did not land | Re-pitches that reply with context and shared terminology |
| Document structure | [`reader-first-writing`](skills/reader-first-writing/) | You have notes, a long draft, or a document with a weak reader journey | Reorders claims, concepts, evidence, sections, and beats |
| Chinese prose | [`chinese-prose-editor`](skills/chinese-prose-editor/) | The structure is stable, but the Chinese sounds formulaic or lecture-like | Revises wording and local paragraph flow while preserving the argument |
| English prose | [`humanizer`](skills/humanizer/) | The structure is stable, but the English carries common AI-writing patterns | Revises wording, rhythm, voice, and local paragraph flow |

`reader-first-writing` combines the structural ideas in `writing-shape` and `writing-beats`. It can shape raw material or audit a complete draft. Once the structure is approved, it marks the document `STRUCTURE FROZEN` and hands it to the matching language editor.

## Recommended workflow

```text
Notes or full draft
        |
        v
reader-first-writing
        |
  STRUCTURE FROZEN
        |
        +--> Chinese --> chinese-prose-editor
        |
        +--> English --> humanizer

Unclear AI reply --> wait-what
```

Use the full document flow when the order of ideas still needs work. If a short draft already has a clear argument and sequence, go straight to the matching language editor. Use `wait-what` during conversation; it is not a required stage in article production.

The language pass may edit sentences and paragraphs inside a structural beat. It should not move evidence, change claims, alter uncertainty, or silently repair a structural gap. If sentence editing exposes a larger problem, return the draft to `reader-first-writing`.

## Examples

### Shape material into an article

Claude Code:

```text
/reader-first-writing Turn these interview notes into an article for readers who know the product but not the research.
```

Codex:

```text
$reader-first-writing Turn these interview notes into an article for readers who know the product but not the research.
```

### Audit a complete draft

```text
Use reader-first-writing in audit mode. Show me the structural ledger and revised beat map before rewriting.
```

### Run the language pass

```text
/chinese-prose-editor Keep the frozen section order and revise the Chinese prose.
/humanizer Keep the frozen section order and revise the English prose.
```

### Repair a conversation

```text
/wait-what
```

## Install

Clone the repository, then copy the four skill folders into the directory used by your agent:

```bash
git clone https://github.com/kydchen/human-readable-writing-skills.git

# Codex and other agents that read ~/.agents/skills
cp -R human-readable-writing-skills/skills/* ~/.agents/skills/

# Claude Code
cp -R human-readable-writing-skills/skills/* ~/.claude/skills/
```

For a project-only install, copy the folders into `.agents/skills/` for Codex or `.claude/skills/` for Claude Code inside that project.

The skills use portable `SKILL.md` files. The optional `agents/openai.yaml` files provide Codex display metadata and do not affect Claude Code.

## Origins and changes

- `reader-first-writing` merges Matt Pocock's [`writing-shape`](https://github.com/mattpocock/skills/tree/main/skills/in-progress/writing-shape) and [`writing-beats`](https://github.com/mattpocock/skills/tree/main/skills/in-progress/writing-beats), then adds audit mode, a structure freeze, and language handoff.
- `chinese-prose-editor` is the public name of our lightly modified fork of Pluviobyte's [`ra-人话`](https://github.com/Pluviobyte/rnskill/tree/main/skills/ra-%E4%BA%BA%E8%AF%9D). The content changes are deliberately small.
- `humanizer` combines ideas and rules from [`blader/humanizer`](https://github.com/blader/humanizer) and [`hardikpandya/stop-slop`](https://github.com/hardikpandya/stop-slop), with language routing, voice calibration, false-positive guidance, and a draft-audit-final loop.
- `wait-what` is a small modification of Matt Pocock's [`wait-what`](https://github.com/mattpocock/skills/blob/main/skills/productivity/wait-what/SKILL.md).

See [`docs/UPSTREAM_CHANGES.md`](docs/UPSTREAM_CHANGES.md) for the exact differences and source snapshots.

## License

This repository uses mixed licensing:

- `skills/chinese-prose-editor/` is licensed under [CC BY-NC 4.0](LICENSES/CC-BY-NC-4.0.txt). It is noncommercial.
- The other skills and repository documentation are licensed under the [MIT License](LICENSES/MIT.txt).

See [`LICENSE`](LICENSE) and [`THIRD_PARTY_NOTICES.md`](THIRD_PARTY_NOTICES.md) for scope and attribution.
