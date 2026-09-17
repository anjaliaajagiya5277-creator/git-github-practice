# Branching

## Status

Draft — needs more detail.

## Why branch

Isolate work in progress from `main` so `main` always stays deployable.

## Commands

```bash
git switch -c feature/my-change
git switch main
git merge feature/my-change
git branch -d feature/my-change
```

## Owner

TBD
