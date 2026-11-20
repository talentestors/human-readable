# Work-item templates and worked examples

Three high-frequency work-item types, each with a different skeleton. What they share: **the one-liner reads in a single breath, and every bullet carries one main clause.**

---

## 1. Bug / defect

```markdown
## One-liner
<Who> hits <what problem> when <in what situation>.

## Current behavior
- Symptom: <something observable — another person could see it too>
- Repro: <1. 2. 3. steps, with concrete inputs>
- Environment: <version / platform / account type / data volume>

## Impact
<Who is affected, how often, at what cost. Numbers if you have them.>

## Expected
- [ ] <verifiable outcome>
- [ ] <verifiable outcome>

## Leads (optional)
<Suspected direction, relevant logs, similar issues. Mark these as guesses — "suspect", "possibly".>

## Out of scope
<Draw the boundary explicitly.>
```

### Example: dropped payment callbacks

```markdown
## One-liner
After WeChat Pay succeeds, 0.3% of orders still show "pending payment" here until the user refreshes.

## Current behavior
- ~12 orders per day since Aug 1 (about 4,000 orders/day).
- WeChat's callback log shows a successful push; our Nginx log has no matching request.
- Repro: in staging, set the callback endpoint to respond after 6 seconds — reproduces every time.
- Environment: production, v3.8.1, began after the new gateway shipped on 2026-08-01.

## Impact
Users pay twice or complain. Support handles ~10 tickets a day at ~15 minutes each.

## Expected
- [ ] With a 6-second callback delay, order status still updates within 10 seconds.
- [ ] Failed callbacks retry 3 times, 30 seconds apart.
- [ ] No update after 1 minute raises an alert to the #payments-incidents channel.

## Leads
Suspect the new gateway's read timeout is set to 5s, shorter than WeChat's 6s callback. Unconfirmed.

## Out of scope
No change to payment channels or the order state machine.
```

---

## 2. Requirement / feature

```markdown
## One-liner
<Who> needs <what>, because <why>.

## Background
<How they cope today, and where it breaks. Two or three sentences — no industry-trend preamble.>

## What we want
- <Capability 1, one sentence>
- <Capability 2, one sentence>

## Acceptance
- [ ] <Observable outcome, with a number or a concrete action>
- [ ] <Observable outcome>

## Out of scope
<What this version explicitly will not do.>
```

### Example: filtered export

```markdown
## One-liner
Ops needs to filter by order date and product category before exporting, because today they can only export everything and filter by hand.

## Background
Ops runs a weekly category review: export 120k rows, filter to three categories in Excel, 40 minutes each time. Another doubling of volume will lock Excel up.

## What we want
- The export dialog filters by date range and product category.
- Filters match the list view's current filters — no second, parallel filter model.

## Acceptance
- [ ] "Last 7 days + Beauty" produces a file containing only those orders.
- [ ] 120k rows export in under 2 minutes.
- [ ] With no filters selected, behavior is unchanged (full export).

## Out of scope
No scheduled exports, no custom export templates.
```

---

## 3. Tech debt / refactor

Tech-debt write-ups turn into essays more easily than anything else. **The test is whether a reader can judge "the cost of not doing it" and "the payoff of doing it."**

```markdown
## One-liner
<Module>'s <problem> makes <who> spend <how much> every time they <do what>.

## What it costs now
- <A specific incident or measured delay that actually happened>
- <Another one>

## What we want instead
<One sentence on the new structure.>

## Done when
- [ ] <Measurable indicator>
- [ ] <Measurable indicator>

## Risk
<What could break, and how we roll back.>
```

### Example: splitting the order service

```markdown
## One-liner
The order service mixes checkout, fulfillment, and after-sales in one process, so touching after-sales means redeploying checkout — and every deploy runs 40 minutes of full regression.

## What it costs now
- Three deploys last month, 40 minutes of regression each; two rolled back because after-sales changes broke checkout.
- After-sales peaks at 20× checkout's QPS; we can only scale them together, about ¥8k extra per month.

## What we want instead
Split into order-core (checkout + fulfillment) and order-aftersale (after-sales), sharing one database and communicating through domain events.

## Done when
- [ ] After-sales ships independently; pre-release regression runs only after-sales cases, under 10 minutes.
- [ ] The two services scale independently.
- [ ] Checkout P99 stays at or below today's 120ms.

## Risk
Cross-service transactional consistency. Plan: event-based compensation plus reconciliation, two weeks of dual-write canary, fall back to in-process calls if it misbehaves.
```

---

## 4. Universal rewrite target: ten AI-flavored sentences → plain English

Use these as reference points while rewriting. The left column is real, high-frequency phrasing.

| AI-flavored original | Symptom | Plain English |
|---|---|---|
| The remediation plan for the weak-network white-screen issue, following completion of the preloading rework, was mitigated. | 28-word subject-verb distance | The homepage showed a white screen on a first load over a weak network. After we shipped preloading, that mostly stopped. |
| Through a review of the event-tracking pipeline, an improvement in data accuracy was achieved. | Light verbs + no agent | Tracking used to miscount because events were reported twice. After the review, the numbers match. |
| This mechanism effectively absorbs the high-concurrency demands from the business side. | Inanimate subject + animate verb | At 8,000 QPS peak, this still holds up. |
| Build an end-to-end observability framework to empower faster issue triage. | Abstraction drift | Add logs and tracing. When something breaks, you can see which step is slow. |
| It is recommended that the relevant pipeline be reviewed and exception handling improved to enhance system robustness. | Light verbs + abstraction + nothing testable | Retry timeouts three times automatically; fail after 30 minutes and log why. |
| This is a multi-strategy, gray-release-capable, multi-tenant configuration-center refactor. | Stacked modifiers | The config center needs three changes: multiple strategies, canary releases, tenant isolation. |
| User-perceived performance has been significantly optimized. | Too abstract to verify | First paint went from 3.2s to 1.1s. |
| Data volume growth drove an increase in processing time — batch logic was not adjusted accordingly — resulting in a task backlog. | Dash instead of connective | Traffic grew tenfold, but the batch job didn't change, so jobs started backing up. |
| Let's calendar it and then alignment it. | Nouns in verb slots | Let's put it on the calendar, then agree on timing. |
| In cold-start scenarios, CF recall suffers from sparsity, necessitating the introduction of content-side signals as a supplement. | Undefined jargon + noun stacks | New users have no history, so "people like you" recommendations are inaccurate — we need product tags to fill some of the gap. |
