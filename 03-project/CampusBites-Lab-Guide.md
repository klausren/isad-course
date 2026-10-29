# CampusBites — Lab Guide (实验指导书)

> *Information Systems Analysis and Design* · 16 weeks · Fall 2026
> **How labs work** — the last 2 hours of each weekly block. Companion to the *Project Guidebook* (what you build) and the *Deadline Schedule* (when it is due). This guide tells you **how to do the work each week**.

---

## ⚠️ 从 W06 起：项目案例已改为学生自主命题

**CampusBites 不再是你们的项目。** 从 W06（Oct 5–11）起，4 人小组自己选题。

| | |
|---|---|
| **新增 W06 任务** | **选题三件套** → [`labs/Lab-07-W06-Choosing-Your-Own-Project.md`](labs/Lab-07-W06-Choosing-Your-Own-Project.md) |
| **W06 补课（10-29）** | **领域建模 v1** → [`labs/Lab-06-W06-Domain-Modeling-v1.md`](labs/Lab-06-W06-Domain-Modeling-v1.md) — 已按 **AI Skin Analysis** 的 FR-1…FR-12 重写；**M0 当堂收** |
| **提交协议** | [`SUBMIT-INSTRUCTIONS-W06-EN.md`](SUBMIT-INSTRUCTIONS-W06-EN.md) — M0 的 push → tag → verify 全流程（学生用）|
| **任务说明** | [`Topic-Selection-Task-选题任务包.md`](Topic-Selection-Task-选题任务包.md) |
| **变更详情与新时间线** | [`项目案例变更说明-CampusBites改为自主命题.md`](项目案例变更说明-CampusBites改为自主命题.md) |
| **三份空白模板** | [`topics-templates/`](topics-templates/) — `Template-01-Candidate-List.md` · `Template-02-Scorecard.md` · `Template-03-Topic-Proposal.md` |

**没变的**：课程方法、里程碑 M0–M5 的内容要求、评分口径（20 分不变）、提交协议（push + tag）、图目录、四常设角色。
**变的**：分析哪个系统，以及**时间线比原计划紧一周**（M0 移到 W07，M1 移到 W08）。

**本文件里 W04–W08 那几周的 CampusBites 具体内容（找 actor、画用例图、写规约、领域模型 v1）**
**做法不变，只是换成你们自己的项目**——步骤、方法、判据全部照用。

---

## 0. How to Read This Guide

Every week you have **4 consecutive hours**, split into two blocks:

| Block | Time | What happens |
|---|---|---|
| **Part 1 — Lecture** | 2 h | Concepts, terminology, worked examples. Slides + whiteboard. |
| **Part 2 — Lab** | 2 h | A guided demo (~25 min) followed by hands-on lab work (~90 min), tied directly to your CampusBites milestone. |

The lab is **not** a separate course. It is where you turn the lecture into your own models, week by week. Everything you build in labs feeds a milestone deliverable; nothing in the lab is throwaway.

### Two documents, two jobs

| Document | Answers | You use it… |
|---|---|---|
| **This guide** (16-week plan) | *What* the lab covers each week, and what it feeds | To plan the term, and to see how the labs build on each other |
| **`labs/Lab-NN-WNN-*.md`** (lab sheet) | *How* to do this week's work, step by step | **In the lab, open on your laptop** — steps, commands, done-when checklists, and what to do when you are stuck |

Each weekly entry below links to its lab sheet. **The lab sheet is the one you work from**; this guide is the map.

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

📄 **Lab sheet**: [`labs/Lab-01-W01-Toolchain-and-First-UML.md`](labs/Lab-01-W01-Toolchain-and-First-UML.md) — toolchain setup, reading your first UML models, first committed diagram.

