# Core Functional Requirements — AI Skin Analysis & Skincare Recommendation
# 核心功能需求说明 · AI 皮肤检测与护肤推荐系统

> **ISAD · Fall 2026** · Information Systems Analysis and Design
> **Audience**: the four-person team · **Use**: as the starting point for M1 requirements (due **Sun Nov 01**)
> **Status**: instructor-provided, **not** the complete requirement list. Your own reading of the
> domain must extend it. If you disagree with something here, write your objection down and bring
> it to the M1 review — do not silently comply.
>
> **本文是教师提供的起点，不是完整需求清单。** M1（Nov 01）要交的是**你们自己**的需求清单，
> 必须包含本文件之外的补充。本文件与你理解不一致的地方，写下来、带到 M1 评审会上讨论，
> 不要沉默地照做。

---

## 0. Scope and Safety Boundary / 范围与安全边界

> ⚠️ **Read this before anything else.**

This is a **modelling exercise**, not a product. The deliverables are UML models and a defence
argument. Nothing is built, nothing is trained, nobody's skin is analysed.

**Therefore:**

1. **No real detection.** Do not train on photographs of real people. Do not test on classmates'
   faces. Stock images at most, and even then only to illustrate a diagram.
2. **No clinical output.** The system's findings are labelled as *screening suggestions*
   (初筛建议), never as diagnosis. Any requirement implying a diagnosis must be rejected at review.
3. **Recommend, never prescribe.** The system recommends products; a practitioner decides. Any
   requirement that has the system instruct a user to apply a product unsupervised must be
   rejected.
4. **Human review before disclosure.** This is the unresolved question from your Topic Proposal §5.
   You may model either choice — but you must **model one**, and say why. "We haven't decided" is
   not a model.

> 这四条不是道德说教，是**建模约束**。第 4 条尤其重要：你的 Analysis 模型必须能表达
> 「结论在复核前能不能给客户看」这个选择。两种做法都合法，但**必须选一种并说清理由**，
> 不能停在"还没定"——那不是模型。

---

## 1. The Case / 案例

**AI Skin Analysis** is an in-store and online service that analyses a client's skin condition from
photographs, produces a structured assessment, and turns it into a personalised skincare regimen
with recommended products.

Clients submit photographs (face, or a specific concern area), the system forwards them to an
**external AI analysis engine**, receives structured findings back, stores them as an
**Analysis record**, and derives a **TreatmentPlan**. A **practitioner** (dermatologist or store
advisor) reviews the findings before the client sees them. Approved plans are turned into a daily
**Regimen** of **Product** recommendations, drawn from the retailer's catalogue and screened
against the client's **Contraindications**. Follow-ups re-open the analysis after an interval.

**AI 皮肤检测**是一项门店与线上结合的服务：通过客户上传的照片分析皮肤状况，产出结构化评估，
并据此生成个性化护肤方案与推荐产品。

客户提交照片（面部或特定问题部位），系统将照片提交给**外部 AI 检测引擎**，取回结构化结论，
存为一条**分析记录**，并据此推导**护理方案**。由**执业人员**（皮肤科医生或门店顾问）复核后，
客户才可见结论。通过复核的方案转为每日**护肤流程**，产品来自零售商目录，并须通过客户
**禁忌**筛查。复检会在间隔期后重新开启分析。

---

## 2. Actors / 参与者

> Counted by "who asks this system for something". Four of these are **outside** your system.
> 这个表就是 S1 的举证材料。

| Actor | Inside / outside | Core goal |
|---|---|---|
| Client (客户) | inside | Understand their skin, get a plan, know which products to use and which to avoid |
| Practitioner (执业人员：皮肤科医生 / 门店顾问) | inside | Review AI findings, approve or amend the plan, sign off before disclosure |
| **AI Analysis Engine（AI 检测引擎）** | **outside** | Receive an image, return structured findings and confidence |
| **Product Catalogue / Retail System（产品目录系统）** | **outside** | Supply available products, ingredients, categories, stock |
| **Payment Provider（支付服务）** | **outside** | Charge for the analysis or for recommended products |
| Compliance Moderation (合规审核) | inside | Ensure published guidance and recommendations do not breach the retailer's medical-claim policy |
| Store Advisor (门店顾问) | inside | Onboard clients, assist with follow-up scheduling |

