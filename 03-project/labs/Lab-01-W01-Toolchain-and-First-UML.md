# Lab 01 · W01 — Toolchain & Your First UML Model

> **ISAD · Fall 2026** · Lab block (last 2 h of the weekly 4 h) · Week 01, Aug 31 – Sep 06
> **Milestone**: none graded this week · **Feeds**: M0 (due Fri Sep 11)
> **Slides**: `W01-Introduction-Systems-Analysts-and-OOAD.pptx`, pages 30–37

**Purpose of this lab.** Today you do two things: get the toolchain working on your own machine, and draw—read—your first UML models. Nothing you produce today is graded. Everything you produce today is the seed of your M0 submission next week.

---

## 0. Before You Start (~5 min)

Tick each box. If one is empty, fix it now, not in Week 4.

- [ ] You have a laptop with you and it is charged (or you are next to power).
- [ ] You can reach `github.com` from your network. *Test it now.* If not, tell the instructor immediately — there is a fallback, but it needs setting up early.
- [ ] You have the **Project Guidebook** open (or the file on disk): `../CampusBites-项目指导书-Project-Guidebook.md`
- [ ] You have the **Deadline Schedule** open: `../CampusBites-Deadline-Schedule-and-Submission-Guide.md`

> **Why we keep saying "read the Guidebook":** there is no written exam in this course. The Guidebook *is* the exam paper. You will be questioned on it at the Week 16 defense.

---

## 1. What the Lecture Gave You

Three things from the first two hours that you will use right now:

| From the lecture | The one line you need |
|---|---|
| IS = people + process + data + technology | If one of the four is missing, it is not yet an information system. |
| Analysis answers **what**; design answers **how** | Your decision rule for Exercises 1.1 and every model after it. |
| Three UML views of one system | Use case = what it does · domain model = the concepts · sequence = how it happens in time. |

**The sentence to remember:** *you do not draw one perfect picture; you draw three partial ones, and each answers a different question.*

---

## 2. Demo — Instructor-Led (~25 min)

The instructor opens a finished **vending machine** model set (use case + domain + sequence) and reads it with you. You are not drawing yet. **You are learning to read.**

**The three-question reading method** — use it on every model you see this semester:

1. **What concepts exist?** (the boxes) — Are they nouns from the real world, or classes from a programming language? At analysis stage they must be real-world nouns.
2. **How are they related?** (the lines and the little numbers) — Those numbers are **multiplicities**, and each one is a decision: can a vending machine have zero products? Apparently yes.
3. **What does each hold?** (the attributes) — These are the facts the system must remember.

Then the instructor jumps the same system to the design level. **Watch for exactly three changes:**

- [ ] **Methods appeared** — `sellProduct()`, `pay()`. Now we are answering *how*.
- [ ] **An interface appeared** — `Payment` with `CardPayment` / `CashPayment` beneath it, dashed arrow = "depends on". The machine depends on the abstraction, not on coins.
- [ ] **Responsibility moved** — each class knows its own job; nothing does everything.

> **The whole course is this jump.** Weeks 4–15 are this jump, practised on CampusBites, over and over, until it stops being hard.

**Your notes** (fill in as you watch — you will be asked about these in Week 2):

```
Concepts I saw in the vending machine domain model:
  ______________________________________________

One multiplicity that surprised me, and what it means:
  ______________________________________________

What changed between the analysis model and the design model:
  ______________________________________________
```

---

## 3. Task A — Set Up Your Toolchain (~30 min)

**Goal.** By the end of this task you can draw a diagram, commit it, and push it. That single loop is what every milestone runs through.

**Input.** Your own laptop, an internet connection, and 30 minutes of undivided attention.

### Steps

1. **draw.io (diagrams.net)** — install the Desktop app, or bookmark <https://app.diagrams.net>.
   - macOS: the `.dmg` from <https://github.com/jgraph/drawio-desktop/releases>; drag to Applications.
   - Windows / Linux: installer or AppImage from the same page.
   - *If GitHub is slow or blocked from your network:* use the web app at <https://app.diagrams.net> and save `.drawio` files locally. Tell the instructor so we set up the fallback together.

2. **Git** — check whether you already have it. Open a terminal and run:

   ```bash
   git --version
   ```

   - You want **2.30 or newer**. macOS: it comes with Xcode Command Line Tools, or install via `brew install git`. Windows: <https://git-scm.com> → accept all defaults → use "Git from the command line and also from 3rd-party software".

3. **GitHub account** — create one at <https://github.com> if you do not have it. Use an email you actually read: every change injection (ΔC1–ΔC3) is announced there.

4. **Introduce yourself to Git** — run these two lines with your own name and email:

   ```bash
   git config --global user.name  "Your Full Name"
   git config --global user.email "your.email@example.com"
   ```

   > Use the **same email as your GitHub account**, or your commits will not be linked to your profile — and your commit history is part of your Individual grade (B2, 15%).

