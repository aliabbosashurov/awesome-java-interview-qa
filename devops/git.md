# Git & Github

### 1. What is version control?

> A system that tracks changes to source code and enables collaboration, history, and controlled evolution of software.
> Version control records every modification made to files, allowing developers to review changes, revert to previous
> states, and collaborate without overwriting each other’s work.
> It provides a structured way to manage parallel development, code reviews, branching, and releases.

---

### 2. Why do we need version control?

> To prevent code conflicts, preserve history, and support parallel development in a controlled, safe manner.
> Without version control, teams risk overwriting each other’s changes, losing work, and creating unstable codebases.  
> A VCS provides structured workflows for branching, merging, reviewing, and releasing software. It enables rollback,
> experimentation, and consistent integration practices that scale with team size.

---

### 3. What are the main benefits of version control?

> Collaboration, history tracking, safe branching, rollback, and structured release management.
> Version control allows multiple developers to work concurrently without overwriting each other.  
> It maintains a full history of changes, supports branching strategies (GitFlow, Trunk-Based), and provides mechanisms
> for controlled merging and code review.  
> Teams can experiment safely, revert problematic changes, and maintain stable release branches.

---

### 4.What is the difference between centralized and distributed version control?

> Centralized VCS stores history on a single server; distributed VCS stores full histories on every developer’s machine.
> In centralized systems (e.g., SVN), the server is the single source of truth, and clients only pull the latest
> snapshot.
> All operations depend on network connectivity.  
> Distributed systems (e.g., Git) give every developer a full copy of the repository, enabling offline work, faster
> operations, and more resilient workflows.  
> Distributed VCS supports advanced branching, merging, and collaboration patterns.

---

### 5. What is Git?

> Git is a distributed version control system optimized for speed, integrity, and non-linear development.
> Git stores the entire repository history on every developer’s machine, enabling fast local commits, branching,
> diffing,
> and merges.  
> It uses snapshots rather than file diffs and relies heavily on hashing for integrity.  
> Git supports flexible workflows, from trunk-based development to complex multi-branch strategies, and integrates
> seamlessly with CI/CD pipelines.

---

### 6.How can we use it?

> We use Git through command-line tools, GUIs, or IDE integrations to track changes, create commits, and manage
> branches.
> Git is primarily operated through commands such as `git init`, `git add`, `git commit`, `git push`, and `git pull`.  
> It integrates with IDEs (IntelliJ, VS Code), CI/CD tools, and platforms like GitHub or GitLab.  
> Developers use it to create branches, merge changes, review code, manage releases, and collaborate safely.

---

### 7.Why do we need Git? (Why is Git so popular?)

> Git is fast, distributed, resilient, and supports powerful branching and merging workflows.
> Git allows offline work, fast local commits, cheap branching, and flexible workflows.  
> Its distributed nature enables every developer to have the full history locally, improving reliability.  
> Git integrates well with modern DevOps pipelines, CI/CD, and cloud-based platforms.

---

### 8.Who created Git and when?

> Linus Torvalds created Git in 2005.
> Git was developed by Linus Torvalds after issues with the previous Linux kernel version control system.  
> It was designed around speed, integrity, and a distributed architecture suitable for large, parallel development
> efforts.

---

### 9.What is a Git repository?

> A Git repository is the data structure that stores your project’s history, commits, and metadata.
> A repository contains a `.git` directory with all objects (blobs, trees), references (branches, tags), and
> configuration.  
> It tracks every change made to the project and enables branching, merging, rollback, and collaboration.  
> Repos can be local (on your machine) or remote (e.g., GitHub).

---

### 10.What is the difference between a local and a remote repository?

> A local repository lives on your machine; a remote repository lives on a server.
> Local repos enable offline work, fast commits, and branching.  
> Remote repos (GitHub, GitLab, Bitbucket) are shared locations used for collaboration, CI/CD, code reviews, and
> backups.  
> Git uses commands like `push`, `pull`, and `fetch` to synchronize the two.

<img src="/assets/git-workflow.png" height=700 weight=1000></img>
---

### 11. How do you configure your name and email in Git?

> Use `git config` to set your global or local identity.
> This information is stored in the global Git config and recorded with each commit.

```shell
git config --global user.name "Your Name"
git config --global user.email "your@email.com
```

---

### 12.What does `git init` do?

> Initializes a new Git repository in the current directory.
> `git init` creates a `.git` directory containing all the internal structures Git needs: object storage, refs, hooks,
> and configuration.  
> It converts an existing folder into a fully functional Git repository.
---