**Count = 7, of which 3 are external systems** (plus payment, making 4 touchpoints if bundled).
Write your counting method in the scorecard the way §3 of the brief demands.

---

## 3. Core Functional Requirements / 核心功能需求

Requirements are numbered `FR-n`. Each one is stated as a **capability**, not an implementation —
you will turn these into use cases in M1.

### FR-1 · Client registration and profile / 客户注册与档案

The system shall maintain a client profile holding personal data, skin type, declared concerns,
allergy history and product sensitivities. A profile is created before any analysis exists and is
referenced by every later record.

系统应维护客户档案，保存个人资料、肤质、自述问题、过敏史与产品敏感信息。档案在分析之前建立，
并被此后的所有记录引用。

> **Why this matters for modelling**: `Contraindication` attaches to the **client**, not to a
> product. That single decision is what makes contraindications reusable across every analysis.

---

### FR-2 · Image capture and submission / 照片采集与提交

The system shall accept photographs from a client, allow the client to identify a specific concern
area, record capture metadata (device, timestamp, lighting condition), and assign each image to an
analysis request.

系统应接收客户上传的照片，允许客户标注具体问题部位，记录采集元数据（设备、时间、光照条件），
并将每张图像关联到一次分析请求。

> **Extensibility hook**: "analysis by photograph" is the **normal** flow. A future `in-store
> device` flow should be addable **without changing** the analysis records. If your design cannot
> absorb that, note it — this is the seam a Facade or Adapter would later close.

---

### FR-3 · AI analysis (external) / AI 检测（外部）

The system shall forward submitted images to the external AI analysis engine, receive structured
findings, and associate each finding with a detected skin concern. Findings carry a confidence
value and remain **pending review**.

系统应将提交的照片转发至外部 AI 检测引擎，接收结构化结论，并将每条结论关联到一处识别出的皮肤问题。
结论带有置信度，且在复核前保持**待审**状态。

> **The boundary is the point.** The engine is not your code. It returns findings you did not
> compute. Design this as an explicit boundary from the first diagram — a wrong Analysis model here
> cannot be fixed in M3.

---

### FR-4 · Analysis record and lifecycle / 分析记录与生命周期

The system shall maintain an `Analysis` with its own lifecycle: `uploaded → analysing → reviewed
→ delivered`, plus a rejection path for results that fail validation.

系统应维护一条具有自身生命周期的 `Analysis`：`uploaded → analysing → reviewed → delivered`，
并为未通过校验的结果提供一条拒绝路径。

> Draw this as a **state machine**, not as a table. W09 is about exactly this.

---

### FR-5 · Practitioner review / 执业人员复核

The system shall let a practitioner review the AI findings, amend them, record the review decision,
and thereby authorise or withhold disclosure to the client.

系统应允许执业人员复核 AI 结论、修订结论、记录复核决定，并据此授权或扣留向客户公开。

> **This is your §5 question, now a requirement.** Whether the client may see an unreviewed
> finding is a real fork. You may resolve it either way — but state the decision, and make it
> visible in FR-4's state machine. If the client can see `analysing` output, that is a visible
> state; if not, the transition goes `analysing → reviewed` without a disclosure event.

---

### FR-6 · Treatment plan generation / 护理方案生成

The system shall derive a `TreatmentPlan` from reviewed findings, stating goals, ordered steps, a
review interval, and the reasoning from each finding to each goal.

系统应依据已复核的结论推导 `TreatmentPlan`，包含目标、有序步骤、复查间隔，
以及从每条结论到每个目标的推导理由。

> The "reasoning from finding to goal" part is not decoration. It is **traceability**, and it is
> what makes the plan defensible at M1 client review.

---

### FR-7 · Product recommendation and screening / 产品推荐与筛查

The system shall recommend `Product`s from the external catalogue for each regimen step, and
**exclude** any product that conflicts with a recorded `Contraindication`. Recommendations must
carry the reason for inclusion.

系统应从外部产品目录为每一步护理推荐 `Product`，并**排除**任何与已记录 `Contraindication`
冲突的产品。推荐必须给出推荐理由。

