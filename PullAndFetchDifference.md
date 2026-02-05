# Difference Between `git fetch` and `git pull`

When working with Git, keeping your local repository up to date with the remote repository is essential. Two commonly used commands for this purpose 
are **`git fetch`** and **`git pull`**. While they seem similar, they behave differently and are used in different situations.

---

## Overview

| Command     | Description                                                                                  |
| ----------- | -------------------------------------------------------------------------------------------- |
| `git fetch` | Downloads changes from the remote repository **without merging** them into your local branch |
| `git pull`  | Downloads changes **and automatically merges** them into your local branch                   |

---

## What is `git fetch`?

`git fetch` retrieves the latest commits, branches, and tags from the remote repository and updates your **remote-tracking branches** (e.g., `origin/main`).
It **does not modify** your working directory or local branches.

### Syntax

```bash
git fetch origin
```

### Key characteristics

* Safe operation (no code changes applied)
* Allows you to **review changes before merging**
* Updates only `origin/<branch>`, not your local branch

---

## What is `git pull`?

`git pull` is a **combination of two commands**:

```bash
git fetch
git merge
```

It fetches changes from the remote repository and **immediately merges** them into your current local branch.

### Syntax

```bash
git pull origin main
```

### Key characteristics

* Updates your local branch automatically
* May cause merge conflicts immediately
* Faster, but less controlled

---

## Example Scenario

### Initial State

Both local and remote repositories are in sync:

```
A---B   (main, origin/main)
```

---

### Teammate pushes a new commit (`C`) to the remote

Remote repository now has:

```
A---B---C   (origin/main)
```

Your local repository is **behind**.

---

## Using `git fetch`

```bash
git fetch origin
```

### Result

```
A---B   (main)
     \
      C   (origin/main)
```

* Local `main` is unchanged
* Remote changes are stored in `origin/main`

### Review changes

```bash
git log main..origin/main
git diff main origin/main
```

### Apply changes manually

```bash
git merge origin/main
```

---

## Using `git pull`

```bash
git pull origin main
```

### Result

```
A---B---C   (main, origin/main)
```

* Changes are fetched and merged automatically
* If conflicts exist, Git will prompt you to resolve them immediately

---

## When to Use Which

### Use `git fetch` when:

* You want to **inspect changes before merging**
* You are working in a team environment
* You need greater control over merges

### Use `git pull` when:

* You want a quick update
* You trust the remote changes
* You are working on a personal or low-risk branch

---

## Summary

| Feature                    | git fetch | git pull |
| -------------------------- | --------- | -------- |
| Downloads remote changes   | ✅         | ✅        |
| Updates local branch       | ❌         | ✅        |
| Risk of merge conflicts    | ❌         | ✅        |
| Allows review before merge | ✅         | ❌        |

---

## Conclusion

* **`git fetch`** is safer and gives you full control over when and how changes are merged.
* **`git pull`** is convenient but should be used carefully, especially in collaborative projects.

---
