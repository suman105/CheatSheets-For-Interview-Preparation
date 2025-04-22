# Git & GitHub Commands Cheatsheet

## 1. **Git Configuration**

### View Configuration
```bash
// Show current username
git config user.name

// Show current email
git config user.email

// List all configurations
git config --list
```

### Set Configuration
```bash
// Set global username
git config --global user.name "Your Name"

// Set global email
git config --global user.email "email@example.com"

// Set default editor (e.g., VS Code)
git config --global core.editor "code --wait"

// Enable color output
git config --global color.ui auto
```

### Alternative: SSH Key Setup
```bash
// Generate SSH key
ssh-keygen -t ed25519 -C "email@example.com"

// Start SSH agent
eval "$(ssh-agent -s)"

// Add SSH key to agent
ssh-add ~/.ssh/id_ed25519

// Copy public key to GitHub (Settings > SSH and GPG keys)
cat ~/.ssh/id_ed25519.pub
```

- **Configuration**: Defines user identity and Git behavior.
- **Approaches**:
  - **Global Config**: Applies to all repositories (`--global`).
  - **Local Config**: Repository-specific (`--local`, default if no flag).
  - **SSH**: Secure alternative to HTTPS, avoids PATs for authentication.
- **Best Practices**:
  - Use a consistent email tied to your GitHub account.
  - Configure SSH for secure, password-less access.
  - Protect SSH keys with passphrases in production.

**Explanation**:
- `git config` manages settings stored in `~/.gitconfig` (global) or `.git/config` (local).
- SSH keys are preferred for private repositories, reducing PAT management.
- Custom editors improve commit message workflows.
- Color output enhances readability of Git commands.

---

## 2. **Initializing and Managing Git Repository**

```bash
// Initialize a new Git repository
git init

// Check status of working directory and staging area
git status

// Create .gitignore file to exclude files
echo "node_modules/" > .gitignore
```

- **Initialization**: Creates a `.git` directory for version control.
- **Best Practices**:
  - Add a `.gitignore` file early to exclude build artifacts, logs, etc.
  - Use `git status` frequently to track changes.
  - Initialize in the project root for proper tracking.

**Explanation**:
- `git init` sets up a new repository, enabling version control.
- `.gitignore` prevents accidental commits of irrelevant files (e.g., `node_modules`, `.env`).
- `git status` provides a snapshot of tracked, staged, and untracked files.

---

## 3. **Cloning Repositories**

### Cloning Public Repository
```bash
// Clone via HTTPS
git clone https://github.com/account/repo.git

// Clone via SSH
git clone git@github.com:account/repo.git
```

### Cloning Private Repository
```bash
// Clone with Personal Access Token (PAT)
git clone https://<PAT>@github.com/account/repo.git

// Clone with SSH (preferred for private repos)
git clone git@github.com:account/repo.git
```

### Cloning with Submodules
```bash
// Clone including submodules
git clone --recurse-submodules https://github.com/account/repo.git

// Update submodules in an existing clone
git submodule update --init --recursive
```

- **Cloning**: Copies a remote repository to your local machine.
- **Approaches**:
  - **HTTPS**: Simple, requires PAT for private repos.
  - **SSH**: Secure, password-less, ideal for frequent access.
  - **Submodules**: Manages nested repositories within a project.
- **Best Practices**:
  - Use SSH for private repositories to avoid PAT expiration.
  - Store PATs securely (e.g., in a password manager).
  - Clone submodules explicitly when needed.

**Explanation**:
- HTTPS is beginner-friendly but requires authentication for private repos.
- SSH avoids repeated credential prompts, streamlining workflows.
- Submodules allow modular project dependencies but add complexity.
- PATs are generated in GitHub Settings > Developer Settings > Personal Access Tokens.

---

## 4. **Working with Staging and Commits**

### Staging Files
```bash
// Stage specific file
git add <file_name>

// Stage all modified files
git add .

// Stage specific changes interactively
git add -p
```

### Committing Changes
```bash
// Commit with message
git commit -m "Add feature X"

// Commit all modified files (skip staging)
git commit -a -m "Update files"

// Amend last commit
git commit --amend
```

### Viewing Commit History
```bash
// Show detailed commit history
git log

// Show one-line commit summary
git log --oneline

// Show graph of branches
git log --graph --all --oneline
```

