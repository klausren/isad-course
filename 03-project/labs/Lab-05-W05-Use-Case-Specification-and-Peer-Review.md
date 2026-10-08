# Lab 05 · W05 — Use Case Specification & Peer Review

> **ISAD · Fall 2026** · Lab block (last 2 h of the weekly 4 h) · **Week 05, delivered Thu Oct 08** (National Day holiday pushed it)
> **Milestone**: ⚠️ **No tag today.** The two exercises below are done in class as practice. **M1 itself is now due Sun Oct 25 (W08)** — that is when you tag `m1`. See the notice below.
> **Slides**: `W05-Use-Case-Specification-and-Scenarios.pptx`, pages 28–37  
> **Handout**: `W05-Handout.html`, sections D–G (page 2)

**Purpose of this lab.** The use case diagram is done; M1 is two thirds text. Today you learn what a specification *is* — nine fields, actor–verb–object steps, a postcondition per exit — by dissecting a bad one, then you apply the twelve-question checklist to each other's work. **M1 closes today**: four artefacts, one tag, one verification command, and the tag belongs to the Release Manager, in this room, not on Sunday night.

---

> ⚠️ **READ FIRST — this lab was rescheduled.**
>
> W05 was originally delivered Sep 28 – Oct 04, with **M1 due at the end of that week**.
> The National Day holiday (Oct 1–8) pushed the delivery to **Thu Oct 08**, so the milestone
> had to move with it. **M1 is now due Sun Oct 25 (W08)**, one week after this class.
>
> **What this means for you today:**
>
> | | |
> |---|---|
> | **Do today** | Exercise 5.1 (find the five planted defects) and Exercise 5.2 (the twelve-question review, both directions). Treat them as **rehearsal for M1**. |
> | **File today** | `docs/reviews/m1-spec-review.md` — you may still push it, it is useful evidence of individual contribution. Just **do not tag**. |
> | **Do NOT do today** | Do not tag `m1`. Do not push a tag. M1 is three weeks away and depends on **your own topic**, which is still being chosen. |
>
> **Why M1 moved:** the team now selects its **own project** rather than analysing the fixed
> CampusBites case. You cannot write a use case specification before the topic is approved, so
> M1 sits after topic selection, not before it.
>
> The exercises are unchanged in substance — same slides, same five defects, same checklist.
> Only the tagging step moves.

---


**No programming today.** Prose, tables, and a Markdown review form. The only code you read is the PlantUML homework you commit tonight.

---

## 0. Before You Start (~5 min)

- [ ] M0 and the W04 push are done: `git log --oneline -5` shows your Week 04 work.
- [ ] You have **two** use case drafts: `Place Order` plus one more of your own choosing.
- [ ] You have the **twelve-question checklist** in front of you (slide 25, handout section E).
- [ ] You know today's four standing roles: **Lead** (keeps time), **Recorder** (writes the one page), **Reviewer** (plays the client), **Release Manager** (pushes and checks the tag).
- [ ] Blank paper for Exercise 5.1 — you answer on paper **first**, before any answer key.

> **The one rule that ends the semester's arguments:** a milestone is **only submitted when the tag is pushed and you have read `git ls-remote --tags origin`**. A `git push` is not a submission.

---

## 1. What the Lecture Gave You

| From the lecture                                                | The one line you need                                                                                          |
| --------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------- |
| A name is a label; a specification is a contract                | M1 is one third diagram, two thirds specification — and the specification is the hard third.                   |
| Nine fields, three compulsory                                   | Main scenario, at least one extension, name + primary actor. The other six earn their place by being testable. |
| One step = one actor–verb–object sentence                       | *The system authorises the amount with the provider.* If you cannot point at what changed, it is not a step.   |
| Write about the system, not the screen                          | No page, no button, no dropdown, no modal. The interface arrives in W10 and the spec must not notice.          |
| An extension resumes; an exception ends                         | *Resume at step 5* or *ends here*. A branch with no destination is a rumour.                                   |
| A postcondition that covers only success is not a postcondition | It is an outcome. Write the failure end state or the kitchen discovers it by accident.                         |

