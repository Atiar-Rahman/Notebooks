Here is a structured Git command guide from **basic to advanced**, with explanations and examples.

# Git Repository Creation

### Initialize a New Repository

```bash
git init
```

Creates a new Git repository in the current directory.

### Clone an Existing Repository

```bash
git clone https://github.com/user/repo.git
```

Downloads a remote repository to your local machine.

Clone into a specific folder:

```bash
git clone https://github.com/user/repo.git myproject
```

---

# Check Repository Status

### Check Current Status

```bash
git status
```

Shows:

- Modified files
    
- Untracked files
    
- Staged files
    
- Current branch
    

### Short Status

```bash
git status -s
```

Example:

```text
M file.txt
?? newfile.txt
```

---

# Git Configuration

### Set Username

```bash
git config --global user.name "Your Name"
```

### Set Email

```bash
git config --global user.email "your@email.com"
```

### View Configuration

```bash
git config --list
```

---

# Add Files

### Add Specific File

```bash
git add file.txt
```

### Add Multiple Files

```bash
git add file1.txt file2.txt
```

### Add All Files

```bash
git add .
```

### Add All Changes

```bash
git add -A
```

---

# Commit Changes

### Commit Staged Changes

```bash
git commit -m "Initial commit"
```

### Commit All Modified Files

```bash
git commit -am "Update files"
```

### Amend Last Commit

```bash
git commit --amend -m "New commit message"
```

---

# View Commit History

### Show Full Log

```bash
git log
```

### One-Line Log

```bash
git log --oneline
```

Example:

```text
a1b2c3d Added login page
e4f5g6h Fixed bug
```

### Graph View

```bash
git log --oneline --graph --all
```

### Last 5 Commits

```bash
git log -5
```

### Show Commit Details

```bash
git show COMMIT_ID
```

---

# Branch Management

### Create Branch

```bash
git branch feature
```

### List Branches

```bash
git branch
```

### Switch Branch

```bash
git checkout feature
```

or

```bash
git switch feature
```

### Create and Switch

```bash
git checkout -b feature
```

or

```bash
git switch -c feature
```

### Delete Branch

```bash
git branch -d feature
```

### Force Delete

```bash
git branch -D feature
```

---

# Merge Branches

### Merge Branch

```bash
git merge feature
```

Example:

```bash
git checkout main
git merge feature
```

### Abort Merge

```bash
git merge --abort
```

---

# Remote Repository

### Add Remote

```bash
git remote add origin https://github.com/user/repo.git
```

### View Remotes

```bash
git remote -v
```

### Change Remote URL

```bash
git remote set-url origin https://github.com/user/newrepo.git
```

### Remove Remote

```bash
git remote remove origin
```

---

# Push Changes

### First Push

```bash
git push -u origin main
```

### Normal Push

```bash
git push
```

### Push Specific Branch

```bash
git push origin feature
```

### Force Push

```bash
git push --force
```

⚠ Use carefully.

---

# Pull Changes

### Pull Latest Changes

```bash
git pull
```

### Pull Specific Branch

```bash
git pull origin main
```

### Fetch Without Merge

```bash
git fetch
```

### Fetch All Remotes

```bash
git fetch --all
```

---

# Compare Changes

### Show Unstaged Changes

```bash
git diff
```

### Show Staged Changes

```bash
git diff --staged
```

### Compare Branches

```bash
git diff main feature
```

### Compare Commits

```bash
git diff COMMIT1 COMMIT2
```

---

# Undo Changes

### Restore File

```bash
git restore file.txt
```

### Unstage File

```bash
git restore --staged file.txt
```

### Reset Last Commit (Keep Changes)

```bash
git reset --soft HEAD~1
```

### Reset Last Commit (Remove Changes)

```bash
git reset --hard HEAD~1
```

### Reset to Specific Commit

```bash
git reset --hard COMMIT_ID
```

---

# Stash Commands

### Save Changes

```bash
git stash
```

### Save with Message

```bash
git stash push -m "Work in progress"
```

### List Stashes

```bash
git stash list
```

### Apply Latest Stash

```bash
git stash apply
```

### Apply and Remove

```bash
git stash pop
```

### Delete Stash

```bash
git stash drop stash@{0}
```

---

# Tag Management

### Create Tag

```bash
git tag v1.0
```

### Annotated Tag

```bash
git tag -a v1.0 -m "Version 1.0"
```

### List Tags

