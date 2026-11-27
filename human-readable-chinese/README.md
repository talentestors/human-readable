# human-readable-chinese

把「AI 味」中文改写成人类一眼能读懂的中文。适用于 workitem、需求文档、bug 描述、复盘、周报。

> 仓库地址：**https://github.com/talentestors/human-readable**
> 英文版：[`human-readable-english`](https://github.com/talentestors/human-readable/tree/main/human-readable-english)

## 它解决什么

AI 写的中文，字都认识、语法也没错，但读三行太阳穴发紧。问题不在词汇，而在**该摊开的地方压紧了，该说清的地方绕开了**。

这个 skill 提供两样东西：可数的诊断指标（不靠感觉判断有没有 AI 味）和可执行的改写动作（每条病症对应一个具体手术）。

## 文件

```
SKILL.md              入口：核心手法 + workitem 骨架 + 按场景索引
references/
├── why-hard.md       三层病理 + 研究出处（DLT / UID / arXiv:2610.29162）
├── diagnosis.md      九种病灶 + 抽主干表 + 三个数别混
├── rewrite-rules.md  R1~R11 逐条手术，带改前改后
├── checklist.md      五步流程 + 自检清单 + 翻车清单 + 量化指标
├── workitem-templates.md  bug / 需求 / 技术债 三类模板 + 十句改写对照
└── prompt-snippet.md 可直接贴进系统提示的精简版（约 450 字 / 120 字）
```

## 安装

```bash
cp -r human-readable-chinese ~/.hermes/skills/
```

其他 skill runner：把整个目录放进 skills 目录即可，`SKILL.md` 的 YAML frontmatter 里有 `name` 和 `description`。

只想用提示词：复制 `references/prompt-snippet.md` 里的代码块。

## 什么时候触发

AI 味太重 / 读不懂 / 不好读 / 说人话 / 优化这段描述 / 主干找不到 / 主谓宾不清 / 写 workitem 描述 / 写需求文档 / 写故障复盘。

## 理论依据

病理分类和机制解释来自 Clark, Martin & Mahowald (2026), *Why is AI-generated language so hard to understand?*（NYU + UT Austin, [arXiv:2610.29162](https://arxiv.org/abs/2610.29162)）。它测了 9 个前沿模型和 5 个小模型：无生主语配有生动词、低频 n-gram 出现得比人类写得多，多数模型还用了更长的依存、更多名词堆叠、更多省略 that 的关系从句；用长度惩罚微调可以复现这个漂移。

依存距离理论出自 Gibson (1998, 2000)，实验证据见 Grodner & Gibson (2005)；UID 假说出自 Levy & Jaeger (2007)。这三项是上面那篇论文接续的基础理论，不是它的原创。

## License

MIT — 见 [LICENSE](LICENSE)
