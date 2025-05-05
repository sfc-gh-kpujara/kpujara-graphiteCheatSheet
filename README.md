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



### 🚧 Opening a Draft PR

If you're not ready for review but want to push your feature branch and open a **draft pull request**, you can do:

```bash
gt submit --draft
```

This will:
- Push your current branch
- Open a draft PR on GitHub
- Let teammates know it's a work-in-progress

Once submitted, you can open the PR in your browser with:

```bash
gt pr
```


### 🚀 Submitting a Stack of PRs

To submit your current PR and any PRs up or down the stack:

```bash
gt submit
```

This will:
- Detect and restack branches if needed
- Push them to GitHub
- Create or update the PRs automatically
- Ensure parent/child relationships stay correct

> 💡 If you're not making code changes but just syncing metadata (e.g. restack or title change), use:

```bash
gt submit --stack --update-only
```

---

### 🛠 If You Used `git push` Instead of `gt submit`

Graphite won’t know you pushed changes unless you run:

```bash
gt submit
```

This tells Graphite to sync its metadata with GitHub and update the PR state.

### 🔁 Transition from Manual Push to Graphite Submit

Previously, we used to commit and manually push like this:

```bash
git add .
git commit -m "Some change"
git push
```

Now, with Graphite, the recommended workflow is:

```bash
git add .
git commit -m "Some change"
gt submit
```

Graphite will:
- Restack branches if needed
- Push your branch and any stacked branches
- Open or update all associated PRs
- Preserve stack relationships


#### 📌 If You Updated the **Base PR** (Lower in the stack):

You must:
```bash
gt submit                  # Push base PR changes
gt co <child-branch>
gt restack                 # Rebase child on updated parent
gt submit                  # Resubmit child PR
```

If you skip this, the child PR will still point to the old base commit and appear out-of-date.

#### 📌 If You Updated the **Top PR** (No children):

You can use either:
```bash
git push                   # Push manually (PR will update on GitHub)
gt submit                  # Optional — syncs Graphite’s metadata
```

---

### 📌 Best Practices Summary

| Action                                 | Recommended Command     |
|----------------------------------------|--------------------------|
| Start a new feature stack              | `gt co main && gt create` |
| Open a draft PR                        | `gt submit --draft`     |
| Submit a PR or stack                   | `gt submit`             |
| Sync PRs after a manual git push       | `gt submit`             |
| Restack child PRs after base changes   | `gt restack && gt submit` |
| Visualize your stack                   | `gt ls` or `gt log`     |
| Open PR in browser                     | `gt pr`                 |

