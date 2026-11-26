# ISAD — Final Defense Grading (Final)

> **Information Systems Analysis and Design** · 64 hours / 16 weeks · English-medium · Fall 2026
> This document covers **the summative assessment only (W16 final defense)**.
> Formative assessment (attendance, class participation, project milestones, assignments) is out of scope here.

---

## 1. How It Counts

```
Course grade = Formative 40 × 100%  +  Summative 100 × 60%      (capped at 100)
                        ↑
                  this document
```

**Summative 100 points × 60% = 60 points of the course grade** — the single heaviest component.

| # | Component | Points |
|---|---|---|
| S1 | Design portfolio walkthrough (team) | **30** |
| S2 | Individual Q&A (5 min per member) | **55** |
| S3 | English communication | **10** |
| S4 | Reflection & contribution report | **5** |
| | **Total** | **100** |

---

## 2. Format

| Segment | Length | Content |
|---|---|---|
| Team walkthrough | 10 min | The whole team presents the analysis & design work |
| **Individual Q&A** | **20 min** | **5 minutes per member; you may be asked about any part of the team's work** |
| Feedback | 5 min | Instructor's feedback |

> ### ⚠️ Three hard rules for the individual Q&A
> 1. **Any part may be asked.** Models your teammate designed, pattern cards someone else wrote — all fair game.
> 2. **You must give the reason.** A conclusion without naming the principle or the pattern does not count as a complete answer.
> 3. **English.** S3 is scored separately, and the quality of your English counts inside S2 too.

**When**: in class, W16 (Dec 21–25). 35 minutes for the one team.

---

## 3. What You Must Submit Before the Defense — M5 Final Package

**Due Sun Dec 27, 23:59 (GMT+8)** · submit with `git tag -a m5 -m "M5 final submission" && git push origin m5`

| # | Deliverable | Requirement |
|---|---|---|
| 1 | **Final report** | ① Vision & stakeholders ② Requirements (incl. your responses to ΔC2 and ΔC3) ③ Analysis models (domain / sequence / state / activity) ④ Design: DCD + GRASP/SOLID application notes ⑤ Pattern catalog ⑥ Architecture view ⑦ **Retrospection: what changed since M1 and why — this section is graded** ⑧ Individual contribution logs |
| 2 | **Individual contribution log** | Per week: what you did + evidence (commit / file / review); plus the parts you can explain best and the parts owned mainly by others that you have studied for the defense |
| 3 | **All diagram source files** | `.drawio` or `.puml` committed to the repo, exported image alongside; **PNG-only is not accepted** |
| 4 | **Pattern catalog cards** | Each with Problem / Solution / Consequences / Where / Why-not |

> **Submission area**: `01-requirements/` `02-analysis/` `03-design/` `04-patterns/` `05-report/` `changes/`
> **Scratch area**: `docs/`
> The tag is the graded snapshot, not your branch head. If GitHub is unreachable, zip the whole repo folder including `.git/`, email it before the deadline (the email timestamp is your proof of timeliness), and restore the repo state — tags included — within 3 days.

---

## 4. Grading Criteria

| # | Component | Pts | Excellent (A) | Adequate (C) |
|---|---|---|---|---|
| **S1** | **Portfolio walkthrough** | **30** | Coherent narrative, models traceable, both requirement changes absorbed gracefully | Covered but disjointed; weak links between views |
| **S2** | **Individual Q&A** | **55** | Answers any question on **any part** of the work with reasoning (principles/patterns) | Answers own slice only; hesitant outside it |
| **S3** | **English communication** | **10** | Precise terminology, clear delivery | Understandable but error-prone |
| **S4** | **Reflection & contribution report** | **5** | Honest, specific, evidence-linked | Generic |

**What S1 looks at**: whether the four analysis views (domain / sequence / state / activity) and the design view are mutually consistent; whether every message in your sequence diagrams has a matching operation in the DCD; and whether the ΔC2 / ΔC3 injections were *absorbed* by your models or merely patched around.

**What S2 looks at**: the *reasoning* behind each principle and pattern, the *alternatives you rejected*, and the *questions you have not resolved*. Acknowledging the edge of your understanding is worth more than a polished but invented answer.

**What S4 looks at**: whether it matches the Git record, and whether it honestly reflects how the work was distributed.

---

## 5. Bonus — up to +5 (course total capped at 100)

| # | Bonus item | Cap |
|---|---|---|
| C1 | Extra patterns beyond 5, correctly applied | +2 |
| C2 | Exceptional refactoring narrative (before/after with metrics or clear argument) | +2 |
| C3 | Outstanding documentation | +1 |

---

## 6. Deductions

| Situation | Rule |
|---|---|
| Late milestone (including the M5 final package) | −10% per calendar day, max 3 days, then 0 for that milestone |
| Plagiarized models | 0 for that milestone + academic misconduct procedure |
| Undisclosed AI-generated bulk content | Treated as plagiarism; **disclosure = no penalty** |
| Non-English deliverable | Returned once for translation (−20% on that item); second time not accepted |

**AI use**: allowed for polishing English and brainstorming, provided you disclose what you used and how in the report. Undisclosed bulk generation is treated as plagiarism.

---

## 7. Grade Bands

| Band | Course total | Band | Course total |
|---|---|---|---|
| A Excellent | 90–100 | D Pass | 60–69 |
| B Good | 80–89 | F Fail | < 60 |

---

## 8. Sample Defense Questions

1. Why does `orderTotal()` live in `Order` and not in `OrderController`? (GRASP)
2. Your `Order` has a giant switch for `status`. Show me how the State pattern would change this code. (State)
3. A new payment method "ApplePay" must be added next semester. Which files change, and why is that acceptable (or not)? (OCP / Factory)
4. Who may observe an order's status changes? How does the customer's app get updated without polling? (Observer)
5. The campus-card system is an Adapter and the notification stack is a Facade — they look the same to me. (Adapter vs. Facade)
6. Point to any bidirectional association in your DCD and defend or remove it. (navigability / coupling)
7. Your teammate designed the domain model you just presented. Walk me through why `Courier` is associated with `Order` and not with `OrderLine`. (individual mastery)

---

## 9. Deferral, Make-up & Disputes

- **Deferred defense**: absent for a valid reason (e.g. illness)? Apply with evidence and defend **individually** in the make-up window after the semester; the individual Q&A is unchanged.
- **Make-up**: if the course total is < 60, you must deliver an individual defense — a full round of individual Q&A on the team's work, plus a corrected or extended contribution section. The formative part is not normally re-done; the defense is re-assessed (100-point scale, × 60%).
- **Disputes**: contribution disputes within the team are settled by **Git history + contribution logs**, arbitrated by the instructor. A grade appeal must be filed **in writing within 3 working days** of publication.

---

*Caliber unified 2026-11-26 · every point value here matches the official Course Assessment Outline and Grading Rubric.*
