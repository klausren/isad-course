# CampusBites — Course Project Guidebook

> *Information Systems Analysis and Design* · Semester Project Handbook · handed out in Week 1
> Read this document fully before Week 2. It tells you everything about the project: what to build, how teams work, what is due each week, how to submit, and how you are graded.

---

## 1. What This Course Asks of You

There is **no written exam** in this course. Your grade comes from one thing you build across the whole semester: a complete analysis & design portfolio for **CampusBites**, a campus food ordering and delivery platform — reviewed at milestones and defended orally in Week 16.

**In one sentence:** you will play the role of a systems analyst team, taking CampusBites from raw requirements to a well-argued object-oriented design, applying GRASP/SOLID principles and GoF design patterns, and defending every decision you make.

| What you produce | When |
|---|---|
| Analysis & design models (use cases, domain, sequence, state, design class diagrams) | Weeks 2–15, milestone by milestone |
| A pattern catalog: 5+ design patterns applied with rationale | Weeks 13–15 |
| A final report + oral defense with **individual Q&A** | Week 16 |

---

## 2. The Project: CampusBites

**CampusBites** is a campus food ordering and delivery platform. Students order meals from campus restaurants via a mobile app; student couriers pick up and deliver the orders. The platform handles menus, ordering, payment (campus card, wallets, cash on delivery), real-time order tracking, notifications, ratings, and promotions.

### Key actors

| Actor | Goal |
|---|---|
| Student customer | Browse menus, order, pay, track delivery, rate |
| Restaurant manager | Manage menu items, accept orders, mark ready |
| Student courier | Accept delivery tasks, update delivery status |
| Campus card system | Third-party legacy payment API (read-only for us) |
| Notification service | SMS/push/in-app messages |

### Why this domain (hint: patterns live here)

Every design pattern you learn in class maps onto a natural CampusBites feature:

| Topic you will learn | Where it lands in CampusBites |
|---|---|
| State machines & State pattern | Order lifecycle: Created → Paid → Preparing → Ready → Delivered |
| Strategy | Pricing rules: happy-hour, student discount, bundle |
| Observer | Customers & couriers subscribe to order status changes |
| Adapter | Legacy campus-card API behind our `PaymentMethod` interface |
| Decorator | Meal customization: toppings, portions, add-ons |
| Factory / Builder / Command / Facade | Payment creation / order assembly / undoable operations / notification stack |

**Scope note:** this is an **analysis & design** course. You do not implement the full system. Deliverables are models, diagrams, and design documents — plus (optionally, for Bonus) small code sketches that prove a pattern works.

---

## 3. Teams & Roles

- The cohort forms **two teams of ~3 students** in Week 2 (lab session).
- Each team appoints a **Team Lead**: runs stand-ups, owns the submission calendar, interfaces with the instructor in reviews. Being Team Lead gives **no extra points**, but you must report on team management at the defense.
- **Roles rotate** across milestones so everyone touches every activity: analyst (requirements, use cases), modeler (domain/sequence/state diagrams), designer (DCD, patterns), reviewer (quality gate before submission), presenter (milestone reviews). In a 3-person team each of you will hold several roles during the semester — plan this in your team charter.
- **Golden rule — "you present it, you own it, you all know it":** at the final defense, **any member can be asked about any part** of the team's work. Individual Q&A is 25% of your grade. A team where only one person understands the domain model will fail that member — and it will show.

---

## 4. How Requirements Work

1. **The requirements pack** (issued in Week 4): the instructor provides the standard CampusBites requirements — vision, stakeholder list, ~20 functional requirements, non-functional requirements, and constraints.
2. **Three planned requirement changes** will be injected during the semester (e.g., a new payment method, a new promotion mechanic, a change to courier dispatch rules). This simulates a real client: expect your models to be *changed*, not frozen. How gracefully your models absorb change is part of the design grade — this is exactly what good OO design is for.
3. **Cross-team client review (Week 5):** the two teams act as each other's **client**. Team A presents its use case model to Team B in English; Team B interrogates it from the client's perspective ("What happens if the courier picks up late? Can I cancel after payment?"). Then roles swap. Asking sharp questions earns Bonus credit (see §8).

