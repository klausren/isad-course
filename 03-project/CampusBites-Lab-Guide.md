# CampusBites — Lab Guide (实验指导书)

> *Information Systems Analysis and Design* · 16 weeks · Fall 2026
> **How labs work** — the last 2 hours of each weekly block. Companion to the *Project Guidebook* (what you build) and the *Deadline Schedule* (when it is due). This guide tells you **how to do the work each week**.

---

## 0. How to Read This Guide

Every week you have **4 consecutive hours**, split into two blocks:

| Block | Time | What happens |
|---|---|---|
| **Part 1 — Lecture** | 2 h | Concepts, terminology, worked examples. Slides + whiteboard. |
| **Part 2 — Lab** | 2 h | A guided demo (~25 min) followed by hands-on lab work (~90 min), tied directly to your CampusBites milestone. |

The lab is **not** a separate course. It is where you turn the lecture into your own models, week by week. Everything you build in labs feeds a milestone deliverable; nothing in the lab is throwaway.

---

## 1. Lab Tools & Environment (set up in W1–W2)

You need these five tools. All are free, and all work on macOS, Windows, and Linux.

| Tool | What it is for | Get it |
|---|---|---|
| **draw.io** (diagrams.net) | Drawing UML diagrams (use case, domain, class, sequence, state, activity) | Desktop app or https://app.diagrams.net |
| **PlantUML** (optional) | Text-based UML — better for version-controlling diagrams | plantuml.com + a VS Code extension |
| **Git + GitHub** | Your team repository — the only submission address | github.com |
| **VS Code** | Editing Markdown + diagram sources | code.visualstudio.com |
| **Markdown** | All documents (requirements, reports, contribution logs) | any editor |

**Rules that affect your grade (from the Guidebook §6):**

1. Every diagram needs a **source file** committed (`.drawio` or `.puml`), not just an exported image.
2. Documents are **Markdown**; exported diagrams are **PNG/SVG**. No `.docx`/`.pdf`-only submissions.
3. One team, **one Git repository**, and **a milestone is only "submitted" when the tag is pushed** (see Deadline Schedule §4).

> **Week 1–2 lab check — done means done:** you have draw.io installed, a GitHub account, VS Code open, and can push one commit. If GitHub is unreachable from your network, register by email and use the zip fallback (Deadline Schedule §4.5) until access is sorted.

---

## 2. Lab Assessment — How Labs Count

Labs are **formative**, not graded directly. There is no "lab participation mark" on a scale. But:

- Lab work **is** your milestone deliverable. Skip labs, and you have nothing to submit at the deadline.
- Lab attendance and participation feed your **Individual Contribution** grade (40%): your Git commit history and contribution log are the evidence, and they are produced *in labs*.
- At the **final defense (W16)** you are asked about any part of the team's work — including work you only saw in a lab. There is no back row.

**One practical rule:** if a lab task is not finished in 90 minutes, it becomes homework. Milestones are due at Sunday 23:59, so the lab is your head start, not your only chance.

---

## 3. Weekly Lab Plan (16 weeks)

Each entry gives: **what the lecture covered**, **what you do in the lab**, and **what it feeds**.

### Module A — Foundations (W1–W3)

#### Lab 1 · W1 (Aug 31–Sep 06) — Course setup & first look at UML
- **Setup**: install draw.io (or PlantUML), create GitHub account, open VS Code.
- **Demo**: the instructor opens a finished vending-machine model (use case + domain + sequence) and reads it with you.
- **Hands-on**: reproduce a tiny domain model (3–4 classes) in draw.io, export PNG + `.drawio`.
- **Deliverable (none graded)**: your first committed diagram. **Homework**: read the Project Guidebook fully before W2.

#### Lab 2 · W2 (Sep 07–Sep 13) — Team formation & M0 kickoff
- **Form teams**: 2 teams × ~3 students; appoint Team Lead; agree role rotation.
- **Hands-on**: ① write the team charter (Guidebook Appendix A) ② list stakeholders ③ write the one-paragraph vision ④ create the repo and invite the instructor (`klausren`).
- **Milestone**: **M0 due Fri Sep 11** (pass/fail) — charter, stakeholder list, vision, repo registered.

#### Lab 3 · W3 (Sep 14–Sep 20) — UML essentials practice
- **Hands-on**: classify a set of descriptions into structure vs. behaviour vs. interaction views; draw one of each for a small familiar system (e.g., the campus library).
- **Purpose**: get fluent with draw.io/PlantUML *before* the graded models arrive. No milestone this week — use the breathing room.

### Module B — Analysis (W4–W9)

#### Lab 4 · W4 (Sep 21–Sep 27) — Requirements pack & use case identification
- **Hands-on**: read the instructor's requirements pack; extract candidate use cases; draw a first use case diagram with all actors.
- **Feeds**: M1.