5. **VS Code** — <https://code.visualstudio.com>. We use it for Markdown and (optionally) PlantUML. Install it now even if you prefer another editor; lab instructions assume it.

6. **PlantUML (optional, recommended)** — only if you want text-based diagrams. Requires a Java runtime. Skip it for now if step 1–5 took longer than 25 minutes; you can add it in Week 3.

### Done when

- [ ] `git --version` prints 2.30 or newer.
- [ ] `git config --global user.name` prints your name.
- [ ] You can log in to GitHub in a browser.
- [ ] draw.io opens and you can create a blank diagram.

### Stuck?

| Symptom | Fix |
|---|---|
| `git: command not found` | Git is not installed, or the terminal was open before install. Restart the terminal first. |
| `Permission denied (publickey)` on push | You are using SSH without a key. Use **HTTPS** remotes for this course, or add an SSH key: <https://docs.github.com/en/authentication> |
| draw.io refuses to open (macOS Gatekeeper) | Right-click the app → **Open** → confirm. This is a one-time action. |
| Corporate / campus proxy blocks GitHub | Tell the instructor **today**. We have a documented fallback (Deadline Schedule §4.5) but it must be set up before a deadline, not during one. |

---

## 4. Task B — Exercise 1.1: Analysis or Design? (~11 min)

**Goal.** Train the WHAT / HOW distinction. This judgement is hidden inside every deliverable you submit from Week 4 onwards.

**Input.** Five statements (slides p.33). Work **individually first** — 6 minutes. Then compare with your neighbour — 5 minutes.

| # | Statement | Your call | One-sentence justification |
|---|---|---|---|
| 1 | A customer can pay by card or by cash. | | |
| 2 | We should use the Strategy pattern for payment. | | |
| 3 | An order has a status that changes over time. | | |
| 4 | The `Order` class should expose a `cancel()` method. | | |
| 5 | The system must notify the courier when an order is ready. | | |

**Rule of thumb:** *does it talk about the problem, or the solution?*

> **Watch statements 3 and 4 together.** The same idea — an order changing over time — first as a domain fact (analysis), then as a method on a class (design). Nothing about the domain changed. Only the question you were answering.

**Done when:** five rows filled, five justifications written. Answers are discussed in class — do not skip ahead, the argument matters more than the tick.

---

## 5. Task C — Exercise 1.2: Stakeholders of CampusBites (~10 min)

**Goal.** Produce the stakeholder list that becomes your **actor list in Week 4** and feeds M0 item ②.

**Input.** The CampusBites brief (Guidebook §2). A stakeholder is *anyone the system affects — or who affects it*. **Not just users.**

### Steps

1. Copy these five to seed your list:

   | Stakeholder | User? | Why they have a stake |
   |---|---|---|
   | Students — they order food | ✔ | |
   | Restaurants — they receive and fulfil orders | ✔ | |
   | Couriers — they deliver | ✔ | |
   | University administration — campus rules, contracts | ✖ | |
   | Payment providers — they move the money | ✖ | |

2. **Now go wider.** The interesting ones never log in. Push yourself to at least **10 rows total**. Ask:
   - Who is affected but has no account? (*canteen staff whose queue gets shorter; the dorm supervisor dealing with couriers at the gate; the IT office keeping it running.*)
   - Who is **excluded** by the system? (*a student with no smartphone; a student without a campus card.*)
   - Who pays, who regulates, who competes?

3. Mark the ✔ column honestly. Confusing "stakeholder" with "user" is the single most common error in Week 4 use case diagrams.

**Done when**

- [ ] At least 10 stakeholder rows.
- [ ] At least 3 marked ✖ (non-users — these are the ones people forget).
- [ ] Every row has a one-line "why".

> **Save this list.** It goes straight into your M0 submission next Friday and reappears as actors in Week 4.

---

## 6. Task D — Exercise 1.3: Systems Around Your Campus (~8 min)

**Goal.** Practise the four-element test, and collect project ideas as a side effect.

**Input.** Your own daily life on campus.

### Steps

1. Draw a line down the middle of a page. Left: **already an information system.** Right: **not yet.**
2. Check each candidate against the four elements — **people, process, data, technology**. If any one is missing, it is not yet a system; it goes on the right.
3. Left side starters: course registration · library borrowing · campus card top-up · exam timetable.
4. Right side starters: the canteen queue · lost-and-found · grabbing a seat in the study room.
5. Add **one of your own** — something that annoys you every week. Run the four-element test on it.

**Done when**

- [ ] ≥ 4 items per column.
- [ ] Your own example, with all four elements named.

> **Every gap on the right is a candidate system someone could build.** If you are ever short of an idea, start from this list.

---

## 7. Task E — Draw and Commit Your First Domain Model (~25 min)

**Goal.** Run the full loop once, end to end, while nothing is at stake: **draw → export → commit → push.** This is the single most useful 25 minutes of Week 1, because the same loop carries M1 through M5.

