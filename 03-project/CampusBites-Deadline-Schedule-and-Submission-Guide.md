# CampusBites — Deadline Schedule & Submission Guide (Fall 2026)

> **Course**: Information Systems Analysis and Design · 16 weeks · Aug 31 – Dec 20, 2026
> **Companion to**: *CampusBites Project Guidebook* (§5 Milestones, §6 Submission Rules)
> All times are **23:59 (GMT+8)** on the day stated. The server clock that matters is the one on your **last `git push`** — not your laptop.

---

## 1. The Golden Rules of Deadlines

1. **Sunday 23:59 is the normal deadline slot.** Everything except M0 and the final package is due end-of-week, so it gets reviewed at the next class. Don't treat Sunday as "start working" — treat it as "already pushed".
2. **A tag is a submission.** A deadline is only met when a tag exists on the remote repository (see §4). Un-pushed work does not exist.
3. **Push early, push often.** Internet problems, GitHub timeouts and OneDrive sync failures are **not** accepted as excuses — they are exactly why the deadline is not "5 minutes before 23:59".
4. **Late policy** (from the Guidebook): −10% per calendar day on that milestone, maximum 3 days, then 0 for the milestone.

---

## 2. Semester Deadline Calendar

> ⚠️ **Revised 2026-10-08 (second revision), then 2026-10-15 (third revision).** Three changes:
> 1. The **National Day holiday (Oct 1–8)** pushed W05's delivery to **Thu Oct 08**, so the whole
>    schedule shifts **one week later**.
> 2. The project begins with **topic selection** (the team chooses its own domain instead of
>    using the fixed CampusBites case).
> 3. **Repository setup moved from M0 to W06.** The topic-selection homework ends with
>    `git push origin main`, so `origin` had to exist on **Oct 15** rather than at M0. M0 now
>    checks charter + stakeholders + vision + tag only.
>
> Milestone *content* and *marks* are unchanged — **only the dates and this one task split**.
> If you are reading an older printout, use this table. W05's own lab sheet carries a rescheduling
> notice, and `labs/Lab-07` §0 is the repository procedure.


| Milestone | What is due (checklist in Guidebook §5) | **Hard deadline** | Reviewed at |
|---|---|---|---|
| — **Topic selection** | Candidate list, three-criteria scorecard, topic proposal (see `topics-templates/`) | **W6 (Oct 12–18)**, in class + homework | **Instructor pass / revise** — no tag, not a milestone |
| **Repository setup** *(pulled forward from M0, Oct 15)* | Repository created, `klausren` invited, all four members cloned and `git config`'d | **W6 (Oct 15), in class** | done — see `labs/Lab-07` §0 |
| **M0 Kickoff** | Team charter (Appendix A), stakeholder list, project vision, **tag `m0`** — *repository already done in W06* | **Sun Oct 25** (W8) | W8 lab — pass/fail |
| **M1 Requirements** | Requirements list, use-case diagram, 2 detailed use-case specifications | **Sun Nov 1** (W9) | **M1 client review, W9 (Nov 2–8)** — instructor as client, formative |
| **M2 Analysis models** | Domain model, 2+ sequence diagrams, Order state machine, activity diagram | **Sun Nov 22** (W12) | **W12 mid-term review (Nov 23–29)** — formative, every member questioned |
| **ΔC2 Change injection #1** *(renumbered — there is no ΔC1)* | First requirement change; response folded into M3 | announced **W10 (Nov 9–15)**, online | — |
| **M3 Design models** | Design class diagram, GRASP/SOLID application notes, DCD-level interaction diagrams | **Sun Dec 6** (W14) | In-class design walkthroughs, W14–W15 |
| **ΔC3 Change injection #2** | Second requirement change; response folded into M4 | announced **W13 (Nov 30–Dec 6)** | — |
| **M4 Patterns** | Pattern catalog (5+ GoF patterns, Appendix C), refactoring narrative, updated DCD | **Sun Dec 20** (W15) | Pattern catalog walkthrough, W16 (Dec 14–20) |
| **M5 Defense** | Final defense — you present, you answer questions | **in class, W16 (Dec 14–20)** | Final defense, ~35 min (one team of four) |
| **M5 Final package** | Final report (Appendix D), individual contribution logs (Appendix E), all diagram sources, tag `m5` | **Sun Dec 20, 23:59** | Graded |

**Why the week numbers and dates pair up this way:**
- Every hard deadline sits at the **end** of the working week, and the review happens at the **start** of the next week's class — you get the weekend to finish, the instructor gets a fresh submission to review.
- Change injections (**ΔC2 and ΔC3** — ΔC1 was cancelled on 2026-10-15) are always announced **right after** a milestone review — when you feel safest — and their response is always folded into the **next** milestone. You never submit a "response to ΔC" as a separate deliverable.
- M0 is a **Friday** deadline: it is pass/fail, and the instructor needs the weekend to verify both repos and access.

---

## 3. Weekly Rhythm at a Glance

