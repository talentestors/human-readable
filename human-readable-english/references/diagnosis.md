# Diagnosis: nine countable smells

Every criterion is countable, so you never argue from taste.

---

## 1. The nine smells at a glance

| # | Smell | How to count | Example |
|---|---|---|---|
| 1 | **Subject-verb distance** | more than 8 words between the subject head and its verb | "The remediation plan for the weak-network white-screen issue, after the preloading rework, was mitigated." → 14 words |
| 2 | **Main clause swallowed by modifiers** | 3+ chained modifiers before the core noun, which arrives last | "event-data-based, new-user-only, multi-strategy cold-start config validation logic" |
| 3 | **Inanimate subject + animate verb** | subject is *approach / system / mechanism / framework / effort / strategy* + verb is *breathe / eat / notice / unlock / carry / drive* | "The new rule *unlocked* operational efficiency." |
| 4 | **Light verbs** | *perform / conduct / carry out / implement / achieve / facilitate / enable* + abstract noun | "We performed an optimization of export performance." |
| 5 | **Noun stacks** | 3+ nouns modifying one head noun | "customer churn prediction pipeline monitoring dashboard" |
| 6 | **Nouns in verb slots** | a noun where a verb belongs | "Let's calendar it." / "I'll inbox you." |
| 7 | **Abstraction drift** | a concrete action floated up to *framework / ecosystem / end-to-end / capability / visibility* | "Build an end-to-end observability framework to empower faster triage." |
| 8 | **Flat rhythm + em-dash chains** | 5 consecutive sentences within 30% of one length; dashes replacing causal/contrastive links | "The model got stronger — but people can't read it — that's not a coincidence." |
| 9 | **Metaphor overload** (the reverse tell) | 3+ metaphors in one paragraph, or a metaphor standing in for the fact | "like a compressed biscuit" → "like hauling cement bags" → "the model's dialect", back to back |

### Smell 9 is a trap

Smells 1–8 are **compressed-biscuit prose**: information packed too tight. Smell 9 is **stand-up-comic prose**: thinning the point with imagery and talking around the plain statement. Both are AI tone; the second is sneakier because it reads as *well written*.

**One metaphor per paragraph at most, and it may only explain a fact — never replace it.**

---

## 2. The English-specific high-frequency failure: mid-sentence subject drift

You start with A, the comma swaps in B, and the final verb belongs to B.

> "The API's response time **during peak hours**, **the on-call engineer** spent hours before finding a missing index."

The first half's subject is the response time; the second half's is the engineer. The reader is forced to reset at the comma. **You can't hear it reading silently — read it aloud and it collapses.**

---

## 3. The fastest check: the spine table

Turn each sentence into a triple. **A sentence you can't reduce to subject-verb-object is a sick sentence.**

| Sentence | Subject | Verb | Object | Distance | Can the subject do it? |
|---|---|---|---|---|---|
| The remediation plan …, following …, was mitigated | the plan | was mitigated | — | 14 words | borderline — a plan ships; it isn't mitigated |
| This mechanism effectively absorbs the business side's high-concurrency demands | this mechanism | absorbs | demands | 2 words | no — mechanisms don't absorb; people do |
| Through a review of the tracking pipeline, an improvement in data accuracy was achieved | (none) | achieved | improvement | — | no subject at all — smell 4, confirmed |

Fill the table for one page of a work item and the distribution of smells falls out. **Fix 1, 3, and 4 first** — those three do the most damage to reading speed.

---

## 4. Three numbers, don't conflate them

The commonest diagnostic error is calling three different quantities one thing:

| Quantity | Definition | Smell |
|---|---|---|
| **Subject-verb distance** | words from the subject head to its verb | #1 |
| **Head-noun position** | words from the start of the clause to the core noun | #2 |
| **Sentence length** | words from period to period | #8 / R3 |

Two sentences, two different numbers:

**A.** "The remediation of the export-timeout issue, where async tasks lacked a fallback mechanism, shipped in v2.3."

| Quantity | Value | Verdict |
|---|---|---|
| Subject head → verb | *remediation* (word 2) → *shipped* (word 14) = **12 words** | #1 fires |
| Head-noun position | word 2 | #2 does not |
| Sentence length | 14 words | fine |

**B.** "A multi-strategy, gray-release-capable, multi-tenant configuration center refactor shipped last week."

| Quantity | Value | Verdict |
|---|---|---|
| Head noun | *refactor*, word 8, behind three modifiers | #2 fires |
| Subject head → verb | 1 word | #1 does not |

Calling #2 "#1" sends you to the wrong surgery: you move the verb when what needs breaking up is the modifier stack — and moving the verb changes nothing.
