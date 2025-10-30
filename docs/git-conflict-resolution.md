# Git Conflict Resolution Guide

## Handling Divergent Branches

When you encounter the error "fatal: Need to specify how to reconcile divergent branches" while pulling from a remote repository, it means your local branch and the remote branch have diverged - they both have commits that the other doesn't have.

### Understanding the Error

```bash
hint: You have divergent branches and need to specify how to reconcile them.
hint: You can do so by running one of the following commands sometime before
hint: your next pull:
hint:
hint:   git config pull.rebase false  # merge
hint:   git config pull.rebase true   # rebase
hint:   git config pull.ff only       # fast-forward only
```

### Solution Options

You have three main strategies to resolve this:

#### 1. Merge Strategy (Recommended for Most Cases)

This creates a merge commit that combines the histories of both branches.

**Set globally (for all repositories):**
```bash
git config --global pull.rebase false
```

**Set locally (for current repository only):**
```bash
git config pull.rebase false
```

**Then pull:**
```bash
git pull origin <branch-name>
```

**Pros:**
- Preserves complete history of both branches
- Safer for collaborative work
- Easy to understand what happened

**Cons:**
- Creates additional merge commits
- Can make history look cluttered

#### 2. Rebase Strategy

This replays your local commits on top of the remote commits, creating a linear history.

**Set globally:**
```bash
git config --global pull.rebase true
```

**Set locally:**
```bash
git config pull.rebase true
```

**Then pull:**
```bash
git pull origin <branch-name>
```

**Pros:**
- Creates a clean, linear history
- No merge commits

**Cons:**
- Rewrites commit history
- Can be dangerous if commits have been pushed and others are working on them
- More complex conflict resolution if conflicts occur

#### 3. Fast-Forward Only

This only updates your branch if it can be "fast-forwarded" (no divergent changes).

**Set globally:**
```bash
git config --global pull.ff only
```

**Set locally:**
```bash
git config pull.ff only
```

**Then pull:**
```bash
git pull origin <branch-name>
```

**Pros:**
- Safest option - prevents accidental merges
- Keeps history clean

**Cons:**
- Will fail if branches have diverged
- Requires manual intervention when conflicts exist

### Quick Fix for Immediate Pull

If you don't want to change your configuration and just want to pull once with a specific strategy:

**Merge (one-time):**
```bash
git pull --no-rebase origin <branch-name>
```

**Rebase (one-time):**
```bash
git pull --rebase origin <branch-name>
```

**Fast-forward only (one-time):**
```bash
git pull --ff-only origin <branch-name>
```

### Handling Merge Conflicts

If conflicts occur during merge or rebase:

#### During Merge:
1. Git will mark conflicted files
2. Open conflicted files and look for conflict markers:
   ```
   <<<<<<< HEAD
   Your changes
   =======
   Remote changes
   >>>>>>> branch-name
   ```
3. Edit files to resolve conflicts
4. Stage resolved files:
   ```bash
   git add <resolved-file>
   ```
5. Complete the merge:
   ```bash
   git commit
   ```

#### During Rebase:
1. Resolve conflicts in files (same as merge)
2. Stage resolved files:
   ```bash
   git add <resolved-file>
   ```
3. Continue the rebase:
   ```bash
   git rebase --continue
   ```
4. Or abort and return to pre-rebase state:
   ```bash
   git rebase --abort
   ```

### Best Practices

1. **Pull frequently** to minimize divergence
2. **Commit your work** before pulling to avoid losing changes
3. **Communicate with team** about rebasing shared branches
4. **Use merge strategy** for public/shared branches
5. **Use rebase strategy** for personal feature branches (before sharing)
6. **Check status** before and after pulling:
   ```bash
   git status
   ```

### Checking Your Current Configuration

To see your current pull configuration:

```bash
git config --get pull.rebase
```

To see all git configurations:

```bash
git config --list
```

### Recommended Workflow

For this repository, we recommend the following workflow:

1. **Before starting work:**
   ```bash
   git pull origin <branch-name>
   ```

2. **Make your changes and commit:**
   ```bash
   git add .
   git commit -m "Your commit message"
   ```

3. **Before pushing, pull latest changes:**
   ```bash
   git pull origin <branch-name>
   ```

4. **Resolve any conflicts if they occur**

5. **Push your changes:**
   ```bash
   git push origin <branch-name>
   ```

### Common Error Solutions

#### "fatal: empty string is not a valid pathspec"
This occurs when you use `git add` with an empty string or incorrect parameters:
```bash
# Wrong - empty string:
git add ''

# Wrong - trailing double dash without a file:
git add -A --

# Correct:
git add -A
# or
git add .
# or (for specific files):
git add filename.txt
```

#### "refusing to merge unrelated histories"
If you need to merge branches with unrelated histories:
```bash
git pull origin <branch-name> --allow-unrelated-histories
```

### Additional Resources

- [Git Documentation - git-pull](https://git-scm.com/docs/git-pull)
- [Git Documentation - git-merge](https://git-scm.com/docs/git-merge)
- [Git Documentation - git-rebase](https://git-scm.com/docs/git-rebase)

---

**Need more help?** Open an issue on the GitHub repository or consult the official Git documentation.
