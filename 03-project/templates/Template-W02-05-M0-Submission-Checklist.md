# M0 Submission Checklist — CampusBites Team __

<!-- Due **Fri Sep 11** · pass / fail · Run this checklist out loud, in order, before you leave the lab -->

> **M0 is small on purpose.** It exists to test your pipeline — repository, commits, tags, English, file formats — before anything is graded. A failed M0 blocks nothing yet. It is your rehearsal.

---

## 1. The four deliverables

| # | Deliverable | File it lives in | Template | Ready? |
|---|---|---|---|---|
| ① | Team charter | `TEAM-CHARTER.md` | `Template-W02-01` | ☐ |
| ② | Stakeholder list (5–8, ≥2 non-users) | `01-requirements/stakeholder-list.md` | `Template-W02-02` | ☐ |
| ③ | Project vision (≤150 words) | `01-requirements/vision.md` (and pasted into charter §8) | `Template-W02-03` | ☐ |
| ④ | Repository created, shared, README filled | `README.md` | `Template-W02-04` | ☐ |

## 2. Content gate — every box before you commit

- [ ] **English only.** A non-English deliverable is returned once for translation (−20% on that item); a second time it is not accepted.
- [ ] No template instruction block or `> Hint:` line survived in any file.
- [ ] Every charter rule is **testable** (who / when / a number).
- [ ] Vision paragraph ≤150 words, no unprovable adjectives, and identical in both files.
- [ ] Stakeholder rows: 5–8, ≥2 marked ✖, every row has a "why" and a source.
- [ ] README milestone table filled, team table filled, repo URL correct.

## 3. Repository gate

- [ ] Repository name: `campusbites-team-01`
- [ ] All three members have write access and have each pushed **at least one commit**
- [ ] Instructor `klausren` invited — access confirmed, not "invitation sent"
- [ ] One-time registration email sent (template in `CampusBites-Deadline-Schedule-and-Submission-Guide.md` §4)
- [ ] Commit history is small and meaningful — not one giant "final commit"

## 4. The submission itself — a tag, not a branch

```bash
# 1. everything committed
git status                      # must print "nothing to commit, working tree clean"

# 2. push the work
git push origin main

# 3. create and PUSH the tag
git tag -a m0 -m "M0 submission"
git push origin m0
```

**Verify — do not skip this:**

```bash
git tag -l                      # m0 exists locally
git ls-remote --tags origin     # m0 exists on GitHub  <-- the graded snapshot
```

> **The one rule that trips people:** a submission exists only when the **tag is pushed**. An unpushed tag is invisible to the instructor and counts as nothing.

## 5. If GitHub is unreachable

Follow the fallback in `CampusBites-Deadline-Schedule-and-Submission-Guide.md` §4 (bundle + timestamped handover). "GitHub was slow" is not an excuse; "I pushed on Tuesday and it failed on Friday with no evidence" is.

## 6. After you submit

- [ ] Update the README milestone table: M0 → `submitted (tag m0)`
- [ ] Screenshot or copy the `git ls-remote --tags origin` output into your team chat
- [ ] Read the Week 3 lab sheet before Tuesday

## 7. Late policy

−10% per calendar day on that milestone, max 3 days, then 0 for the milestone. OneDrive sync failure is not an excuse — push early, push often.

---

## Common failures (seen every year)

| Failure | Why it happens | Fix |
|---|---|---|
| Tag not pushed | `git tag` run but `git push origin m0` forgotten | Always run `git ls-remote --tags origin` |
| Wrong tag name | `M0`, `m0.0`, `v0` | Exactly `m0` … `m5`, lowercase |
| Empty deliverable | Template copied, blanks not filled | Fill every blank; delete every hint |
| Two visions disagree | Charter and vision file edited separately | One source of truth: `01-requirements/vision.md` |
| Instructor has no access | Invitation sent, never accepted | Confirm the collaborator appears in repository settings |
