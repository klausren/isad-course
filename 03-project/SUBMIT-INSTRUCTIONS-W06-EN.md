# Submitting Your Work — W06 (Thu Oct 29)

> **Information Systems Analysis and Design** · Fall 2026 · Team of four
> **Your repository**: <https://github.com/Kasper282/WorkspaceProject>
> **Read this whole page before you push anything.** Five commands. No surprises.

---

## 0. The one rule

> **A milestone is submitted when its tag is pushed.**
> A `git push` without the tag is **not** a submission.

So "I pushed my work" is only half of it. For **M0 today** you need:

1. your files committed and pushed, **and**
2. the tag `m0` pushed, **and**
3. you can see `refs/tags/m0` in the output of a verification command.

That last part matters: **read the output.** A command that fails quietly looks exactly like one
that worked.

---

## 1. First, one thing each of you does (once, not today)

Git records **your name** on every commit you make. If two of you share an identity, the
individual contribution mark at the defence cannot be reconstructed. Do this now:

```bash
git config user.name  "Your Full Name"      # exactly as in the roster
git config user.email "your@university.edu"
```

> ⚠️ **Four different names, four different emails.** If you all commit as one person, the
> teamwork evidence is gone and it cannot be repaired after the fact.

Check it:

```bash
git config user.name && git config user.email
```

---

## 2. Get the folder structure in place

Your repository currently holds only the initial `README.md`. The folder skeleton — and the
instruction files that go with it — is **not** in the remote yet. One person (the Release Manager)
does this once.

If you still have the **`ISAD-Repo-Init-Pack.zip`** from class:

```bash
# 1. unzip it somewhere
# 2. put init-team-repo.sh and isad-seed/ in the same folder
# 3. open the script and replace the two placeholder lines:
#      YOUR_NAME="..."      <- your real name
#      YOUR_EMAIL="..."     <- your real email
# 4. run it from that folder:
bash init-team-repo.sh
```

The script clones the repository, sets your identity, preserves the existing README, copies the
folder structure in, and pushes. **It does not create a tag** — tags are a separate, deliberate
step (section 4).

> ❗ **If you do not have the zip any more, ask in class.** Do not build the structure by hand —
> the instruction files inside it are part of what you are graded on.

---

## 3. Put today's four things in the right place

The folder structure has **two layers**, and mixing them is the most common mistake:

| Layer | What it is | Rule |
|---|---|---|
| `docs/` | **working copies** — where you think | write here |
| `01-requirements/`, `02-analysis/`, … | **what you submit** — what gets graded | the M0 snapshot goes here |

**Today you produce exactly these four files:**

| # | File | Where it goes |
|---|---|---|
| ① | Team charter | `TEAM-CHARTER.md` (repository root) |
| ② | Stakeholder list | `01-requirements/stakeholder-list.md` |
| ③ | Project vision | `01-requirements/vision.md` (and paste the same text into charter §8) |
| ④ | Noun scan + domain model | `docs/analysis/noun-scan.md` · `docs/diagrams/domain-model-v1.puml` **+ its PNG** |

> 📌 **The vision must be word-for-word identical in both files.** If the charter and the vision
> file disagree, M0 is returned to you. Keep one source of truth and paste it.

---

## 4. Commit and push

```bash
git add TEAM-CHARTER.md 01-requirements/ docs/analysis/ docs/diagrams/
git status                    # READ THIS — the file list must be exactly what you expect
git commit -m "M0: charter, stakeholder list, vision; domain model v1"
git push origin main
```

> ⚠️ **`git status` before you commit.** If a photograph of a real person is in that list, stop —
> **it is irreversible once pushed**, even if you delete it afterwards.
> Never commit real photographs. No clinical claims, either: everything your model "recommends"
> is a screening suggestion, never a diagnosis.

---

## 5. Tag it — this is the part that makes it a submission

```bash
git tag -a m0 -m "M0 submission — charter, stakeholders, vision"
git push origin m0
```

## 6. Verify — and actually read the output

```bash
git ls-remote --tags origin
```

You must see a line that contains:

```
<hash>	refs/tags/m0
```

**No line = not submitted.** Not "probably submitted", not "I think it worked". If the line is
missing, the tag did not reach the server. Fix it before you leave the room.

A second check, if you want to be sure the content is right too:

```bash
git ls-remote origin refs/heads/main
```

---

## 7. Update the milestone table in `README.md`

Open `README.md` at the repository root. Find the **Milestone status** table and fill in the
**M0** row:

```markdown
| M0 Kickoff | **Sun Oct 25** | `m0` | 2026-10-29 16:40 | ✅ submitted |
```

Then commit and push that too:

```bash
git add README.md
git commit -m "M0: record submission time in the milestone table"
git push origin main
```

> The tag froze the graded snapshot. Committing the README afterwards is fine and expected — the
> tag stays where it is.

---

## 8. One member's job, four people's evidence

Only the **Release Manager** runs the tag commands in sections 5 and 6. That is not a privilege —
it is a **record of responsibility**: one person is accountable for the submission being real.

But **all four of you must appear in the commit history.** Before you leave:

```bash
git log --oneline --format="%an <%ae>"
```

You should see **four distinct names**. If you see fewer, someone has not committed yet. Have
each of them commit something small and meaningful today.

> One giant "final commit" from one person is a red flag. Commit history is teamwork evidence —
> it is marked at M5.

---

## Stuck?

| Symptom | Fix |
|---|---|
| Push asks for a password | GitHub no longer accepts account passwords. Use a **Personal Access Token** (Settings → Developer settings → Tokens (classic) → scope `repo`), or switch to SSH. |
| `git push` says `rejected` / `fetch first` | Someone pushed before you. `git pull --rebase origin main`, then push again. |
| `git ls-remote --tags origin` answers with nothing | Normal — there are no tags yet. It becomes a problem only after section 5. |
| `fatal: not a git repository` | You are in the wrong folder. `cd` into the cloned repository first. |
| GitHub unreachable from your network | Zip the **entire repository folder including `.git/`**, email it before the deadline with subject `[ISAD] M0 fallback — Team 01`, and push when the network returns. The emailed zip's timestamp is your proof of timeliness. |
| You are about to commit a photograph | **Stop.** `git status`, remove it, commit again. |

---

## The four commands, one more time

```bash
git add TEAM-CHARTER.md 01-requirements/ docs/analysis/ docs/diagrams/
git commit -m "M0: charter, stakeholder list, vision; domain model v1"
git push origin main
git tag -a m0 -m "M0 submission" && git push origin m0
git ls-remote --tags origin        # must show refs/tags/m0
```

---

*W06 · Information Systems Analysis and Design · Fall 2026*
