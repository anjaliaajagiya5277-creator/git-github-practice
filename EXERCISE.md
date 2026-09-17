# Exercise: Branching, PRs, and Conflict Resolution

This repo arrives with the work already done at the git level — four commits, three feature branches, one of which will genuinely conflict when you merge it. Your job is to push it to GitHub and drive the rest of the workflow yourself.

Check the shape before you start:

```bash
git log --oneline --graph --all
git branch -a
```

You should see `main` two commits ahead of `edfb816` (the Python-notes PR and the Anjali-owner PR, already merged), plus one branch — `feature/git-basics-owner-team` — still unmerged and waiting.

## Step 1 — Push to GitHub

Create an empty repo on GitHub (no README, no .gitignore — this repo already has both), then:

```bash
git remote add origin <your-repo-url>
git push -u origin main
git push origin feature/git-basics-owner-team
```

You're pushing `main` and the one unmerged branch. `feature/add-python-notes` and `feature/git-basics-owner-anjali` are already merged into `main`'s history, so there's nothing left to push for them individually.

## Step 2 — Open the conflicting PR

On GitHub: **Pull requests → New pull request** → base `main`, compare `feature/git-basics-owner-team`.

GitHub will show a red **"This branch has conflicts that must be resolved"** banner instead of a green "Able to merge" — because this branch and `main` both changed the `## Owner` line of `notes/git-basics.md` since they diverged. Open the PR anyway; title it "Set git-basics.md owner to docs team." Don't try GitHub's web conflict editor for this — resolve it locally, which is what real teams do for anything beyond a one-line fix.

## Step 3 — Reproduce and resolve the conflict locally

```bash
git switch main
git pull
git switch feature/git-basics-owner-team
git merge main
```

Git will stop and show:

```
Auto-merging notes/git-basics.md
CONFLICT (content): Merge conflict in notes/git-basics.md
Automatic merge failed; fix conflicts and then commit the result.
```

Open `notes/git-basics.md`. You'll see:

```
<<<<<<< HEAD
Docs team (rotating)
=======
Anjali
>>>>>>> main
```

Decide the real answer — not "pick one arbitrarily" but "what should this file actually say." A reasonable resolution: keep both people accountable.

```markdown
## Owner

Anjali (primary), docs team (backup)
```

Delete the `<<<<<<<`, `=======`, `>>>>>>>` markers entirely — leaving one behind is the single most common conflict-resolution mistake. Then:

```bash
git status                              # confirms "both modified", now resolved
git add notes/git-basics.md
git commit                              # completes the merge; Git pre-fills a message
git push origin feature/git-basics-owner-team
```

Refresh the PR on GitHub — the red banner is gone, replaced by "Able to merge." Merge it.

## Step 4 — Clean up

```bash
git switch main
git pull
git branch -d feature/git-basics-owner-team
git push origin --delete feature/git-basics-owner-team
```

## Step 5 — Do it once more, cold

Now repeat the whole loop without the training wheels, to prove it wasn't a fluke:

```bash
git switch -c feature/add-sql-notes
# create notes/sql-notes.md with real content
git add notes/sql-notes.md
git commit -m "Add SQL notes"
git push -u origin feature/add-sql-notes
# open the PR, review your own diff, merge on GitHub
git switch main && git pull
git branch -d feature/add-sql-notes
```

Then force a second conflict deliberately: branch, edit the `## Status` line of any note, push, open a PR — but before merging, switch to `main`, edit that *same line* differently, commit and push directly... except this repo's own rule (see `CONTRIBUTING.md`) says never commit to `main` directly. So instead: branch again from the *old* `main`, edit the same line, push, open a second PR. Merge the first PR. Watch the second PR turn red. Resolve it exactly as in Step 3.

## What you should be able to explain afterward

- Why a merge conflict happens (same lines, changed differently, on two branches that both descend from a common point) versus when Git resolves it silently (different lines, or one branch is a strict fast-forward of the other).
- Why resolving in GitHub's web editor is fine for a one-line typo but risky for anything larger — you lose your own diff tool, tests, and linter.
- The difference between `git merge --abort` (bail out, nothing happened) and finishing a conflicted merge (edit, `add`, `commit`).
- Why `main` never gets direct commits in this workflow, and what that buys you (it's always in a known, reviewed state).
