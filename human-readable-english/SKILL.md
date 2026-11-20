---
name: human-readable-english
description: Rewrite "AI-sounding" English into prose a person can read in one pass — for work items, bug reports, RFCs, docs, and status updates. Use when text feels bloated, nominalized, or hard to follow, or when asked to "say it plainly", "make this readable", "cut the AI tone", or to write a work item / bug description. Triggers: AI-sounding, hard to read, unclear, rewrite this, plain English, work item description, bug report, nominalization, zombie nouns, subject-verb distance.
---

# Plain English: make the main clause visible at a glance

## What this skill fixes

AI-written English has all the right words and no grammatical errors, yet three lines in your reader's eyes glaze over. The problem isn't vocabulary. It's that the sentence **strips out every buffer a reader needs, then packs the material that should be spread apart into one dense lump**.

In a work item the stakes are concrete: a teammate, a tester, or your future self has to scan for ten seconds and answer *"whose problem is this, where does it happen, what do you want me to do?"* If they read forty words without hitting a verb, they have to go back and re-find the subject. **Every re-read costs a unit of trust.**

This skill gives you two things:

1. **Countable diagnostics** — you don't have to judge "AI-ness" by feel.
2. **Specific rewrite moves** — each symptom maps to one operation, not to advice like "be more concise".

---

## Part 1: Why it's hard