```bash
git tag
```

### Push Tag

```bash
git push origin v1.0
```

### Push All Tags

```bash
git push --tags
```

---

# Rebase

### Rebase Current Branch

```bash
git rebase main
```

### Interactive Rebase

```bash
git rebase -i HEAD~5
```

Used for:

- Squash commits
    
- Rename commits
    
- Remove commits
    

### Abort Rebase

```bash
git rebase --abort
```

---

# Cherry Pick

Apply a commit from another branch:

```bash
git cherry-pick COMMIT_ID
```

---

# Clean Untracked Files

### Preview

```bash
git clean -n
```

### Delete Untracked Files

```bash
git clean -f
```

### Delete Files and Directories

```bash
git clean -fd
```

---

# Blame

Show who changed each line:

```bash
git blame file.txt
```

---

# Search

### Search Commit Messages

```bash
git log --grep="bug"
```

### Search Code

```bash
git grep "function_name"
```

---

# Git Aliases

### Create Alias

```bash
git config --global alias.st status
```

Use:

```bash
git st
```

Common aliases:

```bash
git config --global alias.co checkout
git config --global alias.br branch
git config --global alias.cm commit
git config --global alias.lg "log --oneline --graph --all"
```

---

# Most Common Daily Workflow

```bash
# Check status
git status

# Add changes
git add .

# Commit
git commit -m "Added new feature"

# Pull latest updates
git pull origin main

# Push changes
git push origin main
```

# Advanced Workflow Example

```bash
# Create feature branch
git checkout -b feature-login

# Work on code
git add .
git commit -m "Created login page"

# Update from main
git checkout main
git pull origin main

# Merge feature
git checkout feature-login
git merge main

# Push feature
git push origin feature-login

# Create Pull Request on GitHub
```

## Quick Git Cheat Sheet

| Command             | Purpose            |
| ------------------- | ------------------ |
| `git init`          | Create repository  |
| `git clone`         | Copy repository    |
| `git status`        | Check status       |
| `git add .`         | Stage files        |
| `git commit -m`     | Save changes       |
| `git log --oneline` | View history       |
| `git branch`        | List branches      |
| `git checkout -b`   | Create branch      |
| `git merge`         | Merge branch       |
| `git pull`          | Get updates        |
| `git push`          | Upload changes     |
| `git stash`         | Temporary save     |
| `git reset`         | Undo commits       |
| `git rebase`        | Rewrite history    |
| `git cherry-pick`   | Copy commit        |
| `git tag`           | Create release tag |

This covers most Git commands used by developers from beginner to advanced levels.

------------
If you **deleted a file after committing** and want to understand what Git does or how to recover it, here are the common cases:

### 1. File deleted locally, but not committed yet

Check status:

```bash
git status
```

Restore the file from the last commit:

```bash
git restore filename.txt
```

Or restore all deleted files:

```bash
git restore .
```

---

### 2. File deleted and committed, but not pushed

Find the previous commit:

```bash
git log --oneline
```

Restore the file from the previous commit:

```bash
git checkout HEAD~1 -- filename.txt
```

Then commit the restoration:

```bash
git add filename.txt
git commit -m "Restore deleted file"
```

---

### 3. File deleted, committed, and pushed

Restore from an older commit:

```bash
git log -- filename.txt
```

Find the commit where the file existed, then:

```bash
git checkout <commit_id> -- filename.txt
```

Commit and push:

```bash
git add filename.txt
git commit -m "Restore deleted file"
git push
```

---

### 4. Prevent Git from deleting a tracked file

If you accidentally delete a tracked file, Git will show:

```bash
git status
```

Example:

```text
deleted: config.json
```

To cancel the deletion:

```bash
git restore config.json
```

---

### 5. Remove a file from Git but keep it on disk

```bash
git rm --cached filename.txt
git commit -m "Stop tracking file"
```

The file remains in your folder but Git no longer tracks it.

---

### 6. Undo the last commit that deleted files

Keep changes:

```bash
git reset --soft HEAD~1
```

Or completely undo the commit:

```bash
git reset --hard HEAD~1
```

⚠️ `--hard` permanently discards uncommitted changes.

If you tell me:

- Was the file **deleted before or after commit**?
    
- Was the commit **pushed to GitHub**?
    
- Do you want to **recover the file** or **remove it from Git history**?
    

I can give the exact command.





