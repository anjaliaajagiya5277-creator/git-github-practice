# Team Wiki — Git & GitHub Practice Repo

Deliverable for the **Git & GitHub (branching, PRs, conflict resolve)** row of my learning sheet.

This is a tiny internal wiki (three markdown notes). The content doesn't matter — it exists to give you something realistic to branch, open PRs against, and deliberately conflict on.

**Start here → [`EXERCISE.md`](EXERCISE.md).** It walks through the whole GitHub workflow end to end, using the branches already sitting in this repo:

1. Push this repo to GitHub as-is.
2. Open and merge a clean PR (`feature/add-python-notes` → no conflict).
3. Open two more PRs that both touch the same line, merge the first, then hit — and resolve — a real conflict merging the second.

See [`CONTRIBUTING.md`](CONTRIBUTING.md) for the branch-naming and commit-message conventions this repo follows.

## What's in the repo right now

```
notes/
├── git-basics.md
├── branching.md
└── setup.md
```

`main` has the initial commit only. Everything else lives on branches — check `git branch -a` and `git log --all --oneline --graph` to see the shape of it before you start.
