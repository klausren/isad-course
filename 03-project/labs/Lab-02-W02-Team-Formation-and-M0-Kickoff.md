# Lab 02 · W02 — Team Formation & M0 Kickoff

> **ISAD · Fall 2026** · Lab block (last 2 h of the weekly 4 h) · Week 02, Sep 07 – Sep 13
> **Milestone**: **M0 — due Fri Sep 11, 23:59** · pass/fail
> **Slides**: `W02-Object-Oriented-Foundations.pptx`, pages 29–37

**Purpose of this lab.** Two things, in this order: learn to see *responsibilities* instead of methods, then ship your first milestone through the real pipeline — repo, invitation, tag. M0 is small on purpose. It exists to test your pipeline before anything is graded.

---

## 0. Before You Start (~5 min)

- [ ] The toolchain from Lab 01 still works: `git --version` runs, draw.io opens, you can log in to GitHub.
- [ ] You have your **W01 stakeholder list** (Exercise 1.2) — today it becomes an M0 deliverable.
- [ ] You have read the **Project Guidebook §3 (Teams & Roles)** and **Appendix A (Charter template)**.
- [ ] You have the **Deadline Schedule §4** open — you will follow it literally in Task E.
- [ ] You have opened the **M0 templates** in `templates/` — today you fill five of them:

  | Template | Task |
  |---|---|
  | [`Template-W02-01-Team-Charter.md`](../templates/Template-W02-01-Team-Charter.md) | C |
  | [`Template-W02-02-Stakeholder-List.md`](../templates/Template-W02-02-Stakeholder-List.md) | D1 |
  | [`Template-W02-03-Vision-Statement.md`](../templates/Template-W02-03-Vision-Statement.md) | D2 |
  | [`Template-W02-04-Repository-README.md`](../templates/Template-W02-04-Repository-README.md) | E |
  | [`Template-W02-05-M0-Submission-Checklist.md`](../templates/Template-W02-05-M0-Submission-Checklist.md) | F |
  | [`Template-W02-06-Responsibility-Worksheet.md`](../templates/Template-W02-06-Responsibility-Worksheet.md) | A |
  | [`Template-W02-07-Refactoring-Worksheet.md`](../templates/Template-W02-07-Refactoring-Worksheet.md) | homework |

> **The one rule that trips people:** a milestone is **only submitted when the tag is pushed**. `git push` alone is not a submission. Today you will do it once, slowly, while nothing is at stake.

---

## 1. What the Lecture Gave You

| From the lecture | The one line you need |
|---|---|
| A responsibility is **a reason to change** | Two methods that change for the same reason belong together. Two that change for different reasons do not. |
| Encapsulation, inheritance, composition, polymorphism | The four pillars — but today only *cohesion* matters. |
| Program to an interface, not an implementation | Why `PaymentService` beats `chargeCustomer()` inside `Order`. |
| Analysis is about **who is responsible** | Syntax was the warm-up. Deciding who owns what — that is analysis. |

**The sentence to remember:** *a responsibility is a reason to change.*

---

## 2. Demo — Instructor-Led (~10 min)

The instructor reads the messy `Order` class with you and shows how to look **through** the methods to the jobs underneath.

**The move to watch.** You are not counting methods. You are grouping them by *what would make each one change*.

```
placeOrder()      → coordinating
total()           → money      ─┐
applyDiscount()   → money      ─┘ changes when pricing rules change
chargeCustomer()  → payment    ── changes when a payment type appears
notifyRider()     → telling ─┐
sendSms()         → telling ─┤  changes when a channel is added
printReceipt()    → telling ─┘
```

Seven methods, **three jobs**. One class holding all three is doing three jobs, and has three unrelated reasons to change.

> **Remember this class.** We meet it again in **Week 11**, when GRASP tells us how to fix it properly. Today you only have to *see* the problem.

**Your notes:**

```
The three responsibilities I see:
  1. ________________________  2. ________________________  3. ________________________

The one method I could NOT place confidently, and why:
  ______________________________________________
```

---

## 3. Task A — Exercise 2.1: The Class That Does Everything (~25 min)

**Goal.** Turn seven methods into responsibilities. This is the exact judgement that drives your domain model (W6–W7), your GRASP notes (W11) and your SOLID audit (W12).