### 13.What does `git clone` do?

> Copies an existing remote repository to your local machine.
> `git clone` downloads all objects, branches, history, and metadata, creating a full local replica of the remote
> repo.  
> It also sets up the default remote alias `origin`.
---

### 14.What is the difference between git clone and git pull?

> `git clone` creates a new local copy of a remote repository; `git pull` updates an existing local repository.
>- `git clone` downloads the full repository (history, branches, objects) and sets up a local working copy.

- `git pull` fetches new changes from the remote and merges them into the current branch.
  Clone = first-time setup.  
  Pull = synchronize updates.

---

### 15.What are the three main states of files in Git (working directory, staging area, committed)?

> Working directory = modified files; staging area = files prepared for commit; committed = saved in repository history.

- **Working directory**: Your local files; changes here are untracked or modified.
- **Staging area (index)**: A snapshot of changes selected for the next commit.
- **Committed**: Data safely stored in the Git object database.

---

### 16.What is the staging area (index)?

> A temporary area where changes are collected before committing.
> The staging area holds specific files or file changes you intend to commit.  
> It allows batching multiple modifications into a single, meaningful commit.
---

### 17.What does git add do?

> It stages changes by adding them to the index.
> `git add <file>` takes the current version of a file and places it into the staging area.  
> It does not commit; it prepares the commit.
---

### 18.What does git commit do?

> It saves staged changes to the repository’s history as a new commit.
> `git commit` creates a snapshot from the staging area and records metadata (author, timestamp, message).  
> The commit points to a tree object representing the directory state.
---

### 19.What is a good commit message practice?

> Use clear, concise messages describing what and why, not how.

- Use an imperative tone: “Add feature”, “Fix bug”.
- Keep the subject ≤ 50 characters.
- Provide a detailed body when necessary.
  --->

### 20.What does git status show?

> It shows the current state of the working directory and staging area.
> `git status` lists:

- Modified but unstaged files
- Staged files ready to commit
- Untracked files
- Branch information and hints

---

### 21.What does git log show?

> It displays the commit history of the repository.
> `git log` lists commits with details like hash, author, date, and message.  
> You can view full history, filter it, or show graphs with flags.
---

### 22.What is the difference between git log and git reflog?

> `git log` shows project history; `git reflog` shows local reference history (including rewrites).

- `git log`: Displays commits reachable from current branches.
- `git reflog`: Tracks updates to HEAD and branch references, even after resets, rebases, or deleted commits.

---

### 23.What does git diff show?

> It shows line-level differences between file versions.

`git diff` compares:

- Working directory vs staging area
- Staging area vs last commit
- Or any two commits/branches when specified

---

### 24.What is a branch in Git?

> A branch is a lightweight pointer to a specific commit, representing an independent line of development.
> Branches allow developers to work on features, fixes, or experiments without affecting the main code.  
> Each branch is simply a movable pointer (ref) pointing to the latest commit in its sequence.

---

### 25.What is the default branch name (historically and now)?

> Historically `master`; now commonly `main`.
> Early Git repositories used `master` as the default.  
> Modern systems (GitHub, GitLab) use `main` as the new default due to improved naming conventions and inclusivity.

---

### 26. How do you create a new branch?

> Use `git branch <name>` or `git switch -c <name>`.

`git branch feature-x` creates a branch at the current commit.  
`git switch -c feature-x` or `git checkout -b feature-x` creates and switches to it immediately.

---

### 27.How do you switch branches (git checkout vs git switch)?

> `git switch` is the modern, safer command; `git checkout` is older and more general-purpose.

- `git switch <branch>`: Switches branches.
- `git switch -c <branch>`: Creates and switches to a new branch.
- `git checkout <branch>`: Does the same but also handles file checkout, making it easier to misuse.

---

### 28. What does merging in Git mean?

> Combining changes from one branch into another.
> A merge takes the commit history from one branch and integrates it with the target branch.  
> Git attempts to automatically reconcile differences using a common ancestor.

---

### 29. What is fast-forward merge vs three-way merge?

> Fast-forward: simply moves the branch pointer.  
> Three-way: creates a merge commit using two branch tips + a common ancestor.

- **Fast-forward**: Happens when the target branch has no divergent commits. Git just advances the branch pointer to the
  other branch’s tip—no merge commit.
- **Three-way merge**: Happens when both branches have diverged. Git uses the common ancestor to merge differences and
  creates a new commit.

---

### 30.What is a merge conflict?

