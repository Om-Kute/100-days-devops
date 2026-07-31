Day 38 – Git Branching & Merging
🎯 Objective

Learn how to create, switch, merge, and manage Git branches while understanding merge conflicts and their resolution.

🌿 What is a Branch?

A branch is an independent line of development that allows developers to work on features, bug fixes, or experiments without affecting the main codebase.

Benefits of branching:

Develop features independently
Fix bugs safely
Collaborate with multiple developers
Keep the main branch stable
Support parallel development
1. git branch

Create, list, rename, and delete branches.

Syntax
git branch
git branch <branch-name>
git branch -d <branch-name>
git branch -D <branch-name>
Example

2. git switch

Switch to another branch.

Syntax
git switch <branch-name>
git switch -c <branch-name>
Example
git switch feature-login
git switch -c feature-payment
git branch feature-login
git branch

3. git checkout

Older command for switching branches or restoring files.

Syntax
git checkout <branch-name>
git checkout -b <branch-name>
Example
git checkout feature-login
git checkout -b feature-dashboard

4. git merge

Merge another branch into the current branch.

Syntax
git merge <branch-name>
Example
git switch main
git merge feature-login

Merge Types
Fast-Forward Merge
Merge Conflicts

A merge conflict happens when Git cannot determine which changes should be kept because the same section of a file has been modified in different branches.

Example conflict:

<<<<<<< HEAD
Hello DevOps
=======
Hello Git
>>>>>>> feature-login

Occurs when the target branch has no new commits, allowing Git to move the branch pointer forward without creating a merge commit.

Three-Way Merge

Occurs when both branches contain new commits. Git creates a new merge commit to combine histories.

Resolving Merge Conflicts
Step 1

Check the repository status.

git status
Step 2

Open the conflicting file and remove the conflict markers.

Step 3

Save the correct version.

Step 4

Stage the resolved file.

git add file.txt
Step 5

Complete the merge.

git commit -m "Resolve merge conflict"
