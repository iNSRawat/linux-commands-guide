# Git & GitHub Commands

Essential Git commands for version control and GitHub workflows.

## Git Basics

### Setup
```bash
git config --global user.name "Your Name"
git config --global user.email "your@email.com"
git config --list
```

### Initialize Repository
```bash
git init
git clone https://github.com/user/repo.git
```

### Basic Workflow
```bash
git status
git add file.txt
git add .
git commit -m "Commit message"
git push origin main
git pull origin main
```

## Branching

```bash
git branch
git branch feature-branch
git checkout feature-branch
git checkout -b new-branch
git merge feature-branch
git branch -d feature-branch
```

## Remote Operations

```bash
git remote -v
git remote add origin https://github.com/user/repo.git
git push -u origin main
git fetch origin
git pull
```

## History & Logs

```bash
git log
git log --oneline
git log --graph --decorate
git diff
git show commit-hash
```

## Undoing Changes

```bash
git reset HEAD file.txt
git checkout -- file.txt
git revert commit-hash
git reset --hard HEAD~1
```

## GitHub Specific

### SSH Setup
```bash
ssh-keygen -t ed25519 -C "your@email.com"
cat ~/.ssh/id_ed25519.pub
# Add to GitHub Settings > SSH Keys
```

### Clone with SSH
```bash
git clone git@github.com:user/repo.git
```

---

---

## Additional Git Commands

### git stash - Save Work Temporarily
Stash your uncommitted changes so you can switch branches cleanly.
```bash
git stash                           # Save current changes
git stash save "work in progress"   # Save with a name
git stash list                      # See all stashes
git stash pop                       # Restore latest stash & remove it
git stash apply                     # Restore latest stash & keep it
git stash apply stash@{2}           # Restore a specific stash
git stash drop stash@{0}            # Delete a specific stash
git stash clear                     # Delete all stashes
```

### git log - View History (All Variants)
```bash
git log                             # Full log
git log --oneline                   # One line per commit
git log --oneline --graph           # With branch graph
git log --oneline --graph --all     # All branches graph
git log --author="NSRawat"          # Commits by author
git log --since="2 weeks ago"       # Recent commits
git log -p file.txt                 # History of a specific file
git log --stat                      # Show files changed per commit
git shortlog -sn                    # Commit count by author
```

### git diff - See Changes
```bash
git diff                            # Unstaged changes
git diff --staged                   # Staged changes (ready to commit)
git diff HEAD~1                     # Changes since last commit
git diff branch1 branch2            # Compare two branches
git diff commit1 commit2            # Compare two commits
```

### git tag - Mark Releases
```bash
git tag                             # List all tags
git tag v1.0.0                      # Create lightweight tag
git tag -a v1.0.0 -m "Release 1.0" # Annotated tag (recommended)
git push origin v1.0.0              # Push tag to GitHub
git push origin --tags              # Push all tags
git tag -d v1.0.0                   # Delete local tag
git push origin --delete v1.0.0    # Delete remote tag
```

### .gitignore - Ignore Files
Tell Git which files/folders to never track.
```bash
# Create .gitignore
nano .gitignore

# Common entries for DS/Python projects:
```
```
# Python
__pycache__/
*.py[cod]
*.pyo
*.pyd
.Python

# Virtual environments
venv/
env/
.venv/
ds-envs/

# Jupyter Notebooks
.ipynb_checkpoints/
*.ipynb_checkpoints

# Data files (often too large for GitHub)
data/
*.csv
*.xlsx
*.parquet
*.pkl
*.h5

# Models
models/
*.pt
*.pth
*.joblib

# Environment variables / secrets
.env
*.env
secrets.py

# OS files
.DS_Store
Thumbs.db

# IDE files
.vscode/
.idea/
```
```bash
# Check what Git is ignoring
git status --ignored
git check-ignore -v filename        # Why is this file ignored?

# Force add an ignored file (rarely needed)
git add -f file.txt
```

### git remote - Manage Remote Connections
```bash
git remote -v                               # List remotes
git remote add origin <url>                 # Add remote
git remote set-url origin <new-url>         # Change remote URL
git remote rename origin upstream           # Rename remote
git remote remove origin                    # Remove remote

# Fetch without merging
git fetch origin                            # Get updates, don't apply
git fetch --all                             # Fetch all remotes
```

### git cherry-pick - Apply Specific Commits
```bash
git cherry-pick abc1234             # Apply one commit to current branch
git cherry-pick abc1234 def5678    # Apply multiple commits
git cherry-pick --abort             # Cancel cherry-pick
```

### Useful Git Aliases (add to ~/.gitconfig)
```bash
git config --global alias.st status
git config --global alias.co checkout
git config --global alias.br branch
git config --global alias.lg "log --oneline --graph --all"
git config --global alias.unstage "reset HEAD --"

# Now you can use:
git st          # instead of git status
git lg          # instead of git log --oneline --graph --all
```

### SSH Troubleshooting for GitHub
```bash
# Test SSH connection
ssh -T git@github.com
# Expected: Hi username! You've successfully authenticated...

# If it fails, check your key is loaded
ssh-add -l

# Add key to agent
eval "$(ssh-agent -s)"
ssh-add ~/.ssh/id_ed25519

# Check your remote URL (should be git@, not https://)
git remote -v

# Switch from HTTPS to SSH
git remote set-url origin git@github.com:iNSRawat/repo-name.git
```

### Git Workflow for DS Projects (Step-by-Step)
```bash
# 1. Start a new project
git init my-ds-project
cd my-ds-project

# 2. Create .gitignore first
nano .gitignore   # add venv/, data/, *.pkl, .env etc.

# 3. Initial commit
git add .gitignore README.md
git commit -m "Initial commit with gitignore"

# 4. Connect to GitHub
git remote add origin git@github.com:iNSRawat/my-ds-project.git
git push -u origin main

# 5. Daily workflow
git pull                            # Always pull first
# ... make changes ...
git add .
git commit -m "Add feature X"
git push

# 6. Feature branch workflow
git checkout -b feature/churn-model
# ... work on feature ...
git add .
git commit -m "Add churn prediction model"
git push origin feature/churn-model
# Then create PR on GitHub
```

**Previous**: [Data Science Commands](04-data-science-commands.md)
