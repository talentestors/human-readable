# human-readable

Two skills that make AI-written text readable in one pass — `human-readable-chinese` for Chinese, `human-readable-english` for English.

## What it fixes

AI text has correct grammar and the right words, and still reads badly. It deletes the words that give a reader room: connectives, the optional `that`, qualifiers. Then it packs the rest tighter. Reading three lines costs more effort than it should.

The sentences don't fail on vocabulary. They fail on structure.

**Theoretical baseline: Clark, Martin & Mahowald (2026), *Why is AI-generated language so hard to understand?* (NYU + UT Austin, [arXiv:2610.29162](https://arxiv.org/abs/2610.29162)).** Both skills take their symptom list, their metrics and their mechanism from this paper. Gibson's dependency locality theory and Levy & Jaeger's UID hypothesis are the theory it builds on, and each is credited at its own source.

## Who it's for

- People who write work items, bug reports, requirement docs, post-mortems, and status updates
- Agents that write or rewrite those documents for them

## What's inside

```
human-readable-chinese/     中文版：让中文句子一眼看到主干
├── SKILL.md                 entry: core move + skeleton + index (~3.8 KB)
└── references/
    ├── why-hard.md          three pathologies + citations (DLT / UID / arXiv:2610.29162)
    ├── diagnosis.md         9 smells + spine table + the three numbers not to confuse
    ├── rewrite-rules.md     R1–R11, each with a before/after pair
    ├── checklist.md         5 steps + checklist + failure list + metrics
    ├── workitem-templates.md  bug / requirement / tech-debt templates + 10 rewrite pairs
    └── prompt-snippet.md    paste-ready prompt (~450 字 / 120 字)

human-readable-english/     English: make the main clause visible at a glance
├── SKILL.md                 entry: core move + skeleton + index (~4 KB)
└── references/
    ├── why-hard.md          three pathologies + citations
    ├── diagnosis.md         9 smells + spine table + the three numbers not to confuse
    ├── rewrite-rules.md     R1–R11, each with a before/after pair
    ├── checklist.md         5 steps + checklist + failure list + metrics
    ├── workitem-templates.md  bug / requirement / tech-debt templates + 10 rewrite pairs
    └── prompt-snippet.md    paste-ready prompt (~470 / ~130 words)
```

Both versions target work items first. The skeleton has five sections: one-liner, current behavior, impact, expected, out of scope. Bug, requirement, and tech-debt variants are in `references/workitem-templates.md`.

## Two rules both versions enforce

1. **Never chop sentences just to make them short.** Delete the connectives and the reader has to supply the logic, which costs more than the long sentence did.
2. **Fidelity outranks readability.** Rewriting changes the packaging, not the facts. Dropping a qualifier is the worst failure in this skill.

## Install

### Hermes Agent

```bash
cp -r human-readable-chinese ~/.hermes/skills/
cp -r human-readable-english ~/.hermes/skills/
```

### Claude Code / other skill runners

Copy the version you need into your skills directory. Each directory holds a `SKILL.md` with YAML frontmatter (`name`, `description`) and a `references/` folder.

### Just the prompt

To give another agent only the rules, take `references/prompt-snippet.md` and paste the fenced block into its system prompt.

## When it triggers

- Chinese: AI 味太重 / 读不懂 / 说人话 / 优化这段描述 / 写 workitem 描述 / 主谓宾不清
- English: "AI-sounding", "hard to read", "rewrite this", "say it plainly", work item / bug report / RFC drafting

## Research base

- **Primary source.** Clark, T. H., Martin, M. B., & Mahowald, K. (2026). *Why is AI-generated language so hard to understand?* [arXiv:2610.29162](https://arxiv.org/abs/2610.29162). NYU (Clark) and UT Austin (Martin, Mahowald). The study compared nine frontier models and five small open models against human writing and against round-trip translations (English → Japanese → English, via NLLB-200). All nine frontier models used more inanimate subjects with animate verbs and more low-frequency n-grams; most also used longer dependencies, more stacked nouns, and more reduced object relatives. A length-penalty fine-tune reproduced the drift. This paper supplies layers 2 and 3 of both skills.
- **Underlying theory.** Gibson, E. (2000), dependency locality theory — layer 1. Grodner & Gibson (2005), reading-time evidence for it. Levy & Jaeger (2007), the UID hypothesis behind layer 3.
- **Craft, not experiments.** Sword, H. (2012), *Stylish Academic Writing* — "zombie nouns".

## License

MIT