-----
হ্যাঁ, Git-এ **লোকাল কমিট করার পর কিন্তু push করার আগে** কমিট বা ফাইল ডিলিট/পরিবর্তন করা সহজ। তবে **push করার পরে** সেই commit history পরিবর্তন করা উচিত নয়, বিশেষ করে যদি অন্যরাও সেই repository ব্যবহার করে।

### Push করার আগে

শেষ commit মুছে ফেলতে:

```bash
git reset --soft HEAD~1
```

অথবা commit এবং changes দুটোই মুছে ফেলতে:

```bash
git reset --hard HEAD~1
```

নির্দিষ্ট ফাইল restore করতে:

```bash
git restore filename.txt
```

### Push করার পরে

Push হয়ে গেলে commit history পরিবর্তন করলে remote repository-র সাথে conflict হতে পারে।

তবুও জোর করে history rewrite করতে চাইলে:

```bash
git reset --hard HEAD~1
git push --force
```

⚠️ `git push --force` খুব সতর্কতার সাথে ব্যবহার করতে হবে, কারণ এটি remote history overwrite করে।

### নিরাপদ উপায় (Push-এর পরে)

কোনো commit undo করতে:

```bash
git revert <commit_id>
git push
```

এটি নতুন একটি commit তৈরি করে আগের commit-এর পরিবর্তনগুলো বাতিল করে, history নষ্ট না করেই।

**সারাংশ:**

- Push করার আগে → `reset`, `restore`, `amend` ব্যবহার করে সহজে পরিবর্তন/ডিলিট করা যায়।
    
- Push করার পরে → সাধারণত `revert` ব্যবহার করা ভালো।
    
- Push করার পরে `reset + push --force` সম্ভব, কিন্তু সতর্কতার সাথে।







-----------
নিচে প্রতিটি কমান্ড **কখন ব্যবহার করবেন, কী করে, এবং উদাহরণসহ** দেখানো হলো।

# 1. Push করার আগে: `git reset`

## শেষ commit বাতিল, কিন্তু file changes রেখে দিতে

```bash
git reset --soft HEAD~1
```

উদাহরণ:

```bash
git add .
git commit -m "wrong commit"
```

ভুল commit হয়েছে।

```bash
git reset --soft HEAD~1
```

ফলাফল:

- Commit মুছে যাবে
    
- File changes থাকবে
    
- Files staged অবস্থায় থাকবে
    

---

## শেষ commit এবং staging বাতিল

```bash
git reset --mixed HEAD~1
```

অথবা

```bash
git reset HEAD~1
```

ফলাফল:

- Commit মুছে যাবে
    
- Changes থাকবে
    
- Staging থেকে বের হয়ে যাবে
    

---

## সবকিছু মুছে ফেলতে

```bash
git reset --hard HEAD~1
```

ফলাফল:

- Commit মুছে যাবে
    
- File changes মুছে যাবে
    
- Recover করা কঠিন
    

⚠️ সাবধান।

---

# 2. Push করার আগে: `git restore`

## একটি file আগের অবস্থায় ফেরত আনা

```bash
git restore app.js
```

যদি file edit করে থাকেন:

```bash
echo "wrong code" >> app.js
```

ফিরিয়ে আনুন:

```bash
git restore app.js
```

---

## সব file restore

```bash
git restore .
```

---

## Staging থেকে file সরানো

```bash
git restore --staged app.js
```

Equivalent:

```bash
git reset app.js
```

---

# 3. Push করার আগে: `git commit --amend`

## Commit message পরিবর্তন

ভুল:

```bash
git commit -m "frist commit"
```

সংশোধন:

```bash
git commit --amend -m "first commit"
```

---

## নতুন file একই commit-এ যোগ করা

```bash
git add newfile.txt
git commit --amend
```

ফলাফল:

- নতুন commit তৈরি হবে না
    
- আগের commit update হবে
    

---

# 4. Push করার পরে: `git revert`

সবচেয়ে নিরাপদ পদ্ধতি।

ধরুন:

```bash
git log --oneline
```

Output:

```text
a1b2c3 Added login
d4e5f6 Fixed bug
```

`Added login` commit undo করতে:

```bash
git revert a1b2c3
```

তারপর:

```bash
git push
```

ফলাফল:

- History থাকবে
    
- নতুন commit তৈরি হবে
    
- আগের commit-এর effect cancel হবে
    

---
এখন সমস্যাটা পরিষ্কার।

আপনার `git log` দেখাচ্ছে:

```text
commit fb2033368579a7ad0ee5eab110614bd87852102b (HEAD -> master)
    procto-mart project ses s setup
```

শুধু **একটাই commit** আছে। তাই:

```bash
git reset --soft HEAD~1
```

কাজ করবে না, কারণ `HEAD~1` বলতে "HEAD-এর আগের commit" বোঝায়, আর আগের কোনো commit নেই।

এখন আপনি কী করতে চান তার উপর সমাধান নির্ভর করছে।

### যদি শেষ commit undo করতে চান

একটা মাত্র commit থাকলে:

```bash
git update-ref -d HEAD
```

অথবা

```bash
git reset $(git hash-object -t tree /dev/null)
```

কিন্তু সাধারণত এটা দরকার হয় না।

### যদি কিছু file Git-এ না পাঠাতে চান

প্রথমে বলুন:

* GitHub-এ কি `git push` করেছেন?
* নাকি শুধু local commit করেছেন?

#### Local commit হয়েছে, push হয়নি

তাহলে নতুন commit করে unwanted file remove করতে পারেন:

```bash
git rm --cached db.sqlite3
```

`.gitignore`-এ যোগ করুন:

```gitignore
db.sqlite3
```

তারপর:

```bash
git add .gitignore
git commit -m "Remove database file from repository"
```

#### যদি এখনও GitHub-এ push না করে থাকেন

সবচেয়ে ভালো হবে:

```bash
git rm --cached db.sqlite3
echo "db.sqlite3" >> .gitignore
git add .gitignore
git commit --amend
```

এতে শেষ commit-টাই update হয়ে যাবে।

### আমি জানতে চাই

এই command-এর output দিন:

```bash
git remote -v
```

আর বলুন:

> "আমি db.sqlite3 git থেকে বাদ দিতে চাই"

নাকি

> "আমি পুরো শেষ commit delete করতে চাই"

তাহলে exact command দেব।

এটার মানে হলো `find` অনেক `__pycache__` folder খুঁজে পেয়েছে, কিন্তু সেগুলোর সব Git track করছে না। তাই `git rm --cached` সেগুলো খুঁজে পাচ্ছে না।

প্রথমে দেখে নিন Git আসলে কী track করছে:

```bash
git ls-files | grep __pycache__
```

এবং:

```bash
git ls-files | grep .pro_env
```

যদি `.pro_env` ভুল করে commit করে থাকেন, তাহলে সবচেয়ে সহজ উপায়:

```bash
git rm -r --cached .pro_env
```

তারপর `.gitignore`-এ যোগ করুন:

```gitignore
.pro_env/
__pycache__/
*.py[cod]
db.sqlite3
```

এরপর:

```bash
git add .gitignore
git status
```

`git status`-এ যা দেখাবে সেটাই Git থেকে remove হওয়ার জন্য staged আছে।

যেহেতু আপনার repository-তে এখন মাত্র **একটা commit** আছে, চাইলে commit amend করে history পরিষ্কার রাখতে পারেন:

```bash
git commit --amend
```

এখন একটা command চালিয়ে output দিন:

```bash
git ls-files | head -50
```

অথবা আরও ভালো:

```bash
git ls-files | grep -E "(\.pro_env|__pycache__|db.sqlite3)"
```

তাহলে আমি দেখতে পারব কোন unwanted fileগুলো আসলেই Git-এর মধ্যে আছে।


এখন পরিষ্কার যে `__pycache__` ফাইলগুলো Git track করছে।

সবগুলো tracking থেকে সরাতে:

```bash
git ls-files | grep __pycache__ | xargs git rm --cached
```

অথবা:

```bash
git rm --cached config/__pycache__/*
git rm --cached core/__pycache__/*
git rm --cached users/__pycache__/*
git rm --cached users/migrations/__pycache__/*
```

তারপর `.gitignore`-এ নিশ্চিত করুন এগুলো আছে:

```gitignore
# Virtual Environment
.pro_env/

# Python cache
__pycache__/
*.py[cod]

# Django
db.sqlite3

# Environment variables
.env
```

এরপর:

```bash
git add .gitignore
git status
```

যদি `deleted:` হিসেবে `__pycache__` ফাইলগুলো দেখায়, তাহলে ঠিক আছে। এগুলো শুধু Git থেকে remove হবে, আপনার disk থেকে delete হবে না।

তারপর:

```bash
git commit --amend
```