- **Setup**: install draw.io (or PlantUML), create GitHub account, open VS Code.
- **Demo**: the instructor opens a finished vending-machine model (use case + domain + sequence) and reads it with you.
- **Hands-on**: reproduce a tiny domain model (3–4 classes) in draw.io, export PNG + `.drawio`.
- **Deliverable (none graded)**: your first committed diagram. **Homework**: read the Project Guidebook fully before W2.

#### Lab 2 · W2 (Sep 07–Sep 13) — Team formation & M0 kickoff

📄 **Lab sheet**: [`labs/Lab-02-W02-Team-Formation-and-M0-Kickoff.md`](labs/Lab-02-W02-Team-Formation-and-M0-Kickoff.md) — Exercise 2.1 (responsibilities), team charter, stakeholders & vision, `m0` tag. **M0 due Sun Oct 25** — the repo is created earlier, in W06 (`labs/Lab-07` §0).

🧩 **Templates** (fill these in, they *are* the deliverables): [`Team Charter`](templates/Template-W02-01-Team-Charter.md) · [`Stakeholder List`](templates/Template-W02-02-Stakeholder-List.md) · [`Vision Statement`](templates/Template-W02-03-Vision-Statement.md) · [`Repository README`](templates/Template-W02-04-Repository-README.md) · [`M0 Submission Checklist`](templates/Template-W02-05-M0-Submission-Checklist.md). Classwork: [`Responsibility Worksheet`](templates/Template-W02-06-Responsibility-Worksheet.md) · [`Refactoring Worksheet`](templates/Template-W02-07-Refactoring-Worksheet.md).

- **Form the team**: one team of four; name the four standing roles (Lead · Recorder · Reviewer · Release Manager); agree the M1–M5 rotation.
- **Hands-on**: ① write the team charter (Guidebook Appendix A) ② list stakeholders ③ write the one-paragraph vision ④ create the repo and invite the instructor (`klausren`).
- **Milestone**: **M0 due Sun Oct 25** (pass/fail) — charter, stakeholder list, vision, tag `m0`. Repository setup was pulled forward to W06.

#### Lab 3 · W3 (Sep 14–Sep 20) — UML essentials practice

📄 **Lab sheet**: [`labs/Lab-03-W03-UML-Essentials-Practice.md`](labs/Lab-03-W03-UML-Essentials-Practice.md) — Exercise 3.1 (name that diagram), toolchain proof, Exercise 3.2 (library model in PlantUML), the six team diagram conventions. **No milestone this week.**

📄 **Homework text specs**: [`specs/W03-text-specs.md`](specs/W03-text-specs.md) — the two specs students reproduce in PlantUML for the Week 03 homework (a four-class CampusBites domain model, and a `Place an order` sequence diagram).

- **Hands-on**: classify a set of descriptions into structure vs. behaviour vs. interaction views; draw one of each for a small familiar system (e.g., the campus library).
- **Purpose**: get fluent with draw.io/PlantUML *before* the graded models arrive. No milestone this week — use the breathing room.

### Module B — Analysis (W4–W9)

#### Lab 4 · W4 (Sep 21–Sep 27) — Requirements pack & use case identification

📄 **Lab sheet**: [`labs/Lab-04-W04-Finding-Actors-and-Use-Cases.md`](labs/Lab-04-W04-Finding-Actors-and-Use-Cases.md) — Exercise 4.1 (actors, then nine candidates filtered to goals), Exercise 4.2 (draw the diagram, one `<<include>>`, one `<<extend>>`, one sentence per dashed arrow), then a 15-minute defence to the instructor, who plays the client.

- **Hands-on**: read the instructor's requirements pack; extract candidate use cases; draw a first use case diagram with all actors.
- **Deliverable today**: `docs/diagrams/use-case-v1.drawio` + PNG, pushed — **not tagged**.
- **Feeds**: M1 (tag `m1` by Sun Oct 4).

#### Lab 5 · W5 (delivered Thu Oct 08, and Thu Oct 29) — Use case specifications, then domain modeling v1

