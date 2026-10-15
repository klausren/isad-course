# Lab 07 · W06 — Choosing Your Own Project (in-class part)
# 第 07 次实验 · 选题：你们自己的项目（**课上部分**）

> **ISAD · Fall 2026** · Lab block (last 2 h of the weekly 4 h) · Week 06, Oct 12 – Oct 18
> **Milestone**: **none this week — this is a preparation task, no tag required**
> **Class time**: **50 minutes** — §0 repository (15 min) + §1–§3 topic selection (35 min).
> The remaining work — merging, scoring, and
> writing the proposal — is the **homework**: [`../homework/Homework-01-W06-Choosing-Your-Own-Project.md`](../homework/Homework-01-W06-Choosing-Your-Own-Project.md), due before W07.
> **Brief**: [`../Topic-Selection-Task-选题任务包.md`](../Topic-Selection-Task-选题任务包.md)
> **Change note**: [`../项目案例变更说明-CampusBites改为自主命题.md`](../项目案例变更说明-CampusBites改为自主命题.md)

**Purpose of this lab.** From today, the system you analyse is **yours to choose** — the instructor's
CampusBites case is no longer your project. Today you pick it. That sounds like a small task; it is
actually the decision that shapes the next ten weeks, so we spend a full lab on it.

**No diagrams today.** You produce a proposal, not models. Resist the urge to start drawing.

---

## 0. Repository First (~15 min, before anything else)

**The repository does not exist yet.** The Week 02 plan had you create it then; the project was
rescheduled on Oct 08, and today is the first class where you actually need it — the homework ends
with `git push origin main`, and `origin` cannot be empty. **So build it now, at the top of the lab.**

**Who does it.** The **Release Manager**, using one member's GitHub account. The other three
**do not wait** — they start §3's silent brainstorm immediately. Fifteen minutes of three people
watching one person click is fifteen minutes you do not get back.

### Steps

1. **Create the repository** under one member's account. Name it exactly:
   `campusbites-team-01`. Private is fine.

   ```bash
   # Release Manager only
   git init
   git remote add origin https://github.com/<owner>/campusbites-team-01.git
   mkdir -p docs/topics docs/diagrams docs/use-cases docs/reviews 01-requirements
   ```

2. **Invite the instructor.** GitHub → your repo → *Settings* → *Collaborators* →
   *Add people* → **`klausren`** → role **read** is enough. Do not wait for them to accept; verify
   later.

3. **Everyone clones and identifies themselves.** This step is not optional — Git cannot attribute
   a commit without it, and individual contribution is marked at M5.

   ```bash
   git clone https://github.com/<owner>/campusbites-team-01.git
   cd campusbites-team-01
   git config user.name  "Your Full Name"     # exactly as in the roster
   git config user.email "your@student.dlut.edu.cn"
   ```

   > ⚠️ **Use your own name and your own university email.** All four commit authors must be
   > distinguishable, or the individual contribution log at M5 cannot be reconstructed from
   > `git log`.

4. **First commit**, so the team has a shared starting point:

   ```bash
   git commit --allow-empty -m "M0 prep: repository created for topic selection"
   git push -u origin main
   ```

### Done when

- [ ] Repository `campusbites-team-01` exists under one member's account
- [ ] `klausren` invited (read)
- [ ] All four have cloned it and run `git config user.name` / `user.email`
- [ ] The empty first commit is pushed — `git ls-remote --tags origin` answers without an error

> **Repository access for the instructor** is now done. M0 next week checks **charter, stakeholder
> list, vision, and the `m0` tag** — you do **not** need to re-invite anybody. The checklist in
> [`../templates/Template-W02-05-M0-Submission-Checklist.md`](../templates/Template-W02-05-M0-Submission-Checklist.md)
> §3 marks item ④ as already satisfied.

### Stuck?

| Symptom | Fix |
|---|---|
| Push asks for a password | GitHub no longer accepts account passwords. Use a **Personal Access Token** (Settings → Developer settings → Tokens (classic) → scope `repo`), or switch to SSH. |
| Remote repository already exists (someone was faster) | `git remote set-url origin <correct URL>`, then `git pull --rebase` before continuing. |
| Four different GitHub accounts, no idea whose to use | Any one of them. What matters is that it is reachable and that `klausren` has read access. |
| GitHub unreachable | Say so now, and use the fallback in `../CampusBites-Deadline-Schedule-and-Submission-Guide.md` §4.5: zip the folder including `.git/` and email it. Then restore within 3 days. |