> `Contraindication ·blocks· Product` is a **rule**, not an association. If your domain model draws
> it as a plain line between two classes, you have lost the single best relationship in this system.
> Keep the verb.

---

### FR-8 · Regimen construction / 护肤流程编排

The system shall arrange the approved products into a daily `Regimen`, sequencing them
(morning / evening / weekly), and let the practitioner amend the sequence.

系统应将获批产品编排为每日 `Regimen`，安排使用顺序（晨间/晚间/每周），并允许执业人员调整顺序。

---

### FR-9 · Follow-up and re-analysis / 复查与复检

The system shall schedule a follow-up at the plan's review interval, and on completion start a
**new** Analysis rather than overwriting the previous one.

系统应按方案的复查间隔安排复查，并在复查时**新建**一次分析，而不是覆盖原记录。

> `FollowUp ·triggers· Analysis` — note the multiplicity. One analysis per follow-up, and an
> analysis may have many findings. Getting these wrong here means re-drawing the whole model in M2.

---

### FR-10 · Guidance and compliance moderation / 建议内容与合规审核

The system shall pass any published guidance text and product claim through compliance moderation
before it becomes visible to a client.

系统应将任何对外发布的建议内容与产品功效宣称送交合规审核，通过后方可对客户可见。

---

### FR-11 · Client history and comparison / 客户历史与对比

The system shall retain all of a client's analyses and allow comparison between them over time
(e.g. a concern's severity at three review dates).

系统应保留客户的全部分析记录，并支持跨时间对比（如某问题在三个复查时点的严重程度）。

---

### FR-12 · Purchase handoff / 购买衔接

The system shall hand a recommendation set to the external catalogue for purchase and confirm
payment via the external payment provider.

系统应将推荐清单交由外部目录完成购买，并通过外部支付服务确认支付。

---

## 4. What This Package Deliberately Does Not Give You

> **These are yours to find. A requirements list you did not have to think about is not a
> requirements list.**

| Not specified | Why it is yours |
|---|---|
| Whether the client sees unreviewed findings | Your §5 question. Model the choice you make. |
| What happens on a **low-confidence** finding | Threshold? Send to review? Reject the image? |
| Who may correct a **client's self-declared** concern | Trust boundary between client input and practitioner input |
| Whether recommendations differ by **client segment** | This is where your Strategy candidates live (M3/M4) |
| **Retention and deletion** of client photographs | A real obligation with a real model consequence |
| What the client sees on a **rejected** analysis | Silence? A retake prompt? Who tells them, and how? |

> 表里的每一项在答辩时都可能被问到，而它们**不在**教师给的这份文件里。
> 谁先想清楚，谁在评审里说话就更有分量。

---

## 5. Deliverables That Come Next

| Milestone | Due | What you build on top of this |
|---|---|---|
| **M1** | **Sun Nov 01** | Requirements list (extend FR-1…FR-12), use case diagram, **2 detailed use case specifications** |
| **M2** | Sun Nov 22 | Domain model, 2+ sequence diagrams, an Analysis state machine, an activity diagram |

**Suggested pair for the two detailed use case specifications** (choose from these, or justify
another choice):

1. **Submit photo for analysis** — strong extensions: poor lighting, wrong angle, unsupported file,
   AI engine timeout, low-confidence result.
2. **Practitioner reviews findings and authorises disclosure** — strong extensions: contradicts the
   AI finding, withholds disclosure, client disputes the finding.

Between them these two exercise **every actor in §2 except Compliance**, and they are the two flows
where this system's real risk lives.

---

## 6. How to Use This Document / 使用方式

1. **Read it once, then model from your own head.** If you need this file open while drawing,
   the model is not yet yours.
2. **Extend, do not copy.** M1 is marked on a requirements list you produced.
3. **Disagree in writing.** Every requirement above is a claim about the domain. Some are arguable.
   Bring your objection to the M1 review.
4. **Language**: the models are submitted in English. Chinese notes are fine for your own working.

---

*Core functional requirements · v1.0 · issued 2026-10-15 (W06) · AI Skin Analysis ·
Instructor-provided starting point for M1 · Information Systems Analysis and Design · Fall 2026*