**Theoretical baseline: Clark, Martin & Mahowald (2026), *Why is AI-generated language so hard to understand?* (NYU + UT Austin, [arXiv:2610.29162](https://arxiv.org/abs/2610.29162)).**

That paper does the three things this skill rests on: it quantifies, on the output of nine frontier models (plus five small ones), the psycholinguistic features known to slow human reading; it rules out "formal register" with a round-trip translation baseline; and it tests a mechanism with a length-penalty fine-tune.

The three layers below are ordered by cause, and each maps onto a feature class the paper measured:

- **Layer 1 → distance**: longer dependencies
- **Layer 2 → collocation**: inanimate subjects with animate verbs
- **Layer 3 → density**: the removed speed bumps (reduced relatives, stacked nouns, low-frequency n-grams)

The underlying theories behind layers 1 and 3 come from Gibson and from Levy & Jaeger. **What the 2026 paper adds is the connection to LLMs, with measurements and a mechanism** — and that connection is what this skill is built on.

### Layer 1: subject and verb drift apart, and working memory overflows

Two words that depend on each other — subject and predicate, verb and object, noun and modifier — must be active in the reader's mind at the same time. Gibson's **Dependency Locality Theory** (Gibson, 1998, 2000) prices this as *integration cost*: the more material sits between them, the faster the first word's representation decays and the slower the retrieval.

Grodner & Gibson (2005) showed it cleanly: as they lengthened the relative clause in `The administrator [who the nurse (who was from the clinic)] supervised…`, reading time at `supervised` rose steadily.

**This is smell #1.** English wears it differently from Chinese: instead of a thirty-character pre-modifier, you get a subject that leaves the stage and comes back three commas later — often inside a sentence that has quietly changed subjects halfway through.

> The fix for the white screen that appeared on first load of the homepage under weak network conditions and with no local cache, after the resource-preloading rework landed, was mitigated.

Nobody knows what the subject is doing until `was mitigated`, twenty-eight words later. The head noun arrived last, behind a wall of qualifiers with nowhere to attach.

### Layer 2: the verb doesn't fit the subject, so the reader stalls

Readers predict. See a subject, and you pre-activate the predicates it plausibly takes. High-frequency pairings ("the user clicks the button") land instantly; low-frequency pairings ("this redesign breathed new life into the funnel") miss, and the reader has to reclassify.

Clark, Martin & Mahowald (2026) — NYU and UT Austin, preprint [arXiv:2610.29162](https://arxiv.org/abs/2610.29162), *Why is AI-generated language so hard to understand?* — measured this across nine frontier models plus five small ones. One feature it found overrepresented: **inanimate subjects with animate verbs** — abstract nouns doing things only living things do. "This approach *eats* latency." "The pipeline *noticed* the anomaly." "Silence *built* a milestone."

They also ran a **round-trip translation baseline** — the same content paraphrased by translating out and back — and the models' output was still harder than that, so this isn't just formal register. And they reproduced it with a **length-penalty fine-tune**, so it's a preference the model develops.

**This is smell #2.** The test is simple: **could a specific person or object actually do this?** If not, change the subject or change the verb.

### Layer 3: information density got compressed into a brick

The **Uniform Information Density** hypothesis (Levy & Jaeger, 2007) says speakers instinctively spread high-information material out and pad the hard parts with cheap material — function words, optional conjunctions, explicit clause markers. English's optional `that` is a 200-millisecond airbag.

Models remove nearly all of these speed bumps: dropped complementizers, stacked nouns, nouns turned into verbs, very long clauses, rare collocations. The 2026 paper's explanation is **length penalties during post-training** — reward shorter output, and "short" helps the model (fewer tokens) while hurting the reader (more effort). It backs this with a proof of concept: fine-tune a model under a length penalty, and its usage drifts away from human-like, toward exactly the constructions above.

**This matters because it rules out the obvious fix.** Mechanically chopping sentences is wrong. Strip the connectives and the reader must reconstruct the logic; cognitive load goes *up*. **Compress local density peaks, not sentence count.**

---

## Part 2: Eight countable smells

Every criterion below is countable, so you never have to argue from taste.

| # | Smell | How to count | Example |
|---|---|---|---|
| 1 | **Subject-verb distance** | more than 8 words between the subject head and its verb | "The remediation plan for the weak-network white-screen issue, following the completion of the preloading rework, was mitigated." → 28 words |
| 2 | **Main clause swallowed by modifiers** | 3+ chained modifiers before the core noun | "a multi-strategy, gray-release-capable, multi-tenant configuration-center refactor" |
| 3 | **Inanimate subject + animate verb** | subject is *approach / system / mechanism / framework / effort / strategy* + verb is *breathe / eat / notice / unlock / carry / drive* | "The new rule *unlocked* operational efficiency." |
| 4 | **Light verbs** | *perform / conduct / carry out / implement / achieve / facilitate / enable* + abstract noun | "We performed an optimization of export performance." |
| 5 | **Noun stacks** | 3+ nouns modifying one head noun | "customer churn prediction pipeline monitoring dashboard" |
| 6 | **Nouns shoved into verb slots** | a noun sitting where a verb belongs | "Let's calendar it." / "I'll inbox you." |
| 7 | **Abstraction drift** | a concrete action floated up to *framework / ecosystem / end-to-end / capability / visibility* | "Build an end-to-end observability framework to empower faster triage." |
| 8 | **Flat rhythm + em-dash chains** | 5 consecutive sentences within 30% of the same length; dashes replacing causal or contrastive links | "The model got stronger — but people can't read it — that's not a coincidence." |

Plus one English-specific failure you'll hit constantly: **mid-sentence subject drift**. You start with A, the comma swaps in B, and the final verb belongs to B.

> "The API's response time **during peak hours**, **the on-call engineer** spent hours before finding a missing index."

The first half's subject is the response time; the second half's is the engineer. The reader resets at the comma. **You won't hear it reading silently; read it aloud and it collapses.**

---

## Part 3: Nine hard rules

Apply in order, then re-check.

### R1 Lead with the main clause: who + did what + to what. Push modifiers after.

```
Bad:  The remediation of the export-timeout issue, where async tasks lacked a fallback mechanism, shipped in v2.3.
Good: v2.3 fixed one thing: bulk exports could time out, and nothing caught the failure.
```

Land the spine first, then add conditions. Never open with "Regarding the… of the… that…".

### R2 Keep subject and verb adjacent: ≤ 8 words apart, no comma between them

If you need a condition, move it after the main clause or give it its own sentence.

```
Bad:  The white screen that appeared on first load under weak network conditions with an empty cache disappeared after preloading shipped.
Good: The white screen is gone. It hit weak networks on a first load with an empty cache; preloading shipped and it stopped.
```

### R3 One main clause per sentence, 15–35 words

Over 40 words, split. **But restore the connective when you split** — *because / so / but / if*. Two unrelated short sentences are just a different kind of hard.

```
Bad (chopped):  The export failed. The user retried. It failed again.
Good: The export failed, the user retried, and it failed again, because the task queue was full.
```

### R4 The subject must be able to do the verb

Three options: use an agent (person, team, service, script, endpoint) · use passive or a "we" clause · rewrite as cause → effect.

```
Bad:  The refactor gave the order pipeline room to breathe.
Good: After the refactor, changing the order module no longer means touching three other files.
```

> *Service / script / endpoint / job* can be subjects — they really act ("the service returns 500"). *Framework / ecosystem / capability / visibility / dimension* cannot.

### R5 Give the action back to the verb; delete light verbs

"performed an optimization" → "made it faster". "achieved a reduction" → "went from 8s to 2s". "conducted an investigation" → "checked".

```
Bad:  We performed an optimization of export performance, achieving a significant reduction in response time.
Good: Exports went from 8 seconds to 2.
```

**Prefer numbers.** *Significant / substantial / meaningful / notable* is where AI tone lives.

### R6 More than two modifiers: cut them out

Pull the longest modifier into its own sentence, or make it a trailing note.

```
Bad:  a cold-start validation logic that is based on event data, targets new users only, and supports switching between multiple strategies
Good: Cold-start config has a new validation step. It reads event data, only applies to new users, and can switch between strategies.
```

### R7 Make the link explicit: dashes and bare juxtaposition become because / but / if

```
Bad:  Traffic went up tenfold — the batch job didn't change — now everything runs two hours late.
Good: Traffic went up tenfold, but the batch job didn't change with it, so every run now finishes two hours late.
```

### R8 Define jargon where it first appears

Don't leave acronyms for the reader to guess. Drop half a sentence of plain language right next to the term.

```
Bad:  Cold-start depends on CF recall, which is sparse.
Good: New users have no history (cold start), so we rely on collaborative filtering (CF — "people like you liked this"), and with too little data that recommendation is unreliable.
```

### R9 Fidelity: not one atomic proposition may be lost

Rewriting changes **packaging**, never **facts**. Numbers, units, conditions, boundaries, exceptions, timestamps — check each one. Dropping a qualifier because the sentence reads better is the most serious failure mode in this skill.

---

## Part 4: The work-item structure

This is the main battlefield. Goal: **anyone scans for ten seconds and knows who hit what, how bad it is, and what you want.**

### Template

```markdown
## One-liner
<Who> hits <what problem> when <in what situation>.

## Current behavior
- <Fact 1: observable symptom>
- <Fact 2: reproduction steps or trigger>
- <Fact 3: data / logs / version>

## Impact
<Who is affected, how often, at what cost. Numbers if you have them.>

## Expected
- [ ] <verifiable outcome 1>
- [ ] <verifiable outcome 2>

## Out of scope
<Draw the boundary explicitly.>
```

### Before and after (bug)

**Before — one sentence, 78 words, subject and verb 40 words apart:**

> The current stability posture of the Export Center module under large-data-volume scenarios presents a risk, since the absence of an effective fallback for async task timeouts causes users performing bulk exports to experience tasks remaining in a processing state for extended periods without clear feedback, impacting user experience and business efficiency; it is recommended that the relevant pipeline be reviewed and exception-handling logic be improved so as to enhance system robustness.

**After:**

```markdown
## One-liner
When a user exports more than 100k rows, the job sits in "processing" and they can't tell if it's alive.

## Current behavior
- Exports over 100k rows show no status change for 30+ minutes.
- Backend logs record no timeout; the frontend shows no error.
- Repro: Export Center → select all orders (~120k rows) → Export.

## Impact
Support hand-builds a file for the user while it hangs — about 40 minutes each. Six times last week.

## Expected
- [ ] After 5 minutes without progress, the status reads "still running, about N minutes left".
- [ ] After 30 minutes, the job fails automatically and offers a retry.
- [ ] On failure, the reason is written to the log.

## Out of scope
Export format and permission logic stay as they are.
```

Every symptom is gone: light verbs ("presents a risk", "performing exports", "enhance robustness"), abstraction drift ("relevant pipeline", "system robustness"), subject-verb distance, and a subject that is a module rather than a person.

### Requirement and tech-debt templates

See `references/workitem-templates.md`.

---

## Part 5: Workflow

Don't rewrite by feel in one pass. Run these five steps; the last two are the quality gate.

### Step 1 Extract the spine table

Turn each sentence into a triple:

| Sentence | Subject | Verb | Object | Distance | Can the subject do it? |
|---|---|---|---|---|---|
| The remediation plan …, following …, was mitigated | the plan | was mitigated | — | 28 | borderline — a plan ships, it isn't mitigated |

**A sentence you can't turn into a triple is a sick sentence.** This check is faster and more reliable than reading the paragraph ten times.

### Step 2 Operate by symptom

Tag each sentence 1–8 against Part 2, then rewrite in R1→R9 order. Fix 1, 3, and 4 first — they do the most damage.

### Step 3 Restore the links

After splitting, check whether every causal / contrastive / conditional relationship still has an explicit word carrying it. If not, add one.

### Step 4 Verify fidelity

List every number, condition, and proper noun in the original; find each one in the rewrite. **Anything you can't find is something you lost.**

### Step 5 Read it aloud

Where you stumble is where you edit — this is the step that catches mid-sentence subject drift.

---

## Part 6: Pre-delivery checklist

- [ ] Every sentence yields a subject and a verb?
- [ ] Subject head to verb ≤ 8 words, with no comma between them?
- [ ] No main clause buried under "regarding the… of the… that…"?
- [ ] Subjects are things that can act (person / team / service), not *framework / capability / ecosystem*?
- [ ] No *perform / implement / conduct / facilitate* + abstract noun?
- [ ] No more than two modifiers before the head noun?
- [ ] Sentences over 40 words split, with connectives restored?
- [ ] Jargon defined on first use?
- [ ] Numbers, conditions, boundaries, exceptions all preserved?
- [ ] Reads aloud without stumbling, and a reader can answer "who hit what, what do you want" at a glance?

Quantitative spot-check: sample five random sentences and measure average length, median subject-verb distance, and the share of inanimate-subject sentences. Targets: 20–30 words, ≤ 8 words, zero.

---

## Part 7: Don't do these

| Anti-pattern | Why it fails |
|---|---|
| Chopping sentences to make them short | Removing connectives pushes the logic onto the reader; cognitive load rises (the documented failure mode in text-simplification research) |
| Stacking "we" as a slogan | "We will continue to optimize the experience" has no agent — it isn't a person, it's air |
| Deleting qualifiers and exceptions | Readability presupposes fidelity. This is the worst failure |
| Converting to slide-speak (one line per idea, all noun phrases) | Noun phrases have no subject or verb — a different flavor of unreadable |
| Replacing every technical term with plain words | Keep the terms; define them in place (R8) |
| Fixing sentences but not structure | If the order of information is wrong, smooth sentences don't save the document |

---

## Part 8: Ready-to-paste prompt snippet

See `references/prompt-snippet.md` — about 400 words, for use as a system prompt for another agent or inside a work-item template.

---

## References

Cite author and year, not "research shows". Every principle above traces to one of these.

**Primary source — the baseline this skill is built on**

- Clark, T. H., Martin, M. B., & Mahowald, K. (2026). *Why is AI-generated language so hard to understand?* arXiv:2610.29162. <https://arxiv.org/abs/2610.29162>
  NYU (first author) + UT Austin. Nine frontier models plus five small ones; constructions measured include object relatives, long dependencies, low-frequency n-grams, stacked nouns, and inanimate subjects with animate verbs; includes a round-trip translation baseline and a length-penalty fine-tuning experiment.
  **What this skill takes from it:** Layer 2 (inanimate subjects + animate verbs), and in Layer 3 the measured set of removed speed bumps plus the information-density / length-penalty account and its proof of concept.

**Underlying theory — where each layer actually comes from**

- Gibson, E. (1998). Linguistic complexity: Locality of syntactic dependencies. *Cognition*, 68(1), 1–76.
- Gibson, E. (2000). Dependency locality theory: A distance-based theory of linguistic complexity. — the integration-cost account behind Layer 1.
- Grodner, D., & Gibson, E. (2005). Consequences of the serial nature of linguistic input for sentential complexity. *Cognitive Science*, 29(2), 261–290. — the reading-time evidence for Layer 1.
- Levy, R., & Jaeger, T. F. (2007). Speakers optimize information density through syntactic reduction. *NIPS 19*. — the UID hypothesis in Layer 3. **UID is not from the 2026 paper**; that paper uses it to explain model behavior.
- Jaeger, T. F. (2010). Redundancy and reduction: Speakers manage syntactic information density. *Cognitive Psychology*, 61(1), 23–62. — the fuller experimental treatment.

**Writing craft (not experimental papers)**

- Sword, H. (2012). *Stylish Academic Writing*. Harvard University Press. — "zombie nouns".
- On "mechanical chopping makes text harder": a stable observation in the text-simplification literature. Cited here as a general finding, not tied to one paper — replace with a verifiable citation if you need one.
