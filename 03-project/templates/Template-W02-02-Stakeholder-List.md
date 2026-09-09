# Stakeholder List — CampusBites Team __

<!-- M0 deliverable ② · Due **Fri Sep 11** · pass / fail · Save as `01-requirements/stakeholder-list.md` -->

> **How to use this template.** Fill the main table with **5–8 curated stakeholders**, then keep your longer Week 1 brainstorm in the appendix. Delete this block and the `> Hint:` lines before you tag `m0`.
>
> **Two traps.** (1) A stakeholder is not the same as a user — someone can be affected without ever logging in. (2) M0 asks for a *curated* list, not a dump: choose for **coverage**, not for length.

---

## 1. Curated stakeholders (5–8)

| # | Stakeholder | User? (✔/✖) | What they want from the system | Why they have a stake | Where we heard it (source) | Priority |
|---|---|---|---|---|---|---|
| 1 |  |  |  |  |  | High / Med / Low |
| 2 |  |  |  |  |  |  |
| 3 |  |  |  |  |  |  |
| 4 |  |  |  |  |  |  |
| 5 |  |  |  |  |  |  |
| 6 |  |  |  |  |  |  |
| 7 |  |  |  |  |  |  |
| 8 |  |  |  |  |  |  |

**Rules of the table**

- At least **2 rows marked ✖** (affected but never logs in).
- Every row needs a real "why" — not a job title. *"The canteen admin needs compliance reports"* is a why. *"Admin"* is not.
- "Where we heard it" is either the CampusBites brief (Guidebook §2), a class discussion, or an observation you actually made. Write `brief §2`, `W01 class`, or `observed`. Do not invent interviews you did not do.

## 2. Coverage check

Tick every column you cover. An unticked column is a blind spot — and blind spots are exactly how real projects fail.

| Perspective | Covered by (name or ✗) | Note |
|---|---|---|
| **Demand side** — the person who orders |  |  |
| **Supply side** — the person who prepares/delivers |  |  |
| **Operations** — someone who keeps the service running day to day |  |  |
| **Money / compliance** — someone who cares about payment, refunds, rules |  |  |
| **Technical** — an external system or team we must integrate with |  |  |

## 3. Three questions we still cannot answer

Write the questions you would ask a real client if you had one. You will carry these into the Week 5 cross-team client review.

1. `______________________________________________`
2. `______________________________________________`
3. `______________________________________________`

---

## Appendix — the long list (Week 1 brainstorm)

> Not graded, not curated. Keep it: in **Week 4** this list becomes your **actor list** for the use case diagram, and you will be glad you did not delete it.

| Stakeholder | User? | One-line note |
|---|---|---|
|  |  |  |
|  |  |  |
|  |  |  |
|  |  |  |
|  |  |  |
|  |  |  |
|  |  |  |
|  |  |  |
|  |  |  |
|  |  |  |

---

## Quality bar

| ✗ Weak row | ✓ Strong row |
|---|---|
| `Student` · ✔ · `orders food` | `Student living in the north dorm` · ✔ · `wants hot food without queueing 20 min at the canteen` · `loses 30 min of every lunch break to it` |
| `Admin` · ✔ · `manages stuff` | `Canteen compliance officer` · ✖ · `needs a monthly report of every order and refund` · `legally accountable for food-safety traceability` |
| `IT` · ✖ · `technical` | `Campus card centre` · ✖ · `must authorise every campus-card charge through its legacy API` · `owns the money and the fraud risk` |

## Done when

- [ ] 5–8 rows, **≥2 marked ✖**, every row has a "why" and a source.
- [ ] All five coverage perspectives named.
- [ ] Names are concrete (a role with a context), not job-title abstractions.
- [ ] The appendix still holds your longer Week 1 list.
- [ ] File committed — push and tag in `Template-W02-05`.
