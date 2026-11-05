# Lab 09 · W11 — GRASP: Who Does What, and Why You Wrote It Down

> **ISAD · Fall 2026** · Lab block (last 2 h of the weekly 4 h)
> **Milestone**: **M3 in progress** — your GRASP justifications are due at the end of this lab.
> **Your material**: your W10 design class diagram v1 + your W09 domain model
> **Slides**: `W11-GRASP-Principles.pptx`, pages 1–32 (the lecture part)
> **Deliverable format**: the **five-column** table (see §3)

**Purpose of this lab.** You drew a design class diagram last week. It is not wrong yet — but it is
not *defended* yet. Today you find out whether anyone else can continue your model, and you write
down the reasoning in a form a reviewer can check.

**No programming today.** You write **decisions**, not code.

> **Note.** The deck uses `Order` / `OrderManager` as teaching examples. **Use your own classes.**
> That `OrderManager` is the same one from week two's Exercise 2.1 — the class you listed the
> responsibilities of nine weeks ago. It comes back as the exhibit today.

---

## 0. Before You Start (~5 min)

- [ ] Your W10 design class diagram v1 is open
- [ ] Your W09 domain model is open beside it
- [ ] Your W10 `operation-traceability.md` is open
- [ ] You know today's four standing roles: **Lead** (keeps time), **Recorder** (owns the decisions file, and only that file), **Reviewer** (checks every justification against a principle), **Release Manager** (pushes and confirms the files are in the repo)
- [ ] You can find the class in your model with **the most reasons to change** — you found it last week, but look again with today's vocabulary

> **Course default, restated:** the **decisions** are the deliverable this week, not the diagram.

---

## 1. What the Lecture Gave You

| From the lecture | The one line you need |
|---|---|
| Responsibility = knowing + doing | Two questions, not one |
| **Information Expert** | Put the work with the class that holds the data — and write down the coupling it costs |
| **Creator** | Whose lifetime contains the new object's? Five criteria, read in order |
| **Controller** | Receives the system event, delegates the decisions |
| **Low Coupling / High Cohesion** | Count, do not feel. One coin, two sides |
| The other four | Know what they are for, so you can rule them out |
| The format | **Principle → Decision → Consequence → Alternative → Trace** |

**The sentence to remember:** *a principle without a decision is not an answer, and a decision without a consequence is not an argument.*

---

## 2. Exercise 11.1 — GRASP Drill (~25 min)

> **Goal.** Recognise the principle behind a situation, and say what decision follows.

Work through the six situations on slides P35–P36 **before** looking at the answers. Write your
answer in this shape:

```
| # | Principle | Decision | The cost |
|---|---|---|---|
| 1 | | | |
```

**For each situation, answer three things**
1. **Which principle** applies (name it precisely — "Information Expert", not "good design").
2. **What decision follows** — the concrete change to your model.
3. **The cost** — what new dependency or new class you just accepted.

**Then check against the answers (P36).** For each one you got wrong or argued differently, write
one line in the open-questions file: which principle *almost* applied, and why.

> **Watch for the trap.** Sometimes two principles apply and they disagree. The answer is not
> "both" — the answer is **which one won, and why**. Saying so is worth more than being right.

---

## 3. Exercise 11.2 — Justify Three Responsibilities (~30 min)

> **Goal.** Turn three of your own decisions into a written argument.

Pick **three responsibilities** from your own design class diagram. For each, fill in **all five
columns**:

| Column | What goes in it | Example |
|---|---|---|
| **Principle** | The rule you applied, named | Information Expert — the class that holds the data does the work |
| **Decision** | What you decided, in one line | `Order` computes `total()` from its own lines, not a `PricingService` |
| **Consequence** | What it costs you | `Order` now depends on `OrderLine`; the pricing rule lives in one place |
| **Alternative** | What you rejected, and why | `PricingService` — it would need every line anyway, so we would pay the coupling *and* add a class |
| **Trace** | Where the requirement came from | R-14, and the `total()` message in our W08 sequence diagram |

**The Consequence column is the one that makes it an argument.** If you cannot write it, you did
not think it through.