- **Staging and Commits**: Track changes in the repository.
- **Approaches**:
  - **Explicit Staging**: `git add` for granular control.
  - **Auto-Staging**: `git commit -a` for convenience.
  - **Interactive Staging**: `git add -p` for selective changes.
- **Best Practices**:
  - Write clear, concise commit messages (e.g., "Fix bug in login").
  - Follow commit message conventions (e.g., `<type>(<scope>): <description>`).
  - Commit frequently but logically to maintain history clarity.

**Explanation**:
- Staging (`git add`) prepares changes for committing.
- Commits (`git commit`) create snapshots of the repository state.
- Amending rewrites the last commit, useful for fixing typos or adding files.
- `git log` provides insight into project history, with `--oneline` for brevity.

---

## 5. **Pushing to GitHub**

```bash
// Push to main branch
git push -u origin main

// Push to master branch (if used)
git push -u origin master

// Force push (use cautiously)
git push --force

// Force push with lease (safer)
git push --force-with-lease
```

- **Pushing**: Sends local commits to the remote repository.
- **Approaches**:
  - **Standard Push**: `git push` for normal updates.
  - **Force Push**: Overrides remote history, risks overwriting others’ work.
  - **Force-with-Lease**: Prevents overwriting if remote has new commits.
- **Best Practices**:
  - Always pull before pushing to avoid conflicts.
  - Use `--force-with-lease` instead of `--force` for safety.
  - Set upstream (`-u`) on first push to link branches.

**Explanation**:
- `git push -u` links the local branch to the remote branch.
- Force pushes are dangerous in collaborative projects; communicate with team.
- `--force-with-lease` checks remote state, reducing accidental overwrites.
- Use branch protection rules on GitHub to prevent force pushes to main.

---

## 6. **Remote Branch Management**

### Managing Remotes
```bash
// Add remote repository
git remote add origin https://github.com/account/repo.git

// View remote repositories
git remote -v

// Rename remote
git remote rename origin upstream

// Remove remote
git remote remove upstream

// Update remote URL
git remote set-url origin git@github.com:account/repo.git
```

### Pushing to Remote Branches
```bash
// Push to a specific branch
git push origin feature-branch

// Delete remote branch
git push origin --delete feature-branch
```

- **Remote Management**: Configures connections to remote repositories.
- **Best Practices**:
  - Use descriptive names for remotes (e.g., `origin`, `upstream`).
  - Regularly prune stale remote branches (`git fetch --prune`).
  - Verify remote URLs match authentication method (HTTPS/SSH).

**Explanation**:
- `git remote add` links a local repository to GitHub or other hosts.
- `git remote -v` confirms remote URLs and fetch/push settings.
- Deleting remote branches cleans up GitHub after merging.
- Use `git push --delete` cautiously to avoid accidental data loss.

---

## 7. **Working with Branches**

### Branch Operations
```bash
// List local branches
git branch

// List all branches (local + remote)
git branch -a

// Create new branch
git branch feature-branch

// Switch to branch
git switch feature-branch

// Create and switch to new branch
git switch -c feature-branch

// Rename current branch
git branch -m new-name

// Delete local branch (merged)
git branch -d feature-branch

// Force delete unmerged branch
git branch -D feature-branch
```

### Alternative: Using `git checkout`
```bash
// Switch to branch
git checkout feature-branch

// Create and switch to new branch
git checkout -b feature-branch
```

- **Branches**: Isolate work for features, fixes, or experiments.
- **Approaches**:
  - **git switch**: Modern, avoids `checkout` ambiguity.
  - **git checkout**: Legacy, still widely used.
- **Best Practices**:
  - Use descriptive branch names (e.g., `feature/login`, `fix/bug-123`).
  - Delete merged branches to keep repository clean.
  - Follow branching strategies (e.g., Gitflow, trunk-based).

**Explanation**:
- `git switch` is clearer for branch operations, introduced in Git 2.23.
- `git checkout` is versatile but overloaded (branch switching, file reverting).
- Branching enables parallel development without affecting `main`.
- Gitflow uses `main`, `develop`, feature, and release branches; trunk-based uses short-lived branches.

---

