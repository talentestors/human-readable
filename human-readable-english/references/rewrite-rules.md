# Rewrite surgery: R1 – R11

Run them in order. R1–R7 fix structure, R8 lowers the comprehension threshold, R9–R11 fix credibility.

---

## R1 Lead with the main clause: who + did what + to what. Push modifiers after.

```
Bad:  The remediation of the export-timeout issue, where async tasks lacked a fallback mechanism, shipped in v2.3.
Good: v2.3 fixed one thing: bulk exports could time out, and nothing caught the failure.
```

Land the spine first, then add conditions. Never open with "Regarding the… of the… that…".

---

## R2 Keep subject and verb adjacent: ≤ 8 words, no comma between them

If you need a condition, move it after the main clause or give it its own sentence.

```
Bad:  The white screen that appeared on first load under weak network conditions with an empty cache disappeared after preloading shipped.
Good: The white screen is gone. It hit weak networks on a first load with an empty cache; preloading shipped and it stopped.
```

---

## R3 One main clause per sentence, 15–35 words

Over 40 words, split — **but restore the connective** (because / so / but / if). Two unrelated short sentences are a different kind of hard.

```
Bad (chopped):  The export failed. The user retried. It failed again.
Good: The export failed, the user retried, and it failed again, because the task queue was full.
```

---

## R4 The subject must be able to do the verb

Three options: use an agent (person, team, service, script, endpoint) · passive or a "we" clause · rewrite as cause → effect.

```
Bad:  The refactor gave the order pipeline room to breathe.
Good: After the refactor, changing the order module no longer means touching three other files.
```

> **Boundary:** *service / script / endpoint / job* can be subjects — they really act ("the service returns 500"). *Framework / ecosystem / capability / visibility / dimension* cannot.

---

## R5 Give the action back to the verb; delete light verbs

"performed an optimization" → "made it faster". "achieved a reduction" → "went from 8s to 2s". "conducted an investigation" → "checked".

```
Bad:  We performed an optimization of export performance, achieving a significant reduction in response time.
Good: Exports went from 8 seconds to 2.
```

**Prefer numbers.** *Significant / substantial / meaningful / notable* is where AI tone lives; if you keep one, follow it with a number or a concrete fact.

---

## R6 More than two modifiers: cut them out

Pull the longest modifier into its own sentence, or make it a trailing note.

```
Bad:  a cold-start validation logic that is based on event data, targets new users only, and supports switching between multiple strategies
Good: Cold-start config has a new validation step. It reads event data, only applies to new users, and can switch between strategies.
```

---

## R7 Make the link explicit: dashes and juxtaposition become because / but / if

```
Bad:  Traffic went up tenfold — the batch job didn't change — now everything runs two hours late.
Good: Traffic went up tenfold, but the batch job didn't change with it, so every run now finishes two hours late.
```

---

## R8 Define jargon where it first appears

Don't leave acronyms for the reader to guess. Put half a sentence of plain language next to the term.

```
Bad:  Cold-start depends on CF recall, which is sparse.
Good: New users have no history (cold start), so we rely on collaborative filtering (CF — "people like you liked this"),
      and with too little data that recommendation is unreliable.
```

---

## R9 Fidelity: not one atomic proposition may be lost

Rewriting changes **packaging**, never **facts**. Numbers, units, conditions, boundaries, exceptions, timestamps — check each one.

Deleting a qualifier because the sentence reads better is the most serious failure — far worse than being hard to read.

---

## R10 Every number must trace back to a source

**A precise number is more dangerous than a vague adjective, because readers believe it.**

- Before writing it, ask: where did this number come from? Can you point to the sentence it came from?
- If the original said "about half a second", do not write "200 milliseconds". **Precision cannot be invented.**
- When relaying someone else's finding, first pin down whether it measured **cognitive load**, **reading time**, or **answer accuracy**. Secondary write-ups blend the three, and blending them silently strengthens the claim.
- If you're unsure, downgrade to a range or a qualifier ("a few hundred milliseconds", "noticeably slower") and mark it as an estimate.

---

## R11 Metaphor quota: one per paragraph

A metaphor may **explain** a fact. It may not **stand in for** one.

```
Bad:  The models pulled out all the speed bumps, so reading it is like chewing a compressed biscuit; the reader is hauling cement bags.
Good: The models deleted these buffer words. The result is denser local information in each sentence, which costs more to read.
```

Count when you're done: how many metaphors in this paragraph? More than one — cut down to the most accurate.

**The most dangerous move is using a metaphor to cover a place you failed to explain.** The reader feels they understood; they didn't.
