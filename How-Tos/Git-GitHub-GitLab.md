# Git, GitHub, and GitLab

## Change Default Branch Name

Example how to change default branch from `master` to `main`.

### Contributor Renaming Branches

```bash
git branch -m master main
git push -u origin main
# At git server change default branch name from master to main
# At git server add protected branch main
# At git server remove protected branch master
git push origin --delete master
```

### Other Contributors

```bash
# Switch to the "master" branch:
git checkout master

# Rename it to "main":
git branch -m master main

# Get the latest commits (and branches!) from the remote:
git fetch

# Remove the existing tracking connection with "origin/master":
git branch --unset-upstream

# Create a new tracking connection with the new "origin/main" branch:
git branch -u origin/main
```

## GitLab GitHub Synchronization

How to create working GitLab to GitHub repository synchronization.

- Have or create GitHub token named `GitLab GitHub Sync` with scopes:
  - repo
    - repo:status
    - repo_deployment
    - public_repo
    - repo:invite
    - security_events
  - workflow
  - write:packages
    - read:packages
  - delete:packages
- Have or create GitLab repository
- Have or create GitHub repository
- Set up GitLab GitHub synchronization
  - Git repository URL: **[https://user@github.com/org/repo.git](https://user@github.com/org/repo.git)**
  - Password: **`GitLab GitHub Sync` token**
  - Keep divergent refs: **on**
  - Mirror only protected branches: **on**

## Sources

- [Git Tower: Git FAQ - How to Rename the master branch to main in Git](https://www.git-tower.com/learn/git/faq/git-rename-master-to-main/)
- [GitLab Docs: Repository mirroring](https://docs.gitlab.com/ee/user/project/repository/repository_mirroring.html)