## 8. **Working with Remote and Local Branches**

### Fetching and Pulling
```bash
// Fetch updates from remote without merging
git fetch origin

// Fetch specific branch
git fetch origin feature-branch

// Pull updates (fetch + merge)
git pull origin main

// Pull with rebase (cleaner history)
git pull --rebase origin main
```

### Checking Out Remote Branches
```bash
// Track remote branch locally
git checkout --track origin/feature-branch

// View remote branch without switching
git log origin/feature-branch
```

- **Remote Syncing**: Keeps local repository aligned with remote.
- **Approaches**:
  - **git pull**: Merges changes, may create merge commits.
  - **git pull --rebase**: Reapplies local commits, avoids merge commits.
- **Best Practices**:
  - Use `git fetch` to review changes before merging.
  - Prefer `--rebase` for cleaner history in solo workflows.
  - Track remote branches to contribute to shared work.

**Explanation**:
- `git fetch` downloads changes without modifying the working directory.
- `git pull` combines `fetch` and `merge`, updating the local branch.
- Rebasing with `git pull --rebase` maintains a linear history but requires caution in shared branches.
- Tracking remote branches simplifies collaboration.

---

## 9. **Merging Branches**

### Merging
```bash
// Merge branch into current branch
git merge feature-branch

// Merge with no fast-forward (create merge commit)
git merge --no-ff feature-branch

// Abort merge if conflicts arise
git merge --abort
```

### Types of Merges
- **Fast-Forward**: Applies commits directly if no divergence (`git merge`).
- **Merge Commit**: Creates a commit to combine divergent branches (`--no-ff`).
- **Squash Merge**: Combines commits into a single commit (GitHub UI or `git merge --squash`).

- **Best Practices**:
  - Use `--no-ff` for feature branches to preserve history.
  - Resolve conflicts promptly and test post-merge.
  - Use GitHub pull requests for code review before merging.

**Explanation**:
- Fast-forward merges are clean but lose branch context.
- Merge commits document collaboration, useful for audits.
- Squash merges reduce noise in history but obscure individual commits.
- `git merge --abort` safely cancels problematic merges.

---

## 10. **Handling Merge Conflicts**

```bash
// Resolve conflicts in files marked by Git
// Example conflict in file.txt:
<<<<<<< HEAD
Local changes
=======
Remote changes
>>>>>>> feature-branch

// Edit file to resolve, then:
git add file.txt
git commit
```

### Visual Merge Tools
```bash
// Configure merge tool (e.g., VS Code)
git config --global mergetool.vscode.cmd "code --wait $MERGED"
git mergetool
```

- **Conflicts**: Occur when changes overlap in the same file region.
- **Best Practices**:
  - Use visual tools (e.g., VS Code, Beyond Compare) for complex conflicts.
  - Communicate with team to avoid recurring conflicts.
  - Test thoroughly after resolving conflicts.

**Explanation**:
- Git marks conflicts with `<<<<<<<`, `=======`, `>>>>>>>` markers.
- Manual resolution involves choosing or combining changes.
- Visual merge tools streamline conflict resolution, reducing errors.
- Committing resolved files finalizes the merge.

---

## 11. **Push Changes to Remote**

```bash
// Push current branch
git push

// Push all branches
git push --all

// Push tags
git push --tags
```

- **Pushing**: Updates remote repository with local changes.
- **Best Practices**:
  - Verify branch tracking with `git branch -vv`.
  - Use pull requests for team reviews before pushing to `main`.
  - Push tags for releases to share milestones.

**Explanation**:
- `git push` updates the tracked remote branch.
- `--all` pushes all local branches, useful for backups.
- Tags (`--tags`) mark specific commits (e.g., `v1.0.0`) for releases.

---

## 12. **Advanced Git Operations**

### Rebase
```bash
// Rebase current branch onto another
git rebase main

// Interactive rebase for editing commits
git rebase -i HEAD~3
```

### Cherry-Pick
```bash
// Apply specific commit to current branch
git cherry-pick <commit-hash>
```

### Stash
```bash
// Save uncommitted changes
git stash

// Save with message
git stash save "Work in progress"

// List stashes
git stash list

// Apply latest stash
git stash apply

// Apply and remove stash
git stash pop

// Drop specific stash
git stash drop stash@{0}
```

