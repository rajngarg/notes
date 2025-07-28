
## Git Commands

### Basic Operations
- `git init` – Initialize repository
- `git clone <repo>` – Clone remote repository
- `git status` – Show working directory status
- `git add <file>` – Stage changes
- `git commit -m "message"` – Commit changes
- `git push origin main` – Push to remote
- `git pull origin main` – Pull latest changes

### Branch Operations
- `git branch` / `git checkout -b <branch>` – Create/switch branches
- `git merge <branch>` – Merge branches
- `git stash` / `git stash pop` – Store/retrieve changes (removing)
- `git stash` / `git stash apply` – Store/retrieve changes (keeping)

### Remote Operations
- `git remote -v` – View remotes
- `git remote add origin <url>` – Add origin
- `git remote set-url origin <new-url>` – Change origin
- `git remote remove origin` – Remove origin
- `git push -u origin main` – Set upstream

### Rebase Operations
- `git rebase <branch>` – Rebase current branch onto another branch
- `git rebase -i HEAD~<n>` – Interactive rebase of last n commits
- `git rebase --continue` – Continue rebase after resolving conflicts
- `git rebase --abort` – Abort rebase and return to original state
- `git rebase --skip` – Skip current patch and continue rebasing
- `git pull --rebase` – Pull changes and rebase instead of merging
