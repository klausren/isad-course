# Lab 06 · W06 — Domain Modeling v1（今日版：你们自己的需求）

> **ISAD · Fall 2026** · Lab block (last 2 h of the weekly 4 h) · **Thursday Oct 29**
> **Milestone**: **M0 due today** — tag `m0`, push it, read the output.
> **Your material**: `AI-Skin-Analysis-Core-Functional-Requirements.md` (yours, v1.0, issued 2026-10-15)
> **Slides**: `W06-Domain-Modeling.pptx`, **pages 1–29** (the lecture part)
> **Handout**: `W06-Handout.html`, sections D–G (page 2)

**Purpose of this lab.** You wrote twelve functional requirements. Today they become a model.
Every noun you named — `Analysis`, `Finding`, `Contraindication`, `Regimen` — is a candidate
class, and one question decides it: *"can you point at that one?"* You sort your own words into
four buckets, throw most of them away, classify what survives as Entity, Boundary or Control,
draw your first domain model, and **make the decisions your requirements deliberately left open**.

**No programming today.** You write a `.puml` **text file** — that is a model, not a program.
You read it, you edit it, you render it. Nothing is compiled and nothing is deployed.

> **Note.** The exercise pages in the deck (P30–P38) use a different case. Use **your own
> requirements**. That is the point of choosing your own project.

---

## 0. Before You Start (~5 min)

- [ ] `AI-Skin-Analysis-Core-Functional-Requirements.md` is open — but you will work from memory, not from the file
- [ ] Your repository exists and all four of you can push to it
- [ ] PlantUML renders — VS Code extension or <https://www.plantuml.com/plantuml>. Verify it *now*, not at 40 minutes past the hour.
- [ ] You know today's four standing roles: **Lead** (keeps time), **Recorder** (owns the `.puml` file, and only that file), **Reviewer** (checks every class against a requirement line), **Release Manager** (pushes and confirms the file is in the repo)
- [ ] You have read §4 of your requirements — the six things you deliberately did **not** specify

> **Course default, restated:** *model in PlantUML, present in draw.io.* Both source files go in the
> repository. **A PNG on its own is not a submission.**

---

## 1. What the Lecture Gave You

| From the lecture | The one line you need |
|---|---|
| A domain model shows **concepts**, not classes | No methods, no fields, no `getX()` |
| The **noun-phrase heuristic** | The nouns in your requirement sentences are the candidates |
| **Identity**: can you point at one and say "that one"? | If not, it is an attribute |
| Three questions before you draw | Is it a concept? Attribute or class? Does it appear in a requirement? |
| **Entity / Boundary / Control** | Inside the system, on the edge, or one per use case |
| The **three rooms model** | One picture, three questions |
| Association first, multiplicity next | **No multiplicities this week** — that is W09 |

**The sentence to remember:** *a noun is not a class. A relationship that is not "has" is where the modelling lives.*

---

## 2. Demo — Instructor-Led (~10 min)

Watch and note. The instructor scans **your own** requirements, live.

The instructor reads FR-1 aloud and writes on the board:

> FR-1: "The system shall maintain a **client profile** holding personal data, **skin type**,
> declared **concerns**, **allergy history** and product **sensitivities**."

| Word | Bucket | Why |
|---|---|---|
| client profile | **class** | can you point at one and say "that profile"? yes |
| personal data | attribute | belongs to the profile |
| skin type | attribute | cannot be pointed at |
| concern | **class** | a skin concern is tracked over time — FR-11 compares severity across reviews |
| allergy history | **class?** | ⚠️ careful — it has structure and a lifetime. *Decide, and write down why.* |
| sensitivities | attribute | — |

Then the instructor asks the class three questions about each remaining word, and the class answers
loudly. **You will do this for 24 words in Task A.**

**Two words get thrown away** — watch which, and why. One of them is a habit carried over from
another case; the other is an implementation detail wearing a noun's clothes.

---

## 3. Task A — Your Own Noun Scan (~25 min)

**Goal.** Twenty-four words from **your** requirements, sorted into four buckets, each with a reason.

### Steps

1. **Recorder** opens `docs/analysis/noun-scan.md` and creates the four columns:
   `class` · `attribute` · `external actor` · `discard`.
