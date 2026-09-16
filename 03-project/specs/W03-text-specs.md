# Week 03 — Text Specs for the PlantUML Homework

> **ISAD · Fall 2026** · Week 03 · These are the two specs referred to by Homework item 1.
> Referenced from: W03 slide 37, `W03-Handout.html` section G, and `Lab-03-W03-UML-Essentials-Practice.md` §8.

## What you have to do

Reproduce **both** specs below as PlantUML, render them, and commit the sources **and** the exported PNGs:

| Deliverable | File name (per slide 30 conventions) |
|---|---|
| Spec A — domain model | `docs/diagrams/domain-model.puml` + `docs/diagrams/domain-model.png` |
| Spec B — sequence diagram | `docs/diagrams/order-sequence.puml` + `docs/diagrams/order-sequence.png` |

Rules that apply:

- Type the PlantUML out yourself — do not copy a rendered picture, and do not paste a solution from a classmate.
- Lower-case kebab file names, one artefact per file, everything under `docs/diagrams/` (slide 30).
- Commit **from your own account**. These two files count towards your individual contribution (Individual grade B2, 15%).
- A push without a tag is not a submission — the tag protocol is in the Deadline Schedule §4.3. (Week 03 itself carries no milestone tag; this homework is due before the Week 04 class.)
- Stuck on syntax? <https://www.plantuml.com/plantuml> renders any snippet in the browser and shows the error inline.

**Do not look for a finished diagram to copy — there is none.** These specs describe the model in words. Turning words into notation is the skill being assessed.

---

## Spec A — CampusBites domain model

Four concepts, three associations. Read the whole spec before you type anything.

### Classes

**1. `Customer`** — a person who orders food through CampusBites.

| Attribute | Type |
|---|---|
| `id` | `String` |
| `name` | `String` |
| `phone` | `String` |

Operations: none. (A passive record — it holds data, it does not make decisions.)

**2. `Order`** — one placed order, from submission to delivery.

| Attribute | Type |
|---|---|
| `id` | `String` |
| `placedAt` | `LocalDateTime` |
| `status` | `OrderStatus` |

| Operation | Signature |
|---|---|
| total | `+ total() : Money` |
| addItem | `+ addItem(item : MenuItem, qty : int) : OrderLine` |
| cancel | `+ cancel(reason : String) : void` |

**3. `OrderLine`** — one line inside an order: a menu item together with the quantity ordered.

| Attribute | Type |
|---|---|
| `qty` | `int` |
| `lineTotal` | `Money` |

| Operation | Signature |
|---|---|
| setQty | `+ setQty(n : int) : void` |

**4. `MenuItem`** — something on the menu that can be ordered.

| Attribute | Type |
|---|---|
| `code` | `String` |
| `name` | `String` |
| `price` | `Money` |
| `available` | `boolean` |

| Operation | Signature |
|---|---|
| price | `+ price() : Money` |

### Associations

| # | From | Multiplicity | To | Multiplicity | Direction / role | Read as |
|---|---|---|---|---|---|---|
| 1 | `Customer` | `1` | `Order` | `0..*` | `Order` → `Customer`, role name `customer` | A customer places many orders; an order belongs to exactly one customer |
| 2 | `Order` | `1` | `OrderLine` | `1..*` | `OrderLine` → `Order`, role name `order` | An order contains at least one line; a line belongs to exactly one order |
| 3 | `OrderLine` | `0..*` | `MenuItem` | `1` | `OrderLine` → `MenuItem`, role name `item` | A line refers to exactly one menu item; a menu item may appear on many lines |

Notes the model has to show:

- Association 2 is **composition** in the analysis sense: delete the order and its lines go with it. Association 3 is **not** — menu items outlive orders.
- No inheritance anywhere in this model. If you find yourself drawing a generalisation, re-read the class list.
- `OrderStatus` and `Money` are types, not classes in this model. Draw them as plain type names in the attribute lists — do not give them their own boxes.

---

## Spec B — `Place an order` sequence diagram

One scenario, one success path. No alternatives, no error branches.

### Lifelines (three, left to right)

1. `:OrderController` — receives the request from the UI.
2. `:Order` — the order being built.
3. `:OrderLine` — a line created during this scenario.

### Messages, in order

| # | Message | From → To | Kind |
|---|---|---|---|
| 1 | `submit(cart)` | `:OrderController` → `:Order` | synchronous call (filled arrow head) |
| 2 | `validate()` | `:Order` → `:Order` | **self-message** |
| 3 | `<create>` | `:Order` → `:OrderLine` | object creation — the arrow points **at the box**, not at the lifeline |
| 4 | `setQty(2)` | `:Order` → `:OrderLine` | synchronous call |
| 5 | `subtotal : Money` | `:OrderLine` ⇠ `:Order` | return (dashed arrow, **open** arrow head) |
| 6 | `total() : Money` | `:Order` → `:Order` | **self-message**, returns the order total |
| 7 | `notify()` | `:Order` ⇠ `:OrderController` | asynchronous (open arrow head — fire and forget, no return expected) |

Notes the diagram has to show:

- Time runs **downward**. Message 1 is the topmost arrow; message 7 is the bottom one.
- A **return** is drawn dashed with an open arrow head; a **synchronous call** is drawn solid with a filled arrow head. Do not mix them up.
- The activation bar on `:Order` runs from message 1 until after message 6; `:OrderLine`'s activation bar starts at message 3 and ends after message 5.
- Message 7 is the last one and has **no** matching return — an asynchronous message does not answer.
- There is no `alt` fragment in this diagram. One scenario shown, one path.

---

## Checking your own work

Before you commit, ask the question Exercise 3.1 drilled:

| If your diagram… | Then it answers |
|---|---|
| shows boxes joined by lines with multiplicities at the ends | *Which concepts exist, and how are they linked?* |
| shows lifelines and arrows running down a page | *Who sends which message to whom, and in what order?* |

If your Spec A output has arrows running down the page, or your Spec B output has boxes with attribute lists, the notation has drifted — fix it before pushing.

---

*Specs authored for Week 03 of ISAD (Fall 2026), case universe CampusBites. Consistent with W03 slides 11, 14, 18, 24, 30 and 37.*