**Input.** The class on slide 30 — `Order` with `placeOrder`, `chargeCustomer`, `notifyRider`, `printReceipt`, `updateInventory`, `sendSms`, `applyDiscount`.
**Worksheet:** [`Template-W02-06-Responsibility-Worksheet.md`](../templates/Template-W02-06-Responsibility-Worksheet.md) — use it instead of a blank page; it has the two tables and the "reason to change" test built in.

### Steps

1. **Work in pairs first.** One keyboard, two brains. Ten minutes, individually first, then compare.
2. **Do not list the methods.** List the **responsibilities**. If your answer has seven rows, you copied the slide.
3. For each responsibility, fill all four columns:

| # | Responsibility (a noun phrase) | Methods that belong to it | The reason it would change |
|---|---|---|---|
| 1 | | | |
| 2 | | | |
| 3 | | | |
| 4 | | | |

4. **The test for every row:** say out loud *"this changes when \_\_\_\_\_ changes."* If two rows finish that sentence differently, they are genuinely separate. If they finish it the same way, merge them.
5. **Then:** for each responsibility, name the class that *should* own it. Write the class name even if you are unsure — being unsure out loud is the point.

| Responsibility | Class that should own it | One sentence why |
|---|---|---|
| | | |
| | | |

6. Report back as a group. Expect disagreement about `updateInventory()` — that one is genuinely arguable, and the argument is the learning.

**Done when**

- [ ] 3–5 responsibility rows (not 7 method rows).
- [ ] Every row has a "reason to change" that is **different** from the other rows.
- [ ] Every row names an owning class.
- [ ] You can say the whole table out loud in under 60 seconds.

### Stuck?

| Symptom | Fix |
|---|---|
| "I just listed the methods again." | Ask *what makes this method change?* not *what does this method do?* The answer to the first is a responsibility. |
| Everything feels like one responsibility | Push harder on the reason to change: does a new payment type force you to touch `total()`? No. Then they are separate. |
| Only two responsibilities found | Look at `updateInventory()` and `placeOrder()` again — one is about stock, the other is about orchestration. |
| Cannot name an owning class | Name it after the responsibility, not the data: `PaymentService`, `NotificationService`, `PricingCalculator`. |

---

## 4. Task B — Form the Team & Assign Roles (~8 min)

**Goal.** One team of four, with the four standing roles named and a role rotation plan covering M1–M5.

**Input.** The four of you in one room.

### Steps

1. **Confirm the team of four.** The whole cohort is one team. Today you name it, pick the standing roles, and fix the rotation.
2. **Appoint the Team Lead.** Runs stand-ups, owns the submission calendar, talks to the instructor at reviews.
   > **Being Team Lead earns no extra points** (Guidebook §3). It earns you the job of reporting on team management at the defense.
3. **Assign the standing roles** (from slide 34):

   | Standing role | Who starts | What they own |
   |---|---|---|
   | Team Lead | | Calendar, stand-ups, instructor contact |
   | Recorder | | Notes, README, decision lines |
   | Reviewer | | Quality gate before every submission |
   | Release Manager | | Repository, tags — the person who actually pushes `m0`…`m5` |

4. **Fill the rotation table.** Five milestones, five analysis/design roles — rotate so nobody owns one job all term. Copy this into your charter:

   | Milestone | Analyst | Modeler | Designer | Reviewer | Presenter |
   |---|---|---|---|---|---|
   | M1 (Oct 4) | | | | | |
   | M2 (Oct 25) | | | | | |
   | M3 (Nov 22) | | | | | |
   | M4 (Dec 6) | | | | | |
   | M5 (Dec 20) | | | | | |

**Done when**

- [ ] Both tables filled with real names.
- [ ] Every person holds a different role in at least two of the five milestones.
- [ ] Nobody holds "Presenter" for all five. (Tempting. Forbidden.)

> **Golden rule — you present it, you own it, you all know it.** At the final defense any member can be asked about **any** part of the team's work. Individual Q&A carries 55 of the 100 summative points, and the defense is 60% of your course grade.

---

## 5. Task C — Draft the Team Charter (~22 min)

**Goal.** Produce the M0 deliverable ①. This document is what you point at when a milestone slips.

**Input.** **Template [`Template-W02-01-Team-Charter.md`](../templates/Template-W02-01-Team-Charter.md)** (this is the detailed version of Guidebook Appendix A); your Task B tables.

### Steps

