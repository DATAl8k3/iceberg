# Apache Iceberg – Dlake Fork ❄️

This repository is a fork of **Apache Iceberg**.
It exists to maintain **dlake-specific extensions and patches** while staying closely aligned with the upstream Iceberg project.

> This is **not** a standalone distribution.
> The goal is to keep the fork **thin, rebased often, and as close to upstream as possible**.

---

## Repository Structure & Branching Model

We follow a strict branching strategy to minimize drift from upstream.

### Branches

```
upstream/main        → Official Apache Iceberg repository
origin/main          → Clean mirror of upstream/main (NO custom changes)
origin/dlake-main    → Production branch (origin/main + dlake patches)
origin/feature/*     → Feature / fix branches
```

### Rules (Important)

* ❌ **Never commit directly to `origin/main`**
* ❌ **Never commit directly to `origin/dlake-main`**
* ✅ All development happens in `origin/feature/*`
* ✅ `origin/main` must always be a clean rebase of `upstream/main`

---

## Typical Development Flow

### 1. Create a feature branch

```bash
git checkout dlake-main
git checkout -b feature/my-change
```

### 2. Implement your change

* Keep commits small and focused
* Avoid unrelated formatting or refactors
* Prefer extension points over core changes

### 3. Rebase before merging

```bash
git fetch origin
git rebase origin/dlake-main
```

NOTE: Merging or pulling (git pull) is not permitted on fork branches. All branches must use rebase only to maintain a linear history and minimize upstream drift.

### 4. Merge via PR into `dlake-main`

* Squash only if it improves clarity
* Every PR must add an entry to the fork `CHANGELOG` describing the change.

---

## Syncing With Upstream Iceberg

Keeping the fork healthy depends on **frequent upstream rebases**.

### Step 1: Update `origin/main`

```bash
git remote add upstream https://github.com/apache/iceberg.git (once)
git fetch upstream
git checkout main
git rebase upstream/main
git push origin main --force-with-lease
```

### Step 2: Rebase `dlake-main`

```bash
git checkout dlake-main
git rebase main
```

> 🔁 This should be done regularly, even when no new features are added.

If conflicts occur:

- Resolve them carefully and minimally
- Do not introduce refactors or cleanups while resolving conflicts
- Validate that fork-specific changes are still required after the rebase
- When in doubt, stop and consult the fork owner

---

## Upstream Contributions

Whenever possible:

* Changes **should be proposed upstream**
* Internal patches should be treated as **temporary**
* Once a patch is accepted upstream, it **must be removed** from this fork

This keeps:

* Rebase conflicts small
* Maintenance cost low
* Long-term ownership manageable

---

## Questions?

If you’re unsure whether a change belongs here:
**Stop and ask. Fork debt is real.**
