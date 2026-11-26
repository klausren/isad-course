# ISAD — Project Requirements & Grading (Final)

> **Information Systems Analysis and Design** · 64 hours / 16 weeks · English-medium · Fall 2026
> Assessment: **project + milestone reviews + final oral defense** — no written exam
> Cohort: **one team of four** (Team Lead · Recorder · Reviewer · Release Manager)
> Topic: **student-selected** (approved by the instructor in W06) — this team: **AI Skin Analysis**

> 📌 **This document is the single source of truth.** Where any original document
> (assessment outline / syllabus / rubric / guidebook / submission guide / lab guide)
> disagrees with this file, this file wins.
> Caliber baseline: `参考/ISAD口径基准表-2026-11-26.md` (unified 2026-11-26).

---

## 1. Grade Composition

```
Course grade = Formative 40 × 100%  +  Summative 100 × 60%      (capped at 100)
```

| Block | Points | Counts as | Content |
|---|---|---|---|
| Formative | 40 | × 100% (40 pts) | Attendance 0 · Class participation 10 · Level-3 project 20 · Assignments 10 |
| Summative | 100 | × 60% (60 pts) | W16 final defense (team walkthrough + individual Q&A) |

### Formative — 40 points

| # | Item | Pts | Breakdown |
|---|---|---|---|
| F1 | Attendance | **0** | Recorded, not scored; absences handled per school regulations |
| F2 | Class participation | 10 | Weekly in-class exercises 4 · **W09 client-review question quality 2** · peer critique & discussion 2 · engagement & English 2 |
| F3 | **Level-3 project (student-selected topic)** | 20 | **Milestone deliverables 14** (team-shared) + **individual contribution & Git history 6** (yours alone) |
| F4 | Assignments | 10 | 5 sets × 2: W02 refactoring · W04 use-case spec · W07 behavior modeling · W11 design class diagram · W13 pattern card<br>※ *exact week per each lab sheet* |

**F3 milestones — 14 points (shared by the team)**

| Milestone | Week | Pts | Deliverables |
|---|---|---|---|
| M0 Project setup | W07 | 1 | Team charter · stakeholder list · project vision · `m0` |
| M1 Requirements | W08 | 3 | Requirements list · use-case diagram · 2 detailed use-case specs · `m1` |
| M2 Analysis models | W11 | 4 | Domain model (10+ classes) · 2+ sequence diagrams · state machine · activity diagram · `m2` |
| M3 Design models | W13 | 3 | Design class diagram · GRASP/SOLID application notes · DCD-level interaction diagrams · `m3` |
| M4 Pattern catalog | W15 | 3 | 5+ GoF patterns · refactoring narrative · updated DCD · `m4` |

> *English documentation quality is graded inside every milestone item, not as a separate line.*

**F3 individual — 6 points (yours alone)**

| Evidence | Pts |
|---|---|
| Substantive commits across all milestones (small, meaningful, spread out) | 3 |
| Contribution log matching the commit record | 2 |
| Useful reviews of teammates' models / issues | 1 |

### Summative — 100 points (W16 final defense)

| # | Component | Pts | Excellent (A) | Adequate (C) |
|---|---|---|---|---|
| S1 | Portfolio walkthrough (team) | 30 | Coherent narrative, models traceable, both requirement changes absorbed gracefully | Covered but disjointed; weak links between views |
| S2 | **Individual Q&A (5 min per member)** | **55** | Answers any question on **any part** of the work with reasoning (principles/patterns) | Answers own slice only; hesitant outside it |
| S3 | English communication | 10 | Precise terminology, clear delivery | Understandable but error-prone |
| S4 | Reflection & contribution report | 5 | Honest, specific, evidence-linked | Generic |

### Bonus — up to +5 (course total capped at 100)

| # | Bonus item | Cap |
|---|---|---|
| C1 | Extra patterns beyond 5, correctly applied | +2 |
| C2 | Exceptional refactoring narrative (before/after with metrics or clear argument) | +2 |
| C3 | Outstanding documentation | +1 |