যেহেতু আপনার repository-তে মাত্র ১টা commit আছে, `--amend` করলে আগের commit-টাই update হবে এবং `__pycache__`, `.pro_env`, `db.sqlite3` ছাড়া clean commit পাবেন।

এখন `git status`-এর output দেখান। বিশেষ করে `.pro_env` এখনও tracked আছে কিনা সেটা দেখতে চাই। Run করুন:

```bash
git ls-files | grep .pro_env | head
```

এবং output paste করুন।


# 5. Push করার পরে: `reset + force push`

ধরুন:

```text
A
B
C
```

C commit মুছে ফেলতে:

```bash
git reset --hard HEAD~1
```

এখন local:

```text
A
B
```

Remote-এ এখনও:

```text
A
B
C
```

Remote update করতে:

```bash
git push --force
```

---

## আরও নিরাপদ force push

```bash
git push --force-with-lease
```

এটি অন্য কারও নতুন commit থাকলে overwrite করবে না।

---

# Practical Examples

### শেষ commit-এর message ভুল

```bash
git commit --amend -m "Correct message"
```

---

### Commit হয়েছে, push হয়নি

```bash
git reset --soft HEAD~1
```

---

### Push হয়ে গেছে, commit undo করতে হবে

```bash
git revert <commit-id>
git push
```

---

### Push হয়ে গেছে, কিন্তু history থেকেই commit মুছতে হবে

```bash
git reset --hard HEAD~1
git push --force-with-lease
```

---

# Rule of Thumb

|Situation|Command|
|---|---|
|File change বাতিল|`git restore file`|
|Staging থেকে remove|`git restore --staged file`|
|Last commit edit|`git commit --amend`|
|Commit undo (not pushed)|`git reset --soft HEAD~1`|
|Commit delete completely|`git reset --hard HEAD~1`|
|Undo pushed commit safely|`git revert commit_id`|
|Rewrite pushed history|`git reset + git push --force-with-lease`|

**টিমে কাজ করলে push হয়ে যাওয়া commit-এর জন্য `git revert` ব্যবহার করা ভালো। `git push --force` সাধারণত ব্যক্তিগত branch বা বিশেষ প্রয়োজনে ব্যবহার করা হয়।**







----------
Git-এ **version ঠিকভাবে রাখার সবচেয়ে প্রচলিত উপায় হলো Tags এবং Semantic Versioning (SemVer)** ব্যবহার করা।

## 1. Semantic Versioning (SemVer)

ফরম্যাট:

```text
MAJOR.MINOR.PATCH
```

উদাহরণ:

```text
v1.0.0
v1.0.1
v1.1.0
v2.0.0
```

### PATCH (v1.0.1)

Bug fix হলে:

```text
v1.0.0 → v1.0.1
```

### MINOR (v1.1.0)

নতুন feature যোগ হলে:

```text
v1.0.0 → v1.1.0
```

### MAJOR (v2.0.0)

পুরনো API বা functionality break হলে:

```text
v1.5.0 → v2.0.0
```

---

## 2. Git Tag ব্যবহার

Release version mark করার জন্য:

```bash
git tag -a v1.0.0 -m "First stable release"
```

Tags দেখুন:

```bash
git tag
```

Output:

```text
v1.0.0
v1.1.0
v2.0.0
```

---

## 3. Tag Push করা

Commit push করার পর:

```bash
git push origin v1.0.0
```

সব tag push করতে:

```bash
git push --tags
```

---

## 4. Release Workflow Example

ধরুন project শুরু করেছেন:

```bash
git init
git add .
git commit -m "Initial project"
```

প্রথম stable release:

```bash
git tag -a v1.0.0 -m "Version 1.0.0"
git push origin main
git push --tags
```

Bug fix:

```bash
git add .
git commit -m "Fix login bug"

git tag -a v1.0.1 -m "Bug fix release"
git push origin main
git push --tags
```

New feature:

```bash
git add .
git commit -m "Add payment gateway"

git tag -a v1.1.0 -m "Payment feature"
git push --tags
```

---

## 5. Current Version দেখতে

সর্বশেষ tag:

```bash
git describe --tags
```

অথবা:

```bash
git tag --sort=-version:refname
```

---

## 6. Production Branch Strategy

অনেক টিম এই pattern ব্যবহার করে:

```text
main      → Production stable code
develop   → Development
feature/* → New features
hotfix/*  → Emergency fixes
```

