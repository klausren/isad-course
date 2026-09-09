# Exercise 2.1 — Responsibility Worksheet

<!-- In-class worksheet, Week 2 (~25 min). Not an M0 deliverable — but keep it: you will reuse the judgement in W6–W7 (domain model), W11 (GRASP) and W12 (SOLID). -->

> **How to use this template.** Work in pairs first, ten minutes, then compare. Fill the tables by hand or in this file. Delete this block when you hand it in.

---

## The class (slide 30)

```java
public class Order {
    void placeOrder()      { ... }
    void chargeCustomer()  { ... }
    void notifyRider()     { ... }
    void printReceipt()    { ... }
    void updateInventory() { ... }
    void sendSms()         { ... }
    void applyDiscount()   { ... }
}
```

**Your task: list the distinct responsibilities — not the methods.**
If your answer has seven rows, you copied the slide.

## Step 1 — Responsibilities, not methods

| # | Responsibility (a noun phrase) | Methods belonging to it | The reason it would change |
|---|---|---|---|
| 1 |  |  |  |
| 2 |  |  |  |
| 3 |  |  |  |
| 4 |  |  |  |
| 5 |  |  |  |

> **A responsibility is a reason to change.** Two methods that change for the same reason belong together. Two that change for different reasons do not.

**The test for every row:** say out loud *"this changes when ______ changes."* If two rows finish that sentence the same way, merge them.

## Step 2 — Who should own it?

| Responsibility | Class that should own it | One sentence why |
|---|---|---|
|  |  |  |
|  |  |  |
|  |  |  |
|  |  |  |
|  |  |  |

> Name the class after the **responsibility**, not the data: `PaymentService`, `NotificationService`, `PricingCalculator`.

## Step 3 — The one you argued about

| Question | Answer |
|---|---|
| The method I could not place confidently |  |
| The two places it could go |  |
| What I would need to know to decide |  |

> `updateInventory()` is genuinely arguable. The argument is the learning, not the answer.

---

## Done when

- [ ] **3–5 responsibility rows** — not 7 method rows.
- [ ] Every row's "reason to change" is **different** from every other row's.
- [ ] Every row names an owning class.
- [ ] You can say the whole table out loud in under 60 seconds.

## Stuck?

| Symptom | Fix |
|---|---|
| "I just listed the methods again." | Ask *what makes this method change?*, not *what does this method do?* |
| Everything feels like one responsibility | Push harder: does a new payment type force you to touch inventory? No. Then they are separate. |
| Only two responsibilities found | Look at `updateInventory()` and `placeOrder()` again — one is about stock, the other is about orchestration. |
| Cannot name an owning class | Name it after the behaviour, not the noun on the diagram. |

---

*We meet this class again in **Week 11**, when GRASP tells us how to fix it properly. Keep this worksheet.*
