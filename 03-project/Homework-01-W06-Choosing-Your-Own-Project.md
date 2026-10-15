# Homework — Choosing Your Own Project (after class)

# 课后任务 · 选题：把题目定下来

> **ISAD · Fall 2026** · 4 人一个小组 · **Week 06 (Oct 12 – Oct 18)**
> **Milestone**: none — this is a preparation task. **No tag.**
> **Due**: **before Week 07 (Oct 12)**, i.e. pushed to your repository before the next class.
> **In-class part already done**: §0–§3 of `../labs/Lab-07-W06-Choosing-Your-Own-Project.md`
> (read the three criteria, demo, and the **silent** individual brainstorm). You already have your
> two candidates written down. This sheet starts from there.

---

## What you already have

**Before you leave today, the repository already exists.** You created it in class
(`labs/Lab-07` §0): `campusbites-team-01`, instructor invited, all four of you cloned and set
`git config user.name` / `user.email`. So Step 4 below is a real push, not a setup exercise —
if `git push` fails, that is a problem to report, not a step to discover.

In class, **each of the four of you wrote two candidates in silence**, before anyone spoke.
Those eight candidates are the raw material. Nothing else changed.

> ⚠️ **Do not re-open the brainstorm now.** Adding new ideas at home is fine — but the four
> candidates you wrote in silence are your own evidence of individual contribution. Keep them
> word for word, and if you add anything later, mark it clearly as added later.

---

## Step 1 · Merge into one candidate list (~20 min)

**Recorder** opens `docs/topics/candidate-list.md` (template: [`../topics-templates/Template-01-Candidate-List.md`](../topics-templates/Template-01-Candidate-List.md)).

- One block per candidate — **keep the proposer's name on each one**.
- **Do not delete the rejected ones.** Your instructor wants to see what you considered.
- Cross out anything that fails a **hard** check immediately (no one-line pitch, or fewer than 8 nouns).
  Write `✗ failed S1` next to it rather than removing it.

```bash
mkdir -p docs/topics
```

---

## Step 2 · Score against the three hard criteria (~30 min)

**Lead** keeps time. Fill in [`../topics-templates/Template-02-Scorecard.md`](../topics-templates/Template-02-Scorecard.md).

| | Criterion | Pass mark |
|---|---|---|
| **S1** | Actors | **≥ 5**, counting anyone who asks the system for something — **including outside systems** |
| **S2** | Classes & relationships | **≥ 8 conceptual classes** *and* **≥ 6 relationships that are not "has"** |
| **S3** | Lifecycles | **≥ 2 objects** that have a state machine, 3–4 states each |

### The rule that decides most cases

**"Lots of actors" is not an answer.** Write the list and say how you counted:

> ✅ `Resident, Dispatcher, Staff, Contractor, Admin, Notification service (outside), Billing system (outside) — seven, counted by "who asks the system for something".`

**If you cannot agree**, do not settle it by seniority. Write **two** candidates into the scorecard,
both scored, and write one sentence saying which criterion actually separated them.
"We are stuck and here is why" is a passable answer; a silent vote is not.

---

## Step 3 · Write the proposal (~40 min)

Fill in [`../topics-templates/Template-03-Topic-Proposal.md`](../topics-templates/Template-03-Topic-Proposal.md) **together, out loud** — do not split sections and write in silence.

### Section 3 is the part that is marked

For each of S1 / S2 / S3: the evidence **and the counting method**. Section 5 is the next most important:

> **§5 Three pattern questions you have not resolved yet.**
> Write honestly. *"I do not know whether a cancelled work order goes back to `draft` or straight to
> `closed`"* is worth more than a confident wrong answer — W14–W15 is where you resolve exactly
> this, and at the defence the most useful thing you can say is "we know where we are unsure."

---

## Step 4 · Submit (~10 min)

```bash
git add docs/topics/
git commit -m "Add topic selection: candidate list, scorecard, proposal"
git push origin main
```

**No tag this week.** Do not run `git tag`. M0 and tag `m0` are next week's business, after your
topic has been approved.

### Done when

- [ ] `docs/topics/candidate-list.md` — all candidates, proposers named, rejected ones kept
- [ ] `docs/topics/scorecard.md` — every criterion scored, with the counting method written out
- [ ] `docs/topics/Topic-Proposal.md` — §3 evidence complete, §5 honest
- [ ] `git push` done, **and you did not push a tag**

---

## Homework before Week 07

1. **Re-read your own two candidates.** You wrote them under time pressure in class.
   Now that you have seen the accepted example, would you still pick the same two?
   If not, tell the team — changing your mind with a reason is good judgement, not weakness.
2. **Skim Larman chapters 1–2** (Introduction / Object-Oriented Analysis). The vocabulary starts there.
3. **Come with one sentence** you want to say to your instructor when the topic is approved.

---

## Reference

| Document | What it answers |
|---|---|
| [`../Topic-Selection-Task-选题任务包.md`](../Topic-Selection-Task-选题任务包.md) | §1 the three criteria and the three kinds of bad topic |
| [`../labs/Lab-07-W06-Choosing-Your-Own-Project.md`](../labs/Lab-07-W06-Choosing-Your-Own-Project.md) | §2 the accepted / rejected example pair, §8 the in-class part you already did |
| [`../topics-templates/README-模板索引-Template-Index.md`](../topics-templates/README-模板索引-Template-Index.md) | All three blank templates |
| [`../项目案例变更说明-CampusBites改为自主命题.md`](../项目案例变更说明-CampusBites改为自主命题.md) | What changed and what did not |

---

*Homework · W06 · Information Systems Analysis and Design · Fall 2026*
