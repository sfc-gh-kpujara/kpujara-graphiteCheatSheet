## 📚 Graphite Workflow Guide: Creating New Feature Stacks

This project uses [Graphite](https://graphite.dev) to manage pull requests via stacked branches.

---

### 🆕 Starting a New Independent Feature (New Stack)

To ensure a new feature branch is **not stacked on top of an existing branch**, always start from `main`:

```bash
gt co main        # Switch to the main branch
git pull          # Ensure main is up to date
gt create <new-feature-branch>
```

This creates a clean, independent branch and PR directly off `main`.

> ⚠️ If you skip this step and create a branch while on another feature branch, your new branch will be **stacked**, not independent.

---

### 📌 `gt co` Explained

- `gt co` is short for `gt checkout`.
- It switches to an existing branch.
- If no branch name is provided, it opens an interactive branch selector.

```bash
gt co main        # Switch to main
gt co             # Pick a branch interactively
```

---

### 🚧 Opening a Draft PR

If you're not ready for review but want to push your feature branch and open a **draft pull request**, you can do:

```bash
gt submit --draft




### ✅ Best Practices

- Always run `gt co main` before starting new work.
- Use `gt create` to make a new feature branch tracked by Graphite.
- Use `gt submit` to open pull requests.
- Use `gt restack` if branches become misaligned.
- Use `gt ls` or `gt log` to visualize your branch stacks.
