# Homework W02 — Refactoring Worksheet: Extract an Interface

<!-- Individual homework, due before the Week 3 lab. ~40 lines of code is plenty. Bring it to the lab — working or broken. -->

> **How to use this template.** Do the work in your team repository under `03-design/`, then fill this worksheet. Delete this block when you commit.
>
> **The task.** Take the messy `Order` from Exercise 2.1 and extract **one interface and two implementations** — e.g. `PaymentMethod` with `CardPayment` and `CampusCardPayment`. Small is fine.

---

## 1. Before — what you started from

> Paste the original method(s) you are replacing. Keep it honest: an `if`/`else` or `switch` on a type string is expected, and is exactly the point.

```java
// BEFORE
```

| Question | Answer |
|---|---|
| Which method did you change? |  |
| What did it branch on? |  |
| How many lines did you delete? |  |

## 2. The interface

```java
public interface ______________ {
    ______________ ______________(______________);
}
```

| Question | Answer |
|---|---|
| Why this name? |  |
| What is the contract in one sentence? |  |
| What does the caller NOT need to know any more? |  |

## 3. Two implementations

```java
public class ______________ implements ______________ {
    @Override public ______________ ______________(______________) {
        // ...
    }
}

public class ______________ implements ______________ {
    @Override public ______________ ______________(______________) {
        // ...
    }
}
```

| Implementation | How it honours the contract | What it needs from outside |
|---|---|---|
|  |  |  |
|  |  |  |

## 4. The call site — the one line that matters

```java
// AFTER
```

> The goal: **no `if` and no `switch`** left in `Order`. If your call site still asks "which type?", you are not finished.

- [ ] `Order` no longer mentions any concrete payment class.
- [ ] `Order` has no `if` / `switch` on a payment type.
- [ ] Adding a third implementation would require **no change** to `Order`.

## 5. The OCP test

> Imagine the instructor announces next semester: *"We are adding ApplePay."*

| Question | Answer |
|---|---|
| Which files change? |  |
| Which files do **not** change? |  |
| Is that acceptable? Why? |  |

If `Order` appears in the first list, the refactor did not work. Go back to §2.

## 6. Reflection (three sentences — this is what gets read)

1. What got easier? `______________________________________________`
2. What got harder? `______________________________________________`
3. One thing I still do not understand: `______________________________________________`

> Bring question 3 to the lab. *"I did not understand this"* is a better contribution than silence.

---

## Done when

- [ ] One interface, two implementations, committed under `03-design/`.
- [ ] The code compiles — or, if it does not, the broken version is committed with a note on the error.
- [ ] `Order` has no type-based branching left.
- [ ] §5 answers the "ApplePay" question with file names.
- [ ] Committed with a meaningful message (`Extract PaymentMethod interface from Order`), pushed to the team repository.

## Stuck?

| Symptom | Fix |
|---|---|
| The interface ends up with 5 methods | It is too big. One behaviour, one method. Split later. |
| Both implementations share code | Fine — put the shared part in an abstract class, but keep the interface as the type the caller sees (slide 26). |
| `Order` still needs to know which class to `new` | Correct, and that is next week's problem (creation is a separate responsibility — W11 GRASP). For now, pass it in from outside. |
| Nothing compiles and I am stuck | Commit the broken version with the error message in the commit body. Bring it Friday. |