> **The sentence to remember:** *a postcondition that covers only success is not a postcondition — it is an outcome.* (Slide 37, item 03: if you remember one, make it this.)

---

## 2. Demo — Instructor-Led (~25 min)

The instructor puts a full **Place Order** specification on the board and walks it end to end, then breaks it at step 4 four times.

Watch for these four branch points (slide 18):

| Branch | Condition                                                     | Kind          | What the system does                                                           | Then            |
| ------ | ------------------------------------------------------------- | ------------- | ------------------------------------------------------------------------------ | --------------- |
| **4a** | item sold out between browsing and paying                     | Extension     | reports the item, keeps the rest of the cart, offers an update                 | **resume at 1** |
| **4b** | no courier assigned and the restaurant closes in under 20 min | Extension     | accepts the order, sets *Scheduled Delivery*, shows the later time             | **resume at 5** |
| **4c** | payment provider times out or errors                          | **Exception** | creates the order in *Pending Payment*, queues one retry, notifies the student | **ends here**   |
| **4d** | the student already has an open order at this restaurant      | **Exception** | refuses the second order, displays the existing one                            | **ends here**   |

Three of the four **resume** the main line. One does not. That single difference is the whole extension-vs-exception distinction.

Tick what you actually saw, not what you assume:

- [ ] Step 5 has three slots — subject, verb, object — and the object is one of *our* nouns.
- [ ] Six of the eight main steps start with "the system". That is normal, not a smell.
- [ ] There is **no** `if` anywhere in the main success scenario.
- [ ] The last postcondition says: *no kitchen ticket exists unless the order is Accepted.* ← that is the line the kitchen would otherwise have to discover by accident.
- [ ] The branch count (2 extensions + 1 exception) is **not** a target. It is what this use case happened to need.

**Notes — take these down verbatim, you will use them in Task C:**

```
The postcondition that earns its place: ______________________________________________

A branch without a destination is: ____________________________________________________

The one sentence I will use when the client asks "what if payment fails?":
____________________________________________________________________________________
```

> **Common-error gallery (slide 19), six defects seen in real submissions:** the UI leaked into step 1; "System validates the payment" has no observable result; two primary actors; a precondition nobody can set up; a postcondition for success only; an extension that says *None*.

---

## 3. Task A — Exercise 5.1: Find the Five Planted Defects (~30 min)

**Goal.** Find all five planted defects and write the corrected sentence for each. A finding is *"step 2 is wrong"*; a fix is *"step 2 should read …"*.

**Input.** The broken specification below (slide 29 / handout section D). It is a real submitted draft, lightly trimmed.

```text
Use Case:      Process the order
Scope:         CampusBites
Level:         User goal
Primary actor: Student and Kitchen Staff

Preconditions:
  The student is logged in.

Main success scenario:
  1  User navigates to the cart page.
  2  User clicks the Pay button.
  3  System validates the payment.
  4  Order is created.

Extensions: None.

Postconditions:
  The order is created successfully.
```

### Steps

1. **Read it alone. Five minutes. No talking.** The Lead starts the clock and says nothing until all four are done. Pen on paper.
2. Each of you writes **five rows**: where the defect is, which criterion it breaks, and the corrected sentence you would actually write.
3. **Merge onto the Recorder's page.** Recorder writes; everyone dictates their own rows.
4. **Keep the rows you disagreed on.** Do not resolve them — mark them `DISAGREE` and move on. Those rows are the raw material for the client review agenda.
5. Check your five against the authoritative list (slide 30) **after** you have committed to your own answer:
   | # | Where                       | Which criterion it breaks                    |
   | - | --------------------------- | -------------------------------------------- |
   | 1 | Name + primary actor        | name check + one-actor rule                  |
   | 2 | Preconditions               | checklist C1 — preconditions set up the test |
   | 3 | Steps 1–2                   | observable-response rule                     |
   | 4 | Step 4                      | actor–verb–object sentence                   |
   | 5 | Extensions + postconditions | postcondition must cover every exit          |
