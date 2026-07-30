---
name: elibme
description: Calibrate an explanation to Mel's specific reader profile — a Biomedical Engineer with 12 years in IT/web/AI (keep that register at full density, never dumb it down) who is rusty on clinical terminology and novice in scientific-research methodology (define those inline, briefly, on first use — no full tutorial, no assuming he already knows). Use when the user says "elibme", "explain like I'm a BME", invokes /elibme, or asks for something "more professional than eli5 but not as dense as usual" — and proactively whenever a reply is about to lean on clinical or research-methodology jargon undefined, or reach for an analogy that crosses from one domain into the other.
---

# elibme — ground it, don't flatten it

*Elibme* — explain like I'm a Biomedical Engineer — is what you say when an explanation either
talks down to you on the tech side or assumes fluency you don't have on the clinical/research
side. This skill exists because both failure modes happened in the same conversation.

**Who reads the output:** a Biomedical Engineer, 12 years deep in IT/web development, ~2 years
seriously into AI and building toward AI-engineer/CTO. Fluent in software, infrastructure,
LLMs, data pipelines — that register needs **zero simplification**. Rusty on clinical
terminology. Novice in scientific-research methodology (cohorts, denominators, gold standards,
blinding, the shape of a study). Not a beginner in either — a professional who needs the
unfamiliar 20% named plainly, not the familiar 80% re-explained.

**Rule zero — two registers, not one:** this reader is not "less technical," he is
*asymmetrically* technical. Treat software/AI/infra content exactly as you would with any
technical peer. Treat clinical and research-methodology content as genuinely new material that
needs a plain-language handle the first time it appears.

**Rule one — this makes it easier to read, not longer.** The job is swapping a jargon word for a
plain clause, not adding paragraphs. If defining three terms doubles or triples the length of
the passage, that's not elibme working — that's a tutorial, and tutorials are the thing this
skill exists to avoid. A correctly-elibme'd passage is close to the length of the dense version:
the original sentence, plus a short parenthetical per unfamiliar term, and nothing else new.

---

## The one thing that actually causes the overwhelm

**Cross-domain analogies.** Explaining a clinical concept via a software metaphor ("think of a
gold standard like a test suite") or a research-methodology concept via a tech one adds a
translation step — the reader now has to map the analogy correctly *and* extract the real
meaning, and a wrong or strained mapping teaches the wrong thing. This is the specific trigger
that was named directly: analogies from clinical/research to deep tech "trip him up."

**Do this instead: explain each domain directly, in its own plain terms.** A denominator is
"the total group a percentage is measured against — the number on the bottom of the fraction."
A gold standard is "the answer key — a value someone verified by hand, that other results get
checked against." No metaphor required. Plain language is not the same as dumbing down.

---

## Output shape

- **Professional prose**, not a bulleted ELI5 list and not a dense wall of unexplained jargon.
  Short paragraphs are fine; heavy nested bullets are not the default register here.
- **Define on first use, then use freely.** A clinical or research-methodology term gets a
  short inline clause or parenthetical the first time it appears in a reply — "the denominator
  (the total group a rate is measured against)" — and after that, use the term bare. Don't
  re-define it every time; that reads as condescending on the second pass.
- **Technical/software/AI terms get no such treatment.** No inline definitions for things like
  regex, JSONB, LLM, pipeline, extraction — that register is assumed fluent.
- **Numbers and evidence stay concrete.** Don't compress away the specifics that make a claim
  checkable — file paths, counts, percentages, what was actually measured. This skill changes
  *how* something is explained, not how much evidence backs it.
- **No new facts.** A definition explains what a term means, not what happened. Don't reach for
  extra context, backstory, or caveats that weren't in the original passage just because a term
  now has room to breathe — that's scope creep, and it's how a two-line update turns into a
  paragraph.

## Keep / drop

**Keep:** the actual technical mechanism, stated plainly. The one-line definition of any
clinical/research term on first use. The concrete evidence (numbers, what was checked, what
wasn't).

**Drop:** cross-domain analogies (see above). Apologetic hedging ("this might be a bit
technical, but..."). Re-explaining software/AI concepts he already has. Full tutorials on a
research-methodology concept when a one-clause definition would do — if he wants more depth on
a specific term, he'll ask, and he's explicitly comfortable diving deeper on request.

## Worked example

**Before (too dense — assumes research-methodology fluency):**
> The joint-count finding used N=62 as its denominator, but DECISIONS #58's census is N=64 —
> a cohort mismatch between the LLM's disease_variant classification and the ground-truth
> table-structure parse.

**After (elibme):**
> The joint-count finding used 62 notes as its denominator (the group size a rate is measured
> against) — but DECISIONS #58 confirms 64. The two totals track different-sized groups: 62 is
> the model's own guess, 64 is a hand-verified, ground-truth count.

Same information, same numbers, no analogy, no new facts — the only change is naming what
"denominator" and "ground-truth" mean, once, in plain clauses, instead of assuming the reader
already tracks that vocabulary. It runs under half again as long as the dense version, not four
times longer.

## When to fire

- **Explicit:** `/elibme`, "elibme this", "explain like I'm a BME", or a direct request for
  something "more professional than eli5 but not as dense as usual."
- **Proactive:** before sending a reply that is about to (a) use a clinical or
  research-methodology term with no definition anywhere nearby, or (b) reach for an analogy
  that crosses from clinical/research into tech or vice versa. Catch it before sending, not
  after — rewrite the sentence rather than append a glossary at the end.

## What this skill must not do

- Do not simplify or hedge on software/AI/infra content — that is not the gap being closed.
- Do not summarize or compress evidence — that is `mucho-texto`'s job, not this one. The two
  can stack: mucho-texto decides what's worth saying, elibme decides how to say the parts that
  cross into clinical/research territory.
- Do not add a term to a running glossary or ask the reader to look it up elsewhere — define it
  inline, right where it's used, in one clause.
