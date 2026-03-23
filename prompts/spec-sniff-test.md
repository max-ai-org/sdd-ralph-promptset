You are producing a **spec sniff report**: a candid read of where the documentation is harder or messier than it needs to be, without changing product scope or intent. Begin from the project rules and the conventions this team uses for specs—how outcomes and requirements are written, how product and engineering docs link, how IDs and traceability work—and settle on what part of the spec landscape you are reviewing (an outcome, a component, a subtree of docs, or similar).

Use the **catalogs below** as a shared vocabulary. For each problem you report, name the **smell** (or closest match) and state a **refactoring direction**: bring in **candidate technique(s)** and sketch what ought to shift and where you are steering, so **another agent** can continue in their own way with concrete edits and structure. In **`spec-sniff.md`**, techniques land better when they are not naked labels alone—let a short phrase carry what each one is trying to accomplish (the catalog descriptions are a fine source to lean on), so someone who has never heard the name still grasps the gist. A **refactoring direction** is meant to orient, not to spell out every edit; it is closer to a signpost than a recipe. Infer this repository’s templates, glossaries, and ID schemes from the specs themselves; those artifacts hold authoritative detail beyond names and descriptions here.

If a file already claims to be a spec sniff report, look for it at **`spec-sniff.md`** in the project root unless the run context names another path. Read it if it exists, but treat every smell listed there as **unverified gossip** until you have checked it yourself. Your job is still to produce **one** authoritative report. Do your own pass over the specs first; use the old file only to confirm, correct, or retire entries.

Hunt for **spec smells** using the catalog so you do not rely on a single narrow lens. Force at least two genuinely different ways of slicing the same material (for example by outcome, by component, by readability, by link integrity, by template fit, or by how fine-grained requirements are). Combine or choose the views that surface the most useful problems. Stress-test whatever list you have: ask what structural problems a narrow view would miss, and what a skeptical reviewer would say you glossed over. Adjust only when you find a real blind spot; sometimes the first list already holds up.

If you had a prior report, walk every old smell: keep it only if it still holds, and drop or mark resolved anything that does not, with a brief reason where that helps the next reader.

Write the result to **`spec-sniff.md`** in the project root unless context overrides the path. Each entry should read like something the next person can run with: where the issue lives, what is off (a **named smell** from the catalog when it helps), and a **refactoring direction** that names the techniques you have in mind while saying in plain language what those techniques are about and how you would like the spec to read, with meaning and traceability treated as the guardrails. You are not drafting a procedure or line-by-line checklist—leave room for judgment—only enough narrative that the direction feels grounded. Explain how you scoped the review and stress-tested your list. If you reconciled an older file, say which entries survived, which you rejected, and what is new. Order by impact on clarity or consistency. No sneaky scope or intent changes.

You may call the analysis **finished** when you have actually used at least two framings, done a critic-style pass, treated any prior report as unverified input, produced a prioritized actionable file, and honestly believe another lap would not materially improve the list. If the scope is unclear or you cannot meet that bar, you will end with failure as described below—but **do not** put `<promise>` on any earlier line.

If you met the bar, put `<promise>SUCCESS</promise>` on the **last line** of your response. If you did not, put `<promise>FAILURE</promise>` on the **last line** and explain briefly.


## Catalog: spec smells

Smell groups for documentation and requirements-style artifacts. Use names from this catalog when describing problems; they anchor the **refactoring direction** you recommend. Adapt to this project’s doc types and patterns.

### Grounding & scope

Where the obligation sits relative to intent, layer, and context.

| Smell | Description |
|--------|-------------|
| Orphan obligation | A stated requirement or outcome has no clear parent intent, source, or owning artifact. |
| Abstraction mismatch | The amount of detail or vagueness does not fit the layer (e.g. product vs component vs sprint artifact). |
| Unbounded scope | Who must satisfy the obligation, what it applies to, or when it applies is left implicit across the text. |
| Heading-carried meaning | Applicability, scope, or obligation lives only in titles or section hierarchy, not in the spec body. |

### Statement craft & precision

Wording and structure of individual statements or fields.

| Smell | Description |
|--------|-------------|
| Bundled obligation | Multiple independent “musts” or outcomes are fused in one sentence, bullet, or field. |
| Weasel wording | Subjective or ungraded adjectives and adverbs replace criteria readers can evaluate consistently. |
| Escape clause | Hedging phrases defer judgment (“where possible”, “as appropriate”) without naming who decides or when it applies. |
| Ambiguous referent | Pronouns, overloaded nouns, or vague “the system” make it unclear what must hold. |
| Untestable phrasing | Reasonable readers cannot describe an observation or check that would show satisfaction or failure. |

### Structure & template fit

Fit to the team’s agreed shape for specs (sections, slots, record types).