---

## 5. Milestones — What Is Due, Exactly

Every deliverable is **in English**. Every diagram needs a **source file** (.drawio or .puml) committed to your repo, not just an exported image.

> **Hard deadlines with exact dates** are maintained in a companion sheet: `CampusBites-Deadline-Schedule-and-Submission-Guide.md`. The table below tells you *what*; that sheet tells you *when, exactly*.

| Milestone | Due (lab of) | Deliverables checklist | Checked |
|---|---|---|---|
| **M0 Kickoff** | W2 — **Fri Sep 11** | ① Team charter (template: Appendix A) ② Stakeholder list ③ One-paragraph project vision ④ Git repository created & shared with instructor | pass/fail |
| **M1 Requirements** | W5 — **Sun Oct 4** | ① Vision & requirements list (mapped from the requirements pack + your elaboration) ② Use case diagram (all actors) ③ **2 detailed use case specifications** (template: Appendix B) — choose *Place Order* and one more | W05 cross-team client review |
| **M2 Analysis models** | W8 — **Sun Oct 25** | ① Domain model: conceptual classes, attributes, associations with multiplicities (10+ classes) ② **2+ sequence diagrams** (system operations, e.g. `placeOrder`, `pay`) ③ **Order state machine** complete with guards/actions/events ④ 1 activity diagram (e.g. order fulfillment) | W09 mid-term review |
| **M3 Design models** | W12 — **Sun Nov 22** | ① Design class diagram: traceable to sequence messages, visibility & navigability shown ② GRASP/SOLID application notes: for **every** major responsibility decision, name the principle and argue the alternative ③ Interaction diagram updated to DCD level | in-class, W10–12 |
| **M4 Patterns** | W14 — **Sun Dec 6** | ① Pattern catalog: **5+ GoF patterns** applied to CampusBites (template: Appendix C) ② Before/after refactoring narrative for at least one design smell ③ Updated DCD reflecting pattern applications | in-class, W13–15 |
| **M5 Defense** | W16 — **defense in class Dec 14–18; final package Sun Dec 20** | ① Final report (structure: Appendix D) ② Individual contribution logs (template: Appendix E) ③ All diagram source files ④ Pattern catalog cards | final defense |

**Late policy:** −10% per calendar day on that milestone, max 3 days, then 0 for the milestone. Plan ahead; OneDrive sync failure is not an excuse — push early, push often.

---

## 6. Submission Rules — Your Git Repository

1. **One repository per team**, created in Week 2, named `campusbites-team-<A|B>`, shared with the instructor (read access). The instructor's GitHub account is **`klausren`**.
2. **A milestone submission = a pushed tag.** At every deadline, create an annotated tag (`m0` … `m5`) and push it: `git tag -a m1 -m "M1 submission" && git push origin m1`. The tag — not your branch head — is the graded snapshot, and the README.md milestone status table must be updated with it. Full protocol, one-time registration email, and the GitHub-unreachable fallback: `CampusBites-Deadline-Schedule-and-Submission-Guide.md` §4.
3. **Repository layout** (keep it clean — this itself is graded under documentation quality):

```
campusbites-team-a/
├── README.md              # team, members, milestone status table
├── 01-requirements/        # M1 deliverables
├── 02-analysis/           # M2: domain, sequence, state, activity
├── 03-design/             # M3: DCD + principle application notes
├── 04-patterns/           # M4: catalog cards + refactoring narrative
├── 05-report/             # M5: final report + contribution logs
└── changes/               # instructor's requirement-change injections + your responses
```

