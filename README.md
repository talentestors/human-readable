# human-readable

Two skills for writing text a human can read in one pass — one for Chinese, one for English.

Both solve the same problem from the same research base: AI-generated writing has correct grammar and all the right words, yet it strips out the buffers a reader needs. The sentences don't fail on vocabulary; they fail on **structure**.

写给谁读：写 workitem / bug 描述 / 需求文档 / 复盘 / 汇报材料的人，以及替他们写字或改字的 Agent。

---

## Contents

```
human-readable-chinese/     中文版：让中文句子一眼看到主干
├── SKILL.md
└── references/
    ├── prompt-snippet.md        可直接贴进提示词的精简版（约 450 字 / 120 字）
    └── workitem-templates.md    bug / 需求 / 技术债 三类模板 + 十句改写对照

human-readable-english/     English: make the main clause visible at a glance
├── SKILL.md
└── references/
    ├── prompt-snippet.md        paste-ready system prompt (~450 / ~120 words)
    └── workitem-templates.md    bug / requirement / tech-debt templates + 10 rewrites
```

---

## What's inside

| | 中文版 | English |
|---|---|---|
| 核心原理 | 依存距离 / 语义整合 / 均匀信息密度 | dependency locality / selectional fit / uniform information density |
| 可数病症 | 8 种（主谓远隔、空壳动词、无生主语……） | 8 smells (subject-verb distance, light verbs, inanimate subjects…) |
| 改写规则 | R1–R9 | R1–R9 |
| 主战场 | workitem 五段式 | five-section work item |
| 执行流程 | 抽主干表 → 按病开刀 → 补连接 → 保真核对 → 朗读 | spine table → operate by symptom → restore links → verify fidelity → read aloud |

两条最容易被忽略、也最值钱的规则，两版都有：

1. **不要为了短而机械断句** —— 拆掉连接词，逻辑负担转移给读者，反而更难读。
2. **保真优先** —— 只改包装，不改事实；删掉限定条件是最严重的失败。

---

## Install

### Hermes Agent

```bash
cp -r human-readable-chinese ~/.hermes/skills/
cp -r human-readable-english ~/.hermes/skills/
```

### Claude Code / other skill runners

Copy the version you need into your skills directory — each directory contains a `SKILL.md` with YAML frontmatter (`name`, `description`) plus a `references/` folder.

### Just the prompt

If you only want the rules injected into another agent, take `references/prompt-snippet.md` and paste the fenced block into your system prompt.

---

## When it triggers

- 中文：AI 味太重 / 读不懂 / 说人话 / 优化这段描述 / 写 workitem 描述 / 主谓宾不清
- English: "AI-sounding", "hard to read", "rewrite this", "say it plainly", work item / bug report / RFC drafting

---

## Research base

- Clark, T. H., Martin, M. B., & Mahowald, K. (2026). *Why is AI-generated language so hard to understand?* [arXiv:2610.29162](https://arxiv.org/abs/2610.29162) — NYU (Clark) + UT Austin (Martin, Mahowald). Nine frontier models plus five small ones; more inanimate subjects with animate verbs and more low-frequency n-grams than human writing and round-trip translations; a length-penalty fine-tune reproduces the drift. **This paper owns layers 2–3 of both skills**; dependency locality and UID come from earlier work, credited separately.
- Gibson, E. (2000). Dependency locality theory.
- Grodner, D., & Gibson, E. (2005). Consequences of the serial nature of linguistic input for sentential complexity.
- Levy, R., & Jaeger, T. F. (2007). Speakers optimize information density through syntactic reduction.
- Sword, H. (2012). *Stylish Academic Writing* — "zombie nouns".

---

## License

MIT