> A merge conflict occurs when Git cannot automatically reconcile differences between two branches.
> If two branches modify the same lines or incompatible file regions, Git stops and marks the file with conflict
> markers.  
> The developer must choose the correct final version manually.
---

### 31. How do you resolve a merge conflict?

> Edit the conflicting files, choose the correct content, then stage and commit.

1. Open the file and resolve conflict markers (`<<<<<<<`, `=======`, `>>>>>>>`).
2. Decide which changes to keep (yours, theirs, or a combination).
3. Run `git add` on the resolved files.
4. Complete the merge with `git commit`.

---

### 32. What does git rebase do and how is it different from merge?

> `git rebase` rewrites commits onto a new base; merge combines histories without rewriting.

- **Rebase**: Moves or rewrites your branch’s commits so they appear as if created on top of another branch. Produces a
  linear history.
- **Merge**: Combines branches using a merge commit, preserving parallel history.
  Rebase = rewrite + linearize.  
  Merge = preserve + integrate.

---

### 33.What is GitHub?

> A cloud platform for hosting Git repositories with collaboration features.
> GitHub provides remote Git hosting, pull requests, issue tracking, CI/CD (Actions), and team collaboration tools.  
> It integrates with Git to support modern DevOps workflows.
---

### 34.What is the difference between Git and GitHub?

> Git is a version control system; GitHub is a platform that hosts Git repositories.
> Git is a local tool for tracking and managing code changes.  
> GitHub is a cloud service that provides remote repositories, pull requests, CI/CD, issue tracking, and team workflows.

---

### 35. What are popular alternatives to GitHub (GitLab, Bitbucket, etc.)?

> GitLab, Bitbucket, Azure DevOps, Gitea, and AWS CodeCommit.
---

### 36. How do you create a repository on GitHub?

Use the “New repository” button on GitHub.

1. Log into GitHub.
2. Click **New Repository**.
3. Choose a name, description, and visibility.
4. Optionally add a README or .gitignore.
5. Click **Create repository**.

---

### 37. What does git push do?

> Uploads local commits to a remote repository.
> `git push` sends new commits from your local branch to the corresponding remote branch.  
> It updates the remote ref pointer to include your latest work.
---

### 38.What does git pull do?

> Downloads and merges changes from the remote repository into the current branch.
> `git pull` performs:

1. `git fetch` → download updates
2. `git merge` → integrate them into local history

---

### 39. What is the difference between git fetch and git pull?

> Fetch downloads changes; pull downloads and merges them.

- **git fetch**: Updates remote-tracking branches without modifying your working branch.
- **git pull**: Fetches + merges into your current branch.

---

### 40.What is a Pull Request (PR) on GitHub?

> A request to merge changes from one branch into another, usually with review.
> A PR allows developers to propose changes, discuss the implementation, run CI checks, and undergo code review before
> merging into the target branch.  
> It centralizes communication and ensures high-quality contributions.

---

### 41.What is the difference between a Git "pull request" and a "push request"? (Clarifying the common misconception)

> A "pull request" exists; a "push request" does not.
> A **Pull Request (PR)** is a GitHub/GitLab/Bitbucket feature where you ask maintainers to *pull* your changes into
> their branch.  
> There is **no such thing** as a “push request” in Git—people misuse the term, but it's not part of Git or GitHub.

---

### 42.What is the typical Pull Request workflow?

> Branch → Commit → Push → Open PR → Review → Fix → Merge.
> Typical workflow:

1. Create a feature branch.
2. Make commits.
3. Push the branch to GitHub.
4. Open a Pull Request.
5. Run CI (automated tests).
6. Review comments from teammates.
7. Apply fixes and push more commits.
8. Merge PR into the target branch (often `main` or `develop`).

---

### 43.What is forking a repository on GitHub?

> Forking creates your own copy of someone else’s repository under your GitHub account.
> A **fork** is a full server-side replica of a repo. You can modify it independently and later propose changes via Pull
> Requests back to the original project.

---

### 44.When and why would you fork instead of branching?

> Fork when you don’t have write permission to the repo.
> Use a **fork** when:

- You're contributing to open-source projects.
- You don't have push rights to the original repo.
- You want isolated development without affecting the main project’s namespace.
- You want your own remote repo to manage changes.

---

### 45.What is GitHub Pages?

> Free static website hosting directly from a GitHub repository.
> GitHub Pages can host:

- Documentation
- Portfolio websites
- Project pages
- Static HTML/CSS/JS apps  
  It builds from the `main`, `gh-pages`, or `/docs` folder, depending on configuration.

---

### 46.What is a .gitignore file and why is it important?

> A file listing patterns Git should ignore.
> `.gitignore` prevents unwanted files from being tracked, such as:

- Build artifacts
- Logs
- System files
- Secrets (NOT recommended—use vaults instead)
- IDE settings

---

### 47.What is GitHub Actions?

> GitHub’s built-in CI/CD automation platform.
> GitHub Actions lets you automate workflows such as:

- Building
- Testing
- Deploying
- Linting
- Releasing  
  Workflows run as YAML files in `.github/workflows`.

---

### 48.What are protected branches and code owners on GitHub?

> Protected branches enforce rules; code owners define automatic reviewers.
> **Protected branches** can enforce:

- No direct pushes
- Required PR reviews
- Passing CI checks
- Required status checks
- Restrict who can merge

---

### 49.Git Best Practices Every Developer Should Follow

> 1. Commit Often, but Meaningfully

- Make small, focused commits with a single purpose.
- Avoid giant “catch-all” commits that mix unrelated changes.

> 2. Write Clear, Descriptive Commit Messages

- Use present tense, imperative mood: “Fix bug in user login.”
- Include context if necessary, e.g., issue numbers or rationale.

> 3. Use Branching Strategically

- Follow a workflow (Git Flow, GitHub Flow, or trunk-based development).
- Keep `main` or `master` stable; develop features, bug fixes, or experiments in separate branches.

> 4. Keep Branches Up to Date

- Regularly fetch and rebase or merge to minimize conflicts.
- Avoid letting feature branches drift too far from the main branch.

> 5. Review Code via Pull Requests

- Use PRs to enforce code review, CI checks, and discussion.
- Avoid pushing directly to protected branches.

> 6. Use .gitignore Appropriately

- Exclude build artifacts, logs, secrets, IDE configs, and system files.
- Prevents clutter and accidental commits of sensitive information.

> 7. Avoid Committing Secrets

- Never commit passwords, tokens, or API keys.
- Use environment variables or vaults for sensitive configuration.

> 8. Understand Git Internals

- Know the difference between `git fetch`, `git pull`, `git rebase`, and `git merge`.
- Learn when to rebase vs merge to keep history clean.

> 9. Test Before You Push

- Run tests locally before pushing or creating a PR.
- Avoid breaking the main branch for others.

> 10. Document Workflow Conventions

- Ensure your team follows a shared branching, commit, and PR standard.
- Makes collaboration predictable and efficient.

---

### 50.Common Git Mistakes Beginners Make and How to Avoid Them

> 1. Committing Directly to Main
     **Mistake:** Pushing experimental or untested code to `main` or `master`.  
     **Avoid:** Always create a feature branch and use PRs for integration.

> 2. Large, Unfocused Commits
     **Mistake:** Committing too many unrelated changes at once.  
     **Avoid:** Break work into smaller, logical commits.

> 3. Poor Commit Messages
     **Mistake:** Messages like “fix stuff” or “update code.”  
     **Avoid:** Write clear, descriptive messages using imperative mood.

> 4. Ignoring .gitignore
     **Mistake:** Committing temporary files, build artifacts, or secrets.  
     **Avoid:** Configure `.gitignore` and verify before committing.

> 5. Forgetting to Pull/Fetch Before Pushing
     **Mistake:** Overwriting remote changes and causing conflicts.  
     **Avoid:** Always fetch/rebase or merge before pushing.

> 6. Misusing Rebase and Merge
     **Mistake:** Rebasing public branches or merging incorrectly.  
     **Avoid:** Rebase only local branches; understand consequences of rewriting history.

> 7. Accidentally Committing Secrets
     **Mistake:** Committing API keys, passwords, or certificates.  
     **Avoid:** Use `.gitignore`, environment variables, and secret management tools.

> 8. Confusion Between Remote and Local
     **Mistake:** Thinking a `push` automatically syncs everything or misunderstanding tracking branches.  
     **Avoid:** Learn how remotes, upstreams, and tracking branches work.

> 9. Resolving Conflicts Carelessly
     **Mistake:** Using `git merge --abort` or manual edits without verification.  
     **Avoid:** Review conflicts carefully, test code, and ensure the final merge is correct.

> 10. Large Binary Files in Git
      **Mistake:** Committing large binaries directly into Git.  
      **Avoid:** Use Git LFS or store large assets externally to keep repo size manageable.

---