6. Now write the fixes on the Recorder's page, in the shape of slide 31: verb + object name, one primary actor, two real preconditions, 5–9 observable steps, at least one extension with a resume destination, at least one exception that ends, and **one postcondition per exit**.

### Done when

- [ ] Five rows on the page, each with a **corrected sentence** — not a complaint.
- [ ] Row 1 names **both** faults in that line (bad name *and* two primary actors). They are two defects sharing one line.
- [ ] Row 5 states that `Extensions: None` **and** "created successfully" are two faces of the same defect.
- [ ] Your fixes name at least **two new states** that the broken draft never mentioned (for example *Scheduled*, *Pending Payment*).
- [ ] Every DISAGREE row is still visible on the page.

### Stuck?

| Symptom                                                    | Fix                                                                                                                                                                                                                           |
| ---------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| I found four and I am sure one is missing                  | The one you skipped is in a **field you skimmed**. Count the fields: is anything absent that should be present? `Extensions: None` is a claim, not an omission — check whether it should hold.                                |
| I merged defects 3 and 4 into one "it's badly written" row | They break **different** criteria. Step 1–2 leak the **interface**; step 4 has **no subject and no observable result**. Separate rows, separate criteria.                                                                     |
| I only wrote "Extensions: None is wrong"                   | That is half a finding. The postcondition says "created successfully", so the failure path leaves the system in a state **nobody wrote down**. Say both.                                                                      |
| I rewrote the whole spec from scratch                      | You skipped the exercise. Name the defect location first, then the sentence. Full rewrite is Exercise 5.1's *answer*, not its *method*.                                                                                       |
| My corrected precondition is longer than the original      | Good. *"Student is authenticated for this campus; today's menu is published with at least one item available"* is testable. *"The student is logged in"* is not — logged in since when, with which role, at which restaurant? |
| We cannot agree on whether "Kitchen Staff" is a defect     | It is. Two primary actors means two people must be present, which means it is two use cases. Kitchen Staff becomes **secondary**, or it gets its own use case.                                                                |

> **Calibration:** five out of five = pass. Four out of five = you found the easy four (slide 29 footer). The criterion each one breaks is the point — a defect without a criterion is an opinion.

---

## 4. Task B — Exercise 5.2: Review a Partner Spec (~30 min)

**Goal.** Apply the twelve-question checklist to somebody else's specification and produce a review that is **evidence**, not a conversation.

**Input.** Slide 25 (the checklist), slide 32 (the form), slide 33 (the rating scale). Output file: `docs/reviews/m1-spec-review.md`.

### The twelve questions

| Group                                                       | #  | Question                                      |
| ----------------------------------------------------------- | -- | --------------------------------------------- |
| **A · Structure**<br />*can I navigate it in 30 s?*         | A1 | Is the name a verb + object?                  |
|                                                             | A2 | Is there **exactly one** primary actor?       |
|                                                             | A3 | Are **scope** and **level** stated?           |
|                                                             | A4 | Are all **nine fields** present, in order?    |
| **B · Content**<br />*would a tester know what to run?*     | B1 | Is the main scenario 5–9 steps, with no `if`? |
|                                                             | B2 | Is every step an **observable response**?     |
|                                                             | B3 | Is there at least one extension?              |
|                                                             | B4 | Does **every branch say where it goes**?      |
| **C · Consequences**<br />*does anyone know the end state?* | C1 | Do preconditions **set up the test**?         |
|                                                             | C2 | Is there a postcondition **per exit**?        |
|                                                             | C3 | Is the exception **end state** written?       |
|                                                             | C4 | Can I trace a step to a test?                 |