---

## 0b. Before You Start (~3 min, the reading)

- [ ] Read §1 of the brief — **what makes a good topic** (the three hard criteria S1/S2/S3).
- [ ] Read §1's "three bad topics" table. If your favourite idea is on it, you need a second idea.
- [ ] Confirm `docs/topics/` exists in your clone (Step 1 of §0 created it) — `ls docs/topics`
- [ ] You four are **one team**. Today everyone proposes; nobody edits anyone else's text.

> **The one rule that trips people up:** the 20 minutes in **§3 Task A** are **silent and
> individual**. Do not discuss your candidates before the Recorder calls stop. If you talk first,
> four people collapse into one idea, and the person whose idea gets dropped never owned anything.
> The repository work in §0 does **not** break this silence — §0 and §3 overlap on purpose.

---

## 1. What Changed — and What Did Not (~4 min, instructor-led)

| Changed | Unchanged |
|---|---|
| **Which system you analyse** | Method, milestones M0–M5, marking, submission rules, tag protocol, `docs/diagrams/`, the four standing roles |
| The deadline is **one week tighter** | Everything about *how* you are assessed |

Two things you should hear from the instructor before you start:

1. The marking outline says "**三级项目（CampusBites）**". That refers to the **assessment item**,
   not to a compulsory topic. Your topic changes; the 20 marks do not.
2. Your instructor's answer for this lab is **pass / revise**, returned before Week 07.
   You cannot enter M0 until the topic is approved.

---

## 2. Demo — Instructor-Led (~8 min)

Watch and note. The instructor works through **one rejected example** and **one accepted example**.

### The rejected one

> **"A second-hand textbook exchange platform for the university."**
> Sounds perfect: real business, students you know, listings and orders.
>
> Instructor writes the domain nouns on the board:
> `book · seller · buyer · listing · order · message · review · cart · payment · address`
> That is 10 nouns, so the team relaxes.
>
> Then the instructor asks three questions:
> - **S1 — who asks this system for something?** Student, buyer, seller… and then? *Nobody else.*
>   Payments? Outside. Notifications? Outside. **Count = 2. Fails.**
> - **S2 — 10 classes, but what are the relationships?** seller *lists* book, buyer *buys* listing.
>   Everything else is "has". **Relationships = 2 real ones. Fails.**
> - **S3 — what has a lifecycle?** An order: created → paid → shipped → done. **One object only. Fails.**
>
> Verdict: rejected. And the team has 25 minutes left.

### The accepted one

> **"Resident repair and maintenance reporting for a university campus."**
> Real: the campus maintenance desk genuinely does this today, on paper.
>
> Instructor writes the nouns: `fault report · resident · staff · dispatcher · contractor ·
> building · room · equipment · category · priority · work order · parts · invoice · sla`
>
> - **S1 — count = 7.** Resident raises it, dispatcher assigns, staff repairs, contractor fixes
>   what staff cannot, admin manages contractors, **plus two outside systems**:
>   the notification service and the billing system. ✅
> - **S2 — 14 classes.** And the relationships are *not* all "has":
> *dispatcher assigns* work order, *contractor fulfils* work order, *work order references* fault report,
> *category determines* priority (a rule!), *priority drives* sla. ✅
> - **S3 — two lifecycles.** Work order: `draft → assigned → in progress → done → closed`.
>   Fault report: `new → triaged → scheduled → in progress → verified → closed`. ✅
>
> Verdict: accepted — and note the team still flagged one thing they could not resolve
> (does a cancelled work order go back to `draft`, or straight to `closed`?).

**The sentence to remember:** a noun is not a class. A relationship that is not "has" is where the modelling lives.

---

## 3. Task A — Individual Candidates (~20 min, silent)

**Goal.** Two candidate topics per person, written down before anyone speaks.

### Steps

1. Take eight minutes **alone, in silence, no talking**. Brainstorm freely — write down every idea that
   occurs to you, including bad ones. Do not judge yet.
2. From your own list, pick **two** that survive a fast check:
   - Can you say it as **one sentence**: *who, in what situation, asks the system for what, and gets what back?**
   - Can you list **at least eight** domain nouns?
   - Write those two down properly, using the format in §3 of the brief.
