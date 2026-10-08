# Lab 06 · W06 — Domain Modeling v1

> **ISAD · Fall 2026** · Lab block (last 2 h of the weekly 4 h) · Week 06, Oct 05 – Oct 11
> **Milestone**: **none this week** — deliberately. M1 closed on Sun Oct 4. **ΔC1 lands online this week** and counts towards M2 (due Sun Oct 25).
> **Slides**: `W06-Domain-Modeling.pptx`, pages 29–36
> **Handout**: `W06-Handout.html`, sections D–G (page 2)

**Purpose of this lab.** Last week you wrote sentences. This week the sentences pay rent: every noun you named — order, coupon, delivery window, kitchen ticket — is a candidate class, and the only question that decides it is *"can you point at that one?"* You sort eighteen words into four buckets, throw most of them away, draw the first domain model with **14 classes**, and fold in the first requirement change without restarting.

**No programming today.** You write a `.puml` **text file** — that is a model, not a program. You read it, you edit it, you render it. Nothing is compiled and nothing is deployed.

---

## 0. Before You Start (~5 min)

- [ ] M1 is closed: `git ls-remote --tags origin` shows `refs/tags/m1`. *(If it does not, tell the instructor **now** — this week's work builds directly on it.)*
- [ ] Both M1 specifications are committed: `docs/use-cases/`.
- [ ] You can push to `campusbites-team-01`.
- [ ] PlantUML renders — VS Code extension or <https://www.plantuml.com/plantuml>. Verify it *now*, not at 40 minutes past the hour.
- [ ] You know today's four standing roles: **Lead** (keeps time), **Recorder** (owns the `.puml` file, and only that file), **Reviewer** (checks every class against its spec sentence), **Release Manager** (pushes and confirms the file is in the repo).
- [ ] You have checked `changes/` for **ΔC1**. It was announced online this week.

> **Course default, restated:** *model in PlantUML, present in draw.io.* Both source files go in the repository. **A PNG on its own is not a submission.**

---

## 1. What the Lecture Gave You

| From the lecture | The one line you need |
|---|---|
| Identity decides class vs. attribute | Point at one and say "that one" → class. Read it off something else → attribute. |
| A class with no sentence behind it is a guess | "We will probably need it later" is not a sentence. No sentence, no class. |
| Three kinds, no exceptions | Entity · Boundary · Control. A box you cannot classify is a box whose responsibility nobody agreed on. |
| It would survive a language change | `Service`, `Manager`, `Helper`, `DTO`, `Table` are W10 words arriving two weeks early. |
| The words you throw away matter too | Discarding *server, service, table* is how you know where the boundary is. |
| Attributes graduate into classes | `DeliveryWindow` became a class the first time the client asked a second question about fees. |

> **The sentence to remember:** *if you can point at it, it is a class.* (Slide 37, item 01 — it settles in one sentence most arguments that otherwise take ten minutes.)

---

## 2. Demo — Instructor-Led (~20 min)

One sentence from your own M1 specification goes on the board, and the instructor scans it for nouns live:

```text
System creates the order in state Accepted.
```

| # | Noun | What it is | Why |
|---|---|---|---|
| 1 | **System** | **NOT a class** | It is already the actor on your use case diagram. It is the box everything sits in. |
| 2 | **order** | **A conceptual class** | It has identity: point at CB-20419 and say which. *(Yes — "order" is also a verb. Context decides, not the spelling.)* |
| 3 | **state** | **An attribute** | One value of one order. No identity of its own → it becomes an attribute of `Order`. |
| 4 | **Accepted** | **A value, not a noun at all** | One member of a fixed list. W09 turns it into a state machine. |

Tick what you actually saw:

- [ ] "Can you point at this thing and say *that one*?" was the **only** test used.
- [ ] Point at the order → yes → class. Point at "Accepted" → no, you can only read it off an order → attribute value.
- [ ] A noun ending in **-ing** or **-tion** (*validation*, *calculation*) is usually an **operation**, not a class.
- [ ] The test settled in one sentence what the four of you had already argued about for eight minutes.

**Notes — take these down, you will use them in Task B:**

```
Three questions before you draw a box (slide 06):
  1. Is it a concept, or an actor? _________________________________________________
  2. Does it have identity — can I point at one? ______________________________________
  3. Did it earn its place — can I point at the W05 sentence? _________________________

The question that is NOT a modelling criterion: _____________________________________
```

> **Common-error gallery (slide 10), four wrong reasons to add a class:** *"we will need a class for that"* → `OrderHelper`, `OrderUtils`, `OrderDTO`, `OrderInfo`, four classes all meaning `Order`. *"the database needs a table for it"* → relational and object models are not the same thing. *"ten classes looks more professional"* → padding, and this reason is **never valid at any point in the project**. *"it needs behaviour, so it must be a class"* → behaviour on a thing with no identity.

---

## 3. Task A — Exercise 6.1: Sort the Messy List (~30 min)

**Goal.** Sort eighteen words into four buckets, mark every surviving class E / B / C, and write the specification sentence each class came from. **No sentence, no class.**

**Input.** Slide 29 / handout section D. Eighteen words, collected from the specifications, the requirements pack and two team meetings, **sorted by nobody**.

```text
  order          OrderLine      menu item
  total          payment        provider
  cart           coupon         code
  kitchen ticket order time     rating
  delivery       window         fee
  student        validation     calculation
  logging        server         service
  table          interface      ui
```

**Four buckets:** conceptual class · attribute · external actor · discard.
**Then, for each class you keep:** Entity / Boundary / Control.

### Steps

1. **Read alone. Five minutes. No talking.** The Lead starts the clock and says nothing until all four are done. Fill the sheet in handout section D — every row, including the ones you are unsure about.
2. **The four hardest words — decide them yourself before looking at anything:** `delivery window` · `coupon code` · `rating` · `kitchen ticket`.
3. **Merge onto the Recorder's page.** Recorder writes; everyone dictates their own rows. Keep the rows you disagreed on, marked `DISAGREE`.
4. **For every class you keep, write the one specification sentence it came from.** If you cannot point at a sentence in a W05 spec, delete the class.
5. **Compare against the authoritative sort (slides 30–31):**

   | Words | Your call | If a class, then |
   |---|---|---|
   | order · OrderLine · menu item | **3 classes** | three entities. "menu item", not "item" — say which catalogue |
   | total | **attribute** | of `OrderLine`, and **derived**; or of `Order` if you decide to store it — **say which** |
   | payment · provider | **one class, one actor** | `Payment` is a record we keep; the **provider** is outside the boundary and was already on your use case diagram |
   | coupon · code | **class + attribute** | `Coupon` is an entity — students point at their coupons. `code` is only its attribute |
   | delivery · window · fee | **one class** | `DeliveryWindow` is an entity once fees vary by window; `window` and `fee` are its attributes |
   | cart | **discard, or at best an attribute** | "the cart total" is one sentence. A cart is not a thing the kitchen ever hears about |
   | kitchen ticket · order time | **discard as a class** | both are things an `Order` *has* — they appear inside the `Order` box, not beside it |
   | rating | **discard — for now** | it belongs to **Rate Restaurant**, a use case you have not specified yet. Keep it in the appendix, not in the model |
   | student | **external actor** | already on your use case diagram, outside the boundary |
   | validation · calculation · logging | **discard** | gerunds and technology words. None is in a specification sentence |
   | server · service · table · interface · ui | **discard** | implementation words. If one appears in your model, your model is a design model |

6. **Mark E / B / C for every class you kept** — one kind each, no exceptions, each defensible in one sentence.
7. **Write one sentence to close (handout section D):** *the words we threw away were as important as the ones we kept, because they showed us where the ______ is.* → **boundary**.

### Done when

- [ ] All eighteen words are in a bucket. **No word is left blank.**
- [ ] Every kept class has **E / B / C** marked and **one sentence** justifying the mark.
- [ ] Every kept class has a **traceable W05 specification sentence** written next to it.
- [ ] `Cart`, `Provider` and `Rating` are **not** drawn as classes — or you have written one sentence per class saying why you overrode the answer key.
- [ ] The eight discard words are listed, and you can say what each one would have dragged into the model.
- [ ] DISAGREE rows are still on the page.

### Stuck?

| Symptom | Fix |
|---|---|
| I kept `Cart` because it is a noun in step 1 | It only exists between browsing and paying. `OrderLine` already carries it. A cart is a screen state, not a business concept — the kitchen never hears about a cart. |
| I made `Provider` a class because step 4 talks to it | It is **outside the boundary**. It was on your use case diagram as an actor in W04. Naming it `PaymentProvider` as a class is a design decision made in the wrong week. `Payment` is the record you keep; the provider is who you call. |
| I made `Rating` a class because it is clearly needed | It belongs to **Rate Restaurant**, and you have not specified that use case. A class with no sentence behind it is a guess. Put it in the appendix; it arrives in W07–W08. |
| "delivery window" — one class or three words? | One class: `DeliveryWindow`. It graduated from attribute to class the moment the client asked *"can a restaurant charge different fees per window?"* Then `earliest`, `latest` and `fee` are its attributes. |
| "kitchen ticket" is printed, it must be a class | Print it, or model it — that is W10. In the analysis model it is a thing an `Order` *has*: an existence postcondition, not a box. |
| The slide says "seven words discarded" but lists eight | Count the list yourself: validation, calculation, logging, server, service, table, interface, **ui** = eight. The slide's headline is wrong and the page says so. Find the discrepancy yourself — that is the exercise. |
| I put `total` in two boxes | Decide deliberately: derived from the lines, or stored on the order. Either is defensible. Carrying it in both boxes is not. Also: `createdAt / updatedAt / deletedAt` are **audit columns**, an implementation decision, not analysis. |
| Two of us have 15 classes and two of us have 11 | Both are legitimate. This week is not graded on the count. It is graded on **traceability**: a class you cannot trace to a sentence is the only real defect. |

> **Calibration:** the target is **14 classes** (8 entity, 4 boundary, 2 control). Below 10 you have missed part of the domain; above 20 you have drawn the database.

---

## 4. Task B — Exercise 6.2: Draw the First Domain Model (~40 min)

**Goal.** Draw the CampusBites domain model in PlantUML — entities, boundaries and controls, with their attributes and instance operations, plus the associations between them. **No multiplicities. No aggregation diamonds.** Those are W07, and guessing them today is how you end up with `1..*` on everything by W07.

**Input.** Output file: **`docs/diagrams/domain-model-v1.puml`**. Target: **10+ classes** (the reference answer is 14).

### Steps

1. **Roles, four people four jobs.** **Lead** keeps the clock and calls the disagreements. **Recorder owns the `.puml` file, and only that file.** **Reviewer** checks every class against its spec sentence. **Release Manager** pushes and confirms the file is in the repo.
2. **Open the file with this skeleton** — it compiles as-is, so you can render it before you have decided anything:

   ```plantuml
   @startuml
   skinparam classAttributeIconSize 0

   ' ---- Entity classes (8) ----
   class Order <<entity>> {
     orderNumber : String
     placedAt : DateTime
     state : String
     note : String
     cancel(reason : String) : void
     isOpen() : Boolean
   }

   class OrderLine <<entity>> {
     quantity : int
     lineTotal() : Money
   }

   class MenuItem <<entity>> {
     code : String
     name : String
     price : Money
     isAvailable() : Boolean
   }

   class Restaurant <<entity>> {
     name : String
     isOpen() : Boolean
   }

   class Courier <<entity>> {
     name : String
     isAvailable() : Boolean
   }

   class Payment <<entity>> {
     amount : Money
     method : String
     isDeclined() : Boolean
   }

   class Coupon <<entity>> {
     code : String
     discountValue : Money
   }

   class DeliveryWindow <<entity>> {
     earliest : DateTime
     latest : DateTime
     fee : Money
   }

   ' ---- Boundary classes (4): one per way the outside world talks in ----
   class StudentApp <<boundary>> {
     submitCart(cart) : OrderSummary
   }
   class KitchenDisplay <<boundary>> {
     showAcceptedOrders() : void
   }
   class CourierApp <<boundary>> {
     acceptTask(orderNumber) : Boolean
   }
   class RestaurantConsole <<boundary>> {
     markSoldOut(item) : void
   }

   ' ---- Control classes (2): one per use case needing sequencing ----
   class PlaceOrderController <<control>> {
     placeOrder(cart, method) : OrderSummary
   }

   class PayController <<control>> {
     pay(orderNumber, method) : PaymentResult
   }

   ' ---- Associations: plain lines, sayable aloud. NO multiplicities today. ----
   StudentApp --> PlaceOrderController : submits
   PlaceOrderController --> Order : creates
   Order -- OrderLine : contains
   OrderLine --> MenuItem : item
   Order --> Restaurant : from
   Order --> Courier : assigned to
   Order --> Payment : paid by
   Order --> DeliveryWindow : scheduled in
   Order --> Coupon : uses
   KitchenDisplay --> Order : shows
   CourierApp --> Order : tracks
   RestaurantConsole --> MenuItem : manages
   @enduml
   ```

3. **Replace the skeleton with your own model.** Every class must be traceable to a W05 specification sentence — write that sentence as a `' comment` above the class, which is free evidence and diffs cleanly:

   ```plantuml
   ' Order — W05 step 5: "System creates the order in state Accepted."
   class Order <<entity>> {
   ```

4. **Give every class at least one attribute and one operation.** Seven lines for `Order` is the reference standard: four attributes, three operations, every one traceable. `total` is **not** on the list — it is calculated from the lines, and the client never asked to store it.
5. **Only instance attributes and instance operations.** No visibility marks (`+` / `-`) — in an analysis model every member is public, so we do not write them yet. No collection operations (`findOpenFor`, `nearestTo`) — those belong to the control class or to a collection, never to one instance.
6. **Draw the associations with a direction you can say out loud:** *an order has lines*, *a restaurant owns a menu*, *a line refers to exactly one menu item*. An arrow you cannot phrase in English is a fail.
7. **Run the seven-question self-check (slide 33 / handout section F)** before you commit anything:

   | # | Ask this | A pass looks like | A fail looks like |
   |---|---|---|---|
   | 1 | Can I point at the sentence for this class? | "Order" comes from W05 step 5 | "we will probably need it later" |
   | 2 | Which of E, B, C is it — defensible in one sentence? | marked | nothing marked — "conceptual class" is not a category |
   | 3 | Does any name come from a screen? | Order, Courier, Coupon | CartPage, OrderForm, PaymentDTO |
   | 4 | Did a technology word sneak in? | no server, service, table, interface | PaymentService, UserTable |
   | 5 | Is every association sayable aloud? | "an order has one or more lines" | an arrow with no English phrasing |
   | 6 | Could you delete this class? | someone would notice within a day | nothing would notice → padding |
   | 7 | Attributes and instance operations only? | `isOpen()`, `cancel(reason)` | `findOpenFor` → control class |

   **Question 6 is the last gate.** The Reviewer picks the smallest box on the diagram and asks it out loud.

8. **Count and record it** on handout section E:

   ```
   E entity classes = ____     boundary = ____     control = ____
   → total classes = ____        associations drawn = ____
   ```

9. **Render, export the PNG, commit both.** A `.puml` that does not render is not a model. A PNG with no source is not a submission.

   ```bash
   mkdir -p docs/diagrams
   git add docs/diagrams/domain-model-v1.puml docs/diagrams/domain-model-v1.png
   git commit -m "W06: domain model v1 (Ex 6.2) — 14 classes, no multiplicities, traced to W05 sentences"
   git push
   ```

### Done when

- [ ] `docs/diagrams/domain-model-v1.puml` exists and **renders**.
- [ ] **10 or more** classes, every one traceable to a W05 specification sentence, written as a `' comment`.
- [ ] Every class is marked **E / B / C** — one kind each.
- [ ] No name ends in `Service`, `Manager`, `Helper`, `DTO`, `Table` or `Entity`.
- [ ] No actor is a class. `Student`, `Provider`, `Admin` are outside the boundary.
- [ ] Attributes and instance operations only. No visibility marks, no collection operations.
- [ ] **No multiplicities, no aggregation diamonds.**
- [ ] Both the `.puml` **and** the rendered `.png` are committed and pushed.

### Stuck?

| Symptom | Fix |
|---|---|
| Render fails, error is about `<<entity>>` | PlantUML stereotypes use that exact double-angle spelling and must be attached directly to the class name. Also check you closed every `{ }` and typed `@enduml`. |
| Render fails and the message names a line number | The web renderer (<https://www.plantuml.com/plantuml>) shows the error inline with the offending line. Fix the syntax; do not screenshot the error into your notes. |
| `1..*` looks right and I am sure of it | You are sure today, wrong on Friday. Slide 27 is explicit: **do not add multiplicities even if you are sure of them.** Remove them. |
| An entity needs a method like `printTicket()` | That is a **boundary's** job doing an entity's. Move it, or drop it — printing is W10. A boundary containing business rules hides them from review. |
| A boundary class has pricing rules in it | It is hiding them. Business rules belong to the entities; the boundary presents them. |
| `PlaceOrderController` has its own `orderList` field | God object in waiting. A control class **stores nothing** — it asks the entities to record things and forgets about them. |
| My control class is doing three use cases | One control per use case. `OrderService` / `OrderHelper` are W10 design names and they hide the use cases — that is the trap. Expect to reshape controls in W10; that is not a failure, it means you modelled honestly. |
| I put a `Student` class in the model | Student is an actor. It is outside the boundary and lives on the use case diagram. Ask: *does it stand outside the system and use it?* |
| Eighteen classes and rising | Stop and run question 6 on each one. A model of four has missed the domain; a model of thirty has drawn the database. |
| My reviewer cannot find a sentence for a class | Then delete the class. Do not weaken the rule. "Conceptual class" is not a category. |

---

## 5. Task C — Fold in ΔC1 (~20 min)

**Goal.** Absorb the first planned requirement change **without restarting**. A good analysis model makes a change *local*: two or three boxes move and nothing else does. A bad one makes it global: you redraw everything.

**Input.** The new requirement is in your repository, in `changes/`, announced online this week. **Time budget: 30 minutes, and it counts towards M2.** Output file: **`changes/C1-response.md`**.

### Steps

1. **Read it twice before reacting.** First read to find out what it is. Second read to find the nouns.
2. **Name the nouns it introduces.** They are the candidates for new classes. Nothing else is.
3. **Decide, per noun: new class, new attribute, or nothing.** Each noun gets one of those three answers — written down.
4. **Write the paragraph.** One short paragraph per change, in this exact shape:

   ```markdown
   # ΔC1 Response — W06

   **Change:** <one line quoting the new requirement>

   ## What it touches
   <nouns and boxes it touches>

   ## What I changed
   <the diagram edits you made — or "nothing">

   ## What I decided NOT to change — and why
   <the classes, associations or specs you deliberately left alone, with the reason>

   ## Traceability
   <the W05 / ΔC1 sentence behind every new class>
   ```

5. **Update the diagram if you decided to change something.** Commit both files in the same commit:

   ```bash
   git add docs/diagrams/domain-model-v1.puml docs/diagrams/domain-model-v1.png changes/C1-response.md
   git commit -m "W06: domain model v1 + C1 response"
   git push
   ```

6. **One last full push, tag, verify** — the protocol never changes, even in a week with no milestone tag:

   ```bash
   git tag -a w06-domain-model -m "W06: domain model v1 + C1 response"
   git push origin w06-domain-model
   git ls-remote --tags origin     # read the output
   ```

### The four sample changes and how far each travels (slide 35)

| The change says | It touches | You write down |
|---|---|---|
| "Students may rate the **courier**, not only the restaurant." | `Rating` — a **new entity** · `Courier` — already there | `Rating` is a new class **with a target**; `Courier` gains **no new attribute**. Two boxes touched. |
| "Restaurants may print the kitchen ticket themselves." | `KitchenDisplay` — an existing boundary | One association added. **No new class** — the boundary was already there. |
| "Orders can be **scheduled for tomorrow**." | `Order.state` gains a value · `DeliveryWindow` | **No new class at all.** But W09's state machine gains a state — plan for it. |
| "The campus card centre becomes an actor." | The **use case diagram**, not the domain model | Nothing to change here — and **that is a perfectly good answer.** |

### Done when

- [ ] `changes/C1-response.md` exists with all five headings filled.
- [ ] Every noun the change introduces has one of: **new class / new attribute / nothing** — written down.
- [ ] The "decided **not** to change" section is **not empty**. "Nothing to change here" is a legitimate finding; **writing it down is what makes it a finding.**
- [ ] Every new class has a traceability line naming the sentence behind it.
- [ ] `.puml` and `.png` are pushed together with the response.
- [ ] `git ls-remote --tags origin` shows `refs/tags/w06-domain-model`.

### Stuck?

| Symptom | Fix |
|---|---|
| `changes/` is empty or there is no file in it | ΔC1 is announced **online** as well. Ask the instructor in class, or check the course repository before you leave today. Do not invent the change. |
| The change touches five boxes | That is the answer the change gives. Write it down honestly and say *how far it travelled* — distance is the test of the model, not a mark against you. If ΔC1 costs you a day, the model was not finished yet. |
| I cannot tell whether something is a new class or a new attribute | Ask: *can I point at one?* If the client will ask a **second** question about it, it graduates to a class. That is exactly how `DeliveryWindow` happened. |
| I want to restart and redraw everything | You are not allowed to restart. Keep the change local by definition: touch only what the change names. "How far does it travel" is the grade. |
| Nothing in ΔC1 affects the domain model | Then your response file says so, in one paragraph, with the reason. **That is a good answer.** An empty file is not. |
| Our `.png` is newer than our `.puml` or vice versa | They are committed together in one `git add`. If the render is stale, re-render before you commit — a PNG of last week's model is evidence of nothing. |
| We have no milestone tag this week, so we skipped the protocol | The protocol is unchanged. `git tag`, `git push origin <tag>`, `git ls-remote --tags origin`. From M1 onwards the tag is what gets graded — for the weekly tags too, that is how your evidence trail is built. |

---

## 6. Before You Leave (~5 min)

Each of you signs **one** row, and each row is a different box on the diagram. Four signatures of understanding, not one team tick.

| # | Person | Signs off on | Own class | Signature |
|---|---|---|---|---|
| 1 | **Lead** | Time was kept: Demo 20 · Ex 6.1 30 · Ex 6.2 40 · ΔC1 20 · sign-off 5. Nobody left with an empty section. | — | ____________ |
| 2 | **Recorder** | `domain-model-v1.puml` and its `.png` are both committed and pushed, and I can render the `.puml` from a clean clone. | `Payment` | ____________ |
| 3 | **Reviewer** | I checked every class against its W05 sentence, and I asked question 6 out loud on the smallest box. | `DeliveryWindow` | ____________ |
| 4 | **Release Manager** | `changes/C1-response.md` is pushed, the weekly tag is on the remote, and I read `git ls-remote --tags origin`. | `Courier` | ____________ |

**Everyone, before the door — three things coming at you next week:**

- **W07 (Oct 12–18): Domain Relationships.** Multiplicities `1`, `0..*`, `1..*`; aggregation vs. composition; and the attributes that turn out to have been classes all along. The lines you drew roughly today get their numbers.
- **The M1 client review happens in W07's class.** The **instructor plays the client**, 30 minutes: 10 min present, 20 min interrogation. **Bring the questions from Box 5 of your M1 review form** — that list is the agenda.
- **Bring the diagram.** You will be asked to defend any class on it, including the ones you did not draw.

---

## 7. Homework (before Week 07)

1. **Finish the model.** Every class in `docs/diagrams/domain-model-v1.puml` has **at least one attribute and one operation**, each traceable to a W05 specification sentence. Render, export the PNG, commit **both**. Expect to reshape control classes in W10 — that is normal, not failure.
2. **ΔC1 response.** Check `changes/` again for anything that arrived after today's session and fold it into `changes/C1-response.md`. **30 minutes, counted in M2.**
3. **Read Larman** on domain modeling — conceptual classes and the three rooms. Skim association and multiplicity as well, because next week is entirely about them.
4. **Prepare for the client review.** Re-read your own two M1 specifications and your Box 5 list. Any member can be asked about any spec. "I did not write that one" is not an answer you may give.

```bash
git add docs/diagrams/domain-model-v1.puml docs/diagrams/domain-model-v1.png changes/C1-response.md
git commit -m "W06 homework: model finished, every class traceable"
git push
```

> Stuck on an attribute that keeps growing? Write down the second question the client would ask about it. That question is the promotion from attribute to class — and it is exactly the argument you will have in W07.

---

## 8. Reference

| Document | What it answers |
|---|---|
| `../CampusBites-项目指导书-Project-Guidebook.md` | §2 the domain and its actors · §5 M2 deliverables · §6 repository layout and the tag rule |
| `../CampusBites-Deadline-Schedule-and-Submission-Guide.md` | §4.3 the tag protocol, push → tag → verify · §4.4 README status table |
| `../Course-Project-Grading-Rubric.md` | How M2 is scored (milestone points) |
| `../CampusBites-Lab-Guide-实验指导书.md` | §3 the 16-week map · §4 what "done" means |
| `../../01-课件/W06-Domain-Modeling/W06-Handout.html` | Sections D–G: the sort table, the drawing task, the seven-question self-check |
| `../../01-课件/Pseudocode-Conventions-伪代码约定.md` | How notation is written in this course (no programming needed) |
| `Lab-04-W04-Finding-Actors-and-Use-Cases.md` | The actors your model must not turn into classes |
| `Lab-05-W05-Use-Case-Specification-and-Peer-Review.md` | The W05 specifications every class must trace back to |
| `Lab-03-W03-UML-Essentials-Practice.md` | PlantUML syntax and the source + PNG rule |

**Submission address:** `https://github.com/<owner>/campusbites-team-01` — instructor GitHub account **`klausren`** (read access is enough).

*Lab questions go to the instructor in class, or open an issue in the course repository.*

---

*Lab 06 · v1.0 · Information Systems Analysis and Design · Fall 2026*