Every box takes one of exactly two legal answers: **a tick**, or **the sentence you would run as a test**. *"Looks fine"* is not an answer.

### The rating scale

| Score           | What it looks like                                                    | What you write                                       | Next action                                                |
| --------------- | --------------------------------------------------------------------- | ---------------------------------------------------- | ---------------------------------------------------------- |
| **3 — sound**   | A tester could run it today without asking a question.                | "Groups A–C all pass. One note on wording."          | Move on.                                                   |
| **2 — fixable** | The goal is clear and the main path works; a group or two is missing. | The **corrected sentences** — two or three, not ten. | Author applies them, then the review is re-run.            |
| **1 — rewrite** | Goal unclear, two goals fused, or no exceptions at all.               | Which criterion fails. One sentence.                 | Author rewrites; **the reviewer does not touch the file**. |

### Steps

1. **Pair up inside the group.** There is no second team: **Reviewer A** reads the spec written by **B** and **D**; **Reviewer B** reads the spec written by **A** and **C**. Say the swap out loud.
2. **Read alone, 5 minutes, in silence.** Mark the checklist on the **author's** copy. No discussion yet.
3. **10 minutes: the author defends.** The author answers; the reviewer **records, does not argue**. A reviewer who wins the argument has destroyed the review.
4. **Score it 3 / 2 / 1.** If you scored 2, write the corrected sentences — two or three, not ten. If you scored 1, name the failing criterion and stop; you do not edit the file.
5. **Whole team, 10 minutes.** Read out the rows where the group disagreed. Record them; do not resolve them.
6. **Fill all five boxes** of the review form and commit it. Each of you writes **your own section** — the Recorder merges but does not write all four.
   ```bash
   mkdir -p docs/reviews docs/use-cases
   ```
   ```markdown
   # M1 Specification Review — <your name>

   **Spec reviewed:** docs/use-cases/<file>.md · **Author:** <name> · **Words:** <count>

   ## Box 1 — Groups A · Structure
   | Q | Verdict | The sentence I would run as a test |
   |---|---|---|
   | A1 name is verb + object | ☐ pass ☐ fail | |
   | A2 exactly one primary actor | ☐ pass ☐ fail | |
   | A3 scope and level stated | ☐ pass ☐ fail | |
   | A4 all nine fields, in order | ☐ pass ☐ fail | |

   ## Box 2 — Groups B · Content
   Main steps found: ____ · Conditionals in the main scenario: ____ · UI nouns named: ____
   | Q | Verdict | The sentence I would run as a test |
   |---|---|---|
   | B1 main scenario 5–9 steps, no if | ☐ pass ☐ fail | |
   | B2 every step observable | ☐ pass ☐ fail | |
   | B3 at least one extension | ☐ pass ☐ fail | |
   | B4 every branch names its destination | ☐ pass ☐ fail | |

   ## Box 3 — Group C · Consequences
   | Q | Verdict | The sentence I would run as a test |
   |---|---|---|
   | C1 preconditions set up a test | ☐ pass ☐ fail | |
   | C2 postcondition per exit | ☐ pass ☐ fail | |
   | C3 exception end state written | ☐ pass ☐ fail | |
   | C4 step traceable to a test | ☐ pass ☐ fail | |

   ## Box 4 — Score and fixes
   Score: ☐ 3 sound ☐ 2 fixable ☐ 1 rewrite
   Corrected sentences I am handing over (2–3, not ten):
   1.
   2.
   3.

   ## Box 5 — Questions for the client (verbatim, not paraphrased)
   1.
   2.
   ```
7. Commit the form, ideally in the **same commit** as the fix it produced — the diff then shows the spec improving, which is worth more than the review itself.
   ```bash
   git add docs/reviews/m1-spec-review.md docs/use-cases/
   git commit -m "W05: Ex 5.2 spec review (both directions) + fixes applied"
   git push
   ```