3. Fill in the last line of each candidate honestly: **"I think the risk is …"**.
   Writing "I cannot see a lifecycle here" is valid and useful information.
4. **Do not discuss.** Hand your sheet to the Recorder when the timer says stop.

### Done when

- [ ] Two candidates written, each with a one-line pitch
- [ ] Each has 8–12 domain nouns listed
- [ ] Each has an honest risk line
- [ ] Each is labelled with your name
- [ ] Sheets handed to the Recorder — **that is the end of the in-class part**

> **Class time ends here (35 min).** Merging, scoring and the proposal are homework.
> **Keep your sheet.** It is your evidence of individual contribution, and Step 1 of the
> homework builds directly on it — do not rewrite it from memory.

### Stuck?

| Symptom | Fix |
|---|---|
| I cannot think of any topic at all | Look at the accepted example's *domain*, not its app: "campus maintenance" is a topic; "maintenance app" is not. Write the domain, the software follows. |
| My idea is a CRUD system | It probably is one. **Go back to the bad-topics table** and find your second idea. |
| Everyone proposed the same thing | That is a **good** signal, not a problem — it means the topic is the obvious strong one. Pick it and move on to Task B. |
| My idea needs real code to explain | Out of scope. This course does not implement. If you cannot explain it in a diagram, you cannot draw it. |
| We cannot agree on the final topic | You do not have to agree yet. Task B scores them; the criteria decide, not seniority. |

---

> ⚠️ **Everything below has moved to the homework sheet.**
> Sections 4–9 are now in [`../homework/Homework-01-W06-Choosing-Your-Own-Project.md`](../homework/Homework-01-W06-Choosing-Your-Own-Project.md)
> (Step 1 Merge · Step 2 Score · Step 3 Proposal · Step 4 Submit).
> They are kept below unchanged so you can see the whole shape of the work.
> **The 35-minute in-class part is §0–§3 only.**

---

## 4. Task B — Merge and Score (~18 min)

**Goal.** One shortlist, scored against the three hard criteria, ending in **one** decision or an explicit "we are stuck".

### Steps

1. **Recorder** merges all four sheets into `docs/topics/candidate-list.md`.
   Keep the proposer name on every candidate. **Keep the rejected ones** — the instructor wants to see what you considered.
2. Immediately cross out any candidate that fails a hard check (no one-line pitch, or fewer than 8 nouns).
3. **Reviewer** works through the scorecard in `docs/topics/scorecard.md` for each survivor:
   - S1 — can you name **five or more** actors, including at least one **outside** system?
   - S2 — can you list **eight or more** classes **and six or more** relationships that are not "has"?
   - S3 — can you name **two** objects with three or more states each?
4. **Any candidate failing one criterion is eliminated**, however attractive it sounds.
5. **Lead** keeps time. If at 20 minutes you still have no survivor, stop and write in the scorecard:
   *"We could not satisfy the criteria. Here are the six we tried. We need help."* — that is a valid, useful outcome.

### Done when

- [ ] `candidate-list.md` exists, with at least six candidates, each attributed
- [ ] `scorecard.md` completed, showing S1 / S2 / S3 for every candidate
- [ ] Exactly one candidate survives — **or** an explicit "we are stuck" note
- [ ] The chosen one is written down, with the reason in 3–5 sentences referencing a criterion

### Stuck?

| Symptom | Fix |
|---|---|
| A candidate scores ✓ on S1, ✓ on S2, ✗ on S3 | Eliminate it. S3 is what gives you a state machine in M2 and a State pattern in M4. No lifecycle = two empty milestones. |
| The surviving topic is not the one I liked | Fine. The criteria decided. Write down your objection in one line and commit to the decision. |
| We chose one but I genuinely think it is weak | Write the objection **in the scorecard** and move on. Silently resenting the topic helps nobody. |
| Everyone's for a different one | Each of you argues for your own using S1/S2/S3 out loud. Highest total score wins. Two minutes per person, hard cap. |

---

## 5. Task C — Write the Proposal (~26 min)

**Goal.** One page the instructor can mark pass / revise from. (26 min — protect §3 and §5; §1/§2 can be one line each.)

### Steps