#### Lab 5 · W5 (Sep 28–Oct 04) — Use case specifications & cross-team review
- **Hands-on**: write 2 detailed use case specifications (template: Appendix B) — *Place Order* plus one more.
- **Cross-team client review** happens on the first class on/after Oct 4.
- **Milestone**: **M1 due Sun Oct 4** — requirements list, use case diagram, 2 detailed specs.

#### Lab 6 · W6 (Oct 05–Oct 11) — Domain model v1
- **Hands-on**: from the use cases, identify conceptual classes, attributes, and associations; draw the first domain model (10+ classes target).
- **Note**: ΔC1 (requirement change #1) is announced online this week — fold it into M2.

#### Lab 7 · W7 (Oct 12–Oct 18) — Domain relationships
- **Hands-on**: refine associations with multiplicities; decide aggregation vs. composition; drop attributes that are really classes.
- **Feeds**: M2 (domain model).

#### Lab 8 · W8 (Oct 19–Oct 25) — Sequence diagrams
- **Hands-on**: draw 2+ system-sequence / interaction diagrams for key operations (`placeOrder`, `pay`).
- **Milestone**: **M2 due Sun Oct 25** — domain model, 2+ sequence diagrams, Order state machine, 1 activity diagram.

#### Lab 9 · W9 (Oct 26–Nov 01) — State & activity diagrams + mid-term review
- **Hands-on**: complete the Order state machine (guards/actions/events) and one activity diagram.
- **Mid-term review** (formative): 8 min team walkthrough + 10 min individual Q&A — every member questioned.

### Module C — Design (W10–W15)

#### Lab 10 · W10 (Nov 02–Nov 08) — From analysis to design (DCD)
- **Hands-on**: turn the domain model into a first design class diagram (DCD); add operations and navigability.
- **Note**: ΔC2 announced this week.

#### Lab 11 · W11 (Nov 09–Nov 15) — GRASP
- **Hands-on**: for every major responsibility decision, name the GRASP principle and argue the alternative (Information Expert, Creator, Controller, Low Coupling, High Cohesion).

#### Lab 12 · W12 (Nov 16–Nov 22) — SOLID
- **Hands-on**: audit the DCD against SRP/OCP/LSP/ISP/DIP; refactor; write before/after notes.
- **Milestone**: **M3 due Sun Nov 22** — DCD, GRASP/SOLID application notes, DCD-level interaction diagrams.

#### Lab 13 · W13 (Nov 23–Nov 29) — Creational patterns
- **Hands-on**: apply Factory/Builder/etc. to CampusBites (payment creation, order assembly); write pattern catalog cards (Appendix C).
- **Note**: ΔC3 announced this week.

#### Lab 14 · W14 (Nov 30–Dec 06) — Structural patterns
- **Hands-on**: apply Adapter (campus-card API), Decorator (meal customization), Facade (notification stack); update DCD.
- **Milestone**: **M4 due Sun Dec 6** — pattern catalog (5+), refactoring narrative, updated DCD.

#### Lab 15 · W15 (Dec 07–Dec 13) — Behavioural patterns & defense rehearsal
- **Hands-on**: apply State (order lifecycle), Strategy (pricing), Observer (order tracking); rehearse the 30-min defense **out loud, in English, with a timer**.

### Module D — Wrap-up (W16)

#### Lab 16 · W16 (Dec 14–Dec 20) — Final defense & final package
- **Defense in class** (Dec 14–18): 10 min portfolio walkthrough + 15 min individual Q&A — each member questioned on *any* part.
- **Milestone**: **M5 final package due Sun Dec 20** — final report (Appendix D), individual contribution logs (Appendix E), all diagram sources, tag `m5`.

---

## 4. What "Done" Looks Like for a Lab

Finish a lab by checking all three boxes. If any is empty, it is homework.

- [ ] **Models**: the required diagram(s) exist as `.drawio`/`.puml` **and** exported PNG/SVG, committed.
- [ ] **Evidence**: your commit message names the work (e.g. `W8: sequence diagram for placeOrder`), and your contribution log has a row for today.
- [ ] **Explainable**: you can explain every element you drew in one English sentence each. If you cannot, you decorated, not designed — fix it now, not at the defense.

---

## 5. Reference

- **Project Guidebook** (`CampusBites-项目指导书-Project-Guidebook.md`) — what to build, teams, submission rules, templates (Appendices A–E).
- **Deadline Schedule** (`CampusBites-Deadline-Schedule-and-Submission-Guide.md`) — exact dates, tag protocol, fallback channel.
- **Grading Rubric** (`Course-Project-Grading-Rubric.md`) — how each milestone and the defense are scored.
- **Course Standard** (`00-课程文件/Course-Syllabus-课程标准.md`) — full syllabus and weekly schedule.

*Lab questions are raised in class or as issues in the course repository. Build something you can defend.*