### Done when

- [ ] Both directions exist — A→(B,D) and B→(A,C). One direction is half the exercise.
- [ ] All **five** boxes are filled; Box 5 is **verbatim**, not paraphrased.
- [ ] Every checklist row is a tick **or** a test sentence. Zero "looks fine".
- [ ] Every score-2 finding has the **corrected sentence** attached, and the author has applied it.
- [ ] Your own section is in your own words and your own commit.
- [ ] You have **not** edited the other person's spec file yourself when you scored it 1.

### Stuck?

| Symptom                                                                 | Fix                                                                                                                                                                                                    |
| ----------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| Everything scored 3                                                     | You did not read it. Go back to **group C** and look for the postcondition on the failure path — that is where defects hide. An all-3 review is a review nobody did.                                   |
| I want to rewrite their spec because it is bad                          | You may not. Hand over the **sentence you would run**; the author decides the wording. A reviewer who rewrites the spec has taken the author's work and told them nothing.                             |
| The goal itself looks wrong                                             | Never a 2. Ask a question, record it in Box 5. **Only the client may change what the system is for** — and the client is the instructor, in W07.                                                       |
| I cannot decide whether "the system notifies the student" is observable | Ask *what would I look at afterwards?* If there is nothing to look at, it is not observable. If there is — an inbox, a screen, a push notification — it is.                                            |
| The spec has only four main steps, so I scored it 1                     | Wrong reason. B1 says **5–9 steps** — ask for the missing steps first, then re-score. Four steps alone is a **2**, not a **1**.                                                                        |
| Box 5 is empty because "we resolved everything"                         | Then nothing was unresolvable. Anything you would not decide on your own goes in Box 5 — verbatim. **An empty Box 5 means the review was cosmetic**, and Box 5 is the agenda for the M1 client review. |
| We are two people, there is nobody else to review                       | There is no second team. Peer review happens **inside** the group of four, in pairs. From W05 the client is the instructor.                                                                            |

---

## 5. Task C — Close Out M1: Finalise, Tag, Verify (~25 min)