2. Take **eight minutes alone, in silence**. Re-read FR-1 … FR-12 and write down every candidate
   noun you can find — from your own head first, then check the file.
3. **Aim for about 24 words.** Do not aim for a number you can defend. Aim for every noun you can find.
4. Sort each word into a bucket. **Every word needs a reason, and the reason must cite a requirement
   line or say "no requirement mentions this".**
5. Now the hard part: **cross out anything that fails a hard check** — and write `✗` next to it
   rather than deleting it. You want to see what you considered.
6. For each surviving **class**, answer one more question in a second column:
   **can you point at one of these and say "that one"?** If the answer is no, it moves to `attribute`.

**Where do the words come from?** Use at least these sources:

| Source | Words you should find |
|---|---|
| FR-1 (client profile) | client profile, skin type, concern, allergy history, sensitivity |
| FR-2 (image capture) | image, capture metadata, device, lighting condition, analysis request |
| FR-3 (AI analysis) | finding, confidence value, detected concern |
| FR-4 (analysis record) | analysis, state, rejection path |
| FR-5 (practitioner review) | review decision, disclosure |
| FR-6 (treatment plan) | treatment plan, goal, step, review interval |
| FR-7 (product recommendation) | product, ingredient, contraindication |
| FR-8 (regimen) | regimen, sequence, morning/evening |
| FR-9 (follow-up) | follow-up, re-analysis |
| FR-10 (moderation) | guidance text, product claim, moderation |
| FR-11 (history) | severity, comparison |
| FR-12 (purchase handoff) | recommendation set, purchase |

### Done when

- [ ] About 24 words, each with a bucket **and** a reason
- [ ] Every word cites a requirement line, or says "no requirement mentions this"
- [ ] Rejected words are struck through with `✗`, not deleted
- [ ] Every surviving class has an explicit identity verdict

### Stuck?

| Symptom | Fix |
|---|---|
| I cannot tell whether something is a class or an attribute | Ask: *does it have its own lifetime?* `skinType` lives inside a profile. A `concern` is followed across three reviews. |
| Everything ends up in "class" | You are counting nouns, not concepts. `confidence` and `severity` are values. |
| Everything ends up in "attribute" | You are only reading one requirement at a time. `Finding` appears in FR-3, FR-5 and FR-11 — that repetition is the signal. |
| A word has no requirement behind it | That is the answer — put it in `discard` and write "no requirement mentions this". **Do not keep it.** |
| A word is both | Write the verdict for the one you chose **and one line** saying what would have to be true for the other reading. |

---

## 4. Task B — Classify, Then Draw (~45 min)

**Goal.** Every surviving class marked E, B or C, and a first domain model with associations.

### Step B1 — Mark each class (~10 min)

| | Test | If yes |
|---|---|---|
| **Entity** | Does it exist in the real world, have identity, and change over time? | Entity |
| **Boundary** | Does an actor or an external system interact with it directly? | Boundary |
| **Control** | Does one use case drive it? | Control |

Watch the case the deck uses for the external system: **the AI analysis engine is not your code.**
It is an **actor outside your boundary**, not a boundary class of yours. Your FR-3 says so in one
sentence, and your first diagram has to show it.

**Two classes need a decision you must write down:**

| Class | The question |
|---|---|
| `Contraindication` | FR-1 says it attaches to the **client**, not to a product. Does that make it an Entity of the client, or an attribute of the client profile? Argue it. |
| `AllergyHistory` | It has structure and a lifetime. Class or attribute? Argue it. |

### Step B2 — Draw the model (~35 min)

Create `docs/diagrams/domain-model-v1.puml`:

```plantuml
@startuml
skinmodel

skinmodel "AI Skin Analysis" {
  class Client {
  }
  class Analysis {
  }
  class Finding {
  }
  class ClientApp {
  }
  class AnalysisController {
  }
}

Client "1" --o{ "0..*" Analysis : has >
Analysis "1" --o{ "1..*" Finding : contains >
ClientApp ..> AnalysisController
AnalysisController ..> Analysis

@enduml
```

Rules for today:

- **Associations only. No multiplicities, no aggregation diamonds, no visibility markers.**
  Multiplicity is W09, and a diamond you are not sure about is a diamond you will regret.
- Name each association with a **verb** — `has` is allowed, but if every association is `has`
  your model says nothing.