📄 **W05 sheet**: [`labs/Lab-05-W05-Use-Case-Specification-and-Peer-Review.md`](labs/Lab-05-W05-Use-Case-Specification-and-Peer-Review.md) — Exercise 5.1 (find the five planted defects), Exercise 5.2 (the twelve-question review checklist and the 3/2/1 scale, filed as `docs/reviews/m1-spec-review.md`). §5 (Close Out M1 / tag `m1`) is **parked** — M1 is now due Sun Nov 01.

📄 **W06 sheet (today, Oct 29)**: [`labs/Lab-06-W06-Domain-Modeling-v1.md`](labs/Lab-06-W06-Domain-Modeling-v1.md) — rewritten for **AI Skin Analysis**: noun scan on your own FR-1…FR-12, E/B/C classification, the first domain model in PlantUML, and **one open decision modelled and argued**.

- **Milestone**: **M0 due today** — charter, stakeholders, vision, then `git tag m0` and verify with `git ls-remote --tags origin`.
- **Feeds**: M1 (requirements list, use case diagram, 2 detailed specifications), **due Sun Nov 01**.


#### Lab 6 · W6 (Oct 05–11) — Choosing your own project

📄 **In class (35 min)**: [`labs/Lab-07-W06-Choosing-Your-Own-Project.md`](labs/Lab-07-W06-Choosing-Your-Own-Project.md) — read the three criteria (S1 actors >= 5 · S2 classes >= 8 with >= 6 non-"has" relationships · S3 objects with lifecycles >= 2), watch the rejected-vs-accepted demo, then **20 minutes of silent, individual brainstorming**: two candidates each, written down before anyone speaks. Sheets are collected at minute 35.
📄 **In class (55 min) — Domain modeling as a method**: slides `W06-Domain-Modeling.pptx` **P01–P29** — noun scan and the identity test, analysis vs. design classes, entity/boundary/control, the three rooms model, attributes vs. values, associations before multiplicities. **P30–P38 are not used this week** (they carry the CampusBites word list). Teacher's script: [`../02-教案/W06-课堂教案-领域建模方法.md`](../02-教案/W06-课堂教案-领域建模方法.md).
📄 **Homework (≈1.9 h, due before W7)**: [`homework/Homework-01-W06-Choosing-Your-Own-Project.md`](homework/Homework-01-W06-Choosing-Your-Own-Project.md) — Step 1 merge the candidate list (keep the proposer's name, keep the rejected ones), Step 2 score against the three criteria **and write down how you counted**, Step 3 write the proposal (§3 evidence, §5 the pattern questions you have not resolved), Step 4 push. **No tag this week.**
- **Instructor answer**: **pass / revise**, returned **before W7**. You cannot enter M0 until the topic is approved.
- **Why 20 minutes stay in class even though the rest is homework**: if you talk first, four people collapse into one idea, and whoever's idea is dropped never owned anything. That is individual-contribution evidence, which is why it does not move to homework.

#### Lab 7 · W7 (Oct 12–18) — M0 Kickoff

📄 **Lab sheet**: *to be written.* Method unchanged from `labs/Lab-04-W04-Finding-Actors-and-Use-Cases.md`; the case is now **your own topic**.

- **Hands-on**: team charter (Appendix A), stakeholder list, project vision, repository created and instructor invited.
- **Milestone**: **M0 due Sun Oct 18** — `git tag m0`, verify with `git ls-remote --tags origin`.
- **Also this week**: the **M1 client review is now W9** (Oct 26–Nov 01), instructor as client, 30 min, formative.

#### Lab 8 · W8 (Oct 19–25) — Requirements & use case specifications

📄 **Lab sheet**: *to be written.* Reuse the **method** of `labs/Lab-05-W05-Use-Case-Specification-and-Peer-Review.md` (Exercise 5.1 find the five planted defects; Exercise 5.2 the twelve-question review checklist and the 3/2/1 scale, filed as `docs/reviews/m1-spec-review.md`), but write the specs for **your own topic**.

- **Hands-on**: requirements list, use case diagram, **2 fully-dressed specifications** (Appendix B) on your own use cases.
- **Milestone**: **M1 due Sun Oct 25** — `git tag m1`, verify with `git ls-remote --tags origin`.
- **Note**: the twelve-question review checklist from W05 is the same instrument you will be graded on at the W9 client review.

#### Lab 9 · W9 (Oct 26–Nov 01) — M1 client review & sequence diagrams

📄 **Lab sheet**: *to be written.* Method unchanged from the sequence-diagram lab of the same name; the case is now **your own**.

- **Hands-on**: draw 2+ system-sequence / interaction diagrams for your own key operations.
- **Also this week**: the **M1 client review** — instructor as client, 30 min (10 min present, 20 min interrogation), formative.
- **Milestone**: **M1 due Sun Nov 01** — requirements list, use case diagram, 2 detailed specifications. Tag `m1`, verify with `git ls-remote --tags origin`.
- **Feeds**: M2 (domain model), **due Sun Nov 22**.

#### Lab 10 · W9 (Oct 26–Nov 01) — State & activity diagrams, and the mid-term review
- **Hands-on**: complete the Order state machine (guards/actions/events) and one activity diagram.
- **Mid-term review** (formative): 8 min team walkthrough + 10 min individual Q&A — every member questioned. It shares the week with the M1 client review, so expect both in the same session.

### Module C — Design (W10–W15)

#### Lab 11 · W10 (Nov 02–Nov 08) — From analysis to design (DCD)
- **Hands-on**: turn the domain model into a first design class diagram (DCD); add operations and navigability.
- **Note**: ΔC2 announced this week.

#### Lab 12 · W11 (Nov 09–15) — GRASP
- **Hands-on**: for every major responsibility decision, name the GRASP principle and argue the alternative (Information Expert, Creator, Controller, Low Coupling, High Cohesion).

#### Lab 13 · W12 (Nov 16–22) — SOLID
- **Hands-on**: audit the DCD against SRP/OCP/LSP/ISP/DIP; refactor; write before/after notes.
- **Milestone**: **M3 due Sun Nov 22** — DCD, GRASP/SOLID application notes, DCD-level interaction diagrams.

#### Lab 14 · W13 (Nov 23–29) — Creational patterns
- **Hands-on**: apply Factory/Builder/etc. to CampusBites (payment creation, order assembly); write pattern catalog cards (Appendix C).
- **Note**: ΔC3 announced this week.

#### Lab 15 · W14 (Nov 30–Dec 06) — Structural patterns
- **Hands-on**: apply Adapter (campus-card API), Decorator (meal customization), Facade (notification stack); update DCD.
- **Milestone**: **M4 due Sun Dec 6** — pattern catalog (5+), refactoring narrative, updated DCD.

#### Lab 16 · W15 (Dec 07–Dec 13) — Behavioural patterns & defense rehearsal
- **Hands-on**: apply State (order lifecycle), Strategy (pricing), Observer (order tracking); rehearse the 30-min defense **out loud, in English, with a timer**.

### Module D — Wrap-up (W16)

#### Lab 17 · W16 (Dec 14–Dec 20) — Final defense & final package
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
- **Template library** (`templates/README-模板索引-Template-Index.md`) — every fill-in document, which week it belongs to, and where it must be saved in your repository.
- **Deadline Schedule** (`CampusBites-Deadline-Schedule-and-Submission-Guide.md`) — exact dates, tag protocol, fallback channel.
- **Grading Rubric** (`Course-Project-Grading-Rubric.md`) — how each milestone and the defense are scored.
- **Course Standard** (`00-课程文件/Course-Syllabus-课程标准.md`) — full syllabus and weekly schedule.

*Lab questions are raised in class or as issues in the course repository. Build something you can defend.*
