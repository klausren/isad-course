# Lab 04 · W04 — Finding Actors & Use Cases

> **ISAD · Fall 2026** · Lab block (last 2 h of the weekly 4 h) · Week 04, Sep 21 – Sep 27
> **Milestone**: **M1 opens today — due Sun Oct 4** · this week's deliverable: the **use case diagram**
> **Slides**: `W04-Requirements-and-Use-Case-Modeling.pptx`, pages 30–37
> **Handout**: `W04-Handout.html`, sections D–G (page 2)

**Purpose of this lab.** The requirements pack is in your hands. Today you turn twenty sentences of prose into a picture: first the actors, then the candidate goals, then the diagram — and then you defend it, because in Week 05 the instructor plays the client and will ask why every ellipse is there.

**No programming today.** Everything is text, ellipses and arrows in draw.io.

---

## 0. Before You Start (~5 min)

- [ ] You have the **CampusBites requirements pack** (issued in class today; also in `04-项目实践/` on the course drive).
- [ ] draw.io opens and you can export a PNG (checked in Lab 01).
- [ ] Your `campusbites-team-01` repository clones cleanly and you can push.
- [ ] You know today's four standing roles: **Lead** (keeps time), **Recorder** (writes the one page), **Reviewer** (plays the client), **Release Manager** (pushes and checks the tag).

> **The one rule that trips people:** a milestone is **only submitted when the tag is pushed**. `git push` alone is not a submission.

---

## 1. What the Lecture Gave You

| From the lecture | The one line you need |
|---|---|
| Functional says what, non-functional says how well | If you cannot say how you would test it, you have not finished writing it. |
| An actor is a **role**, not a person | Li Wei is one person and three actors. |
| A use case is a **user goal**, not a function | It ends, it belongs to one actor, it can fail and still be one. |
| The boundary test | Could we rewrite it from scratch? Yes → inside. No → outside, and it becomes an actor. |
| `<<include>>` is inevitable, `<<extend>>` is conditional | Is the base still complete without it? No → include. Yes → extend. |
| Two heuristics: event table and noun–verb scan | Run both. Where they disagree you have found a question to ask. |

---

## 2. Demo — Instructor-Led (~10 min)

The instructor reads the first two sentences of pack §2.1 aloud and marks them on the board:

- nouns → **blue** (candidate actors and concepts)
- verbs → **amber** (candidate use cases, then filtered)

Watch for three things:

1. **"the campus card centre" is a noun that becomes an actor, not a use case** — we cannot rewrite it.
2. **"calculates the total" is a verb that does not survive** — nobody wakes up wanting it.
3. **"authenticates the student" is a verb that survives as an `<<include>>`**, not as a use case.

---

## 3. Task A — Exercise 4.1 A: List the Actors (~20 min)

### Steps

1. Read pack §2.1 **twice**. First for the story, then with a pen.
2. Four people, five minutes each **alone**: list every role that stands outside CampusBites and talks to it.
3. Merge onto the Recorder's page. **Keep the rows you disagreed on** — they are the material for Task D.
4. For each row fill the handout table: actor · primary/secondary · the goal they own · why they are here.
5. Target: five to seven rows. Nine is fine; three means you stopped reading.

### Stuck?

| Symptom | Fix |
|---|---|
| Only two or three actors | You listed job titles. Ask *who is affected but never logs in?* — the kitchen, the administrator. |
| "Process Payment" is in the actor list | Right instinct, wrong column: the actor is the **Payment Provider**; the behaviour is what it does *for us*. |
| "Li Wei" or "the Marketing Department" | Name the role, not the person or the department. |
| Cannot decide primary or secondary | Ask *who waits, and who is called?* The one who starts it is primary. |
| Nobody can say why a row is there | Delete the row. An actor with no reason is a guess. |

---

## 4. Task B — Exercise 4.1 B/D: Filter the Candidates (~25 min)

### Steps

1. Take the verbs you underlined and write **nine candidates**, each as verb + object, in business words.
2. For each, answer in one line: **is this a user goal, or a step inside one?**
3. For every "No", say what it really is — a **step** (→ scenario text, Week 05), an **`<<include>>`**, or an **external system** (→ actor).
4. For every "Yes", write **the end condition**: "ends when …". A goal with no end is not a goal.
5. Check the two from the full pack that the slide gives you: **Suspend Restaurant** and **Close the Day** — both goal level. The second one's actor is a clock.

### Stuck?

| Symptom | Fix |
|---|---|
| Everything looks like a goal | Apply the end test: name the moment the actor says "that is it". No moment → not a goal. |
| "Calculate Total" passed as a use case | Ask who wakes up wanting it. It is one line inside the Place Order scenario. |
| "Manage Order" is on the list | That is a database table with a verb glued on. Split it into Place Order and Cancel Order. |
| "Authenticate" passed as a use case | Nobody comes to log in for the pleasure of it. Make it an `<<include>>`. |
| Nine candidates but all Yes | You filtered nothing. Go back and find the steps — every narrative has at least three. |

---

## 5. Task C — Exercise 4.2: Draw the Diagram (~30 min)

### Steps

1. Open draw.io. Draw the **boundary rectangle first**, name it `CampusBites` at the top.
2. Put the surviving use cases **inside** as ellipses; the actors **outside** (external systems as labelled boxes, on the right).
3. Draw solid lines — **no arrowheads**; it is a conversation, not a flow.
4. Add exactly **one `<<include>>`**: arrow leaves the base and arrives at what it always needs.
5. Add exactly **one `<<extend>>`**: arrow leaves the extra and **returns** to the base, with the condition written as a note.
6. For each dashed arrow, write **one sentence** in the notes area: what it means and why the arrow points that way.
7. Run the eight-item self-check on handout page 2, section F. Every box must be ticked.
8. Export **both**: `use-case-v1.drawio` (the source) and `use-case-v1.png`.

