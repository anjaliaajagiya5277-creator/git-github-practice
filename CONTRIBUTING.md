# Contributing

Conventions this repo follows, so PRs stay reviewable.

## Branch names

```
feature/<short-description>    new content or functionality
fix/<short-description>        correcting something wrong
docs/<short-description>       documentation-only changes
```

Never commit directly to `main`. Every change arrives via a branch and a pull request, even in a one-person repo — it's the habit that matters, not the audience.

## Commit messages

- Imperative mood: "Add SQL notes" not "Added SQL notes" or "Adds SQL notes".
- First line under ~50 characters. Body (if needed) explains *why*, separated by a blank line.
- One logical change per commit. If your commit message needs "and" to describe it, it's probably two commits.

## Pull requests

- Title says what changed, not "fix stuff" or "updates".
- Description says why, and calls out anything the reviewer should look at closely.
- Keep PRs small enough to review in one sitting. A 400-line diff gets a rubber-stamp approval; a 40-line diff gets a real review.
- Resolve conflicts by merging (or rebasing onto) the latest `main` locally, fixing the conflict there, then pushing — never by re-editing the file through GitHub's web UI, which hides what actually changed.

## Merging

This repo merges with a merge commit (not squash, not rebase) so the branch structure stays visible in `git log --graph` — useful while you're still learning to read it. Once branching feels natural, squash merges are usually the better default for a real team.