উদাহরণ:

```text
main      -> v1.0.0
main      -> v1.0.1
main      -> v1.1.0
main      -> v2.0.0
```

প্রতিটি release-এ একটি tag থাকে।

---

## Recommended Practice

1. প্রতিটি meaningful release-এ tag দিন।
    
2. `main` branch-এ শুধু stable code রাখুন।
    
3. Version format ব্যবহার করুন:
    
    - `v1.0.0`
        
    - `v1.0.1`
        
    - `v1.1.0`
        
    - `v2.0.0`
        
4. GitHub/GitLab Release তৈরি করুন tag-এর উপর ভিত্তি করে।
    

এভাবে ১ বছর পরেও আপনি সহজে বলতে পারবেন: "এই bug কোন version-এ এসেছে?" বা "v1.1.0-এর code checkout করতে হবে"—

```bash
git checkout v1.1.0
```

এবং Git সেই version-এর exact source code দেখাবে।

------

Version-wise deployment-এর জন্য Git খুব ভালোভাবে ব্যবহার করা যায়। সাধারণত **Git Tags + Branch Strategy + CI/CD** একসাথে ব্যবহার করা হয়।

## সহজ Version-Based Deployment Workflow

### Step 1: Code Commit করুন

```bash
git add .
git commit -m "Add payment feature"
```

### Step 2: Version Tag তৈরি করুন

ধরুন এটি প্রথম production release:

```bash
git tag -a v1.0.0 -m "Production release v1.0.0"
```

Push করুন:

```bash
git push origin main
git push origin v1.0.0
```

অথবা

```bash
git push --tags
```

---

### Step 3: Server-এ নির্দিষ্ট Version Deploy

সার্ভারে:

```bash
git clone <repo-url>
cd project
```

সব tags আনুন:

```bash
git fetch --tags
```

v1.0.0 deploy করতে:

```bash
git checkout v1.0.0
```

এখন server-এ v1.0.0 version চলছে।

---

## New Release

নতুন feature যোগ করলেন:

```bash
git add .
git commit -m "Add notification feature"
```

নতুন version:

```bash
git tag -a v1.1.0 -m "Notification feature release"
git push origin main
git push --tags
```

Server-এ:

```bash
git fetch --tags
git checkout v1.1.0
```

---

## Rollback (খুব গুরুত্বপূর্ণ)

ধরুন v1.1.0-এ bug আছে।

আগের stable version-এ ফিরে যান:

```bash
git checkout v1.0.0
```

Deploy restart করুন।

এটাই version-based deployment-এর সবচেয়ে বড় সুবিধা।

---

## Branch Strategy

অনেক টিম:

```text
main      -> Production
develop   -> Testing/Staging
feature/* -> New Features
```

Workflow:

```text
feature/login
      ↓
develop
      ↓
main
      ↓
v1.0.0 tag
      ↓
Deploy
```

---

## Release History

Tags দেখুন:

```bash
git tag
```

Output:

```text
v1.0.0
v1.0.1
v1.1.0
v2.0.0
```

Specific version inspect করুন:

```bash
git show v1.0.0
```

---

## CI/CD Example

যদি GitHub Actions, GitLab CI বা Jenkins ব্যবহার করেন:

Tag push হলেই deployment trigger করতে পারেন।

উদাহরণ:

```bash
git tag -a v2.0.0 -m "Release v2.0.0"
git push origin v2.0.0
```

CI/CD detect করবে:

```text
v2.0.0 tag created
↓
Build
↓
Test
↓
Deploy Production
```

---

## Real-World Recommended Structure

```text
main
├── v1.0.0
├── v1.0.1
├── v1.1.0
├── v1.2.0
└── v2.0.0
```

Commands:

```bash
# Create release
git tag -a v1.0.0 -m "Release"

# Push release
git push --tags

# Deploy specific version
git checkout v1.0.0

# Rollback
git checkout v0.9.0
```

### Best Practice

- `main` = production-ready code
    
- প্রতিটি release-এ tag দিন
    
- Production deploy করুন tag থেকে, branch থেকে নয়
    
- Rollback করুন tag change করে
    
- CI/CD-তে tag-triggered deployment ব্যবহার করুন
    

এভাবে আপনি `v1.0.0`, `v1.1.0`, `v2.0.0` ইত্যাদি version অনুযায়ী deploy, rollback এবং release management খুব সহজে করতে পারবেন।