4. **Commit discipline**: small, meaningful commits with clear messages (`Add state machine guards for cancel-before-pay`). Commit history is teamwork evidence — it feeds your Individual Contribution grade (§8). One giant "final commit" is a red flag.
5. **File formats**: Markdown for documents, .drawio or .puml for diagram sources, exported PNG/SVG alongside each diagram. No .docx/.pdf-only submissions.
6. **Language**: everything in English. A non-English deliverable is returned once for translation (−20% on that item); a second time it is not accepted.

---

## 7. Reviews & Defense — What Happens on Stage

| Event | Week | Format |
|---|---|---|
| **Cross-team client review** | W5 | Each team 25 min: 10 min present use case model in English, 15 min interrogation by the other team (as client) |
| **Mid-term review** | W9 | Each team 20 min: 8 min walkthrough of M1+M2, **10 min individual Q&A (every member questioned)**, 2 min feedback. Formative — this is where you find out what to fix |
| **Final defense** | W16 | Each team 30 min: 10 min design portfolio walkthrough, **15 min individual Q&A — each member questioned on ANY part of the work**, 5 min feedback. Summative |

**Defense question style** (from the question bank — samples):

- *Why does `orderTotal()` live in `Order` and not in `OrderController`?* (GRASP)
- *Your `Order` has a `status` field with a giant switch. Show me how the State pattern would change this.* 
- *A new payment method "ApplePay" must be added next semester. Which files change, and why is that acceptable (or not)?* (OCP / Factory)
- *Your teammate designed the domain model you just presented. Walk me through why `Courier` is associated with `Order` and not `OrderLine`.* (individual mastery)

With ~6 students in the room, there is no back row. Everyone speaks, everyone is questioned.

---

## 8. Grading

### Group Project Deliverables — 50% (shared by the team)

| # | Criterion | Weight |
|---|---|---|
| A1 | Requirements & use case model | 15% |
| A2 | Analysis models (domain, sequence, state) | 25% |
| A3 | Design class diagram | 20% |
| A4 | Principle application (GRASP/SOLID) | 15% |
| A5 | Pattern catalog (5+) | 20% |
| A6 | English documentation quality | 5% |

*(weights within the 50% group component)*

### Individual Defense & Contribution — 40% (yours alone)

| # | Criterion | Weight |
|---|---|---|
| B1 | Final defense individual Q&A (W16) | 25% |
| B2 | Contribution log & Git history | 15% |

### Bonus — up to 10%

| # | Bonus item | Cap |
|---|---|---|
| C1 | Extra patterns beyond 5, correctly applied | +3% each, up to +6% |
| C2 | Exceptional refactoring narrative (before/after with clear argument or metrics) | +4% |
| C3 | Outstanding documentation | +2% |
| C4 | High-quality client-review questions in W05 / peer sessions | +2% |

Weekly in-class exercises are **formative** — checked and discussed in class, not graded. They exist to feed your milestones.

---

## 9. Policies

- **Academic integrity**: plagiarized models = 0 for the milestone + academic misconduct procedure. **AI tools**: you MAY use AI for polishing English and brainstorming, if you disclose what and how in the report; undisclosed AI-generated bulk content is treated as plagiarism. Disclosure = no penalty — we care that you understand what you submit.
- **Attendance**: lab sessions (the 4th hour each week) build your milestone deliverables step by step; participation is part of the defense assessment.
- **Grade disputes**: in writing within 3 working days of grade publication.

---

## 10. Tips from Past Cohorts

1. **Start the domain model in pencil.** The first version is always wrong; the point is arguing your way to the second version.
2. **Never draw a diagram you cannot explain in one sentence per element.** If you can't, you decorated, not designed.
3. **Traceability is free points**: every message in your sequence diagrams should appear as an operation in your DCD. Check it before every milestone.
4. **The requirement changes are not sabotage — they are the exam.** A design that survives a change with 3 touched classes beats a design that needs 30.
5. **Rehearse the defense in English, out loud, with a timer.** Then rehearse it again with one teammate asking random questions from this guidebook.

---

## 11. FAQ

