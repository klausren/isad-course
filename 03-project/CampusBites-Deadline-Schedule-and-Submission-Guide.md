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

| Milestone | What is due (checklist in Guidebook §5) | **Hard deadline** | Reviewed at |
|---|---|---|---|
| **M0 Kickoff** | Team charter (Appendix A), stakeholder list, project vision, **Git repo created & instructor invited** | **Fri Sep 11** (W2) | W2 lab — pass/fail |
| — Requirements pack issued | Instructor publishes the standard CampusBites requirements | in class, **W4 (Sep 21–25)** | — |
| **M1 Requirements** | Requirements list, use-case diagram, 2 detailed use-case specifications | **Sun Oct 4** (W5) | Cross-team client review — first class session on/after Oct 4 (see §5 note) |
| **ΔC1 Change injection #1** | New requirement lands in your repo's `changes/` folder; your response is folded into M2 | announced **W6 (Oct 5–11)**, online | — |
| **M2 Analysis models** | Domain model, 2+ sequence diagrams, Order state machine, activity diagram | **Sun Oct 25** (W8) | **W9 mid-term review (Oct 26–30)** — formative, every member questioned |
| **ΔC2 Change injection #2** | Second requirement change; response folded into M3 | announced **W10 (Nov 2–6)** | — |
| **M3 Design models** | Design class diagram, GRASP/SOLID application notes, DCD-level interaction diagrams | **Sun Nov 22** (W12) | In-class design walkthroughs, W10–W13 |
| **ΔC3 Change injection #3** | Third requirement change; response folded into M4 | announced **W13 (Nov 23–27)** | — |
| **M4 Patterns** | Pattern catalog (5+ GoF patterns, Appendix C), refactoring narrative, updated DCD | **Sun Dec 6** (W14) | Pattern catalog walkthrough, W15 (Dec 7–11) |
| **M5 Defense** | Final defense — you present, you answer questions | **in class, W16 (Dec 14–18)** | Final defense, ~30 min per team |
| **M5 Final package** | Final report (Appendix D), individual contribution logs (Appendix E), all diagram sources, tag `m5` | **Sun Dec 20, 23:59** | Graded |

**Why the week numbers and dates pair up this way:**
- Every hard deadline sits at the **end** of the working week, and the review happens at the **start** of the next week's class — you get the weekend to finish, the instructor gets a fresh submission to review.
- Change injections (ΔC1–ΔC3) are always announced **right after** a milestone review — when you feel safest — and their response is always folded into the **next** milestone. You never submit a "response to ΔC" as a separate deliverable.
- M0 is a **Friday** deadline: it is pass/fail, and the instructor needs the weekend to verify both repos and access.

---

## 3. Weekly Rhythm at a Glance

```
Week  Date range      Project focus
W01   Aug 31–Sep 06   Course kickoff; read Guidebook; form teams
W02   Sep 07–Sep 13   M0: charter + repo created            → M0 due FRI SEP 11
W03   Sep 14–Sep 20   OO foundations — no deliverable (breathing room)
W04   Sep 21–Sep 27   Requirements pack issued in class
W05   Sep 28–Oct 04   Requirements & use cases              → M1 due SUN OCT 04
W06   Oct 05–Oct 11   (National Day week) ΔC1 announced online
W07   Oct 12–Oct 18   M1 cross-team client review (first class back)
W08   Oct 19–Oct 25   Analysis modeling                     → M2 due SUN OCT 25
W09   Oct 26–Nov 01   MID-TERM REVIEW (M1+M2, formative)
W10   Nov 02–Nov 08   Design begins; ΔC2 announced
W11   Nov 09–Nov 15   DCD & GRASP/SOLID in-class reviews
W12   Nov 16–Nov 22   Design models finalize                → M3 due SUN NOV 22
W13   Nov 23–Nov 29   Patterns begin; ΔC3 announced
W14   Nov 30–Dec 06   Pattern catalog & refactoring         → M4 due SUN DEC 06
W15   Dec 07–Dec 13   Pattern walkthroughs; defense rehearsal
W16   Dec 14–Dec 20   FINAL DEFENSE in class                → M5 package due SUN DEC 20
```

---

## 4. Submission Address & Protocol — Exactly How to Submit

### 4.1 Where your work lives

**One Git repository per team** (this is the only submission address):

```
https://github.com/<your-team-account>/campusbites-team-a     (Team A)
https://github.com/<your-team-account>/campusbites-team-b     (Team B)
```

- Created under **any one member's GitHub account** in Week 2.
- The instructor's GitHub account **`klausren`** is invited as a collaborator (**read** access is enough) — do this in W2, it is part of M0.
- Repository layout: exactly as Guidebook §6.

### 4.2 One-time registration (part of M0, by Fri Sep 11)

One member sends a **single email** to the instructor (address announced in W1 class):

```
Subject: [ISAD] Repo registration — Team A

Team name:    Team A
Members:      Full Name 1 (leader), Full Name 2, Full Name 3
Repo URL:     https://github.com/xxx/campusbites-team-a
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
| M0        | 2026-09-11 | m0  | 2026-09-10 21:40    | ✅ pass     |
| M1        | 2026-10-04 | m1  | 2026-10-04 22:15    | ✅          |
| M2        | 2026-10-25 | m2  |                     | 🚧 in progress |
```

This table is the first thing the instructor reads. Keep it true.

### 4.5 Fallback channel (GitHub unreachable)

If GitHub is unreachable from your network at deadline time:

1. Create a zip of the **entire repository folder** (including `.git/`): `campusbites-team-a-m1.zip`
2. Email it to the instructor **before the deadline** with subject `[ISAD] M1 fallback — Team A`.
3. Push to GitHub as soon as access returns; the emailed zip's timestamp is your proof of timeliness.

The fallback covers **submission** only — you are still expected to restore the repo state (tags included) within 3 days.

---

## 5. Schedule Notes & Caveats

- **National Day week (Oct 1–8)** sits inside W5–W6. Hard deadlines are online and **do not move**; only the *in-class* cross-team client review (planned W5) moves to the **first class session of W7 (Oct 12 or 13)**. If the university's calendar gives you class sessions on Sep 28–29, the review may happen there instead — the instructor will confirm in class.
- If the university calendar shifts any teaching week (make-up classes, weather, etc.), **hard deadlines stay where they are** unless the instructor explicitly announces a change in class and in the course repo. Silence = no change.
- All change injections (ΔC) are announced **in the course repository and by email** — check both after every milestone week.
- **Answer to the question you are about to ask**: yes, the Sunday 23:59 deadline means the *last useful moment* is around 22:00, when you still have time to fix a failed push. Plan accordingly.

---

*Version 1.0 · issued Week 1 · changes to this schedule are announced in class and committed to the course repository.*