> *Sharp client-review questions are graded in F2, not as bonus.*

### Deductions

| Situation | Rule |
|---|---|
| Late milestone | −10% per calendar day, max 3 days, then 0 for that milestone |
| Plagiarized models | 0 for the milestone + academic misconduct procedure |
| Undisclosed AI-generated bulk content | Treated as plagiarism; **disclosure = no penalty** |
| Non-English deliverable | Returned once for translation (−20% on that item); second time not accepted |

### Grade bands

| Band | Range | Band | Range |
|---|---|---|---|
| A Excellent | 90–100 | D Pass | 60–69 |
| B Good | 80–89 | F Fail | < 60 |

---

## 2. Project Requirements

### What you must deliver

| # | Deliverable | Requirement |
|---|---|---|
| 1 | **Final report** | ① Vision & stakeholders ② Requirements (incl. responses to ΔC2/ΔC3) ③ Analysis models ④ Design (DCD + GRASP/SOLID notes) ⑤ Pattern catalog ⑥ Architecture view ⑦ **Retrospection: what changed since M1 and why — this section is graded** ⑧ Individual contribution logs |
| 2 | **Individual contribution log** | Per week: what you did + evidence (commit / file / review); plus the parts you can explain best and the parts owned mainly by others that you have studied for the defense |
| 3 | **All diagram source files** | `.drawio` or `.puml` committed to the repo, exported image alongside; **PNG-only is not accepted** |
| 4 | **Pattern catalog cards** | Each with Problem / Solution / Consequences / Where / Why-not |

### Milestones & deadlines

> **All deadlines are Sunday 23:59 (GMT+8).** Late = −10% per day.

| Milestone | Due | Tag | Deliverables |
|---|---|---|---|
| M0 | **Sun Oct 25** | `m0` | Charter · stakeholders · vision (pass/fail) |
| M1 | **Sun Nov 01** | `m1` | Requirements list · use-case diagram · 2 detailed specs |
| M2 | **Sun Nov 22** | `m2` | Domain model · 2+ sequence diagrams · state machine · activity diagram |
| M3 | **Sun Dec 06** | `m3` | DCD · GRASP/SOLID notes · DCD-level interaction diagrams |
| M4 | **Sun Dec 20** | `m4` | Pattern catalog 5+ · refactoring narrative · updated DCD |
| M5 | **Sun Dec 27** | `m5` | Final report · contribution logs · all diagram sources · pattern cards |

**Prep task (W06 · Oct 12–18 — not a milestone, no tag)**: three topic-selection deliverables — candidate list · three-criteria scorecard · topic proposal. Repository setup on Oct 15.

### Submission protocol

1. **Repository**: `Kasper282/WorkspaceProject`, instructor account `klausren` (read access)
2. **A submission is four steps**: commit → push → annotated tag → update the README milestone status table
   ```bash
   git tag -a m2 -m "M2 submission — analysis models"
   git push origin m2
   ```
   **The tag — not your branch head — is the graded snapshot.**
3. **Layout**: `01-requirements/` `02-analysis/` `03-design/` `04-patterns/` `05-report/` `changes/` are the **submission area**; `docs/` is your **scratch area**
4. **Diagram sources**: `.drawio` or `.puml` plus the exported image — no image-only submissions
5. **Language**: everything in English. A non-English deliverable is returned once for translation (−20% on that item); second time it is not accepted.
6. **Commit discipline**: small, meaningful commits with clear messages. One giant "final commit" is a red flag.
7. **Fallback**: if GitHub is unreachable, zip the whole repo folder including `.git/`, email it before the deadline (the email timestamp is your proof), and restore the repo state — tags included — within 3 days.

### Reviews & defense

