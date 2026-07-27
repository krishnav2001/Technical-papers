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
nce the changes are complete​, the staging area will contain one or more files that need to be committed. Creating a commit will cause Git to take the new code from the staging area and make the commit to the main repository​. This commit is then moved to the commit area.

## 3. The Git Lifecycle

The standard Git workflow consists of five primary commands.

| Command | Git Command | Description |
|---------|-------------|-------------|
| **Clone** | `git clone <repository-url>` | Downloads an existing repository from a remote server (such as GitHub) to your local machine. |
| **Add** | `git add <file-name>` or `git add .` | Moves changes from the working directory to the staging area. |
| **Commit** | `git commit -m "Commit message"` | Saves the staged changes to the local repository with a descriptive message. |
| **Push** | `git push origin <branch-name>` | Uploads local commits to the remote repository (GitHub). |
| **Pull** | `git pull origin <branch-name>` | Fetches and merges changes from the remote repository into your local repository. |
