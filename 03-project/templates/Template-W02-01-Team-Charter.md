# Team Charter — CampusBites Team __

<!-- M0 deliverable ① · Due **Fri Sep 11** · pass / fail · Save as `TEAM-CHARTER.md` in your repository root -->

> **How to use this template.** Copy it into your team repository. Fill every blank. Delete this grey instruction block and every `> Hint:` line before you tag `m0`. Keep the headings — the instructor checks against them.
>
> **The one idea behind this document.** A charter is a contract **between the four of you**, not with the instructor. When a milestone slips, this is the document you point at.

---

## 1. Team name

`________________________________`

> One line. You will be called this all semester, including on stage at the defense.

## 2. Members

| Name | Student ID | Email | GitHub username | Standing role |
|---|---|---|---|---|
|  |  |  |  |  |
|  |  |  |  |  |
|  |  |  |  |  |

## 3. Standing roles

| Standing role | Who | What they own |
|---|---|---|
| **Team Lead** |  | Calendar, stand-ups, instructor contact, owns the submission moment |
| **Recorder** |  | Meeting notes, README, the written decision log |
| **Reviewer** |  | Quality gate before every submission — nothing ships unread |

> Being Team Lead earns **no extra points**. It earns you the job of reporting on team management at the defense (Guidebook §3).

## 4. Role rotation (M1–M5)

Five milestones, five roles. Rotate so nobody owns one job all term.

| Milestone | Analyst | Modeler | Designer | Reviewer | Presenter |
|---|---|---|---|---|---|
| M1 — Oct 4 |  |  |  |  |  |
| M2 — Oct 25 |  |  |  |  |  |
| M3 — Nov 22 |  |  |  |  |  |
| M4 — Dec 6 |  |  |  |  |  |
| M5 — Dec 20 |  |  |  |  |  |

> Four people, five roles: in most milestones one person holds two hats. Say so explicitly and swap next time. **Nobody holds "Presenter" for all five.**

**Worked example** (members A / B / C / D — copy the shape, put in your own names):

| Milestone | Analyst | Modeler | Designer | Reviewer | Presenter |
|---|---|---|---|---|---|
| M1 — Oct 4 | **A** | B | C | D | **A** |
| M2 — Oct 25 | **B** | C | D | A | **B** |
| M3 — Nov 22 | **C** | D | A | B | **C** |
| M4 — Dec 6 | **D** | A | B | C | **D** |
| M5 — Dec 20 | B | C | D | A | *all four* |

Rule: each person presents exactly once in M1–M4; the "double hat" moves one letter each milestone; M5 is a full-team defense.

## 5. Communication rules

| Question | Our answer |
|---|---|
| Where we talk (channel + link) |  |
| Reply expectation | e.g. *within 12 h on weekdays, 24 h on weekends* |
| Stand-up cadence | e.g. *10 min after every Tuesday lab* |
| How we decide (default rule) | e.g. *proposal in writing → 24 h to object → silence is consent* |
| What counts as an emergency | e.g. *"I cannot finish my part before the deadline"* |
| What we do with the instructor's change injections | e.g. *Lead logs it in `changes/` within 24 h, team estimates by the next lab* |

## 6. Conflict rule

When two members disagree on a technical decision, we:

1. `______________________________________________`
2. `______________________________________________`
3. If still unresolved after `____` hours, the `____________` decides, and the decision is written down here or in the decision log.

> Decide this **now**, not at 23:59 on a deadline. Teams that "never disagree" are teams that have not started working.

## 7. Definition of done (our quality gate)

A deliverable is ready to submit when **all** of these are true:

- [ ] It is written in English, and one member other than the author has read it.
- [ ] Every diagram has a committed source file (`.drawio` / `.puml`) **and** an exported image in `docs/diagrams/`.
- [ ] Every model element traces to something real: a requirement, a use case, or a decision we can defend.
- [ ] The README milestone table is updated.
- [ ] It is committed and pushed — and if it is a deadline, the tag is pushed (see `Template-W02-05`).

We add our own rule: `______________________________________________`

## 8. Project vision (one paragraph)

> Paste the final text from `Template-W02-03-Vision-Statement.md`. One paragraph, ≤150 words. Do not keep two versions — if this one differs from that file, that file wins.

`______________________________________________`

## 9. Repository

| Field | Value |
|---|---|
| Repository name | `campusbites-team-01` |
| URL | `https://github.com/____________/____________` |
| Members with write access |  |
| Instructor `klausren` invited | ☐ pending ☐ done |

## 10. Signatures

We have read this charter and we will hold each other to it.

| Name | Date |
|---|---|
|  |  |
|  |  |
|  |  |

---

## Quality bar — read before you submit

| ✗ Not a rule | ✓ A rule |
|---|---|
| "We will communicate well." | "We reply in the group within 12 hours on weekdays; the Lead escalates after 24 hours of silence." |
| "Everyone does their share." | "Every member owns at least one deliverable section per milestone; the Recorder names who wrote what in the README." |
| "We will avoid conflicts." | "If we disagree, each writes three sentences; the Lead decides if there is no consensus in 24 h." |
| "Code will be good." | "Nothing merges without a second pair of eyes; the Reviewer has veto until the deadline minus 24 h." |

**Test for every line you wrote:** could a stranger tell whether you kept it? If not, add the *when*, the *who*, or a number.

## Done when

- [ ] All required sections present: name · roles · rotation · communication · conflict.
- [ ] Every rule is **testable**.
- [ ] Rotation table has real names in every cell that matters, and no one repeats Presenter throughout.
- [ ] Vision paragraph pasted in (≤150 words).
- [ ] Repository URL correct and the instructor has access.
- [ ] File committed — the push and tag happen in `Template-W02-05`.