- **No attributes and no methods inside any box.** This is a conceptual model. Attributes are next week.
- **Target: 8 or more classes.** Fewer than eight means you have discarded too much — check whether
  you threw away a real concept because it looked like a detail.

### Done when

- [ ] Every class marked E, B or C, in a column
- [ ] The two argument rows written up, one or two sentences each
- [ ] `docs/diagrams/domain-model-v1.puml` exists and renders
- [ ] The `.puml` source **and** the rendered PNG are both in the repo
- [ ] 8 or more classes, associations named with verbs, no attributes or methods

### Stuck?

| Symptom | Fix |
|---|---|
| The model is only 5 or 6 boxes | Go back to FR-1…FR-12. You have at least 12 candidate concepts. |
| Every association is `has` | Find the non-"has" ones: the AI engine **detects** lesions; the practitioner **reviews** findings; a plan **derives from** findings; a regimen **sequences** products. |
| The AI engine ended up as a boundary class | It is outside. Draw a rectangle around **your** system and put the engine outside it. |
| I do not know which classes are boundary | Look at what a person or an external system touches: the app, the console, the form. |
| I put attributes inside the boxes | Delete them. Conceptual models have no attributes. |
| The `.puml` will not render | Check the `@startuml` / `@enduml` pair and that the file name matches the path you pushed. |

---

## 5. Task C — Make the Open Decisions (~20 min)

**Goal.** Your requirements deliberately left six things unspecified. **Decide one, model it, and
say why.** "We haven't decided" is not a model.

Your FR-3, FR-4 and §4 of the requirements document give you these:

| # | The open question | What a model decision looks like |
|---|---|---|
| 1 | Does the client see findings **before** review? | An association `Analysis → Client` with a guard, or a state on `Analysis` |
| 2 | What happens on a **low-confidence** finding? | A threshold, a routing rule, a state transition |
| 3 | Who may correct a **client's self-declared** concern? | Two roles on the same association, or a rule on the association |
| 4 | Do recommendations differ by **client segment**? | A class, or a rule attached to `Product` |
| 5 | How long are client photographs **retained**? | An attribute with a constraint, or a lifecycle on `Image` |
| 6 | What does the client see on a **rejected** analysis? | A state on `Analysis`, and something the client can see |

### Steps

1. Pick **one** question. (Two if you finish early.)
2. Write the decision in **one sentence** — the rule, not the topic.
   ✅ "Findings with confidence below 0.70 go to `pendingReview` and are never shown to the client."
   ❌ "We would probably just leave it for the practitioner to decide."
3. **Model it.** Change the diagram so the decision is visible. If the decision is about state, add
   the state. If it is about who may act, change the association.
4. Write **one more sentence**: why this way and not the other. Your requirements say *"you must
   model one, and say why."*

### Done when

- [ ] One open question decided, in one clear sentence
- [ ] The diagram shows the decision — not just the note
- [ ] One sentence of reasoning
- [ ] All four members can state the decision without reading it

### Stuck?

| Symptom | Fix |
|---|---|
| The decision is about something outside the system | Then it is not a modelling decision. Pick a different question. |
| We genuinely cannot decide | Then say what you **would** need in order to decide, and model the conservative option. "Not decided" is not a model, but "we modelled the safe option pending X" is. |
| Our decision needs a new class | Good — that is what a model is for. Add it and re-run the identity test. |
| Two members disagree | Model both. Say which one you would ship and why. **Disagreement in writing is worth more than silent agreement.** |

---

## 6. M0 Close-Out (~15 min)

**Goal.** Four artefacts, one tag, one command whose output you read.

**Roles.** Lead calls the time and the go/no-go. Recorder owns the files. Reviewer confirms the
model is consistent with the requirements. **Release Manager pushes and tags** — this cannot be
done at home on Sunday night.

### Steps

1. **Freeze the team charter.** `docs/m0/team-charter.md` (Appendix A). Four names, four roles, the
   submission protocol every member agrees to.
2. **Freeze the stakeholder list.** `docs/m0/stakeholders.md`. Start from the seven actors in §2 of
   your requirements, and mark each **inside** or **outside**. Add anyone the requirements imply but
   never named.
3. **Freeze the project vision.** `docs/m0/vision.md`. One paragraph: who has this problem, what
   the system does about it, and what "good enough" looks like. Add the **safety boundary** from
   §0 — a system that recommends but never prescribes is a different system from one that does not.
