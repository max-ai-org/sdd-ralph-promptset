You are producing a **code sniff report**: where the code is more complex or tangled than it needs to be, with **behavior preserved**—no new features, no scope creep. Start from the project rules and workflow, including how to build and test, and decide which code you are inspecting (a file, package, component, or similar).

Use the **catalogs below** as a shared vocabulary. For each problem you report, name the **smell** (or closest match) and state a **refactoring direction**: bring in **candidate technique(s)** and sketch what ought to shift and where you are steering, so **another agent** can continue in their own way with concrete steps, tests, and edits. In **`code-sniff.md`**, techniques land better when they are not naked labels alone—let a short phrase carry what each one is trying to accomplish (the catalog descriptions are a fine source to lean on), so someone who has never heard the name still grasps the gist. A **refactoring direction** is meant to orient, not to spell out every keystroke; it is closer to a signpost than a recipe. [SourceMaking’s refactoring hub](https://sourcemaking.com/refactoring) is the place for full mechanics when you need more than names and descriptions here.

If a prior sniff report exists, default path is **`code-sniff.md`** in the project root unless context says otherwise. Read it if present, but every smell in it is **unverified** until you have checked the current code yourself. Produce a single authoritative report: analyze fresh first, then use the old file only to validate, correct, or remove entries.

Look for **code smells**—needless complexity, duplication, weak boundaries or names, coupling issues, and anything that could be simpler without changing what the program does. Use the smell list to avoid a single narrow lens. Force at least two different ways of slicing the same code (for example by complexity hotspots, coupling, readability, duplication, or interface boundaries). Combine or choose the views that reveal the most useful problems. Then stress-test your list: what would a narrow reading miss, and what would a harsh reviewer say you skipped? Expand or tighten only when you find a genuine gap; keeping the list unchanged is fine if it already holds.

If there was an earlier report, reconcile it line by line against the current code. Keep only smells that still apply; drop or mark resolved what no longer does, with a short reason when it helps.

Write the outcome to **`code-sniff.md`** in the project root unless context overrides. Each entry should read like something the next person can run with: where the issue lives, what is off (a **named smell** from the catalog when it helps), and a **refactoring direction** that names the techniques you have in mind while saying in plain language what those techniques are about and how you would like this code to move, with behavior preserved as the usual guardrail. You are not drafting a procedure or line-by-line checklist—leave room for judgment—only enough narrative that the direction feels grounded. Note how you scoped the review and stress-tested the list. If you updated an existing file, record what you verified, rejected, and newly found. Prioritize by maintainability impact.

Finish only when two framings were genuinely used, a blind-spot or critic pass happened, any prior file was treated as untrusted input, the written report is prioritized and actionable, and you believe another iteration would not materially improve the list. If scope is unclear or you cannot reach that bar, plan to fail as below—without emitting `<promise>` until the last line.

On the **last line**: `<promise>SUCCESS</promise>` if you met the bar, otherwise `<promise>FAILURE</promise>` with a brief explanation.


## Catalog: code smells

Smell descriptions in the spirit of SourceMaking. Use names from this catalog when describing problems; they anchor the **refactoring direction** you recommend. Category pages: `https://sourcemaking.com/refactoring/smells/…`

**Bloaters** — code, methods, or classes grown unwieldy.

| Smell | Description |
|--------|-----------|
| Long Method | A method has grown so long that its behavior is hard to follow and change safely. |
| Large Class | One class hoards too much state or behavior and becomes a change magnet. |
| Primitive Obsession | Domain ideas are modeled as strings and numbers instead of dedicated types. |
| Long Parameter List | Too many parameters make calls brittle and obscure what the method really needs. |
| Data Clumps | The same bunch of fields or parameters travel together and belong in one object. |

**Object-orientation abusers** — incomplete or incorrect use of OO.

| Smell | Description |
|--------|-----------|
| Switch Statements | Type-based branching scattered in switches (or if-chains) fights polymorphism. |
| Temporary Field | An instance field is only meaningful in some code paths, confusing the object’s invariant. |
| Refused Bequest | A subclass inherits API or state it does not want and works around the parent. |
| Alternative Classes with Different Interfaces | Two classes do the same job but expose incompatible interfaces to callers. |

**Change preventers** — one logical change forces edits in many places or tangled ripples.

| Smell | Description |
|--------|-----------|
| Divergent Change | One class changes for many unrelated reasons because it mixes concerns. |
| Shotgun Surgery | One kind of change forces many small edits across lots of classes. |
| Parallel Inheritance Hierarchies | Every subclass on one side needs a matching subclass on another tree. |

**Dispensables** — noise or cost without earning its keep.

| Smell | Description |
|--------|-----------|
| Comments | Comments compensate for unclear code instead of fixing the code’s expression. |
| Duplicate Code | The same logic exists in more than one place, so fixes must be repeated. |
| Lazy Class | A class does so little it should be folded into its collaborators. |
| Data Class | A class is mostly getters and setters with behavior living elsewhere. |
| Dead Code | Code is never executed or never reached and only obscures the real flow. |
| Speculative Generality | Abstractions exist for imagined futures that never arrived. |

**Couplers** — excessive coupling or wrong delegation boundaries.

| Smell | Description |
|--------|-----------|
| Feature Envy | A method reaches into another object’s data more than it uses its own. |
| Inappropriate Intimacy | Classes depend on each other’s private details instead of stable interfaces. |
| Message Chains | Callers chain through intermediaries (`a.getB().getC()`) and break when structure shifts. |
| Middle Man | A class exists mostly to forward calls and adds little of its own. |
| Incomplete Library Class | A reused class is almost right but missing behavior you keep patching around. |


## Catalog: refactoring techniques

Technique descriptions in the spirit of SourceMaking. In a **refactoring direction** they read as intent rather than a script; folding in the idea behind a technique next to its name keeps **`code-sniff.md`** legible for people who have not internalized the whole catalog. Detail pages: `https://sourcemaking.com/refactoring/…`

**Composing methods** — streamline methods, remove duplication, clarify control flow.

| Technique | Description |
|-----------|-----------|
| Extract Method | Move a coherent fragment into a new method and call it from the original site. |
| Inline Method | Replace a trivial delegating method with its body at call sites when the name adds no clarity. |
| Extract Variable | Name the result of a complex expression so the intent reads in the surrounding code. |
| Inline Temp | Remove a temp that is only assigned once and does not clarify anything. |
| Replace Temp with Query | Replace a temp whose value is derivable with a method (or query) that computes it. |
| Split Temporary Variable | Replace one temp reused for different meanings with separate variables per meaning. |
| Remove Assignments to Parameters | Stop reassigning parameters; use locals so callers’ mental model stays valid. |
| Replace Method with Method Object | Turn a long method with many temps into an object whose fields hold the state and `compute()` runs the logic. |
| Substitute Algorithm | Swap the body of a method for a clearer or faster algorithm with the same outcome. |

**Moving features between objects** — relocate behavior and data between classes without changing outward behavior.

| Technique | Description |
|-----------|-----------|
| Move Method | Place a method on the class that owns the data it uses most. |
| Move Field | Relocate a field to the class that is most responsible for it. |
| Extract Class | Split one class doing two jobs by moving part of its state and behavior into a new class. |
| Inline Class | Merge a class whose responsibilities belong naturally inside another. |
| Hide Delegate | Have the host expose a simple method instead of leaking the delegate object. |
| Remove Middle Man | Let clients talk to the real object when the wrapper only forwards everything. |
| Introduce Foreign Method | Add a helper function (on your side) when you cannot change the source class. |
| Introduce Local Extension | Subclass or wrap a library class to add the behavior you need in one place. |

**Organizing data** — richer types and sane associations.

| Technique | Description |
|-----------|-----------|
| Self Encapsulate Field | Access a field only through getters/setters even inside the owning class. |
| Replace Data Value with Object | Turn a primitive (or simple value) into an object when behavior or validation appears. |
| Change Value to Reference | Share one instance across many references when identity matters, not just value. |
| Change Reference to Value | Make an immutable value object when identity and sharing are unnecessary. |
| Replace Array with Object | Replace positional array slots with named fields on a dedicated type. |
| Duplicate Observed Data | Sync domain data with UI (or other views) via proper observation instead of manual mirroring. |
| Change Unidirectional Association to Bidirectional | Add a back-pointer when both sides must navigate the relationship. |
| Change Bidirectional Association to Unidirectional | Drop the redundant link when one direction suffices. |
| Replace Magic Number with Symbolic Constant | Name a literal whose meaning matters to readers and maintainers. |
| Encapsulate Field | Hide a public field behind accessors so representation can evolve. |
| Encapsulate Collection | Return read-only views or copies so callers cannot break invariants on collections. |
| Replace Type Code with Class | Replace a coded primitive with a class that represents the category safely. |
| Replace Type Code with Subclasses | Use subclasses when behavior varies by type and instances are stable. |
| Replace Type Code with State/Strategy | Use state or strategy objects when the type can change at runtime or behavior varies a lot. |
| Replace Subclass with Fields | Collapse subclasses that differ only by constant data into one class with fields. |

**Simplifying conditional expressions** — branching easier to read, test, and extend.

| Technique | Description |
|-----------|-----------|
| Decompose Conditional | Extract conditions, then-parts, and else-parts into named methods. |
| Consolidate Conditional Expression | Merge duplicated boolean checks into one expressive predicate. |
| Consolidate Duplicate Conditional Fragments | Hoist identical code from branches so it runs once after the fork. |
| Remove Control Flag | Replace a boolean flag that steers loops with `break`, `return`, or structured exits. |
| Replace Nested Conditional with Guard Clauses | Handle exceptional cases with early returns and keep the happy path flat. |
| Replace Conditional with Polymorphism | Dispatch on type with polymorphic methods instead of big switches or if-ladders. |
| Introduce Null Object | Replace repeated null checks with a benign object that implements the same interface. |
| Introduce Assertion | Document and enforce assumptions that must hold for the code to be correct. |

**Simplifying method calls** — clearer APIs: names, parameters, error style.

| Technique | Description |
|-----------|-----------|
| Rename Method | Give a method a name that says what it does for its callers. |
| Add Parameter | Extend a method’s inputs when callers must supply new data. |
| Remove Parameter | Drop an unused or redundant parameter to shrink the surface area. |
| Separate Query from Modifier | Split a method that returns a value and has side effects into a getter and a command. |
| Parameterize Method | Replace several methods that differ only by literals with one method taking the varying value. |
| Replace Parameter with Explicit Methods | Replace a flag-controlled method with separate methods per case for clarity. |
| Preserve Whole Object | Pass an object instead of pulling many fields out as separate parameters. |
| Replace Parameter with Method Call | Have the callee derive a value the caller was computing and passing in. |
| Introduce Parameter Object | Group parameters that clump together into a single object argument. |
| Remove Setting Method | Delete a setter when a field should not change after construction. |
| Hide Method | Narrow visibility when a method is only for internal use. |
| Replace Constructor with Factory Method | Use a named factory when construction is non-trivial or should be polymorphic. |
| Replace Error Code with Exception | Signal exceptional failures with exceptions instead of magic return values. |
| Replace Exception with Test | Use a precondition check instead of exceptions for expected control flow. |

**Dealing with generalisation** — inheritance, interfaces, subclassing vs delegation.

| Technique | Description |
|-----------|-----------|
| Pull Up Field | Move a common field to the superclass to remove duplication. |
| Pull Up Method | Move identical or near-identical methods from subclasses to the superclass. |
| Pull Up Constructor Body | Move shared constructor initialization into the superclass constructor. |
| Push Down Method | Move a method to only the subclasses that actually need it. |
| Push Down Field | Move a field out of the superclass when only some subclasses use it. |
| Extract Subclass | Create a subclass for a subset of features that vary from the rest of the class. |
| Extract Superclass | Factor common parts of two classes into a new shared superclass. |
| Extract Interface | Define a narrow interface that multiple clients can depend on instead of concrete classes. |
| Collapse Hierarchy | Merge superclass and subclass when the distinction no longer pays for itself. |
| Form Template Method | Structure shared algorithm steps in a superclass with hooks for varying steps in subclasses. |
| Replace Inheritance with Delegation | Prefer composition over subclassing when behavior should be swapped or shared flexibly. |
| Replace Delegation with Inheritance | Use subclassing when delegation duplicates the whole interface of the delegate. |