1. Copy the template into your repository root as `TEAM-CHARTER.md`.
2. Fill the five sections that slide 34 asks for:

   | § | What goes in | Watch out |
   |---|---|---|
   | 1 | Team name — one line | You will be called this all semester |
   | 2–3 | Members + standing roles (Lead / Recorder / Reviewer) with GitHub usernames | Paste the M1–M5 rotation table from Task B |
   | 4 | Communication rules: channel, reply expectation, stand-up cadence, emergency definition | "We will communicate well" is not a rule |
   | 5 | Conflict rule | Decide it **now**, not at 23:59 on a deadline |
   | 6 | Vision paragraph — drafted in Task D | Paste the same text as `01-requirements/vision.md` |

3. Keep the template's **Definition of done** (§7) and **Repository** (§9) sections — they are part of M0.
4. Sign it (§10). Three names, three dates.

**Quality bar.** "We will communicate well" is not a rule. "We reply in the group within 12 hours on weekdays; the Lead escalates after 24 hours of silence" is a rule.

**Done when**

- [ ] All five sections from slide 34 are present (team name / roles / communication / rotation / conflict).
- [ ] Every rule is **testable** — a stranger could tell whether you kept it.
- [ ] The file is committed (Task E covers the push).

### Stuck?

| Symptom | Fix |
|---|---|
| "We agree on everything, we don't need a conflict rule." | That is the moment to write it. Teams that never disagree are teams that have not started working. |
| Rotation table looks impossible for 4 people across 5 roles | Correct — in most milestones one person holds two hats. Say so explicitly and swap next time. |
| Charter is 3 lines long | You wrote a wish, not a contract. Add the *when* and the *who* to every sentence. |

---

## 6. Task D — Stakeholder List & Vision Paragraph (~18 min)

**Goal.** Produce M0 deliverables ② and ③.

**Input.** Your W01 Exercise 1.2 list; the CampusBites brief (Guidebook §2); slide 35.
**Templates:** [`Template-W02-02-Stakeholder-List.md`](../templates/Template-W02-02-Stakeholder-List.md) → `01-requirements/stakeholder-list.md`; [`Template-W02-03-Vision-Statement.md`](../templates/Template-W02-03-Vision-Statement.md) → `01-requirements/vision.md`

### D1. Stakeholder list — pick 5–8

Your W01 brainstorm may have 15+ names. **M0 asks for 5–8** (slide 33) — a curated list, not a dump. Choose for *coverage*, not for length: at least one per perspective in the template's coverage check.

The template adds two columns the lecture did not show — **where we heard it** and **priority**. Fill them; an unsourced stakeholder is a guess.

| Stakeholder | User? (✔/✖) | What they want | Why they have a stake | Source | Priority |
|---|---|---|---|---|---|
| | | | | | |
| | | | | | |
| | | | | | |
| | | | | | |
| | | | | | |
| | | | | | |
| | | | | | |
| | | | | | |

> **Stakeholder ≠ user.** Someone can be affected without ever logging in. Keep at least **two rows marked ✖** — the canteen admin who needs compliance reports, IT services who keep it running, the dorm supervisor handling the delivery hand-off. Missing them is exactly how real projects fail. Keep your longer W01 list in an appendix; you will add the rest in **Week 4**, when this becomes your actor list.

### D2. The vision paragraph — ≤150 words

Use the skeleton from slide 35:

```
For <target users>
who <what they want>,
CampusBites is a <what kind of system>
that <what it does>.
Unlike <the current alternative>,
it <the one thing that makes it better>.
```

**Good vs bad** — the difference is specificity:

| ✗ Weak | ✓ Strong |
|---|---|
| "CampusBites is a convenient, modern, user-friendly platform that makes campus life better." | "For students living in dorms who want hot food without queueing, CampusBites is a mobile ordering platform that connects dorm kitchens and student couriers. Unlike calling the canteen and waiting at the gate, it lets a student track the courier in real time and pay with the campus card they already carry." |

**Done when**

- [ ] 5–8 stakeholder rows, ≥2 marked ✖, every row has a "why" **and a source**.
- [ ] All five coverage perspectives named (demand / supply / operations / money-compliance / technical).
- [ ] Vision paragraph ≤150 words, following the skeleton.
- [ ] The vision names **who**, **what**, and **what it beats** — all three.
- [ ] No adjective survived that you could not prove ("modern", "seamless", "user-friendly" → cut).
- [ ] The same vision text is pasted into `TEAM-CHARTER.md` §8 — one version only.

### Stuck?

| Symptom | Fix |
|---|---|
| Vision sounds like an advert | Delete every adjective. What is left is either a fact or an empty sentence. |
| Cannot name the "unlike" | You have not studied the current process. Go and watch someone order lunch today. |
| All 8 stakeholders are users | You listed job titles, not stakeholders. Ask *who is affected but never logs in?* |

