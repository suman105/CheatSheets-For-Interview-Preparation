# Git & GitHub Commands Guide

## 1. **Git Configuration**
- **For Current Configuration:**
    - `git config user.name` — Shows the current username.
    - `git config user.email` — Displays the current email address.

- **Set Global Configuration:**
    - `git config --global user.name "username"` — Sets your global username.
    - `git config --global user.email "email@example.com"` — Sets your global email.

## 2. **Initializing and Managing Git Repository**
- `git init` — Initializes a new Git repository.
- `git status` — Checks the status of your working directory and staging area.

## 3. **Cloning Repositories**
- **Cloning Public Repo:**
    - `git clone https://github.com/account/repo.git` — Clones a public repository.

- **Cloning Private Repo:**
    - To clone a private repository, you'll need a **Personal Access Token (PAT)**:
      - Go to GitHub Settings → Developer Settings → Personal Access Tokens → Create a token.
      - Copy the token (you won’t be able to see it again).
      - Clone the private repository using:
        - `git clone https://<PAT>@github.com/account/repo.git`

## 4. **Working with Staging and Commit**
- **Stage Files:**
    - `git add <file_name>` — Adds a specific file to the staging area.
    - `git add .` — Adds all modified files to the staging area.

- **Commit Changes:**
    - `git commit -m "Your commit message"` — Commits staged changes with a message.

- **View Commit History:**
    - `git log` — Shows the commit history of the repository.

## 5. **Pushing to GitHub**
- `git push -u origin main` — Pushes changes from the local `main` branch to the remote repository.
- If you're using the **master** branch:
    - `git push -u origin master` — Pushes changes to the remote `master` branch.

## 6. **Remote Branch Management**
- **Add Remote Repository:**
    - `git remote add <name> <url>` — Adds a remote repository.
    - `git remote add origin <url>` — Adds the default remote repository (usually called "origin").

- **View Remote Repositories:**
    - `git remote -v` — Shows the URLs of remote repositories associated with your local repository.

- **Rename Remote Branch:**
    - `git remote rename <old_name> <new_name>` — Renames a remote branch.

- **Remove Remote Branch:**
    - `git remote remove <name>` — Removes a remote branch.

## 7. **Working with Branches**
- **View Branches:**
    - `git branch` — Lists all branches in your local repository.

- **Create a New Branch:**
    - `git branch <branch_name>` — Creates a new branch.
    - `git switch <branch_name>` — Switches to the specified branch.
    - `git switch -c <branch_name>` — Creates and switches to a new branch.

- **Rename Current Branch:**
    - `git branch -m <new_name>` — Renames the current branch.

- **Delete a Branch:**
    - `git branch -d <branch_name>` — Deletes a local branch (use `-D` for force delete).

## 8. **Working with Remote and Local Branches**
- **Fetch Updates from Remote:**
    - `git fetch <remote> <branch>` — Fetches updates from a specific remote branch.
    - `git fetch` — Fetches updates from all branches in the remote repository.

- **Pull Updates to Working Directory:**
    - `git pull` — Fetches and merges updates from the remote repository into the working directory.

- **Checkout Remote Branch:**
    - `git checkout <branch_name>` — Switches to the specified branch.
    - `git checkout origin/<branch_name>` — Switches to a remote branch without affecting the working directory.

## 9. **Merging Branches**
- **Merge Branches:**
    - `git merge <branch_name>` — Merges the specified branch into the current branch.

- **Types of Merges:**
    - **Fast-Forward Merge**: When no divergent work exists, Git will perform a fast-forward merge.
    - **Merge with Conflicts**: If there are changes in both branches that conflict, you’ll need to manually resolve conflicts.

## 10. **Handling Merge Conflicts**
- When conflicts arise, Git will mark the conflict in the file. Open the file, resolve the conflict, and then add the resolved file to the staging area:
    - `git add <file_name>`
    - `git commit` — Finalize the merge after resolving conflicts.

## 11. **Push Changes to Remote**
- After merging or committing, push the changes to the remote repository:
    - `git push` — Pushes changes to the corresponding remote branch.

## 12. **Advanced Git Operations**
- **Rebase:**
    - `git rebase <branch_name>` — Re-applies commits from the current branch onto the specified branch.

- **Stash Changes:**
    - `git stash` — Temporarily saves changes that are not yet committed.
    - `git stash pop` — Restores the saved changes from the stash.

- **Tagging:**
    - `git tag <tag_name>` — Creates a tag at the current commit.
    - `git tag -a <tag_name> -m "message"` — Creates an annotated tag with a message.
    - `git push origin <tag_name>` — Pushes the tag to the remote repository.

## 13. **Resetting and Undoing Changes**
- **Undo Changes in Working Directory:**
    - `git checkout -- <file_name>` — Reverts changes in a specific file.
    - `git reset` — Removes changes from the staging area.

- **Undo the Last Commit:**
    - `git reset --soft HEAD~1` — Moves the HEAD back but keeps changes in the staging area.
    - `git reset --hard HEAD~1` — Removes the last commit and all changes (dangerous operation).
