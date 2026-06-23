[https://git-scm.com/book/en/v2](https://git-scm.com/book/en/v2)

| Method                | Best For...                      | How it Works                                                                                                                 |
| --------------------- | -------------------------------- | ---------------------------------------------------------------------------------------------------------------------------- |
| **Shared Repository** | Private teams or small groups    | The owner adds you as a collaborator. You get direct push/pull access to the repository.                                     |
| **Fork & Pull**       | Open-source or external projects | You fork the repository (copy it to your account), make changes, and submit a pull request to the original repository owner. |

### Key Difference

* **Shared Repository** → Direct access to the same repository.
* **Fork & Pull** → Work on your own copied repository first, then request changes to be merged.

----------
# Shared Repository Workflow (Step by Step)

## 1. Repository Owner Creates a Repository

A project owner creates a repository on [GitHub](https://github.com/?utm_source=chatgpt.com).

Example:

- Repository Name: `AI-CCTV-Project`
    

---

## 2. Owner Adds Collaborators

The repository owner gives team members access.

### Steps:

1. Open the repository
    
2. Go to **Settings**
    
3. Click **Collaborators and teams**
    
4. Click **Add people**
    
5. Enter collaborator’s GitHub username
    
6. Send invitation
    

The collaborator receives an invitation and accepts it.

---

## 3. Collaborator Clones the Repository

After access is granted, collaborators copy the repository to their computer.

### Command:

```bash
git clone https://github.com/username/repository-name.git
```

Example:

```bash
git clone https://github.com/team/AI-CCTV-Project.git
```

This downloads the project locally.

---

## 4. Open Project Locally

Move into the project folder.

```bash
cd AI-CCTV-Project
```

Now the collaborator can edit files.

---

## 5. Create or Modify Files

Examples:

- Add source code
    
- Fix bugs
    
- Update README
    
- Add datasets or documentation
    

---

## 6. Check Changed Files

See modified files before saving changes.

```bash
git status
```

---

## 7. Add Changes to Staging Area

Prepare files for commit.

```bash
git add .
```

Or add a specific file:

```bash
git add app.py
```

---

## 8. Commit Changes

Save changes with a message.

```bash
git commit -m "Added login feature"
```

A commit works like a project snapshot.

---

## 9. Push Changes to Shared Repository

Upload changes directly to the main repository.

```bash
git push origin main
```

Now all collaborators can access the updated code.

---

## 10. Other Team Members Pull Latest Changes

Team members download the newest updates.

```bash
git pull origin main
```

This keeps everyone synchronized.

---

# Complete Flow Diagram

```text
Owner Creates Repo
        ↓
Owner Adds Collaborators
        ↓
Collaborator Clones Repo
        ↓
Edit Files Locally
        ↓
git add
        ↓
git commit
        ↓
git push
        ↓
Repository Updated
        ↓
Other Members git pull
```

# Advantages of Shared Repository

- Faster collaboration
    
- Direct push access
    
- Easy for small/private teams
    
- Simple workflow
    
- Good for academic/team projects
    

# Disadvantages

- Risk of overwriting code
    
- Everyone has write access
    
- Mistakes can directly affect the main repository
    
- Requires team coordination
    

# Best Use Cases

- Final year projects
    
- Private company teams
    
- Small developer groups
    
- Trusted collaborators

---------
# How to Solve Shared Repository Disadvantages

| Disadvantage                                         | Solution                                                                                                                                                                                                                                                                                       |
| ---------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Risk of overwriting code**                         | Use separate branches for each feature or developer instead of working directly on `main`. Example: `feature-login`, `bugfix-camera`.                                                                                                                                                          |
| **Everyone has write access**                        | Give limited permissions. Only trusted members should push to the `main` branch. Use branch protection rules.                                                                                                                                                                                  |
| **Mistakes can directly affect the main repository** | Require code reviews and pull requests before merging into `main`. Also use backups and version control history.                                                                                                                                                                               |
| **Requires team coordination**                       | Use task management and communication tools like [GitHub Projects](https://github.com/features/issues?utm_source=chatgpt.com), [Trello](https://trello.com?utm_source=chatgpt.com), or [Slack](https://slack.com?utm_source=chatgpt.com). Team members should regularly sync using `git pull`. |

# Best Practice Workflow

```text
main branch (stable)
    ↑
Pull Request + Review
    ↑
Developer Branches
(feature-login, feature-ui, etc.)
```

# Recommended Team Rules

## 1. Never Work Directly on `main`

Create a new branch:

```bash
git checkout -b feature-authentication
```

---

## 2. Pull Latest Changes Before Starting

```bash
git pull origin main
```

This reduces merge conflicts.

---

## 3. Commit Frequently

```bash
git commit -m "Fixed login validation"
```

Small commits are easier to manage and revert.

---

## 4. Use Pull Requests

Instead of direct pushing to `main`:

* Push branch
* Create Pull Request
* Review code
* Merge safely

---

## 5. Backup Important Versions

Create tags/releases:

```bash
git tag v1.0
```

---

## 6. Resolve Merge Conflicts Carefully

When conflicts happen:

* Compare changed lines
* Keep correct code
* Test before pushing

---

# Professional Team Workflow

```text
Clone Repository
       ↓
Create New Branch
       ↓
Write Code
       ↓
Commit Changes
       ↓
Push Branch
       ↓
Create Pull Request
       ↓
Code Review
       ↓
Merge into Main
```

This workflow is commonly used in professional software development teams and helps avoid most shared repository problems.
# How to Apply Restrictions on the `main` Branch in GitHub

You can protect the `main` branch using **Branch Protection Rules** in [GitHub](https://github.com?utm_source=chatgpt.com).

This prevents:

* Direct pushes to `main`
* Accidental deletion
* Unreviewed code merging
* Force push mistakes

---

# Step-by-Step Setup

## 1. Open Your Repository

Go to your GitHub repository.

Example:

```text
https://github.com/username/project-name
```

---

## 2. Open Repository Settings

Click:

```text
Repository → Settings
```

---

## 3. Go to Branch Rules

From the left sidebar:

```text
Code and automation → Branches
```

---

## 4. Add Branch Protection Rule

Click:

```text
Add branch protection rule
```

---

## 5. Enter Branch Name

In:

```text
Branch name pattern
```

Type:

```text
main
```

---

# Important Restrictions to Enable

## ✅ Require a Pull Request Before Merging

Enable:

```text
Require a pull request before merging
```

Effect:

* Nobody can push directly to `main`
* All changes must go through Pull Requests

---

## ✅ Require Approvals

Enable:

```text
Require approvals
```

Set:

```text
1 approval
```

Effect:

* Another teammate must review before merge

---

## ✅ Require Status Checks (Optional)

Enable:

```text
Require status checks to pass before merging
```

Used for:

* CI/CD
* Automated testing
* Build verification

---

## ✅ Restrict Who Can Push

Enable:

```text
Restrict who can push to matching branches
```

Add:

* Specific users
* Team members

Effect:

* Only selected people can update `main`

---

## ✅ Block Force Push

Keep disabled:

```text
Allow force pushes ❌
```

Effect:

* Prevents history rewriting

---

## ✅ Prevent Branch Deletion

Enable:

```text
Do not allow deletion
```

Effect:

* Protects the `main` branch from accidental deletion

---

# Recommended Settings for Student/Small Teams

```text
✔ Require Pull Request
✔ Require 1 Approval
✔ Restrict Push Access
✔ Disable Force Push
✔ Prevent Deletion
```

---

# Safe Workflow After Protection

```text
Create Branch
      ↓
Write Code
      ↓
Push Branch
      ↓
Create Pull Request
      ↓
Review Approval
      ↓
Merge into main
```

---

# Example Commands

## Create New Branch

```bash
git checkout -b feature-login
```

---

## Push Branch

```bash
git push origin feature-login
```

---

## Create Pull Request

On GitHub:

```text
Compare & Pull Request
```

After approval:

```text
Merge Pull Request
```

---

# Result

After protection:

* `main` becomes stable
* Team collaboration becomes safer
* Accidental mistakes reduce
* Professional workflow is maintained