| Smell | Description |
|--------|-------------|
| Pattern violation | Content ignores the project’s agreed pattern (required headings, slots, tables, or front matter). |
| Field leakage | Information sits in the wrong structural bucket (e.g. rationale mixed into the normative obligation). |
| Metadata in prose | Identifiers, owners, status, or trace hints only appear in running text instead of stable fields or links. |
| Missing structural anchor | A required template element is absent (e.g. missing ID block, acceptance section, or owner field). |

### Trace & navigation

Links, identifiers, and whether following references actually works.

| Smell | Description |
|--------|-------------|
| Broken or stale link | Cross-references point to moved, removed, or renamed targets. |
| Trace gap | The team’s process expects an upward or downward pointer, but none exists. |
| Identifier chaos | Duplicate IDs, unstable handles, or different names for the same logical item across artifacts. |
| Trace theater | Links or IDs are present but fail a literal follow (wrong target, wrong abstraction level, or decorative only). |

### Verifiability & corpus integrity

Evidence paths and whether the spec set tells one coherent story.

| Smell | Description |
|--------|-------------|
| Duplicate claim | The same obligation appears in more than one place with different wording and no single canonical copy. |
| Glossary drift | One concept appears under incompatible names or definitions in different documents. |
| Contradictory requirement | Mutually exclusive obligations appear without explicit precedence, scope split, or supersession. |
| Numeric or unit skew | Targets, limits, or tolerances disagree across artifacts with no recorded reconciliation. |


## Catalog: refactoring techniques

Techniques for **specifications and docs**. In a **refactoring direction** they read as intent rather than a script; folding in the idea behind a technique next to its name keeps **`spec-sniff.md`** legible for people who have not internalized the whole catalog.

### Decompose & clarify

Split and untangle meaning while preserving intent.

| Technique | Description |
|-----------|-------------|
| Split obligation | Break independent “musts” into separate statements or records, each with its own trace and test hook where needed. |
| Extract applicability | State modes, preconditions, environments, or user classes explicitly instead of burying them in one dense block. |
| Move rationale aside | Relocate intent, history, or motivation out of the normative obligation into rationale, notes, or metadata. |
| Active explicit subject | Name who or what shall act, hold state, or be responsible so the obligation has a clear actor. |
| Positive restatement | Prefer a positive obligation when it removes ambiguity, double negatives, or unclear scope of negation. |
| Untangle conditionals | Replace nested if/unless chains with structured conditions, numbered cases, or a small decision table. |
| Remove escape clause | Replace hedging with explicit scope, a bounded exception list, or a named owner/decision record. |

### Define & quantify

Make terms and measures concrete.

| Technique | Description |
|-----------|-------------|
| Introduce glossary entry | Define the term once in a shared glossary and reference it from requirements. |
| Replace vague qualifier | Swap subjective words for thresholds, examples, or explicitly bounded lists. |
| Add measurable threshold | Attach numbers, SLOs, latency/accuracy limits, or other tolerances with units and context. |
| Enumerate allowed set | Close open-ended lists with an explicit inventory or a clear rule for what may be added later. |
| Name magic literal | Replace unexplained constants or absolutes with named values and documented meaning. |
| Clarify modality policy | Align must, should, and may with team rules and fix statements that contradict that policy. |

### Anchor & weave

Repair the graph of intent and implementation artifacts.

| Technique | Description |
|-----------|-------------|
| Add parent link | Tie the item to an outcome, epic, higher requirement, or concept it is intended to satisfy. |
| Add child link | Point to derived specs, tasks, interfaces, or tests that elaborate or realize the item. |
| Fix cross-reference | Update or create links and anchors so navigation matches the current repository layout. |
| Document trace gap | When a parent or source is missing, record the gap, risk, and proposed owner instead of pretending trace exists. |
| Stabilize identifier | Assign or repair a unique, stable ID and naming convention aligned with project standards. |

### Refit & organize

Shape and layout without changing the underlying obligation.

| Technique | Description |
|-----------|-------------|
| Move to correct field | Relocate content into the template slot or section the team expects for that kind of information. |
| Apply project pattern | Restate using the agreed pattern (slots, headings, tables) without altering product meaning. |
| Improve scanability | Use lists, short paragraphs, or tables so obligations and exceptions are easy to find and compare. |
| Collapse duplication | Merge near-identical text into one canonical statement; replace copies with a pointer to the canonical copy. |

### Evidence & harmonize

Connect to checks and align the corpus.

| Technique | Description |
|-----------|-------------|
| Bind acceptance criterion | Link or add observable success conditions, scenario IDs, or examples that clarify “done.” |
| Attach verification hook | Name the artifact, test suite, metric, review, or method that will demonstrate satisfaction. |
| Add interface or data contract | Specify boundaries (APIs, schemas, events, files) needed to build or test against the text. |
| Deduplicate across corpus | Remove or merge repeated obligations across files; establish a single source of truth with references. |
| Resolve conflict explicitly | Record decision, precedence, supersession, or scope split when two statements disagree. |
| Harmonize terminology | Choose one canonical term and align sibling requirements and linked documents to use it. |
