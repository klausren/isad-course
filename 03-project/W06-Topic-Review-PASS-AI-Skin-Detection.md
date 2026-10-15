# Topic Selection Review · PASS · W06
# 选题评审 · 通过 · 第 06 周

> **ISAD · Fall 2026** · four people, one team
> **Submitted**: `docs/topics/candidate-list.md` · `scorecard.md` · `Topic-Proposal.md`
> **Reviewed**: 2026-10-15 · **Decision: PASS** — you may enter M0
> **Next**: M0 due **Sun Oct 25** (tag `m0`). Bring the charter, the stakeholder list, and the vision.

---

## 1. The Decision

**PASS.** All three hard criteria (S1 / S2 / S3) are satisfied, and satisfied with room to spare.
This is a stronger topic than the instructor's worked example in several ways — see §3.

---

## 2. How It Scores Against the Three Criteria

### S1 · Participants ≥ 5, counting outside systems — **PASS (~8)**

Counted by "who asks this system for something":

| Actor | Inside or outside the system? |
|---|---|
| Client / consumer | inside |
| Practitioner (dermatologist, consultant) | inside |
| **AI analysis engine** | **outside** |
| **Product catalogue / e-commerce** | **outside** |
| **Payment provider** | **outside** |
| **Logistics / fulfilment** | **outside** |
| Store advisor | inside |
| Compliance moderation | inside |

> **Note the AI engine counts as an outside system.** It is not part of your application — it is a
> service you send an image to and receive a finding from. That is precisely what S1 is asking you
> to notice, and the fact that your domain supplies one for free is the first sign this topic works.

### S2 · ≥ 8 conceptual classes and ≥ 6 non-"has" relationships — **PASS (~16 classes, 8+ non-has)**

Classes the proposal can support (naming is yours to argue): Client · SkinConcern · Analysis ·
Lesion · Finding · Recommendation · TreatmentPlan · Regimen · Product · Ingredient ·
Contraindication · Practitioner · FollowUp · Moderation · Image.

Relationships that are **not** "has" — this is the part that decides it:

| From | Verb | To |
|---|---|---|
| AI engine | **detects** | Lesion |
| Practitioner | **reviews** | Finding |
| SkinConcern | **drives** | TreatmentPlan |
| TreatmentPlan | **recommends** | Product |
| Regimen | **sequences** | Product |
| Contraindication | **blocks** | Product |
| Client | **adheres to** | Regimen |
| FollowUp | **triggers** | re-analysis |

> ⚠️ **This is the one thing you must get right in the proposal.** "We have 16 classes and lots of
> relationships" is not evidence. The scorecard must contain the **verb** on each arrow. If any
> of the eight above is missing, replace it with something that is not "belongs to".

### S3 · ≥ 2 objects with a lifecycle of 3–4 states — **PASS (three objects qualify)**

| Object | Chain |
|---|---|
| **Analysis** | uploaded → analysing → reviewed → delivered |
| **TreatmentPlan** | draft → proposed → active → evaluating → revised |
| **Lesion** | detected → classified → confirmed → resolved |

TreatmentPlan is the richest of these: `evaluating → revised` gives you a loop, and loops are
where the interesting decisions live.

---

## 3. Why This Is a Strong Topic

Say this to yourselves before you forget it:

1. **The domain is real and you can test it.** Any of the four of you can be the test subject with a phone camera. A pure CRUD topic has no way to check whether the model is right.
2. **The domain hands you a real policy problem.** "AI says the client has a lesion" is not a modelling question. The interesting question is what the system is *allowed to do next*. That is exactly the kind of argument the defence wants.
3. **It has a genuine external dependency.** Every diagram will show a boundary between your system and a black box. Boundaries are where architecture lives.
4. **It crosses at least two state machines and a workflow.** That means W09's state machine and activity diagram are not exercises — they are the answer.

---

## 4. Two Risks the Instructor Sees

Neither blocks your pass. Both will be asked about at the defence, and both are better answered now
than improvised then.

### Risk A · The medical boundary

Your system produces something that resembles a **diagnosis**, and it **recommends products that a
person then puts on their face**. Two questions follow, and they are not modelling questions:

- *May the client see the AI finding before a practitioner reviews it, or is it clinician-only until review?*
- *If the AI is wrong, who is liable — the system, the practitioner who signed off, or nobody?*

**Do not resolve these by guessing.** Put them in **§5 of your proposal** as open questions. This
is precisely what §5 is for, and a team that names its unresolved liability model is demonstrating
exactly the judgement the rubric rewards.

> A note on your own safety: this is a modelling exercise. Say so in your proposal. Do **not** build
> a working detector, do not train on photographs of real people, and do not let the system give
> clinical advice. You are being marked on models, not on software.

### Risk B · Classes are not the same as relationships

A domain this rich will let you list twenty classes in ten minutes. That is not the test. The test
is whether you can say **what each one does to the others**. The scorecard's verbs are the
evidence. If a classmate asked you to point at one arrow and name its relationship, you must be able
to do it for all eight.

---

## 5. What to Do Now

Proceed to **M0**. From this week onward the fixed CampusBites case is gone — everything you
produce is about your own topic.

| # | Task | Template | Due |
|---|---|---|---|
| 1 | Team charter | `templates/Template-W02-01-Team-Charter.md` | Sun Oct 25 |
| 2 | Stakeholder list (5–8, ≥ 2 non-users) | `templates/Template-W02-02-Stakeholder-List.md` | Sun Oct 25 |
| 3 | Project vision (≤ 150 words) | `templates/Template-W02-03-Vision-Statement.md` | Sun Oct 25 |
| 4 | Fill the README milestone table | `templates/Template-W02-04-Repository-README.md` | Sun Oct 25 |
| 5 | Tag and push `m0` | `templates/Template-W02-05-M0-Submission-Checklist.md` | Sun Oct 25, 23:59 |

**The repository already exists** — you created it in W06 and `klausren` already has read access.
You do **not** need to re-invite anybody. See `labs/Lab-07` §0 and checklist §3.

> ⚠️ **The charter must reflect your own topic.** If any line still says CampusBites, fix it before
> you tag. The charter is read as the description of *your* project.

### One suggestion for the charter

The **conflict rule** row is where a small team actually needs it. With four people and one client
who is also the person being analysed, disagreements about "how much AI is enough" will surface
early. Write the rule before it is needed: *who decides, and what happens if you cannot agree.*

---

## 6. If You Disagree

A pass is not a statement that the topic is perfect. If any of the four of you genuinely believes
something here is weak — a class that will not survive M2, a boundary you cannot draw — **write the
objection in one line and commit to the decision.** Silently resenting the topic helps nobody.

---

*Reviewer: 任政 · 2026-10-15 · Topic selection, W06 · Decision recorded in `scorecard.md` in your repository.*