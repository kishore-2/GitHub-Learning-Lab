# git notes:

### creating a file

```bash
    mkdir github-certifications-example
```

### generating the ssh keys

```bash
    ssh-keygen -t ed25519
    ssh -T git@github.com
```

### installing the github cli (gh)

```bash
    winget install --id GitHub.cli
    gh --version
    gh auth login
    gh auth status
    gh repo create github-example-demo --private --description "This is my GitHub CLI repo"
    gh repo view kishore-2/github-example-demo
    gh repo list

```

#### It asks

1. GitHub.com or Enterprise? → Choose GitHub.com
2. HTTPS or SSH? → Choose SSH (if you’ve set up SSH keys)
3. Login via Browser or PAT? → Choose Browser
4. Copy the one-time code & paste it into GitHub
5. Done! You're now authenticated.

## update the readme.md file

```bash
    git init
    git add README.md
    git commit -m "readme updated"
    git push
```

### Set main as Default for Future Repos:

```bash
    git config --global init.defaultBranch main

    git branch -m master main  # Rename branch locally
    git push -u origin main    # Push the renamed branch to GitHub
    git remote set-head origin -a  # Set the remote default branch to main

```
```bash
    git remote add origin git@github.com:kishore-2/github-examples.git
    git push -u origin main 
```

### if the default branch is master then

```bash
    git config --global init.defaultBranch main  # Set main as Default for Future Repos
    git branch -m master main  # Rename branch locally
    git push -u origin main    # Push the renamed branch to GitHub
    git remote set-head origin -a  # Set the remote default branch to main
```