**The Alternative column is the one that makes it engineering.** If you did not consider a second
option, you did not choose — you just landed somewhere.

### Where the three come from

Pick deliberately:

- [ ] **One** where you followed Information Expert
- [ ] **One** where you created an object (Creator)
- [ ] **One** where you deliberately **did not** put something in the obvious class

That third one is the interesting one. "I put `printReceipt` in a `ReceiptPrinter` rather than in
`Order` because printing is presentation, not order business" is a judgement. "I put it in
`ReceiptPrinter`" is a fact.

---

## 4. Exercise 11.3 — Refactor the God Class (~25 min)

> **Goal.** Split the class in your model with the most reasons to change.

### Step 1 — Find it (~8 min)

In your own design class diagram, find the class with **the most unrelated reasons to change**.
Count them: how many different business events would make you edit this class?

Write the count down. If the answer is one or two, you do not have one — look for the class that
everybody touches.

### Step 2 — Split it (~12 min)

Split it into **at least three** classes. For each new class, write **one sentence** on why it
exists:

```
ReceiptPrinter — exists to hold the printing job, so Order does not depend on a printer.
Notification — exists to hold how and where we notify, so Order does not know about channels.
Payment      — exists to hold the payment and its state, so Order does not perform charges.
```

Each sentence must be a **reason to change**, not a description. "Holds the receipt data" is a
description. "Changes when the receipt format changes" is a reason.

### Step 3 — Check the cost (~5 min)

- [ ] Does any class now have **more than one** reason to change? Split it again.
- [ ] Did the split make anything **less** readable? If a reviewer now has to open three files to
      understand one order, you over-split.
- [ ] Write down what the split **cost**: more classes, more files, more to coordinate.

> **The honest answer.** The class count went up. That is not a failure — it is the point. What
> matters is that each class now has one reason to change and can be tested on its own.

---

## 5. Submitting M3 (GRASP justifications)

> Full push/tag protocol: [`../SUBMIT-INSTRUCTIONS-W06-EN.md`](../SUBMIT-INSTRUCTIONS-W06-EN.md)
> (your tag for this milestone is **`m3-v1`**).

### Files you commit

```
docs/design/decision-log.md          ← the five-column table, three rows per team member
docs/design/refactor-notes.md         ← Exercise 11.3: the split and its cost
docs/design/open-questions.md         ← updated: which principle almost applied
```

### What goes in `decision-log.md`

One table per team member. Each row is one decision.

| Principle | Decision | Consequence | Alternative rejected | Trace |
|---|---|---|---|---|
| | | | | |

### What goes in `open-questions.md`

| Question | Which principle almost applied | What you need to know | Who will you ask |
|---|---|---|---|
| | | | |

**An empty open-questions file is a red flag.** A real one is evidence of judgement.

---

## 6. Homework

1. Read Larman on the GRASP chapters. **Take it slowly** — this is the heart of the course.
2. Write **one responsibility argument** for your own project, in the five-column format.
3. For every class in your design class diagram, write one sentence: *"This class exists
   because …"*. Bring it to week twelve.

---

## 7. What the Reviewer Will Check

| # | Check | How it fails |
|---|---|---|
| 1 | Principle named precisely | "Good design" instead of "Information Expert" |
| 2 | Decision is a concrete change | "Better structure" |
| 3 | Consequence is stated | Empty cell, or "none" |
| 4 | Alternative considered and rejected | Empty cell |
| 5 | Trace to a requirement ID | No ID |
| 6 | The god class split, each new class with one reason | Two reasons in one sentence |
| 7 | Splitting cost acknowledged | "More classes" with no further thought |
| 8 | Open questions written down | Silent guesses |

> **Note.** The deck's exercise pages (P34–P37) use a different case. Use **your own project**.

---

## 8. Two Things That Are Not Acceptable

**"I applied GRASP."** Which principle? What decision? What did it cost? A row that cannot
answer those three is not a justification.

**"Information Expert says put it with the data, so I did."** That is the rule without the
judgement. Information Expert has a cost — coupling — and you must have decided that the cost was
worth paying. If you did not write the cost down, you did not make the decision; you followed a
rule and hoped.
