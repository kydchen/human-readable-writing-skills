# 让 AI 写出人能读懂的文章

[English](README.md)

这是四个小技能，处理 AI 辅助写作中最常见的三层问题：对话没讲明白、全文结构走不通、句子仍有明显的 AI 腔。

难读不一定是措辞的问题。有时，上一条回复缺少背景；有时，一篇文章把概念和证据放错了顺序；还有一些文章结构已经成立，只是句子太公式化。这个仓库把三类问题分开处理，避免用改词句的工具硬修全文结构。

## 四个技能，三个层次

| 层次 | 技能 | 什么时候用 | 改什么 |
| --- | --- | --- | --- |
| 对话 | [`wait-what`](skills/wait-what/) | AI 上一条回复没讲明白 | 补回必要背景，用共同术语重新解释上一条回复 |
| 全文结构 | [`reader-first-writing`](skills/reader-first-writing/) | 手上是笔记、长文草稿，或者文章的阅读路径不清楚 | 调整主张、概念、证据、章节与写作节拍的顺序 |
| 中文表达 | [`chinese-prose-editor`](skills/chinese-prose-editor/) | 结构已经稳定，但中文仍公式化、像在讲课 | 修改措辞与段内衔接，同时保留原来的判断 |
| 英文表达 | [`english-prose-editor`](skills/english-prose-editor/) | 结构已经稳定，但英文仍有常见 AI 写作痕迹 | 修改措辞、节奏、声音与段内衔接 |

`reader-first-writing` 融合了 `writing-shape` 和 `writing-beats` 的结构方法。它既能把原始材料组织成长文，也能审计一篇完整草稿。结构确认以后，它会把文档标记为 `STRUCTURE FROZEN`，再告诉用户下一步该调用哪个语言编辑技能。

## 推荐流程

```text
笔记或完整草稿
       |
       v
reader-first-writing
       |
 STRUCTURE FROZEN
       |
    用户调用
       |
       +--> 中文 --> chinese-prose-editor
       |
       +--> 英文 --> english-prose-editor

对话没听懂 --> wait-what
```

只要文章还需要调整观点和证据的顺序，就先走完整流程。短文如果论点和顺序已经清楚，可以直接使用对应语言的编辑技能。`wait-what` 负责对话中的即时补救，不是文章生产的必经步骤。

语言编辑可以修改一个结构节拍内部的句子和段落，但不能搬动证据、改变主张、改写不确定性，或者悄悄补上原文没有的材料。句子修改如果暴露出更大的结构问题，就把草稿退回 `reader-first-writing`。

仓库名本身不是一个可以调用的技能。两个语言编辑器都只能由用户明确调用，模型不会自动选择。在 Claude Code 中使用 `/english-prose-editor` 或 `/chinese-prose-editor`，在 Codex 中使用 `$english-prose-editor` 或 `$chinese-prose-editor`。

## 使用示例

### 把材料组织成文章

Claude Code：

```text
/reader-first-writing 把这些访谈笔记组织成一篇文章。读者了解这个产品，但不了解这项研究。
```

Codex：

```text
$reader-first-writing 把这些访谈笔记组织成一篇文章。读者了解这个产品，但不了解这项研究。
```

### 审计完整草稿

```text
用 reader-first-writing 的 audit mode 检查这篇文章。先给我结构台账和新的节拍图，再重写。
```

### 做语言编辑

Claude Code：

```text
/chinese-prose-editor 保留已经冻结的章节顺序，修改中文表达。
/english-prose-editor Keep the frozen section order and revise the English prose.
```

Codex：

```text
$chinese-prose-editor 保留已经冻结的章节顺序，修改中文表达。
$english-prose-editor Keep the frozen section order and revise the English prose.
```

### 修复一次没讲明白的对话

```text
/wait-what
```

## 安装

先克隆仓库，再把四个技能目录复制到相应智能体使用的位置：

```bash
git clone https://github.com/kydchen/human-readable-writing-skills.git

# Codex 及其他读取 ~/.agents/skills 的智能体
cp -R human-readable-writing-skills/skills/* ~/.agents/skills/

# Claude Code
cp -R human-readable-writing-skills/skills/* ~/.claude/skills/
```

如果只想在一个项目中使用，可以把这些目录复制到项目内的 `.agents/skills/` 或 `.claude/skills/`。

四个技能都使用可移植的 `SKILL.md`。可选的 `agents/openai.yaml` 只提供 Codex 的界面信息，不影响 Claude Code。

## 来源与修改

- `reader-first-writing` 融合了 Matt Pocock 的 [`writing-shape`](https://github.com/mattpocock/skills/tree/main/skills/in-progress/writing-shape) 和 [`writing-beats`](https://github.com/mattpocock/skills/tree/main/skills/in-progress/writing-beats)，并加入结构审计、结构冻结和语言交接。
- `chinese-prose-editor` 是我们对外使用的名字，源自 Pluviobyte 的 [`ra-人话`](https://github.com/Pluviobyte/rnskill/tree/main/skills/ra-%E4%BA%BA%E8%AF%9D)。我们只做了少量必要修改。
- `english-prose-editor` 融合了 [`blader/humanizer`](https://github.com/blader/humanizer) 与 [`hardikpandya/stop-slop`](https://github.com/hardikpandya/stop-slop)，并加入语言分流、声音校准、误判提示和“草稿、审计、定稿”循环。
- `wait-what` 修改自 Matt Pocock 的 [`wait-what`](https://github.com/mattpocock/skills/blob/main/skills/productivity/wait-what/SKILL.md)。

每项修改和本次比对使用的上游版本都记录在 [`docs/UPSTREAM_CHANGES.md`](docs/UPSTREAM_CHANGES.md)。

## 许可证

这个仓库使用混合许可证：

- `skills/chinese-prose-editor/` 使用 [CC BY-NC 4.0](LICENSES/CC-BY-NC-4.0.txt)，不可用于商业用途。
- 其余三个技能和仓库文档使用 [MIT License](LICENSES/MIT.txt)。

具体范围和署名见 [`LICENSE`](LICENSE) 与 [`THIRD_PARTY_NOTICES.md`](THIRD_PARTY_NOTICES.md)。
