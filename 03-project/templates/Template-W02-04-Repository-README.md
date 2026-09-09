# README template — campusbites-team-___

<!-- M0 deliverable ④ · Due **Fri Sep 11** · pass / fail · Save as `README.md` in the repository root -->

> **How to use this template.** This *is* the README of your team repository — copy its content into `README.md` and fill the blanks. Delete this block once the repository is real.
>
> **Why it is graded.** A clean, navigable repository is part of your documentation quality mark. The instructor should be able to open this file and find any milestone artefact in under 30 seconds.

---

````markdown
# CampusBites — Team ___

> Information Systems Analysis and Design · Fall 2026 · Team project repository

## 1. Team

| Name | Student ID | GitHub | Standing role |
|---|---|---|---|
|  |  |  | Team Lead |
|  |  |  | Recorder |
|  |  |  | Reviewer |

Team charter: [`TEAM-CHARTER.md`](./TEAM-CHARTER.md)

## 2. One-paragraph vision

_(paste from `01-requirements/vision.md` — keep them identical)_

## 3. Milestone status

| Milestone | Due | Deliverable | Tag | Status |
|---|---|---|---|---|
| M0 Kickoff | Fri Sep 11 | charter · stakeholder list · vision · repo | `m0` | ☐ in progress |
| M1 Requirements | Sun Oct 4 | vision & requirements list · use case diagram · 2 use case specs | `m1` | ☐ not started |
| M2 Analysis models | Sun Oct 25 | domain model · 2+ sequence diagrams · order state machine · activity diagram | `m2` | ☐ not started |
| M3 Design models | Sun Nov 22 | design class diagram · GRASP/SOLID application notes | `m3` | ☐ not started |
| M4 Patterns | Sun Dec 6 | pattern catalog (5+) · refactoring narrative · updated DCD | `m4` | ☐ not started |
| M5 Defense | Sun Dec 20 | final report · contribution logs · all sources · catalog cards | `m5` | ☐ not started |

> A submission exists only when the **tag is pushed** — see §6.

## 4. Repository layout

```
campusbites-team-___/
├── README.md               # this file — team, vision, milestone status
├── TEAM-CHARTER.md         # M0 ①
├── 01-requirements/        # M1: vision, stakeholder list, requirements, use cases
├── 02-analysis/            # M2: domain model, sequence, state, activity
├── 03-design/              # M3: design class diagram, principle notes
├── 04-patterns/            # M4: pattern catalog cards, refactoring narrative
├── 05-report/              # M5: final report, contribution logs
├── changes/                # instructor requirement-change injections + our responses
└── docs/diagrams/          # ALL diagram sources (.drawio/.puml) + exported PNG/SVG
```

**Conventions**

- Diagram sources go in `docs/diagrams/` with an exported image next to each one — one place, no hunting.
- Markdown for documents, `.drawio` or `.puml` for diagrams. No `.docx`-only deliverables.
- Everything in **English**.
- Small, meaningful commits (`Add state machine guards for cancel-before-pay`). One giant "final commit" is a red flag.

## 5. How we work

| Item | Answer |
|---|---|
| Chat channel |  |
| Stand-up |  |
| Decision rule |  |
| Conflict rule |  |

Full detail in [`TEAM-CHARTER.md`](./TEAM-CHARTER.md).

## 6. How to submit

```bash
git add -A
git commit -m "M0: charter, stakeholders, vision"
git push origin main

git tag -a m0 -m "M0 submission"
git push origin m0          # <-- without this line, nothing was submitted
```

Verify from a clean place:

```bash
git ls-remote --tags origin    # m0 must appear
```

Full protocol (registration email, GitHub-unreachable fallback, late policy):
`CampusBites-Deadline-Schedule-and-Submission-Guide.md` §4.

## 7. Decision log

| Date | Decision | Why | Who |
|---|---|---|---|
|  |  |  |  |
````

---

## Done when (repository, M0)

- [ ] Repository name is `campusbites-team-___` and it is **not** private to one member.
- [ ] All three members can push; instructor `klausren` has access.
- [ ] `README.md` follows the layout above and the milestone table is filled.
- [ ] `TEAM-CHARTER.md` and `01-requirements/` exist.
- [ ] One small test commit proves the pipeline works **before** the deadline.
- [ ] Tag `m0` created **and pushed**.