### Stuck?

| Symptom | Fix |
|---|---|
| The extend arrow looks wrong but I cannot say why | Say it out loud: "Apply Coupon **adds itself to** Place Order." The extra points back at the base. |
| I drew a dashed arrow at an actor | Dashed arrows never touch actors. Only solid associations do. |
| The payment provider ended up inside the box | Could we rewrite it from scratch? No. Move it outside. |
| Twenty ellipses on the page | You modelled the menu, not the goals. Look for the CRUD quartet and merge it. |
| Cannot export a PNG in draw.io | File → Export as → PNG, uncheck *Transparent Background*, zoom 200%. |

---

## 6. Task D — Defend It to the Client (~15 min)

The **instructor plays the client**; the **Reviewer** takes notes on what the client asks.

Each of the four defends one block, ~3 min each:

| Person | Defends |
|---|---|
| Lead | The actor list — especially the three secondary ones |
| Recorder | The nine candidates and why three of them did not survive |
| Reviewer | The two dashed arrows: meaning, direction, condition |
| Release Manager | The boundary: what is inside, what is outside, and why |

Questions the client will ask — have the answer ready:

- *"Why is 'Manage Order' not on this diagram?"*
- *"Who is this actor and what happens to them if the system goes down?"*
- *"You put the payment provider outside. Who do I call when payments break?"*
- *"Show me the one that only sometimes happens. What is the condition?"*

> **A diagram without the sentence is a drawing; with it, it is a model.** Every difference from the reference solution needs one sentence — and a defensible difference earns full marks.

---

## 7. Submit — What Leaves the Room Today

```
campusbites-team-01/
└── docs/
    └── diagrams/
        ├── use-case-v1.drawio      ← the source: required
        └── use-case-v1.png         ← the export: required
```

```bash
git add docs/diagrams/use-case-v1.drawio docs/diagrams/use-case-v1.png
git commit -m "W04: first use case diagram (Exercise 4.2)"
git push
```

**Do not tag yet.** M1 is tagged once, on or before **Sun Oct 4**, when the requirements list and the two briefs are also in. Today's push is your contribution evidence.

| Role | Signs off |
|---|---|
| Release Manager | Both files are in `docs/diagrams/` and pushed |
| Recorder | The one page (actors + nine candidates) is committed as `docs/w04-exercise-4-1.md` |
| Reviewer | The client's questions are written down — they become next week's TODO list |
| Lead | Time was kept; nobody left with an empty section |

---

## 8. Homework (before Week 05)

1. **Finish the diagram** — source file and PNG in `docs/diagrams/`, pushed.
2. **Write two use case briefs**: `Place Order` and one you choose. Half a page each: the goal in one sentence, the primary actor, and the one thing that can go wrong. Full specifications are Week 05.
3. **Read Larman, Chapter 6 (use cases)** — twenty pages, not the whole chapter.
4. **Bring one question the narrative could not answer.** The instructor will answer it as the client in Week 05.
5. **Add the requirements list** (functional and non-functional, each testable) — this is the third M1 item.

> Stuck on a brief? Write the version you are not sure about and bring it. A wrong brief is a better starting point than a blank page.

---

## 9. The Road to M1

| When | Do this |
|---|---|
| **Today — in the lab** | Exercises 4.1 and 4.2; the diagram is pushed (not tagged) |
| **Before next Monday** | Diagram finished · two briefs · Larman Ch. 6 · one question |
| **Week 05 (Sep 28 – Oct 4)** | Client review with the instructor; use case specifications |
| **Sun Oct 4** | Tag `m1`, push the tag. **This is the submission.** |

```bash
git tag -a m1 -m "M1: requirements, use case diagram, two briefs" && git push origin m1
git ls-remote --tags origin      # check it landed
```

> M1 has three items: the requirements list, the diagram, and two briefs. Missing source file = 0 for that item; missing tag = not submitted.

---

## 10. Reference

| Document | What it answers |
|---|---|
| `../CampusBites-项目指导书-Project-Guidebook.md` | §4.1 requirements pack · §4.2 planned change injections · §5 milestones |
| `../CampusBites-Project-Brief.md` | §2 the narrative behind the pack |
| `../Course-Project-Grading-Rubric.md` | How M1 is scored (F3 milestone points) |
| `../CampusBites-Deadline-Schedule-and-Submission-Guide.md` | §4.3 tag protocol · §4.5 GitHub-unreachable fallback |
| `../../01-课件/W04-Requirements-and-Use-Case-Modeling/W04-Handout.html` | Sections D–G: the fill-in tables used today |
| `../../01-课件/Pseudocode-Conventions-伪代码约定.md` | How notation is written in this course (no programming needed) |
| `Lab-01-W01-Toolchain-and-First-UML.md` | draw.io setup, PNG export, first commit |
| `Lab-02-W02-Team-Formation-and-M0-Kickoff.md` | Standing roles and the tag protocol |

**Submission address:** `https://github.com/<owner>/campusbites-team-01` — instructor GitHub account **`klausren`** (read access is enough).

*Lab questions go to the instructor in class, or open an issue in the course repository.*

---

*Lab 04 · v1.0 · Information Systems Analysis and Design · Fall 2026*
