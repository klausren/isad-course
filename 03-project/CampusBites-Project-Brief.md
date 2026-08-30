# CampusBites — Team Project Brief

> Running project for *Information Systems Analysis and Design* · 16 weeks · teams of 5–6 · full English deliverables

## 1. The Case

**CampusBites** is a campus food ordering and delivery platform. Students order meals from campus restaurants via a mobile app; student couriers pick up and deliver the orders. The platform handles menus, ordering, payment (campus card, wallets, cash on delivery), real-time order tracking, notifications, ratings, and promotions.

### Stakeholders

| Actor | Goal |
|---|---|
| Student customer | Browse menus, order, pay, track delivery, rate |
| Restaurant manager | Manage menu & items, confirm & prepare orders, view sales |
| Courier (student runner) | Claim available deliveries, update delivery status |
| Platform admin | Manage restaurants & users, configure promotions, view reports |
| Payment provider (campus card center) | Charge/refund campus cards (third-party, legacy API) |
| Notification service | Deliver email / SMS / push messages |

### Why this domain?

Every technique in this course maps naturally onto CampusBites:

| Course topic | CampusBites hook |
|---|---|
| Use case modeling | 6+ core use cases with rich extensions |
| Domain modeling | Orders, order lines, menus, couriers, payments, reviews |
| Sequence diagrams | Order placement, payment, tracking workflows |
| State machines | Order lifecycle: Created → Paid → Preparing → Ready → Delivered / Cancelled |
| GRASP / SOLID | Where does `orderTotal()` live? Who creates `Payment`? |
| Strategy | Pricing rules: happy-hour, student discount, bundle |
| Observer | Customers & couriers subscribe to order status changes |
| State (pattern) | Refactor the order lifecycle switch into state classes |
| Adapter | Legacy campus-card API behind our `PaymentMethod` interface |
| Decorator | Meal customization: toppings, portions, combo add-ons |
| Facade | One front door to the notification stack |
| Builder | Assemble a complex customized order step by step |
| Command | Order operations with undo (cancel/modify before preparing) |

## 2. Team Setup

- Teams of **5–6** students, formed in Week 2 (lab).
- Roles rotate: analyst, modeler (2), implementer/refactorer, reviewer, presenter. Every member must be able to explain every model at the defense.
- Two-track requirement model (see `项目分组与评审机制-Grouping-and-Review.md`): Track A teams receive requirements from the **client** (domain expert, co-reviewed with instructor); Track B teams receive requirements from the **instructor** (instructor sole reviewer).

## 3. Milestones

| Milestone | Due (lab) | Deliverable | Weight hint |
|---|---|---|---|
| M0 Kickoff | W2 | Team charter, stakeholder list, project vision | pass/fail |
| M1 Requirements | W5 | Vision & requirements list, use case model, 2 detailed use case specs | foundation for review |
| M2 Analysis models | W8 (reviewed W9) | Domain model, 2+ sequence diagrams, order state machine | mid-term review |
| M3 Design models | W12 | Design class diagram + GRASP/SOLID application notes | scored |
| M4 Pattern catalog | W15 | 5+ patterns applied: problem → pattern → UML → code sketch → consequence | scored |
| M5 Final defense | W16 | Final report + full portfolio + oral defense | final |

## 4. Deliverable Format Requirements

1. **Language**: all English (quality of English is graded — see rubric).
2. **Diagrams**: source files (.drawio or .puml) must be committed alongside exported images.
3. **Pattern cards**: one card per pattern application, fixed template provided in W13.
4. **Traceability**: each DCD operation must trace to at least one sequence-diagram message; each sequence diagram to a use case step. A traceability matrix is required in the final report.
5. **Versioning**: all deliverables in the team's Git repository; commit history is teamwork evidence.

## 5. Rules of the Game

- Models must be **your own** — no copying from last year's projects or online repositories (checked at defense).
- AI tools may be used for English polishing or syntax checking **if disclosed** in the final report; models and design decisions must be human-made.
- Late milestone submission: −10% per day, max 3 days, then not accepted without prior approval.
- Bonus (up to 10%): extra patterns beyond 5, exceptional refactoring narratives, outstanding documentation quality.
