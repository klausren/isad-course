# Course Project Grading Rubric — CampusBites

> *Information Systems Analysis and Design* · Small cohort (4 students, one team) · **Official formula: Course grade = Formative assessment (40 pts × 100%) + Summative assessment (100 pts × 60%)** — project + oral defense, no written exam

## 1. Formative Assessment — 40 points

| # | Item | Points | Evidence |
|---|---|---|---|
| F1 | Attendance | 0 | Recorded every session; not scored. Absences handled per school regulations |
| F2 | Class participation | 10 | Weekly in-class exercises (4) · W05 client-review questions (2) · peer critique & discussion (2) · engagement & English (2) |
| F3 | Level-3 project — CampusBites | 20 | Milestone deliverables 14 + individual contribution & Git 6 (see 1.1 / 1.2) |
| F4 | Assignments | 10 | 5 homework sets × 2: W02 refactoring · W04 use case specification · W07 behavior modeling · W11 design class diagram · W13 pattern card |

### 1.1 F3a — Milestone deliverables (14 points, shared by the team)

| Milestone | Due | Points | Excellent (A) | Adequate (C) |
|---|---|---|---|---|
| M0 Project setup | W2 | 1 | Charter, stakeholders, vision, repo & tag pipeline all working on time | Missing pieces or late |
| M1 Requirements | W5 | 3 | Complete, correct include/extend usage, well-formed specs | Core cases present, minor notation defects |
| M2 Analysis models | W9 | 4 | Domain / sequence / state / activity consistent across views; guards & actions complete | Models present but with gaps/inconsistencies |
| M3 Design models | W12 | 3 | DCD traceable to sequence messages; every GRASP/SOLID decision argued | Mostly complete, weak argumentation |
| M4 Pattern catalog | W15 | 3 | 5+ patterns, right pattern for the problem, consequences honestly stated | Patterns applied, some forced/misfit |

*English documentation quality is graded inside every milestone item, not as a separate line.*

### 1.2 F3b — Individual contribution & Git history (6 points, yours alone)

| Evidence | Points |
|---|---|
| Substantive commits across all milestones (small, meaningful, spread out) | 3 |
| Accurate contribution log (Guidebook Appendix E) matching the commit record | 2 |
| Useful reviews of teammates' models / issues | 1 |

### 1.3 F4 — Assignments (5 × 2 points)

Each homework: **2** = complete and correct · **1** = submitted with gaps · **0** = missing or copied. Late homework: −1 point per calendar day.

## 2. Summative Assessment — Final Defense, W16 (100 points × 60%)

| # | Component | Points | Excellent (A) | Adequate (C) |
|---|---|---|---|---|
| S1 | Portfolio walkthrough (team) | 30 | Coherent narrative, models traceable, the three requirement changes absorbed gracefully | Covered but disjointed; weak links between views |
| S2 | Individual Q&A (5 min per member) | 55 | Answers any question on **any part** of the work with reasoning (principles/patterns) | Answers own slice only; hesitant outside it |
| S3 | English communication | 10 | Precise terminology, clear delivery | Understandable but error-prone |
| S4 | Reflection & contribution report | 5 | Honest, specific, evidence-linked | Generic |

## 3. Bonus — up to +5 points (course total capped at 100)

| # | Bonus item | Cap |
|---|---|---|
| C1 | Extra patterns beyond 5, correctly applied | +2 |
| C2 | Exceptional refactoring narrative (before/after with metrics or clear argument) | +2 |
| C3 | Outstanding documentation (instructor's judgment) | +1 |

*High-quality client-review questions are graded in F2 (class participation) — not as bonus.*

## 4. Deductions

| Item | Rule |
|---|---|
| Late milestone | −10% of that milestone's points per calendar day, max 3 days, then 0 for that milestone |
| Plagiarized models | 0 for the milestone + academic misconduct procedure |
| Undisclosed AI-generated bulk content | Treated as plagiarism; disclosure = no penalty |
| Non-English deliverable | Returned once for translation (−20% on that item); second time not accepted |

## 5. Defense Question Bank (sample)

1. Why does `orderTotal()` live in `Order` and not in `OrderController`? (GRASP)
2. Your `Order` has a `status` field with a giant switch. Show me how State pattern would change this code. (State)
3. A new payment method "ApplePay" must be added next semester. Which files change, and why is that acceptable (or not)? (OCP / Factory)
4. Who may observe an order's status changes? How does the customer's app get updated without polling? (Observer)
5. Why is the campus-card system an Adapter and the notification stack a Facade — they look the same to me. (Adapter vs. Facade)
6. Point to any bidirectional association in your DCD and defend or remove it. (navigability/coupling)
7. Your teammate designed the domain model you just presented. Walk me through why `Courier` is associated with `Order` and not with `OrderLine`. (individual mastery check)

> With four students, every question-bank item can be covered in the single defense, and each student faces 5+ individual questions at W16.
