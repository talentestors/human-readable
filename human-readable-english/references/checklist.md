# Process, checklist, and failure list

Read `diagnosis.md` before you start, consult `rewrite-rules.md` while rewriting, and use this page before you deliver.

---

## 1. Five steps

Don't rewrite by feel in one pass. The last two are the quality gate — don't skip them.

**Step 1 Spine table** — reduce each sentence to `subject | verb | object | subject-verb distance`. A sentence you can't reduce is a sick sentence.

**Step 2 Operate by smell** — number each sentence 1–9, then rewrite in R1→R11 order. Fix 1, 3, and 4 first.

**Step 3 Restore the links** — after splitting, check that every causal, contrastive, and conditional relationship still has an explicit word carrying it. If not, add one.

**Step 4 Verify fidelity** — list every number, condition, and proper noun from the original, then find each in the rewrite. **Anything you can't find is something you lost.**

**Step 5 Read aloud** — where you stumble is where you edit; this is the step that catches mid-sentence subject drift.

---

## 2. Checklist (go through it before delivering)

**Structure**

- [ ] Every sentence yields a subject and a verb?
- [ ] Subject head to verb ≤ 8 words, with no comma between them?
- [ ] No main clause buried under "regarding the… of the… that…"?
- [ ] No more than two modifiers before the head noun?
- [ ] Sentences over 40 words split, with connectives restored?

**Word choice**

- [ ] Subjects are things that can act (person / team / service), not framework / capability / ecosystem?
- [ ] No *perform / implement / conduct / facilitate* + abstract noun?
- [ ] Jargon defined on first use?
- [ ] Every abstract qualifier (significant, substantial, effective) followed by a number or a fact?

**Credibility**

- [ ] Numbers, conditions, boundaries, exceptions all preserved?
- [ ] Every precise number traces to a source, and no relayed finding got strengthened? (R10)
- [ ] At most one metaphor in the paragraph, and none of them covering an unclear spot? (R11)

**Overall**

- [ ] Reads aloud without stumbling, and a reader can answer "who hit what, what do you want" at a glance?

---

## 3. Metrics, if you want to quantify

Sample five random sentences and count three things:

| Metric | Target |
|---|---|
| Average sentence length | 20–30 words |
| Median subject-verb distance | ≤ 8 words |
| Share of inanimate-subject sentences | 0 |

**Don't conflate the three numbers** — subject-verb distance, head-noun position, and sentence length are different quantities. See `diagnosis.md` §4.

---

## 4. Failure list

| Anti-pattern | Why it fails |
|---|---|
| Chopping sentences to make them short | Delete the connectives and the reader must supply the logic; cognitive load rises. **Note:** that finding is about cognitive load — don't restate it as "answer accuracy drops", which is a different experiment's metric |
| Inventing a precise number with no source | "200 milliseconds", "a 47% improvement" sound expert, so readers believe them. Precision cannot be invented (R10) |
| Two or three metaphors per paragraph | The reader feels they understood; they didn't. Metaphor is an explanatory tool, not the content (R11) |
| Stacking "we" as a slogan | "We will continue to optimize the experience" has no agent — it isn't a person, it's air |
| Deleting qualifiers and exceptions | Readability presupposes fidelity. This is the worst failure |
| Converting to slide-speak (one line per idea, all noun phrases) | Noun phrases have no subject or verb — a different flavor of unreadable |
| Replacing every term with plain words | Keep the terms; define them in place (R8) |
| Fixing sentences but not structure | If the order of information is wrong, smooth sentences don't save the document |

---

## 5. The one line people most often get wrong in a prompt

**Don't write "keep sentences as short as possible."** It pushes the model to delete connectives and chop mechanically, dumping the logic on the reader — worse than the original.

Write instead: **subject to verb in 8 words or fewer; never drop a number, condition, or exception.**

More anti-prompts: `prompt-snippet.md`.
