# Homework W02 — Refactoring Worksheet: Extract an Interface (on paper)

<!-- Individual homework, due before the Week 3 lab. **No programming required** — you do this
with pseudocode and a small class diagram. Bring it to the lab, finished or half-finished. -->

> **How to use this template.** Do the work in your team repository under `03-design/`, then fill this worksheet. Delete this block when you commit.
>
> **The task.** Take the messy `Order` from Exercise 2.1 and extract **one interface and two implementations** — e.g. `PaymentMethod` with `CardPayment` and `CampusCardPayment`. Express it as **pseudocode plus a class diagram**. Writing runnable code is optional (Bonus C2) and never expected.
>
> **Pseudocode refresher:** `Class Order` · `− lines : OrderLine[0..*]` (private, zero or more) · `+ pay() : Receipt` (public operation) · `PaymentMethod (interface)` · `Class X implements Y` · `Class B extends A`. Full conventions: `01-slides/Pseudocode-Conventions.md`.

---

## 1. Before — what you started from

> Write out the operation you are replacing. Keep it honest: a list of `if` / `switch` branches on a type is expected, and is exactly the point.

```text
# BEFORE

+ checkout(order)
    if type = CARD    -> chargeCard(order)
    ...
```

| Question | Answer |
|---|---|
| Which operation did you change? |  |
| What did it branch on? |  |
| How many branches did you delete? |  |

## 2. The interface

```text
______________ (interface)
    + ______________(______________) : ______________
```

| Question | Answer |
|---|---|
| Why this name? |  |
| What is the contract in one sentence? |  |
| What does the caller NOT need to know any more? |  |

## 3. Two implementations

```text
Class ______________ implements ______________
    + ______________(______________) : ______________
        ...

Class ______________ implements ______________
    + ______________(______________) : ______________
        ...
```

| Implementation | How it honours the contract | What it needs from outside |
|---|---|---|
|  |  |  |

## 4. The call site — the one line that matters

```text
# AFTER

r = method.pay(order.total())
```

> The goal: **no `if` and no `switch`** left in `Order`. If your call site still asks "which type?", you are not finished.

- [ ] `Order` no longer mentions any concrete payment class.
- [ ] `Order` has no `if` / `switch` on a payment type.
- [ ] Adding a third implementation would require **no change** to `Order`.

## 5. The OCP test

> Imagine the instructor announces next semester: *"We are adding ApplePay."*

| Question | Answer |
|---|---|
| Which of your boxes do you touch? |  |
| Which files would NOT change? |  |
| One sentence: why is this "open for extension, closed for modification"? |  |

## 6. The diagram (sketch)

> Draw the interface, the two implementations, and `Order` pointing at the interface — not at the implementations. Photo or PlantUML, either is fine; save it as `03-design/payment-extract.png` / `.puml`.

## 7. Optional — code sketch (Bonus C2 only)

> Only if you want to. Any language. If you do, add a short paragraph: what surprised you when you actually wrote it. Push it under `03-design/` and say so in your contribution log.
>
> **Not writing a single line of code costs you nothing in this course.**