---

## 7. Task E — Create the Repo, Invite the Instructor, Register (~20 min)

**Goal.** Produce M0 deliverable ④ and send the one-time registration email.

**Input.** One GitHub account (any member's), Deadline Schedule §4.2.

### Steps

1. **Create the repository** under one member's account. Name it exactly:

   ```
   campusbites-team-01
   ```

2. **Create the folder skeleton** (Guidebook §6). Run in the repo root:

   ```bash
   mkdir -p 01-requirements 02-analysis 03-design 04-patterns 05-report changes docs/diagrams
   touch docs/diagrams/.gitkeep
   git add . && git commit -m "M0: repository skeleton" && git push
   ```

   > `docs/diagrams/` is where every diagram lives from **Week 3** onwards (convention formalised in Lab 03). Create it now — the path must be right *before* M1, not during it.

3. **Invite the instructor.** GitHub → your repo → *Settings* → *Collaborators* → *Add people* → **`klausren`** → role **read** is enough.
   > Do not wait for the instructor to accept. The invitation being *sent* is what M0 checks.

4. **Write `README.md`** with the milestone status table (Deadline Schedule §4.4):

   ```markdown
   # CampusBites — Team <A|B>
   Members: <names>   ·   Team Lead: <name>
   Repo: https://github.com/<owner>/campusbites-team-01

   | Milestone | Due        | Tag | Submitted at | Status         |
   |-----------|------------|-----|--------------|----------------|
   | M0        | 2026-09-11 | m0  |              | 🚧 in progress |
   | M1        | 2026-10-04 | m1  |              |                |
   | M2        | 2026-10-25 | m2  |              |                |
   | M3        | 2026-11-22 | m3  |              |                |
   | M4        | 2026-12-06 | m4  |              |                |
   | M5        | 2026-12-20 | m5  |              |                |
   ```

   > This table is the **first thing the instructor reads** at every deadline. Keep it true.

5. **Send the one-time registration email** — one email per team (Deadline Schedule §4.2):

   ```
   Subject: [ISAD] Repo registration — Team 01

   Team name:    Team 01
   Members:      Full Name 1 (leader), Full Name 2, Full Name 3
   Repo URL:     https://github.com/xxx/campusbites-team-01
   Access:       klausren invited as collaborator (done / pending)
   ```

**Done when**

- [ ] Repo exists with the correct name and the full folder skeleton.
- [ ] `klausren` invited as collaborator.
- [ ] `README.md` committed with the milestone table.
- [ ] Registration email sent.

### Stuck?

| Symptom | Fix |
|---|---|
| `failed to push some refs` | Someone pushed first. `git pull --rebase` then `git push`. |
| `Permission denied (publickey)` | You cloned with SSH but have no key. Switch to HTTPS: `git remote set-url origin https://github.com/<owner>/<repo>.git` |
| Password rejected on push | GitHub no longer accepts account passwords. Use a **Personal Access Token** (Settings → Developer settings → Tokens (classic) → scope `repo`) as the password, or set up SSH. |
| Cannot reach GitHub at all | Do **not** wait. Register by email anyway with a note, and use the fallback (Deadline Schedule §4.5): zip the whole repo folder **including `.git/`** and email it before the deadline, subject `[ISAD] M0 fallback — Team A`. Then restore the repo within 3 days. |

---

## 8. Task F — Submit M0: Tag and Push the Tag (~12 min)

**Goal.** Turn your work into an actual submission. **This is the step students get wrong every year.**

**Input.** Four committed deliverables: charter, stakeholder list, vision, README in a registered repo.
**Checklist:** [`Template-W02-05-M0-Submission-Checklist.md`](../templates/Template-W02-05-M0-Submission-Checklist.md) — run it line by line, out loud.

### Steps

1. **Check the four M0 items are in the repo** (slide 33):

   | # | Item | Where it lives | Ready? |
   |---|---|---|---|
   | ① | Team charter | `TEAM-CHARTER.md` (repo root) | ☐ |
   | ② | Stakeholder list (5–8) | `01-requirements/stakeholder-list.md` | ☐ |
   | ③ | One-paragraph vision (≤150 words) | `01-requirements/vision.md` — and the same text in charter §8 | ☐ |
   | ④ | Repository registered | `README.md` + `klausren` invited + email sent | ☐ |

2. **Commit whatever is left:**

   ```bash
   git add .
   git commit -m "M0: charter, stakeholders, vision"
   git push
   ```

3. **Tag the commit — this is the submission:**

   ```bash
   git tag -a m0 -m "M0 submission"
   git push origin m0
   ```

4. **Verify it is actually on the remote.** Do not trust the absence of an error message:

   ```bash
   git ls-remote --tags origin
   ```

   You must see `refs/tags/m0`. If you do not, M0 has not been submitted.

5. **Update the README table** with the tag name and timestamp, commit and push again:

   ```bash
   git add README.md && git commit -m "M0: record submission" && git push
   ```

> **A push without a tag is not a submission.** The tag — not your branch head — is the graded snapshot. Full protocol: Deadline Schedule §4.3.

**Done when**

- [ ] `git ls-remote --tags origin` lists `refs/tags/m0`.
- [ ] The four items are inside the tagged commit (check with `git show m0 --stat`).
- [ ] README table updated.

### Stuck?

| Symptom | Fix |
|---|---|
| Tagged the wrong commit | Before the deadline only: `git tag -f -a m0 -m "M0 submission" <correct-sha>` then `git push -f origin m0`. After the deadline, nothing counts. |
| `git push origin m0` silently did nothing | Tags are **not** pushed by a plain `git push`. You must name the tag explicitly, or use `git push --follow-tags`. |
| Pushed more work after tagging | Re-tag with `-f` before 23:59. Anything pushed after the deadline does not count. |
| Missed the deadline | Late policy: −10% per calendar day, max 3 days, then 0. M0 is pass/fail — email the instructor immediately. |

---

## 9. Before You Leave (~5 min)

- [ ] **The team exists** — 3 members, a named Lead, and a rotation plan covering M1–M5.
- [ ] **The four M0 items are in the repo** — charter, stakeholders, vision, registered repo with `klausren` invited.
- [ ] **`refs/tags/m0` is on the remote** — verified with `git ls-remote --tags origin`, not assumed.

**The countdown** (from slide 37):

| When | Do this |
|---|---|
| **Today — in the lab** | Form the team. Appoint the Lead. Draft the charter. |
| **Wed Sep 09** | Stakeholder list. Vision paragraph, first draft. |
| **Thu Sep 10** | Create the repo. Invite `klausren`. Push the README. |
| **Fri Sep 11 · 23:59** | Tag `m0` and push the tag. **This is the submission.** |

> **M0 is small on purpose.** It exists to test your pipeline before anything is graded. A failed M0 blocks nothing yet — it is your rehearsal.

---

## 10. Homework (before Week 3)

1. **Refactor the Order class.** Extract **one interface and two implementations** from the messy version in Task A (e.g. `PaymentMethod` with `CardPayment` / `CampusCardPayment`). Small is fine — 40 lines is plenty.
2. **Push it to your team repo.** A commit history is your contribution evidence. Start it now.
3. **Read Larman on OO basics** — chapters as assigned. Skim for vocabulary, not for mastery.
4. **Draft your vision paragraph** if it did not survive Task D.

> Stuck on the refactor? Bring the **broken** version to next week's lab. That is a better question than no question.

---

## 11. Reference

| Document | What it answers |
|---|---|
| `../CampusBites-项目指导书-Project-Guidebook.md` | §3 Teams & roles · §5 Milestones · §6 Submission rules · Appendix A charter template |
| `../templates/README-模板索引-Template-Index.md` | Which template to use for which deliverable, and where to save it |
| `../CampusBites-Deadline-Schedule-and-Submission-Guide.md` | §4.2 registration email · §4.3 tag protocol · §4.4 README table · §4.5 GitHub-unreachable fallback |
| `../CampusBites-Lab-Guide-实验指导书.md` | The 16-week lab plan at a glance |
| `../Course-Project-Grading-Rubric.md` | How M0 and later milestones are scored |
| `../../00-课程文件/Course-Syllabus-课程标准.md` | Full syllabus and weekly schedule |
| `Lab-01-W01-Toolchain-and-First-UML.md` | Toolchain setup, first domain model, Exercise 1.2 stakeholder method |

**Submission address:** `https://github.com/<owner>/campusbites-team-01` — instructor GitHub account **`klausren`** (read access is enough).

*Lab questions go to the instructor in class, or open an issue in the course repository.*

---

*Lab 02 · v1.0 · Information Systems Analysis and Design · Fall 2026*