**Q: Do we write code?**
A: Models and documents are the deliverables. Small code sketches proving a pattern (e.g. a 40-line State implementation) earn Bonus (C2), but no full implementation is required or expected.

**Q: Can we choose a different domain than CampusBites?**
A: No. The two teams build the same domain so that cross-review and the client review work; your differentiation comes from design quality, not domain choice.

**Q: What if a teammate disappears?**
A: Report it early — the instructor mediates. Contribution logs + Git history decide the Individual component; a non-contributing member cannot pass the individual Q&A anyway.

**Q: How perfect must the English be?**
A: Precise and professional beats beautiful. Correct terminology ("association", "multiplicity", "cohesion") matters more than grammar. But careless English costs documentation points.

**Q: draw.io or PlantUML?**
A: Either. draw.io is friendlier for exploration; PlantUML is better for version-controlling changes. Both are accepted; pick one per team and stay consistent.

---

## Appendix A — Team Charter Template

```markdown
# Team Charter — CampusBites Team A
Members: (name, student ID, email)
Team Lead: (name) — responsibilities: ...
Project vision: (one paragraph)
Role rotation plan:
  | Milestone | Analyst | Modeler | Designer | Reviewer | Presenter |
  |---|---|---|---|---|---|
  | M1 | ... | ... | ... | ... | ... |
Working agreement: (meeting cadence, decision rule, conflict escalation)
Repository: (URL, all members + instructor have access)
```

## Appendix B — Use Case Specification Template

```markdown
## UC-01 Place Order
- Actor(s): Student customer
- Precondition: customer is logged in; at least one restaurant is open
- Main success scenario:
  1. Customer browses menus and adds items to cart
  2. Customer reviews cart and proceeds to checkout
  3. System computes total (pricing rules apply)
  4. Customer selects payment method and pays
  5. System creates order (status: Created → Paid) and notifies restaurant
- Extensions (alternates):
  3a. Payment fails: ...
  3b. Item sold out during checkout: ...
- Postcondition: order persisted; restaurant notified; customer sees tracking view
- Non-functional notes: checkout response < 2 s (NFR-3)
```

## Appendix C — Pattern Catalog Card Template

```markdown
## Pattern #1 — State (Behavioral)
- **Problem**: Order status transitions were one `status` field + a giant switch; adding "Refunding" state touched 6 files (violated OCP).
- **Solution**: State pattern — `OrderState` interface, concrete states (CreatedState, PaidState, ...), `Order` delegates status behavior.
- **Consequences**: adding a state = one new class (+ OCP); more classes overall; state transitions explicit and testable.
- **Where**: DCD p.3, sequence diagram "pay order", classes `order/OrderState.java` (sketch)
- **Why not Strategy?**: states have *ordering constraints* (legal transitions), strategies don't.
```

## Appendix D — Final Report Structure

1. Vision & stakeholders (updated from M1)
2. Requirements (incl. responses to the 3 requirement changes)
3. Analysis models (domain, sequence, state, activity)
4. Design: DCD + GRASP/SOLID application notes
5. Pattern catalog (cards from M4)
6. Architecture view (layering; MVC where applicable)
7. Retrospection: what changed since M1 and why (this section is graded — treat your project's history as an asset)
8. Individual contribution logs (Appendix E, one per member)

## Appendix E — Individual Contribution Log Template

```markdown
## Contribution Log — (name)
| Week | What I did | Evidence (commit / file / review) |
|---|---|---|
| W4 | Drafted UC-01 and UC-05 specs | commits 3f2a1b, 88c0d2 |
| W6 | Domain model v1: Order, OrderLine, Courier associations | 02-analysis/domain-v1.drawio |
| ... | ... | ... |
- Parts of the project I can explain best: ...
- Parts owned mainly by others that I have studied for the defense: ...
```

---

*Questions about this guidebook? Raise them in Week 2 lab, or open an issue in the course repository. Good luck — build something you will enjoy defending.*