### Tagging
```bash
// Create lightweight tag
git tag v1.0.0

// Create annotated tag
git tag -a v1.0.0 -m "Release 1.0.0"

// Push tag to remote
git push origin v1.0.0

// Delete tag
git tag -d v1.0.0
git push origin --delete v1.0.0
```

### Reflog
```bash
// View reference log
git reflog

// Recover lost commit
git checkout <commit-hash>
```

### Bisect
```bash
// Start bisect to find buggy commit
git bisect start
git bisect bad HEAD
git bisect good <known-good-commit>

// Mark commits as good/bad
git bisect good
git bisect bad

// End bisect
git bisect reset
```

- **Advanced Operations**:
  - **Rebase**: Rewrites history for cleaner commits.
  - **Cherry-Pick**: Selectively applies commits.
  - **Stash**: Temporarily shelves changes.
  - **Tagging**: Marks releases or milestones.
  - **Reflog**: Recovers lost commits or branches.
  - **Bisect**: Debugs by binary search.
- **Best Practices**:
  - Use interactive rebase to squash or edit commits before sharing.
  - Cherry-pick sparingly to avoid duplicate commits.
  - Name stashes for clarity.
  - Tag releases with semantic versioning (e.g., `v1.0.0`).

**Explanation**:
- Rebase linearizes history but rewrites commits, avoid on shared branches.
- Cherry-pick is useful for hotfixes or backporting.
- Stash enables context switching without committing.
- Reflog is a lifesaver for recovering “lost” work.
- Bisect automates debugging by narrowing down faulty commits.

---

## 13. **Resetting and Undoing Changes**

### Undo Working Directory Changes
```bash
// Revert changes in a file
git checkout -- <file_name>

// Revert all uncommitted changes
git restore .
```

### Unstage Changes
```bash
// Remove file from staging
git restore --staged <file_name>

// Legacy: Remove all from staging
git reset
```

### Undo Commits
```bash
// Soft reset: Keep changes in staging
git reset --soft HEAD~1

// Hard reset: Discard changes (dangerous)
git reset --hard HEAD~1

// Reset to specific commit
git reset <commit-hash>
```

### Revert Commit
```bash
// Create new commit undoing specified commit
git revert <commit-hash>
```

- **Undoing**:
  - **Restore**: Reverts file changes.
  - **Reset**: Moves HEAD, adjusting history.
  - **Revert**: Creates a new commit to undo changes.
- **Best Practices**:
  - Use `revert` for shared branches to preserve history.
  - Confirm `hard` resets with backups or reflog.
  - Test after reverting to ensure functionality.

**Explanation**:
- `git restore` (or `git checkout --`) reverts uncommitted changes.
- `git reset --soft` is safe for reworking commits; `--hard` deletes changes.
- `git revert` is collaborative, avoiding history rewrites.
- Reflog can recover from accidental resets.

---

## 14. **Git Submodules**

```bash
// Add submodule
git submodule add https://github.com/account/submodule-repo.git path/to/submodule

// Clone with submodules
git clone --recurse-submodules https://github.com/account/repo.git

// Update submodules
git submodule update --init --recursive

// Pull submodule updates
git submodule update --remote
```

- **Submodules**: Embed repositories within a repository.
- **Best Practices**:
  - Use submodules for stable dependencies.
  - Update submodules regularly to avoid drift.
  - Document submodule usage for team clarity.

**Explanation**:
- Submodules manage external repositories (e.g., libraries) as dependencies.
- `--recurse-submodules` ensures submodules are cloned.
- Updates require explicit commands, unlike regular branches.
- Alternatives like Git subtree or npm packages may be simpler.

---

## 15. **Git Hooks**

```bash
// Example: Pre-commit hook to run linter
// .git/hooks/pre-commit
//!/bin/sh
npm run lint

// Make executable
chmod +x .git/hooks/pre-commit
```

- **Hooks**: Scripts triggered by Git events (e.g., pre-commit, post-merge).
- **Best Practices**:
  - Use hooks for linting, testing, or formatting.
  - Share hooks via `.githooks` directory or tools like Husky.
  - Test hooks locally to avoid breaking workflows.

