# Why AI-written English is hard to read

Three pathologies, in causal order. Once you've read this page you know where every rule downstream comes from.

**Theoretical baseline: Clark, Martin & Mahowald (2026), *Why is AI-generated language so hard to understand?* (NYU + UT Austin, [arXiv:2610.29162](https://arxiv.org/abs/2610.29162)).** Nine frontier models, five small open models, six features, two controlled comparisons, one mechanism test.

---

## Layer 1: subject and verb drift apart, and working memory overflows

Two words that depend on each other — subject and predicate, verb and object, noun and modifier — must be active in the reader's mind at once. Gibson's **Dependency Locality Theory** (Gibson, 1998, 2000) calls this *integration cost*: the more material sits between them, the more the first word's representation decays and the slower the retrieval.

Grodner & Gibson (2005) showed it cleanly: as they lengthened the relative clause in `The administrator [who the nurse (who was from the clinic)] supervised…`, reading time at `supervised` rose.

**In this paper's terms, layer 1 is *dependency length*.** The models use longer dependencies than human writers do.

---

## Layer 2: the verb doesn't fit the subject, so the reader stalls

Readers predict. See a subject and you pre-activate the predicates it plausibly takes. A high-frequency pairing ("the user clicks the button") lands instantly; a low-frequency one ("this redesign breathed new life into the funnel") misses, and the reader has to reclassify.

Clark, Martin & Mahowald (2026) measured this across nine frontier and five small models. One of the six features they scored is **inanimate subjects with animate verbs** — abstract nouns doing what only living things do:

- "The approach *eats* latency."
- "Silence *built* a milestone."
- "The pipeline *noticed* the problem."

The other five: **object relative clauses without `that`** (reduced relatives), **denominal verbs** ("calendar it"), **stacked nouns**, **dependency length** (layer 1), and **low-frequency / unattested n-grams**.

They also ran a **round-trip translation baseline** — each sentence translated out and back (English → Japanese → English, via NLLB-200), so the content is fixed and only the wording changes. The models' output stayed harder to read than that round-tripped paraphrase. **So this is a preference the models developed, not a side effect of formal register.**

> The test: **could a specific person or object actually do this?** If not, change the subject or change the verb.

---

## Layer 3: information density compressed into a brick

The **Uniform Information Density** hypothesis (Levy & Jaeger, 2007) says speakers instinctively spread high-information material out and pad the hard parts with cheap material — function words, optional conjunctions, explicit clause markers. English's optional `that` is the classic buffer. (This buffer framing comes from the UID literature, **not** from arXiv:2610.29162.)

Clark et al. (2026) found the models remove nearly all of these buffers: dropped relativizers, stacked nouns, nouns in verb slots, long clauses, rare collocations.

**Why?** Their hypothesis: human language is optimized for successful communication, while AI text is increasingly optimized for math, code, and reasoning — pressures that reward **information density** rather than intelligibility. They test it with a **length-penalty fine-tune**: reward a model for writing shorter, and its usage drifts away from human-like, toward exactly these constructions, even generalizing to sentence patterns never targeted in training.

**This is the counter-intuitive part, because it rules out the obvious fix: chopping sentences is wrong.**

Strip the connectives and the reader must reconstruct cause and contrast themselves; cognitive load goes *up*. Research on text simplification has criticized traditional readability formulas (FKGL, SMOG) for exactly this: they count sentence length and word length, which pushes models to delete logical connectives, and **comprehension effort rises**. (A general finding in that field, unrelated to arXiv:2610.29162 — cite a specific paper if you need one.)

> Compress **local density peaks**, not the number of sentences.
>
> And keep the metrics separate: that finding is about **cognitive load**. In controlled studies of properly simplified text, readers' **answer accuracy goes up**. Two different measures — secondary write-ups routinely conflate them.

---

## One-sentence summary

**AI English is hard to read not because it is too complex, but because it compresses what should be spread out and talks around what should be said plainly.**

The first is *compressed-biscuit prose* (smells 1–8). The second is *stand-up-comic prose* (smell 9).

---

## References

**The baseline this skill is built on**

- Clark, T. H., Martin, M. B., & Mahowald, K. (2026). *Why is AI-generated language so hard to understand?* arXiv:2610.29162. <https://arxiv.org/abs/2610.29162>
  NYU (first author) + UT Austin. Nine frontier models + five small open models; six features (inanimate subjects with animate verbs, low-frequency n-grams, dependency length, stacked nouns, reduced object relatives, denominal verbs); round-trip translation via Japanese (NLLB-200); length-penalty fine-tune as mechanism test.

**The underlying theory it builds on**

- Gibson, E. (1998). Linguistic complexity: Locality of syntactic dependencies. *Cognition*, 68(1), 1–76.
- Gibson, E. (2000). Dependency locality theory: A distance-based theory of linguistic complexity.
- Grodner, D., & Gibson, E. (2005). Consequences of the serial nature of linguistic input for sentential complexity. *Cognitive Science*, 29(2), 261–290.
- Levy, R., & Jaeger, T. F. (2007). Speakers optimize information density through syntactic reduction. *NIPS 19*.
- Jaeger, T. F. (2010). Redundancy and reduction: Speakers manage syntactic information density. *Cognitive Psychology*, 61(1), 23–62.

**Craft, not experiments**

- Sword, H. (2012). *Stylish Academic Writing* — "zombie nouns".
- "Mechanical chopping makes text harder": a stable observation in text simplification; cited here as a general finding, not tied to one paper.
