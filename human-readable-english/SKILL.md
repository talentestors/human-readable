---
name: human-readable-english
description: Rewrite "AI-sounding" English into prose a person can read in one pass — for work items, bug reports, RFCs, docs, and status updates. Use when text feels bloated, nominalized, metaphor-heavy, or hard to follow, or when asked to "say it plainly", "make this readable", "cut the AI tone", or to write a work item / bug description. Triggers: AI-sounding, hard to read, unclear, rewrite this, plain English, work item description, bug report, nominalization, zombie nouns, subject-verb distance, too many metaphors.
---

# Plain English: make the main clause visible at a glance

AI-written English has all the right words and no grammatical errors, yet three lines in your reader's eyes glaze over. The problem isn't vocabulary. It's that **the places that should be spread out got compressed, and the places that should be stated plainly got talked around**.

A reader scanning a work item needs to answer *whose problem is this, where does it happen, what do you want me to do*. If they read forty words without hitting a verb, they go back and re-find the subject. **Every re-read costs a unit of trust.**

This skill gives you two things: **countable diagnostics** (you don't judge "AI-ness" by feel) and **specific rewrite moves** (each symptom maps to one operation).

---

## The core move: the spine table

Reduce every sentence to `subject | verb | object | subject-verb distance`.

**A sentence you can't reduce to a spine is a sick sentence.** This check beats reading the paragraph ten times.

```markdown
| Sentence | Subject | Verb | Distance | Can the subject do it? |
| The remediation plan…, following…, was mitigated | the plan | was mitigated | 14 words | no — a plan ships, it isn't mitigated |
```

---

## Default skeleton (work item)

```markdown
## One-liner    <who> hits <what problem> when <in what situation>
## Current      symptom / repro / environment — one line each
## Impact       who is affected, how often, at what cost; numbers if you have them
## Expected     [ ] verifiable checkboxes
## Out of scope draw the boundary explicitly
```

Full bug / requirement / tech-debt templates: `references/workitem-templates.md`

---

## Index: read by situation

| What you're doing | Read this |
|---|---|
| Understanding *why* it's hard, or defending the standard to someone | `references/why-hard.md` |
| **Locating the fault in a paragraph** (9 smells + spine table + three numbers you must not confuse) | `references/diagnosis.md` |
| **Actually rewriting** (R1–R11, each with before/after) | `references/rewrite-rules.md` |
| Pre-delivery pass (5 steps + checklist + failure list + metrics) | `references/checklist.md` |
| Writing a work item / requirement / tech debt (templates + 10-row rewrite table) | `references/workitem-templates.md` |
| Just the prompt to paste into an agent (450-word and 120-word versions) | `references/prompt-snippet.md` |

### Common paths

- **Fixing one paragraph**: `diagnosis.md` → `rewrite-rules.md` → `checklist.md`
- **Writing a new work item**: `workitem-templates.md` → `checklist.md`
- **Writing a prompt for someone else**: copy `prompt-snippet.md`; don't improvise it
- **Someone challenges the standard**: `why-hard.md` has the citations (DLT, UID, arXiv:2610.29162)

---

## The three most-violated rules

1. **Subject and verb adjacent** — ≤ 8 words apart, no comma between them (R2)
2. **The subject must be able to do the verb** — people / teams / services, not framework / capability / ecosystem (R4)
3. **Fidelity beats readability** — not one number, condition, or exception may be dropped (R9, R10)

---

## Boundaries: what this skill doesn't do

- Doesn't judge whether the content is correct or the logic holds — only the expression
- Doesn't replace technical terms with plain words; it requires defining them in place (R8)
- Doesn't delete qualifiers to make a sentence flow
- Doesn't do layout, figures, or slide structure

**Root principle: rewriting changes the packaging, never the facts.**
