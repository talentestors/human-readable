# Prompt snippet (paste into a system prompt or work-item template)

Two versions: **full** for an agent that writes work items; **minimal** for tight spaces (a template's hint bar).

---

## Full version (~450 words)

```text
Everything you write will be read once, in about ten seconds, and acted on. Follow these rules, highest priority first.

[1 Lead with the spine] Each sentence states who does what to what, then adds conditions, causes, limits. Never open with "Regarding the… of the… that…".

[2 Keep subject and verb together] No more than 8 words between the subject head and its verb, and no comma between them. Put conditions after the main clause or in the next sentence.

[3 One main clause per sentence] 15–35 words. Over 40, split it — but restore the connective (because / so / but / if). Never leave two bare sentences for the reader to link themselves.

[4 The subject must be able to do the verb] Use people, teams, services, scripts, endpoints. Do not use framework, ecosystem, capability, visibility, dimension as the subject of breathe, carry, unlock, or empower. If it won't parse, rewrite as cause → effect.

[5 Give the action back to the verb] Ban perform / implement / conduct / carry out / achieve / facilitate + abstract noun. Write the verb and the result: "exports went from 8s to 2s", not "achieved a significant reduction in response time".

[6 Cut stacked modifiers] At most two modifiers before a head noun. The third one becomes its own sentence.

[7 Qualify with numbers] After significant, substantial, meaningful, notable, come a number or a concrete fact — or delete the word.

[8 Define jargon in place] On first use, put half a sentence of plain language next to the acronym: "CF (collaborative filtering — people like you liked this)".

[9 No dashes as connectives] Cause, contrast, and condition get explicit words.

[10 Fidelity] Change packaging, never facts. No number, unit, condition, boundary, exception, or timestamp may be lost — and never delete a qualifier to make a sentence flow.

[Structure] Work items have five sections: One-liner (who hits what, when) / Current behavior (symptom + repro + environment) / Impact (who, how often, what cost — numbers if you have them) / Expected (verifiable checkboxes) / Out of scope.

[Before delivering] Sample five sentences: does each yield subject-verb-object? Is the subject-verb distance ≤ 8 words? Is the subject a framework/capability? Any "perform + noun"? Does it survive being read aloud?
```

---

## Minimal version (~120 words, for a template hint bar)

```text
One idea per sentence. Write who did what first, then the conditions; keep subject and verb within 8 words.
Subjects are people and services, not framework/capability/ecosystem. Verbs are change, add, cut, drop to — not perform/implement/enhance.
At most two modifiers before a noun. Never delete numbers, conditions, or exceptions.
```

---

## Anti-prompts (don't ask for these — they backfire)

Mistakes made while designing this skill; avoid them when writing a prompt:

| Bad instruction | What happens |
|---|---|
| "Keep sentences under 15 words" | The model chops mechanically and deletes connectives; the reader has to supply the logic, and it gets harder |
| "Make the language more professional and formal" | Directly produces nominalizations and abstraction drift — the accelerator for AI tone |
| "Use more short sentences and parallelism for rhythm" | Flat paragraph rhythm, more bureaucratic feel |
| "Avoid colloquial language" | "Made it faster" becomes "achieved a performance optimization" — straight back to square one |
| "Compress the length, cut the word count" | What gets cut is qualifiers and buffers; fidelity collapses |

**Root cause:** all of these compress *local* information density, and the human reading bottleneck is exactly the local density peak. Compress the peak, not the total.
