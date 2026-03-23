You are writing an **implementation gap analysis**: where running code diverges from what the specifications say should happen—missing behavior, mismatched behavior, or implementation choices that contradict documented requirements. Ground yourself in the project rules and where specs live (product intent, acceptance criteria, engineering specs), then choose the slice of code or scripts you are comparing to those specs.

If a file already presents itself as an implementation gap analysis, default path is **`implementation-gap-analysis.md`** in the project root unless context specifies otherwise. Read it if it exists, but every claim there is **unverified** until checked against both spec and code. Produce one authoritative report: analyze from scratch first, then use the old file only to verify, reject, or extend.

Compare implementation to spec using at least two genuinely different lenses (for example by requirement, by component, by data flow, or by public interfaces). Combine or choose what surfaces the truest mismatches. Typical gaps include behavior the spec promises but code does not deliver, code that does things the spec forbids or omits, or contradictions between layers of documentation and what ships. Stress-test the list: what would a single slice miss, and what would a critic say you ignored or overweighted? Refine when you find a real hole.

If you inherited a prior analysis, reconcile claim by claim against spec and implementation. Keep verified and new gaps; remove or resolve what no longer holds, with a brief rationale when useful.

Write the result to **`implementation-gap-analysis.md`** in the project root unless context overrides. Each gap should tie to a location, what the spec says, and what the implementation actually does. Note scoping and stress-testing. If you updated an older file, record verified, rejected, and new items. If no gaps remain, state that and how you verified. Prioritize by impact or how critical the spec is.

Call the analysis **done** when two framings were used, a critic pass happened, any prior file was treated as untrusted input, the written report is prioritized and actionable, and another iteration would not materially improve coverage. If scope is unclear or you cannot reach that bar, plan to fail as below, without `<promise>` until the final line.

On the **last line**, output `<promise>SUCCESS</promise>` if you met the bar, otherwise `<promise>FAILURE</promise>` with a brief explanation.