4. **Commit the model with the M0 work.** The domain model from Task B is **not** M2, but it should
   not be lost either:

   ```bash
   git add docs/m0/ docs/analysis/ docs/diagrams/
   git commit -m "M0: charter, stakeholders, vision; domain model v1 from the W06 lab"
   ```

5. **Tag `m0`** — Release Manager only, and only **after** step 4 succeeded:

   ```bash
   git tag -a m0 -m "M0: charter, stakeholders, vision"
   git push origin m0
   ```

6. **Verify.** Run it. Read the output.

   ```bash
   git ls-remote --tags origin
   ```

   You must see a line containing `refs/tags/m0`. No line = not submitted. Do not assume; read.

### Done when

- [ ] `docs/m0/team-charter.md`, `docs/m0/stakeholders.md`, `docs/m0/vision.md` committed
- [ ] `docs/diagrams/domain-model-v1.puml` committed **and** its PNG
- [ ] `docs/analysis/noun-scan.md` committed
- [ ] `git ls-remote --tags origin` shows `refs/tags/m0`. You have read the line, not assumed it.

### Stuck?

| Symptom | Fix |
|---|---|
| `git ls-remote --tags origin` shows nothing | The tag was never pushed. Run `git push origin m0` again. If the tag does not exist locally either, `git tag -a m0 -m "M0"` first — and make sure the commit it points at is already on the remote, or the tag points at nothing the reviewer can fetch. |
| `fatal: tag 'm0' already exists` | Someone tagged already. Check `git tag -l` and `git ls-remote --tags origin`. If the remote already has `m0` from today, **do not** force-move it — verify what it points at and move on. |
| Pushed, tagged, and the tag is on the wrong commit | `git tag -f -a m0 -m "M0 corrected"` then `git push origin m0 --force` — legal **only before Sun Nov 01 23:59**, per the Deadline Schedule. After the deadline nothing counts. |
| The charter mentions only 3 of the 4 members | Add the fourth before you tag. Four names, four roles. |
| The vision paragraph mentions the AI engine as "our model" | Fix the wording. The engine is external — your §0 already says so. |

---

## 7. Before You Leave (~5 min)

Each of you signs off one item. **Four people, four lines — not one team signature.**

| Who | Checked |
|---|---|
| ____________ | I wrote my own candidates in Task A before anyone spoke |
| ____________ | Every class in the model has an identity verdict and an E/B/C mark |
| ____________ | I can state our open decision and its reason, without reading it |
| ____________ | `refs/tags/m0` appears in `git ls-remote --tags origin`. I read the output. |

> **Leaving with one question still open is fine. Leaving without a model is not.**

---

## 8. Homework (before Week 09)

1. **Write the other five decisions — one line each.** Not decided yet is fine, but each one must
   name what you would need in order to decide. You will say them aloud at the M1 review.
2. **Extend the requirement list.** M1 is due **Sun Nov 01**: requirements list, use case diagram,
   **2 detailed use case specifications**. Your §5 already suggests the two use cases — decide.
3. **Skim Larman chapter 4** (Use case modelling). You need the nine-field template.

---

## 9. Reference

| Document | What it answers |
|---|---|
| `AI-Skin-Analysis-Core-Functional-Requirements.md` | **Your own material** — FR-1…FR-12, the seven actors, and the six open questions |
| `W06-Topic-Review-PASS-AI-Skin-Detection.md` | Why your topic was approved; the S1/S2/S3 evidence you committed to |
| `../../01-课件/W06-Domain-Modeling/W06-Domain-Modeling.pptx` | The lecture slides; P12–P19 for E/B/C, P26–P29 for building the model |
| `../../01-课件/W06-Domain-Modeling/W06-Handout.html` | Sections D–G — the same material as a printable sheet |
| `../CampusBites-项目指导书-Project-Guidebook.md` | Appendix A — the team charter template |
| `../CampusBites-Deadline-Schedule-and-Submission-Guide.md` | §4 — the submission protocol and the tag rules |
| Larman, *Applying UML and Patterns*, 3e — ch. 4 | The nine-field use case template, for M1 |

---

*Lab 06 · W06 · Information Systems Analysis and Design · Fall 2026*
