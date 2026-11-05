# Lab 08 · W10 — From Analysis to Design: Your Design Class Diagram v1

> **ISAD · Fall 2026** · Lab block (last 2 h of the weekly 4 h)
> **Milestone**: **M3 starts today** — your design class diagram v1 is due at the end of this lab.
> **Your material**: your own W08 use case specifications + your W09 domain model
> **Slides**: `W10-Design-Class-Diagrams.pptx`, pages 1–29 (the lecture part)
> **Deliverable format**: the **Principle → Decision → Consequence** table (see §4)

**Purpose of this lab.** Last week you decided *which concepts exist*. Today you decide *what they
can do*. Every message arrow in your W08 sequence diagrams becomes an operation on the class that
receives it. Every attribute becomes private with a getter or a query. Every association gets one
owner and one arrow. And the ones you cannot justify go into the open-questions file.

**No programming today.** You edit a `.puml` **text file** — a design model, not a program.

> **Note.** The deck uses `Order` / `OrderLine` / `Customer` / `Payment` as teaching examples.
> **Use your own classes.** The value of this exercise is entirely in the transfer.

---

## 0. Before You Start (~5 min)

- [ ] Your W08 use case specifications are open — the **main success path** and the **extension** paths of your three most important use cases
- [ ] Your W09 domain model is open beside them (`.puml` and/or the rendered image)
- [ ] PlantUML renders — verify it *now*, not at 40 minutes past the hour
- [ ] You know today's four standing roles: **Lead** (keeps time), **Recorder** (owns the `.puml` file, and only that file), **Reviewer** (checks every operation against a message arrow), **Release Manager** (pushes and confirms the file is in the repo)
- [ ] You have your M3 tracking file open (you created it in week nine)

> **Course default, restated:** *model in PlantUML, present in draw.io.* Both source files go in the
> repository. **A PNG on its own is not a submission.**

---

## 1. What the Lecture Gave You

| From the lecture | The one line you need |
|---|---|
| Design class = analysis class + what the code must do | The **same nouns**, plus operations |
| **Every message arrow becomes an operation** | On the class that **receives** it |
| Replies do **not** create operations | A reply answers a call you already counted |
| Visibility: `+` public, `−` private, `#` protected | **Attributes are private, always** |
| Navigability = permission to know | One arrow per association; name the owner |
| Contracts: pre / post | Precondition → the test setup; postcondition → the assertion |
| The traceability chain | `requirement → use case → message → operation → contract → test` |

**The sentence to remember:** *if you cannot point at the message arrow, you cannot have the operation.*

---

## 2. Exercise 10.1 — Operations from Messages (~35 min)

> **Goal.** Turn your sequence diagrams into operation signatures.

### Step 1 — List the messages (~12 min)

Open your W08 sequence diagram for your **three most important use cases**. For each message
arrow, write one line:

```
| # | Use case | From → To | Message label | Query or command? |
```

Rules:
- **Only arrows that arrive at a class you own.** If the arrow arrives at an external system
  (payment gateway, notification service), it is *their* operation, not yours — note it in the
  open-questions file instead.
- **Replies do not go in this table.** They are answers, not calls.
- Mark **query** (returns a value, changes nothing) or **command** (changes state). If you cannot
  tell, ask: "if I call this twice, do I get the same answer?"

### Step 2 — Write the signatures (~12 min)

For each operation, write a full signature:

```
+ placeOrder(items : List<OrderItem>) : Order
+ total() : Money                              ← query
+ cancel(reason : String) : void               ← command
```

- **Visibility**: `+` for anything another class calls. If only your class calls it, `−`.
- **Return type**: `void` when nothing useful comes back.
- **Types**: use your own domain's types. If a type does not exist yet, write it in the
  open-questions file rather than inventing a class today.

### Step 3 — Cross-check (~11 min)

For every operation, point at the message arrow it came from. **Recorder** writes the arrow's
identifier next to the operation in the tracking file.

- [ ] Every operation has a message arrow behind it
- [ ] No reply arrow became an operation
- [ ] Every query returns something, or is `void` on purpose
- [ ] Every operation that changes state is marked as a command

> **Reviewer note.** If you cannot find the arrow for an operation, that is the finding — write it
> in the open-questions file. Do not delete it quietly.

---

## 3. Exercise 10.2 — Visibility and Navigation (~25 min)

> **Goal.** Turn a working design class diagram into one a reviewer can check.

### Step 1 — Visibility audit (~10 min)

For **every** member of **every** class, set the visibility symbol. Use this table:

| Symptom | Fix |
|---|---|
| An attribute is `+` | Make it `−`, and add a query if someone needs to read it |
| A setter exists (`setStatus`, `setTotal`) | Replace with an intent-named command that validates (`cancel(reason)`, `markPaid()`) |
| An operation is `+` but no class calls it | Make it `−`, or delete it |
| Two classes write the same attribute | One of them should not be able to — find the owner |

### Step 2 — Navigation audit (~10 min)

For **every** association, answer three questions in writing:

1. **Who owns the link?** — one class, named in one line
2. **Which direction has the arrow?** — at most one
3. **What breaks if this arrow disappears?** — if the answer is "nothing", delete it

Then check for the four smell signals:

- [ ] Arrows both ways on one link
- [ ] A to-many and a to-one on the same pair
- [ ] Every class points at every class
- [ ] A cycle of three or more arrows

### Step 3 — Fix the worst one (~5 min)

Pick **one** association and fix its ownership. Write down what you changed and why.

> **The point of this exercise.** Most student design class diagrams have the same three problems:
> public attributes, two-way associations, and operations with no message behind them. Finding them
> yourself now is worth more than being told later.

---

## 4. Exercise 10.3 — Contracts (~15 min)

> **Goal.** Write contracts for the operations where a caller could get it wrong.

Pick **two** operations from your model — a command and a query if you have both. For each:

```
+ cancel(reason : String) : void
  pre:  status == PLACED
  pre:  reason is not empty
  post: status == CANCELLED
  post: the reserved stock is released
```

**Rules**
- **Preconditions belong to the caller.** If the condition is about the caller's own data, it is a
  precondition. If it is about the callee's internal state, say so explicitly.
- **Postconditions belong to the callee.** Write what is true afterwards, not what happened.
- **Two preconditions, two postconditions** is a good target. One is a start; five is a paragraph
  in disguise.
- **Do not write contracts for trivial getters.** "The object exists" is not a contract.

Then write the **test** that comes from each contract, in one line:

```
test_cancel_rejects_paid_order:
  given  an order with status PLACED
  when   cancel("changed mind")
  then   status == CANCELLED
  and    the reserved stock is released
```

- [ ] Every contract has a matching test line
- [ ] One test covers a **failing** precondition — write it down even if you cannot run it

---

## 5. Submitting M3 (Design Class Diagram v1)

> Full push/tag protocol: [`../SUBMIT-INSTRUCTIONS-W06-EN.md`](../SUBMIT-INSTRUCTIONS-W06-EN.md)
> (the same push → tag → verify procedure; your tag for this milestone is **`m3-v1`**).

### Files you commit

```
docs/design/design-class-diagram.puml        ← the model source
docs/design/design-class-diagram.png         ← the rendered image
docs/design/operation-traceability.md        ← Exercise 10.1's table
docs/design/contracts.md                     ← Exercise 10.3's contracts and tests
docs/design/open-questions.md                ← everything you could not decide
```

### What goes in `operation-traceability.md`

The table from Exercise 10.1, plus one more column:

```
| # | Use case | From → To | Message | Kind | Operation | Requirement ID |
```

### What goes in `open-questions.md`

| Question | Which principle/rule almost applied | What you need to know to decide | Who will you ask |
|---|---|---|---|
| e.g. Does `Finding` belong to `Analysis` or to `Regimen`? | Information Expert — both hold part of the data | Does a Finding ever exist without an Analysis? | client / instructor |

**An empty open-questions file is a red flag.** A real one is evidence of judgement.

---

## 6. Homework

1. Read Larman on design class diagrams and contracts (as assigned).
2. **Trace three messages → three operations** in your own project, one paragraph of rationale each.
3. For each of your three classes, write one sentence: *"This class exists because …"*. If you
   cannot, the class may not survive week eleven's GRASP review.

---

## 7. What the Reviewer Will Check

| # | Check | How it fails |
|---|---|---|
| 1 | Every operation traces to a message arrow | Operation with no arrow |
| 2 | Visibility set on every member | Public attribute |
| 3 | No setter-named operations | `setStatus` |
| 4 | One owner per association, one arrow | Two arrows on one link |
| 5 | Signatures have types | `placeOrder()` with no types |
| 6 | Contracts on the operations that need them | Public operation with no pre/post |
| 7 | Open questions written down | Silent guesses |

> **Note.** The deck's exercise pages (P31–P34) use a different case. Use **your own project**.
> The whole point of M3 is that it is yours.

---

## 8. A Note on the "Nothing to Change" Answer

If you conclude that one of your classes needs no operations at all, that is a legitimate finding
— but write it down and say why. "This class has no operations because it is a value object with
no behaviour beyond equality" is a finding. A class with no operations and no explanation is a
question you did not ask.
