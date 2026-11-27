# human-readable-english

Rewrite "AI-sounding" English into prose a person can read in one pass. For work items, bug reports, RFCs, docs, and status updates.

> Repository: **https://github.com/talentestors/human-readable**
> Chinese version: [`human-readable-chinese`](https://github.com/talentestors/human-readable/tree/main/human-readable-chinese)

## What it fixes

AI text has correct grammar and the right words, and still reads badly. It deletes the words that give a reader room: connectives, the optional `that`, qualifiers. Then it packs the rest tighter.

The sentences don't fail on vocabulary. They fail on structure.

This skill gives you countable diagnostics (you don't judge "AI-ness" by feel) and specific rewrite moves (each symptom maps to one operation).

## Files

```
SKILL.md              entry: core move + work-item skeleton + index
references/
├── why-hard.md       three pathologies + citations
├── diagnosis.md      9 smells + spine table + the three numbers not to confuse
├── rewrite-rules.md  R1–R11, each with a before/after pair
├── checklist.md      5 steps + checklist + failure list + metrics
├── workitem-templates.md  bug / requirement / tech-debt templates + 10 rewrite pairs
└── prompt-snippet.md paste-ready prompt (~470 / ~130 words)
```

## Install

```bash
cp -r human-readable-english ~/.hermes/skills/
```

Other skill runners: drop the whole directory into your skills folder. The `SKILL.md` frontmatter carries `name` and `description`.

Just want the prompt? Copy the fenced block in `references/prompt-snippet.md`.

## When it triggers

"AI-sounding", "hard to read", "rewrite this", "say it plainly", "cut the AI tone", or any request to write a work item, bug report, requirement, or RFC.

## Research base

The symptom list and mechanism come from Clark, Martin & Mahowald (2026), *Why is AI-generated language so hard to understand?* (NYU + UT Austin, [arXiv:2610.29162](https://arxiv.org/abs/2610.29162)).

That study compared nine frontier models and five small open models against human writing and against round-trip translations (English → Japanese → English, NLLB-200). All nine frontier models used more inanimate subjects with animate verbs and more low-frequency n-grams; most also used longer dependencies, more stacked nouns, and more reduced object relatives. A length-penalty fine-tune reproduced the drift.

Dependency locality theory comes from Gibson (1998, 2000), with reading-time evidence in Grodner & Gibson (2005). The UID hypothesis comes from Levy & Jaeger (2007). Those three are the theory the 2026 paper builds on, not its own contribution.

## License

MIT — see [LICENSE](LICENSE)