**Explanation**:
- Hooks automate tasks, improving code quality.
- Pre-commit hooks prevent bad commits (e.g., failing tests).
- Husky simplifies hook management in JavaScript projects.
- Hooks are local unless shared explicitly.

---

## 16. **Git LFS (Large File Storage)**

```bash
// Install Git LFS
git lfs install

// Track large files (e.g., images)
git lfs track "*.png"

// Commit and push
git add .gitattributes
git commit -m "Add LFS tracking"
git push
```

- **Git LFS**: Manages large files (e.g., images, videos) outside Git.
- **Best Practices**:
  - Track specific file types with `.gitattributes`.
  - Ensure team members install Git LFS.
  - Monitor LFS storage quotas on GitHub.

**Explanation**:
- Git LFS replaces large files with pointers, reducing repository size.
- `.gitattributes` defines tracked files.
- Requires Git LFS setup on all clients.
- Alternatives include external storage (e.g., S3) with references.

---

## 17. **Git Worktrees**

```bash
// Create new worktree for branch
git worktree add ../new-worktree feature-branch

// List worktrees
git worktree list

// Remove worktree
git worktree remove ../new-worktree
```

- **Worktrees**: Multiple working directories for a single repository.
- **Best Practices**:
  - Use worktrees for parallel feature development.
  - Clean up unused worktrees to save space.
  - Avoid modifying the same branch in multiple worktrees.

**Explanation**:
- Worktrees allow simultaneous work on multiple branches without cloning.
- Each worktree has its own working directory and index.
- Useful for testing or hotfixes without switching branches.
- Requires Git 2.5+.

---

## 18. **GitHub-Specific Features**

### Pull Requests
```bash
// Create branch and push
git switch -c feature-branch
git push -u origin feature-branch

// Create pull request via GitHub UI
// - Visit repository on GitHub
// - Select "Pull Requests" > "New Pull Request"
```

### GitHub Actions (CI/CD)
```yaml
// .github/workflows/ci.yml
name: CI
on:
  push:
    branches: [ main ]
jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - name: Set up Node.js
        uses: actions/setup-node@v3
        with:
          node-version: '16'
      - run: npm install
      - run: npm test
```

- **Pull Requests**: Facilitate code review and merging.
- **GitHub Actions**: Automate testing, building, and deployment.
- **Best Practices**:
  - Write clear PR descriptions with context and testing steps.
  - Use Actions for CI/CD to catch errors early.
  - Protect `main` branch with required reviews and checks.

**Explanation**:
- PRs enable collaborative review, ensuring quality.
- GitHub Actions run workflows on events (e.g., push, PR).
- Branch protection prevents direct pushes to critical branches.
- Actions support complex pipelines with reusable steps.

---

## 19. **Best Practices**

- **Commit Messages**:
  - Use format: `<type>(<scope>): <short description>` (e.g., `feat(login): add OAuth support`).
  - Types: `feat`, `fix`, `docs`, `style`, `refactor`, `test`, `chore`.
- **Branching**:
  - Follow Gitflow (`main`, `develop`, `feature/*`, `release/*`) or trunk-based (short-lived branches).
  - Name branches descriptively (e.g., `feature/login`, `bugfix/issue-123`).
- **Security**:
  - Protect PATs and SSH keys; never commit them.
  - Use `.gitignore` for sensitive files (e.g., `.env`).
- **Collaboration**:
  - Pull before pushing to avoid conflicts.
  - Use PRs for team contributions with reviews.
  - Squash commits for cleaner history when merging.

**Explanation**:
- Clear commit messages improve traceability.
- Branching strategies streamline collaboration.
- Security practices prevent leaks of credentials.
- Collaborative workflows ensure code quality and team alignment.

---

## 20. **Cheat Codes**

```bash
// Show changes in one line
git diff --stat

// Clean untracked files
git clean -fd

// Alias common commands
git config --global alias.co checkout
git config --global alias.br branch
git config --global alias.ci commit

// Show who changed a line
git blame <file_name>

// Stash only staged changes
git stash push --staged
```

**Explanation**:
- `git diff --stat` summarizes changes concisely.
- `git clean` removes untracked files, useful for resets.
- Aliases reduce typing for frequent commands.
- `git blame` tracks authorship for debugging.
- Stashing staged changes isolates specific work.