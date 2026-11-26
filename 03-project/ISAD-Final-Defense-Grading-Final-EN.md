# ISAD — Final Defense Grading (Final)

> **Information Systems Analysis and Design** · Fall 2026 · English-medium
> This document covers **the summative assessment only (W16 final defense)**.
> Formative assessment (attendance, class participation, milestones, assignments) is out of scope here.

## 1. The Five Artifacts You Are Examined On

| # | Artifact | What you submit in the final package |
|---|---|---|
| ① | **Use case diagram** | All actors, all use cases, include/extend relationships |
| ② | **Use case specification** | 2–3 detailed specs (main success scenario + extensions + pre/post-conditions + NFR references) |
| ③ | **Activity diagram** | One core business process (order fulfillment or equivalent), with branches, merges and swimlanes |
| ④ | **Sequence diagram** | 2+ sequence diagrams for system operations (lifelines, messages, alt/loop/opt fragments) |
| ⑤ | **UI prototype** | Wireframes of the key screens (≥ 4: list / detail / form / result-or-error), with navigation annotated |

---

## 2. How It Counts & How the Defense Runs

```
Course grade = Formative 40 × 100%  +  Summative 100 × 60%      (capped at 100)
```

| # | Component | Points |
|---|---|---|
| S1 | **Walkthrough of the five artifacts** (team) | **30** |
| S2 | **Individual Q&A** (5 min per member) | **55** |
| S3 | English communication | **10** |
| S4 | Reflection & contribution report | **5** |
| | **Total** | **100** |

| Segment | Length | Content |
|---|---|---|
| Walkthrough | 10 min | Present the five artifacts in the order ①→⑤ |
| **Individual Q&A** | **20 min** | **5 minutes per member; every question comes from the five artifacts above, and you may be asked about one you did not build** |
| Feedback | 5 min | Instructor's feedback |

---

## 3. S1 — Walkthrough Scoring (30 points)

| Artifact | Pts | Excellent (A) | Adequate (C) |
|---|---|---|---|
| ① Use case diagram | 5 | Actors complete (external systems included), system boundary clear, include/extend used correctly and sparingly, use cases named as verb phrases | Use cases present, boundary broadly right, relationships misused or missing |
| ② Use case specification | 6 | Main success scenario executable step by step, extensions cover real failure branches, pre/post-conditions traceable to NFR numbers | Main success scenario present, extensions incomplete, pre/post-conditions vague |
| ③ Activity diagram | 5 | Branch conditions mutually exclusive and exhaustive, merge semantics correct, swimlanes match actors, consistent with the spec's extensions | Main flow correct, some branch conditions overlap or missing |
| ④ Sequence diagram | 8 | Messages map one-to-one to spec steps, fragment semantics correct (alt guards exclusive, loop bounds stated), boundary and control objects placed sensibly | Main message chain complete, fragments missing or semantically vague |
| ⑤ UI prototype | 6 | Screens map one-to-one to use cases, navigation covers the main success scenario, error / empty / loading states included, widgets consistent with the domain model | Screens present, navigation has gaps, only the happy path |

---

## 4. S2 — Individual Q&A (55 points)

**How questions are drawn**: 2–3 questions are prepared per artifact. Each member is asked 3–4, **including artifacts they did not build**.
**How answers are judged**: correct answer **plus the reason** (which principle, which requirement ID, which constraint) = top band. Answering only your own slice, or hesitating outside it = adequate band.

| Artifact | Sample questions |
|---|---|
| ① Use case diagram | Why is this an actor? What breaks if you move X outside the system boundary?<br>How do you tell include from extend here — and why not the other way round? |
| ② Use case specification | What happens if step 4 succeeds and step 5 fails? Which extension covers it?<br>Where does this pre-condition come from? Which requirement ID is it? |
| ③ Activity diagram | Are these branch conditions mutually exclusive? Is there a third case that falls through?<br>Why is a merge needed here? Which segment of the graph is the exception path? |
| ④ Sequence diagram | Which step of the spec does this message correspond to? What breaks if the order changes?<br>Are these alt guards mutually exclusive? Why is X created here rather than earlier? |
| ⑤ UI prototype | What can the user do on this screen? Which use case does it belong to?<br>What does it show when the list is empty? Which extension does this error message come from? |

---

## 5. What You Must Submit Before the Defense — M5 Final Package

**Due Sun Dec 27, 23:59 (GMT+8)** · `git tag -a m5 -m "M5 final submission" && git push origin m5`

| # | Deliverable | Requirement |
|---|---|---|
| 1 | **The five artifacts** | All of ①–⑤ above, with **diagram sources (`.drawio` / `.puml`) committed** and exported images alongside |
| 2 | **Final report** | A narrative through the five artifacts: requirement source → use cases → business process → interaction flow → screens; including your responses to the ΔC2 and ΔC3 requirement changes |
| 3 | **Individual contribution log** | Per week: what you did + evidence (commit / file / review); plus the parts you can explain best and the parts owned mainly by others that you have studied for the defense |

> **Submission area**: `01-requirements/` `02-analysis/` `03-design/` `04-patterns/` `05-report/` `changes/` · **scratch area**: `docs/`
> The tag is the graded snapshot. If GitHub is unreachable, zip the whole repo folder including `.git/`, email it before the deadline (the email timestamp is your proof of timeliness), and restore the repo state — tags included — within 3 days.

---

## 6. Remaining Components

| # | Component | Pts | Excellent (A) | Adequate (C) |
|---|---|---|---|---|
| S3 | English communication | 10 | Precise terminology, clear delivery | Understandable but error-prone |
| S4 | Reflection & contribution report | 5 | Honest, specific, evidence-linked | Generic |

**Bonus (≤5, course total capped at 100)**: extra design patterns +2 · exceptional refactoring narrative +2 · outstanding documentation +1

**Deductions**: late milestone (incl. M5) −10% per calendar day, max 3 days, then 0 · plagiarized models = 0 for that milestone + academic misconduct procedure · undisclosed AI-generated bulk content treated as plagiarism (disclosure = no penalty) · non-English deliverable returned once for translation (−20% on that item), second time not accepted

**Grade bands**: A 90–100 · B 80–89 · C 70–79 · D 60–69 · F < 60

**Deferral / make-up / disputes**: absent for a valid reason? Defend individually in the make-up window (Q&A unchanged) · if the course total is < 60, deliver a full round of individual Q&A; the formative part is not re-done · contribution disputes settled by Git history + contribution logs; appeals in writing within 3 working days of publication

---

*Caliber unified 2026-11-26 · point values match the official Course Assessment Outline and Grading Rubric.*