1. Fill in `docs/topics/Topic-Proposal.md` **together**, out loud — do not split sections and write in silence.
2. **Section 3 is the part that matters.** For each of the three criteria, write your answer *and how you counted it*.
   "≥5 actors: Resident, Dispatcher, Staff, Contractor, Admin, Notification service (outside),
   Billing system (outside) — seven, counted by 'who asks the system for something'" is passable.
   "Lots of actors" is not.
3. **Section 4: two objects with lifecycles.** Write each state chain now, in full.
   You will draw these as state machines in M2 — doing it now means M2 is a drawing job, not a thinking job.
4. **Section 5: three pattern questions you cannot answer yet.**
   *"Does a cancelled work order go back to draft, or straight to closed?"*
   *"Should priority be a field on the work order, or a rule that computes it?"*
   Write what you genuinely do not know. **This is the most valuable section of the proposal** —
   W13 and W14 exist to answer these, and the instructor wants to see that you know where the edges are.
5. **Release Manager** commits and pushes when you are done (see §6).

### Done when

- [ ] Proposal is **one page** — not two, not a page and a half
- [ ] Section 1 pitch is a **single sentence** with an actor in it
- [ ] Section 3 shows S1, S2, S3 with the counting method spelled out
- [ ] Section 4 has two state chains, each 3+ states
- [ ] Section 5 has three genuine open questions
- [ ] Section 6 lists what you still need to find out

### Stuck?

| Symptom | Fix |
|---|---|
| The pitch needs two sentences | The topic is too big. Cut a scope: not "a maintenance platform" but "fault reporting and work assignment for one campus". |
| Section 3 is all "yes" but you can't show the count | Then it's not satisfied. Go and count, right now, out loud, together. |
| Section 5 feels awkward — we have no idea yet | Good. That is exactly what the field is for. Three honest unknowns beat three invented answers. |
| The proposal runs over a page | Cut section 2, not sections 3–5. Sections 3–5 are what the instructor marks. |

---

## 6. Submit (~5 min)

```bash
git add docs/topics/
git commit -m "Add topic selection: candidate list, scorecard, proposal"
git push origin main
```

**No tag this week.** This is a preparation task, not a milestone. M0 and tag `m0` come next week,
after the instructor has passed your topic.

### Done when

- [ ] Three files in `docs/topics/`, pushed to the repository
- [ ] Instructor invited as collaborator (should already be, from M0 setup)
- [ ] **No tag pushed** — tagging happens next week

---

## 7. Before You Leave (~5 min)

Each of you signs off one item. **Four people, four lines — not one team signature.**

| Who | Checked |
|---|---|
| ____________ | I wrote two candidates myself, before any discussion |
| ____________ | I checked that our chosen topic has at least **two** objects with lifecycles |
| ____________ | I can say our pitch as **one sentence**, without reading it |
| ____________ | All three files are pushed, and I did **not** push a tag |

> **Leaving with one question still open is fine. Leaving without knowing your own topic is not.**

---

## 8. Homework (before Week 07)

1. **Re-read your own two candidates.** You wrote them an hour ago under time pressure.
   Now that you have seen the accepted example, would you still pick the same two? If not, tell the team.
2. **Skim Larman chapters 1–2** (Introduction / Object-Oriented Analysis) — the vocabulary starts here.
3. **Come with one sentence** you will want to say to the instructor when you present.

---

## 9. Reference

| Document | What it answers |
|---|---|
| [`../Topic-Selection-Task-选题任务包.md`](../Topic-Selection-Task-选题任务包.md) | The three hard criteria, the bad-topics list, the three deliverable formats |
| [`../项目案例变更说明-CampusBites改为自主命题.md`](../项目案例变更说明-CampusBites改为自主命题.md) | What changed, what did not, the revised timeline |
| [`../templates/README-模板索引-Template-Index.md`](../templates/README-模板索引-Template-Index.md) | The M0 templates you will use next week |
| [`../Course-Project-Grading-Rubric.md`](../Course-Project-Grading-Rubric.md) | How the whole project is marked — read it before you pick a topic |
| [`../CampusBites-项目指导书-Project-Guidebook.md`](../CampusBites-项目指导书-Project-Guidebook.md) | §2 is the *example* of a good domain; §1–§11 are the rules you follow |

---

*Lab 07 · v1.0 · Information Systems Analysis and Design · Fall 2026 · four people, one team, one topic*
