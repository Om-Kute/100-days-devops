🚀 Day 40 – Advanced Git
🎯 Objective

Learn advanced Git features used to manage changes, maintain clean repository history, handle mistakes safely, manage releases, and automate Git workflows.

This is the final day of the Git & GitHub phase of my 100 Days of DevOps journey.

1. 📦 Git Stash

git stash temporarily saves uncommitted changes without creating a normal commit.

Save Changes
git stash
Save With a Message
git stash push -m "WIP: login feature"
View Stashes
git stash list
Apply Latest Stash
git stash apply
Apply and Remove Latest Stash
git stash pop
Delete a Stash
git stash drop stash@{0}

2. 🔄 Git Rebase

git rebase reapplies commits from one branch on top of another base.

Example:

git switch feature-login
git rebase main
Interactive Rebase
git rebase -i HEAD~3

Interactive rebase can be used to:

Reorder commits
Squash commits
Edit commits
Reword commit messages
Continue After Resolving Conflicts
git add .
git rebase --continue
Abort Rebase
git rebase --abort

⚠️ Avoid rebasing commits that other people are already using on shared branches unless your team workflow explicitly allows it.