| Event | Week | Length | Format | Scored |
|---|---|---|---|---|
| M1 client review | W09 | 30 min | 10 min present + 20 min interrogation (instructor as client) | Formative, not scored |
| Mid-term review | W12 | 30 min | 10 min walkthrough + 15 min individual Q&A (~4 min each) + 5 min feedback | Formative, not scored |
| M4 pattern walkthrough | W16 | — | Pattern catalog, item by item | Formative, not scored |
| **Final defense** | W16 (in class Dec 21–25) | **35 min** | **10 min walkthrough + 20 min individual Q&A (5 min each) + 5 min feedback** | **Summative 100 pts** |

> **Individual Q&A: any member may be asked about any part of the work.** With four people in the room, there is no back row.

### Requirement-change injections

- **ΔC2** (announced W10) → your response is folded into **M3**
- **ΔC3** (announced W13) → your response is folded into **M4**
- You never submit a "response to ΔC" as a separate deliverable. How gracefully your models absorb the change counts in S1.

### Academic integrity & AI use

- Plagiarized models = 0 for that milestone + academic misconduct procedure.
- **AI is allowed** for polishing English and brainstorming, if you disclose what you used and how in the report.
- **Undisclosed AI-generated bulk content is treated as plagiarism. Disclosure carries no penalty.**

---

## 3. Semester Calendar

| Week | Dates | Project focus | Milestone / review |
|---|---|---|---|
| W01 | Aug 31 – Sep 06 | Course kickoff · read the Guidebook | — |
| W02 | Sep 07 – Sep 13 | OO foundations · toolchain | Assignment 1 refactoring |
| W03 | Sep 14 – Sep 20 | UML essentials | — |
| W04 | Sep 21 – Sep 27 | Requirements & use-case modeling | Assignment 2 use-case spec |
| W05 | Sep 28 – Oct 04 (**delivered Thu Oct 08** — National Day) | Use-case specification | — |
| W06 | **Oct 12 – Oct 18** | Domain modeling as a method · **topic selection** | Selection pack (no tag) · **repository setup Oct 15** |
| W07 | **Oct 19 – Oct 25** | M0 | **M0 due Sun Oct 25** |
| W08 | **Oct 26 – Nov 01** | Requirements & use cases | **M1 due Sun Nov 01** |
| W09 | **Nov 02 – Nov 08** | **M1 client review** | Instructor as client, 30 min (not scored) |
| W10 | **Nov 09 – Nov 15** | Analysis → design | **ΔC2 announced** |
| W11 | **Nov 16 – Nov 22** | Analysis models finalize | **M2 due Sun Nov 22** |
| W12 | **Nov 23 – Nov 29** | **Mid-term review** | Formative, not scored |
| W13 | **Nov 30 – Dec 06** | Design modeling | **ΔC3 announced** · **M3 due Sun Dec 06** |
| W14 | **Dec 07 – Dec 13** | Pattern catalog (creational / structural) | — |
| W15 | **Dec 14 – Dec 20** | Pattern walkthroughs · defense rehearsal | **M4 due Sun Dec 20** |
| W16 | **Dec 21 – Dec 27** | **Final defense** | Defense in class Dec 21–25 · **final package due Sun Dec 27** |

---

## 4. Source Documents

| File | Purpose |
|---|---|
| `00-课程文件/Course-Assessment-Outline-课程考核大纲.md` | Official assessment outline |
| `00-课程文件/Course-Syllabus-课程标准.md` | Course syllabus |
| `04-项目实践/Course-Project-Grading-Rubric.md` | Rubric: A/B/C criteria and the defense question bank |
| `04-项目实践/CampusBites-项目指导书-Project-Guidebook.md` | Method handbook: teams, milestones, templates A–E |
| `04-项目实践/CampusBites-Deadline-Schedule-and-Submission-Guide.md` | Submission protocol: tag procedure, README format, fallback |
| `04-项目实践/CampusBites-Lab-Guide-实验指导书.md` | Lab guide for all 16 weeks |
| `04-项目实践/Topic-Selection-Task-选题任务包.md` | The three hard criteria for W06 topic selection |
| `参考/ISAD口径基准表-2026-11-26.md` | **Caliber baseline — single source of truth** |

---

*Caliber unified 2026-11-26 · the grading formula and every point value are unchanged since the course began.*