```
Week  Date range      Project focus
W01   Aug 31–Sep 06   Course kickoff; read Guidebook
W02   Sep 07–Sep 13   OO foundations; toolchain setup
W03   Sep 14–Sep 20   UML essentials — no deliverable (breathing room)
W04   Sep 21–Sep 27   Requirements & use case modeling
W05   Oct 08          Use case specification  ← DELIVERED THU OCT 08 (National Day holiday)
W06   Oct 12–Oct 18   Domain modeling as a method + TOPIC SELECTION starts (no tag)
W07   Oct 19–Oct 25   Topic selection due + M0: charter + vision + repo → M0 due SUN OCT 25
W08   Oct 26–Nov 01   Requirements & use cases                → M1 due SUN NOV 01
W09   Nov 02–Nov 08   M1 CLIENT REVIEW — instructor as client (30 min, formative)
W10   Nov 09–Nov 15   Analysis modeling; **ΔC2** announced online (there is no ΔC1)
W11   Nov 16–Nov 22   Analysis models finalize              → M2 due SUN NOV 22
W12   Nov 23–Nov 29   MID-TERM REVIEW (M1+M2, formative, not graded)
W13   Nov 30–Dec 06   Design modeling                      → M3 due SUN DEC 06
W14   Dec 07–Dec 13   Pattern catalog; **ΔC3** announced
W15   Dec 14–Dec 20   Pattern walkthroughs; defense rehearsal → M4 due SUN DEC 20
W16   Dec 21–Dec 27   FINAL DEFENSE in class                → M5 package due SUN DEC 27
```

> ⚠️ **This timeline was revised twice on 2026-10-08.**
> 1. **The National Day holiday (Oct 1–8)** pushed W05's delivery to **Thu Oct 08**,
>    so every week from here on is **one week later** than the original calendar.
> 2. The team had not started, and now **selects its own topic** instead of using the
>    fixed CampusBites case, so the project begins with **topic selection** and the
>    milestones follow it.
>
> See `项目案例变更说明-CampusBites改为自主命题.md` §4 and `labs/Lab-05-W05-Use-Case-Specification-and-Peer-Review.md`
> for the rescheduling notice the students read.
>
> **What did not change**: the submission protocol in §4 below (push + tag `m0`…`m5`),
> the diagram directory `docs/diagrams/`, and the PlantUML + draw.io dual-source rule.

---

## 4. Submission Address & Protocol — Exactly How to Submit

### 4.1 Where your work lives

**One Git repository per team** (this is the only submission address):

```
https://github.com/<your-team-account>/campusbites-team-01
```

- Created under **any one member's GitHub account** in Week 2.
- The instructor's GitHub account **`klausren`** is invited as a collaborator (**read** access is enough) — do this in W2, it is part of M0.
- Repository layout: exactly as Guidebook §6.

### 4.2 One-time registration — done in Week 06, Oct 15

One member sends a **single email** to the instructor (address announced in W1 class):

```
Subject: [ISAD] Repo registration — Team 01

Team name:    Team 01
Members:      Full Name 1 (leader), Full Name 2, Full Name 3
Repo URL:     https://github.com/xxx/campusbites-team-01
Access:       klausren invited as collaborator (done / pending)
```

> If you cannot reach GitHub from your network in W2, register by email anyway with a *local* note, and use the fallback in §4.5 until access is sorted.

### 4.3 Per-milestone submission (every deadline)

A milestone is submitted when **all three** are done:

```bash
# 1. your work is committed and pushed
git add ... && git commit -m "M2: domain model v2" && git push

# 2. create the milestone tag (this freezes the graded snapshot)
git tag -a m2 -m "M2 submission — analysis models"
git push origin m2

# 3. update the milestone status table in README.md, commit & push
```

| Milestone | Tag name |
|---|---|
| M0 … M5 | `m0`, `m1`, `m2`, `m3`, `m4`, `m5` |

The **tag**, not your branch head, is what gets graded. Anything pushed after the tag but before the deadline can be re-tagged with `-f`; nothing after the deadline counts.

### 4.4 README.md milestone status table (kept in your repo)

```markdown
| Milestone | Due        | Tag | Submitted at        | Status      |
|-----------|------------|-----|---------------------|-------------|
| M0        | 2026-10-25 | m0  |                     | ⏳ ahead    |
| M1        | 2026-11-01 | m1  |                     | ⏳ ahead    |
| M2        | 2026-11-22 | m2  |                     | 🚧 in progress |
```

This table is the first thing the instructor reads. Keep it true.

### 4.5 Fallback channel (GitHub unreachable)

If GitHub is unreachable from your network at deadline time:

1. Create a zip of the **entire repository folder** (including `.git/`): `campusbites-team-01-m1.zip`
2. Email it to the instructor **before the deadline** with subject `[ISAD] M1 fallback — Team 01`.
3. Push to GitHub as soon as access returns; the emailed zip's timestamp is your proof of timeliness.

The fallback covers **submission** only — you are still expected to restore the repo state (tags included) within 3 days.

---

## 5. Schedule Notes & Caveats

- **National Day week (Oct 1–8)** sits inside W5–W6. Hard deadlines are online and **do not move**; only the *in-class* client review (planned W5) moves to the **first class session of W7 (Oct 12 or 13)**. If the university's calendar gives you class sessions on Sep 28–29, the review may happen there instead — the instructor will confirm in class.
- If the university calendar shifts any teaching week (make-up classes, weather, etc.), **hard deadlines stay where they are** unless the instructor explicitly announces a change in class and in the course repo. Silence = no change.
- Change injections (**ΔC2, ΔC3** — ΔC1 was cancelled) are announced **in the course repository and by email** — check both after every milestone week.
- **Answer to the question you are about to ask**: yes, the Sunday 23:59 deadline means the *last useful moment* is around 22:00, when you still have time to fix a failed push. Plan accordingly.

---

*Version 1.0 · issued Week 1 · changes to this schedule are announced in class and committed to the course repository.*