> 🔴 **NOT TODAY.** This section is **parked**, not cancelled. It runs in **W08 (Oct 26 – Nov 01)**,
> when M1 is actually due. It also depends on your **own topic**, which is still being chosen —
> so there is nothing to finalise yet.
>
> **What to do instead today:** §0–§4 only. Then push the review file (§4's output) and stop.
> Reading §5 now is still useful — it tells you what M1 will demand of you in three weeks.

**Goal.** Four artefacts, one tag, one command whose output you read.

**Roles.** Lead calls the time and the go/no-go. Recorder owns the files. Reviewer confirms group A–C pass on **both** specs. **Release Manager pushes and tags** — this cannot be done at home on Sunday night.

### Steps

1. **Freeze the requirements list.** `docs/requirements.md`, one row per requirement, functional and non-functional marked separately, with a test column you can fill in later. An empty test column is a bad sign, not a formatting note.
2. **Freeze the use case diagram.** `docs/diagrams/use-case-v1.drawio` **and** its `.puml` source, plus the PNG. A PNG on its own is not a diagram.
3. **Freeze both specifications.** `docs/use-cases/place-order.md` and your second one. All nine fields. Postconditions for **every** exit. The second spec must be a different goal — not *Print Ticket* wearing a trench coat.
4. **Confirm four sets of handwriting.** Two specs written by one person has cost this milestone its grade before. Check the commit history:
   ```bash
   git log --oneline --since="7 days ago"
   ```
   Four members, four contributions in the M1 window.
5. **Push the work.**
   ```bash
   git add docs/requirements.md docs/diagrams/ docs/use-cases/ docs/reviews/
   git commit -m "M1: requirements list, use case diagram, two detailed specifications"
   git push
   ```
6. **Tag `m1`** — Release Manager only, and only **after** step 5 succeeded.
   ```bash
   git tag -a m1 -m "M1: requirements, use case diagram, two detailed specs"
   git push origin m1
   ```
7. **Verify. Run it. Read the output.** This is the step everyone skips, and it is the step that proves the submission:
   ```bash
   git ls-remote --tags origin
   ```
   You must see a line containing `refs/tags/m1`. No line = not submitted. Do not assume; read.
8. **Update the README milestone status table** in the repo, commit, push. The tag — not your branch head — is the graded snapshot.

### Done when

- [ ] `docs/requirements.md` — every requirement testable, functional and non-functional marked separately.
- [ ] `docs/diagrams/` — **both** source files (`.drawio` and `.puml`) plus the PNG.
- [ ] `docs/use-cases/` — **two** specs, nine fields each, postconditions on every exit.
- [ ] `docs/reviews/m1-spec-review.md` — both directions, four authors.
- [ ] `git ls-remote --tags origin` shows `refs/tags/m1`. You have read the line, not assumed it.
- [ ] README milestone table updated, committed, pushed.

### Stuck?

| Symptom                                                      | Fix                                                                                                                                                                                                                                                      |
| ------------------------------------------------------------ | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `git ls-remote --tags origin` shows nothing                  | The tag was never pushed. Run `git push origin m1` again. If the tag does not exist locally either, `git tag -a m1 -m "M1"` first — and make sure the commit it points at is already on the remote, or the tag points at nothing the reviewer can fetch. |
| `fatal: tag 'm1' already exists`                             | Someone tagged already. Check `git tag -l` and `git ls-remote --tags origin`. If the remote already has `m1`, **do not** force-move it — verify what it points at and move on.                                                                |
| Pushed, tagged, and the tag is on the wrong commit           | `git tag -f -a m1 -m "M1 corrected"` then `git push origin m1 --force` — legal **only before Sun Oct 25 23:59**, per the Deadline Schedule. After the deadline nothing counts.                                                                            |
| Our second spec is just Place Order with different wording   | That is one use case written twice. Pick a different goal from your own diagram — `Track Order`, `Cancel Order`, `Rate Restaurant`. One primary actor, one goal, one ending.                                                                             |
| A postcondition only describes success                       | The single most common defect in student specifications. For each exception, write the end state explicitly: *"the order exists in Pending Payment and no kitchen ticket was printed."*                                                                  |
| The client review is next week and we have no open questions | An empty Box 5 means the review was cosmetic. Naming an open question is what the client is actually paying for — go find one.                                                                                                                           |
| GitHub is unreachable from this network                      | Deadline Schedule §4.5: use the zip fallback channel **and** tell the instructor today. A sync failure is not an excuse; an unannounced one is a zero.                                                                                                   |

---

## 6. Before You Leave (~5 min)

Each of you signs **one** row. This is individual evidence — four signatures, not one team tick.

| # | Person              | Signs off on                                                                                                                    | Signature     |
| - | ------------------- | ------------------------------------------------------------------------------------------------------------------------------- | ------------- |
| 1 | **Lead**            | Time was kept: Demo 25 · Ex 5.1 30 · Ex 5.2 30 · M1 close 25 · sign-off 5. Nobody left with an empty section.                   | \____________ |
| 2 | **Recorder**        | The five defects, the corrected sentences, and all DISAGREE rows are on one committed page — written from four voices, not one. | \____________ |
| 3 | **Reviewer**        | Both review directions are filed, Box 5 is non-empty, and I played the client against my own team's spec.                       | \____________ |
| 4 | **Release Manager** | `refs/tags/m1` appears in `git ls-remote --tags origin`. I read the output.                                                     | \____________ |


**And one last thing before the door** — the client review is **next week's class (Oct 12–13)**, the instructor plays the client, 30 minutes: 10 min present, 20 min interrogation. Have one answer ready for each of these (slide 35):

- *"What happens if payment fails?"* — weak: "we show an error message." Strong: "Pending Payment, one retry queued, no ticket printed — see 4c."
- *"Why is this one use case and not two?"* — weak: "because it felt like one." Strong: "one primary actor, one goal, reached at step 5 regardless of the branches."
- *"How do I know the order is correct now?"* — weak: "it will be in the database." Strong: "the postcondition names the state, and it holds on every exit."
- *"Is the payment centre part of your system?"* — weak: "no, but it is drawn inside the box." Strong: "it is outside the boundary, so it is an actor — we call it, we do not design it."
- *"Which step did you not finish?"* — weak: "none, it is complete." Strong: "the retry count for 4c is undecided — it is question 3 on the agenda, and we need your answer."

---

## 7. Homework (before Week 06 / next class)

1. **Finish §4's output and push it.** `docs/reviews/m1-spec-review.md` — it is M1 evidence
   and it costs you nothing today.
2. **Re-read your two candidates for next week's topic selection.** The silent brainstorm
   happens in class next week, so arrive with one idea already half-formed.
3. **Skim Larman chapter 3** (Use Cases). You will write two full specifications on *your own*
   project in W08 — a week sooner than you would have on the old fixed case.

1. **One SSD skeleton — `docs/diagrams/place-order-ssd.puml`.** Two lifelines only: `Student` and `CampusBites` treated as one box. One message per main step, dashed returns, **no internal objects**. Every message must be traceable to a numbered step in your specification — if you cannot point at the step, delete the arrow.
2. **Read Larman** on system sequence diagrams and operation contracts. Two pages, a skim is fine — you are looking for the pre/post-condition template, not the whole argument.
3. **Bring Box 5.** Next week the instructor works through your client questions **first**. Empty box = the review was cosmetic.
4. **Count your nouns.** Next week every noun you wrote — order, cart, coupon, delivery window, kitchen ticket — becomes a candidate class. Count them before you arrive.

```bash
git add docs/diagrams/place-order-ssd.puml docs/diagrams/place-order-ssd.png
git commit -m "W05 homework: Place Order SSD skeleton"
git push
```

> Stuck on the SSD? Two lifelines and eight arrows is the whole diagram. If you have drawn three boxes, you have written a design model — delete the extras.

---

## 8. Reference

| Document                                                                | What it answers                                                                                   |
| ----------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------- |
| `../CampusBites-项目指导书-Project-Guidebook.md`                             | §5 M1 deliverables · Appendix B the use case specification template · §7 the client review format |
| `../CampusBites-Deadline-Schedule-and-Submission-Guide.md`              | §4.3 the tag protocol · §4.4 the README status table · §4.5 the GitHub-unreachable fallback       |
| `../Course-Project-Grading-Rubric.md`                                   | How M1 is scored (milestone points)                                                               |
| `../CampusBites-Lab-Guide-实验指导书.md`                                     | §3 the 16-week map; §4 what "done" means                                                          |
| `../CampusBites-项目指导书-Project-Guidebook.md` §4                          | How requirements and the three planned change injections work                                     |
| `../../01-课件/W05-Use-Case-Specification-and-Scenarios/W05-Handout.html` | Sections D–G: the defect table, the review form, the tag drill                                    |
| `../../01-课件/Pseudocode-Conventions-伪代码约定.md`                           | How notation is written in this course (no programming needed)                                    |
| `Lab-03-W03-UML-Essentials-Practice.md`                                 | PlantUML syntax and the source + PNG rule                                                         |
| `Lab-04-W04-Finding-Actors-and-Use-Cases.md`                            | The actors and use cases your two specifications hang off                                         |

**Submission address:** `https://github.com/<owner>/campusbites-team-01` — instructor GitHub account **`klausren`** (read access is enough).

*Lab questions go to the instructor in class, or open an issue in the course repository.*

---

*Lab 05 · v1.0 · Information Systems Analysis and Design · Fall 2026*