**Input.** draw.io, the reading method from §2, and this tiny brief:

> *A customer places orders. An order contains one or more order lines. Each order line refers to a menu item. A menu item belongs to a restaurant.*

### Steps

1. **Draw it.** Four classes — `Customer`, `Order`, `OrderLine`, `MenuItem` — as rectangles with a name compartment. Connect them with plain association lines.
2. **Add multiplicities** on both ends of every line. A customer places `0..*` orders; an order belongs to exactly `1` customer. *Every number you write is a decision — be ready to defend it.*
3. **Add attributes** you can justify: `Order` → `total`, `status`, `placedAt`. `MenuItem` → `name`, `price`.
4. **Do not add methods.** This is an analysis model. No `cancel()`, no `pay()`. If you are tempted, ask yourself which question you are answering.
5. **Export twice:**
   - `File → Save As → .drawio` — **the source file**. Non-negotiable (Guidebook §6 rule 1).
   - `File → Export As → PNG` (200% zoom, transparent background off) — for humans to look at.
6. **Commit and push.** In your team repo (or a scratch repo if teams are not formed yet):

   ```bash
   mkdir -p docs/diagrams
   git add docs/diagrams/domain-first-try.drawio docs/diagrams/domain-first-try.png
   git commit -m "W01 lab: first domain model (Customer-Order-OrderLine-MenuItem)"
   git push
   ```

   > `docs/diagrams/` is where every diagram lives from here on — the convention is formalised as a team rule in Week 3 (see `Lab-03-W03-UML-Essentials-Practice.md`, Task D). Start using the path now so you never have to move files later.
   >
   > If you have no repo yet: create one now — `campusbites-team-a` or `campusbites-team-b`, or `isad-scratch-<yourname>` if teams are not final. Creating it today removes 80% of the Week 2 M0 panic.

### Done when

- [ ] A `.drawio` source file and a `.png` export both exist.
- [ ] 4 classes, 3+ associations, multiplicities on **both** ends of each.
- [ ] No methods anywhere in the model.
- [ ] `git log` shows the commit; `git status` says "nothing to commit".

### Stuck?

| Symptom | Fix |
|---|---|
| "Is `OrderLine` really a class?" | Yes — it holds a quantity. An attribute that needs attributes of its own is a class in disguise. |
| Unsure about a multiplicity | Say it out loud as a sentence: "one customer places zero or more orders." If the sentence is nonsense, the number is wrong. |
| `git push` asks for a password | GitHub stopped accepting account passwords. Use a **Personal Access Token** (Settings → Developer settings → Tokens → classic → `repo` scope), or set up SSH. |
| `failed to push some refs` | Someone pushed first. Run `git pull --rebase` then `git push` again. |

---

## 8. Before You Leave (~5 min)

Three boxes. If any is empty, it is homework — and milestones do not wait for homework.

- [ ] **Toolchain works** — you can draw, commit, and push without help.
- [ ] **One diagram committed** — source file *and* PNG are in a repository you can show me.
- [ ] **You can explain every element you drew** in one English sentence each. If you cannot, you decorated, not designed — fix it now, not at the defense.

**Also, today:** form your team of ~3 and agree who is Team Lead. Teams are formalised in the Week 2 lab, but arriving with a plan halves the argument.

---

## 9. Homework (before Week 2)

1. **Read the Project Guidebook in full.** Milestones, submission rules, grading, templates. It is handed out today.
2. **Read the Deadline Schedule in full.** Every hard deadline with dates. The first is **M0 — Friday, Sep 11**.
3. **Skim Larman Ch. 1–2.** Skim, do not study. It frames Weeks 2–3.
4. **Write 150 words:** *"One information system I use daily, and what would break if the analyst had failed."*
   - 150 words is short. The hard part is being specific — *"the app would be bad"* is not an answer. Name the breakdown, name who suffers.

---

## 10. Reference

| Document | What it answers |
|---|---|
| `../CampusBites-项目指导书-Project-Guidebook.md` | What to build · teams · milestones · submission rules · grading |
| `../CampusBites-Deadline-Schedule-and-Submission-Guide.md` | Exact dates · tag protocol (`m0`…`m5`) · GitHub-unreachable fallback |
| `../CampusBites-Lab-Guide-实验指导书.md` | The 16-week lab plan at a glance |
| `../Course-Project-Grading-Rubric.md` | How each milestone and the defense are scored |
| `../../00-课程文件/Course-Syllabus-课程标准.md` | Full syllabus and weekly schedule |

**Submission address:** one Git repository per team. The instructor's GitHub account is **`klausren`** — invite it as a collaborator during the Week 2 lab; it is part of M0.

*Lab questions go to the instructor in class, or open an issue in the course repository.*

---

*Lab 01 · v1.0 · Information Systems Analysis and Design · Fall 2026*
