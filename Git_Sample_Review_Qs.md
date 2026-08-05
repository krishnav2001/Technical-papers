# Technical Guide: Version Control with Git

## 1. Introduction to Version Control
Version control is a management system that allows you to record and track changes in your source code and files so that you can recall certain versions later. It’s like a Google Doc for programming, where you can collaborate with multiple people working on the same code and see the source code’s history.

Ultimately, using a version control system allows teams to streamline their development process, which improves their overall efficiency.

### What is git?
Git is a free, open-source distributed version control system. It keeps track of projects and files as they change over time with the help of different contributors.Git helps keep track of changes made to a code. If at any point during coding you hit a fatal error and don’t know what’s causing it, Git allows you to revert back to a stable state. It also helps you see what changes have been made to the code over time.

## 2. Core Concepts and Terminology

### The Repository (Repo)
A repository (commonly referred to as repo) is a collection of source code. A repository has commits to the project or a set of references to the commits (i.e., heads).

### Commits
A commit logs a change or series of changes that you have made to a file in the repository. A commit has a unique SHA1 hash which is used to keep track of files changed in the past. A series of commits comprises the Git history.

### Branches
A branch is essentially a unique set of code changes with a unique name. Each repository can have one or more branches. The main branch — the branch where all the changes eventually get merged into - is called the master. This is the official working version of your project and the one that you will see when you visit the project repository at github.com/yourname/projectname.

### Working directory
The working directory is where new files are created, old files are deleted, or where changes are made to already existing files.

### Staging area
The staging area is basically a sort of temporary middle layer where all the changes that were made in the files are managed and organised before they are permanently saved in the git repositry.

### Commit area
once the changes are complete​, the staging area will contain one or more files that need to be committed. Creating a commit will cause Git to take the new code from the staging area and make the commit to the main repository​. This commit is then moved to the commit area.

## 3. The Git Lifecycle

The standard Git workflow consists of five primary commands.

| Command | Git Command | Description |
|---------|-------------|-------------|
| **Clone** | `git clone <repository-url>` | Downloads an existing repository from a remote server (such as GitHub) to your local machine. |
| **Add** | `git add <file-name>` or `git add .` | Moves changes from the working directory to the staging area. |
| **Commit** | `git commit -m "Commit message"` | Saves the staged changes to the local repository with a descriptive message. |
| **Push** | `git push origin <branch-name>` | Uploads local commits to the remote repository (GitHub). |
| **Pull** | `git pull origin <branch-name>` | Fetches and merges changes from the remote repository into your local repository. |

## 4. Branching and Merging

Branching allows developers to work on new features without affecting the main codebase.

### Feature Branches

Feature branches are created to develop new features or fix bugs independently from the main branch.

**Create and switch to a new branch:**

```bash
git checkout -b <branch-name>
```

Example:

```bash
git checkout -b leaf
```

**View all branches:**

```bash
git branch
```

**Switch to an existing branch:**

```bash
git checkout <branch-name>
```

Example:

```bash
git checkout master
```

---

### Merging

Merging combines the changes from one branch into another.

**Merge a branch into the current branch:**

```bash
git merge <branch-name>
```

Example:

```bash
git checkout master
git merge leaf
```

> **Note:** Before merging, switch to the branch that should receive the changes (for example, `master`).

---

### Pull Requests (PR)

A **Pull Request (PR)** is a request to merge changes from one branch into another. It is commonly used for code reviews and collaboration before merging code.

There is no Git command to create a Pull Request. PRs are created on Git hosting platforms such as **GitHub** after pushing your branch.

**Push the feature branch to GitHub:**

```bash
git push origin <branch-name>
```

Example:

```bash
git push origin leaf
```

After pushing, open GitHub and click **Compare & pull request** to create the Pull Request.

## 5. Sample Review Exercise

### 1. Initialize the Repository

Creating a new folder and initializing it as a Git repository.

```bash
mkdir my-project
cd my-project
git init
```
This creates a hidden '.git' folder that will basically allow git to keep track of the project folder.

### 2. Add a File and Make the First Commit

```bash
touch a.txt
git add a.txt
git commit -m "Add initial file a.txt"
```
The 'git add' command stages the file and sends it to staging area while the 'git commit' command saves the changes in the git repo history.

### Step 3: Create a New Branch

```bash
git checkout leaf
```
The 'git checkout' command allows us to swicth to the leaf branch directly.

### 4. Add a File and Commit on the New Branch

```bash
touch b.txt
git add b.txt
git commit -m "Add b.txt on leaf branch"
```
### Step 5: Merge the Branch into Master

Switching back to the main branch and merging the feature branch.

```bash
git checkout master
git merge leaf
```
Due to this merging the entire history of the "leaf" branch is integrated into the "master" branch.

## 6. Checking Understanding

### What is the Staging Area?
The staging area is basically a sort of temporary middle layer where all the changes that were made in the files are managed and organised before they are permanently saved in the git repositry.

### Where is `HEAD` Right Now?
In Git, 'HEAD' is a pointer to the most recent commit on the branch you are currently working on.So by that logic, 'HEAD' points to the merge commit on the 'master' branch.



# RESOURCES
https://www.youtube.com/watch?v=RGOj5yH7evk
