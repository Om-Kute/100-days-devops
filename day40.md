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

3. 🏷️ Git Tags

Tags mark important points in Git history and are commonly used for software releases.

List Tags
git tag
Lightweight Tag
git tag v1.0
Annotated Tag
git tag -a v1.0 -m "Version 1.0 release"
Push One Tag
git push origin v1.0
Push All Tags
git push origin --tags
git add .
git rebase --continue
Abort Rebase
git rebase --abort

⚠️ Avoid rebasing commits that other people are already using on shared branches unless your team workflow explicitly allows it.

4. ↩️ Git Reset

git reset moves HEAD and the current branch pointer to another commit.

Soft Reset
git reset --soft HEAD~1

Moves HEAD back while keeping changes staged.

Mixed Reset
git reset --mixed HEAD~1

Moves HEAD back and keeps changes in the working directory but unstaged.

--mixed is the default mode.
5. 🔙 Git Revert

git revert creates a new commit that reverses the changes introduced by an earlier commit.

git revert <commit-id>

Example:

git revert a1b2c3d
Reset vs Revert
git reset	git revert
Moves branch history	Creates a new undo commit
Can rewrite history	Preserves history
Useful for local cleanup	Safer for shared branches
--hard can remove work	Existing history remains visible
Hard Reset
git reset --hard HEAD~1

Moves HEAD back and resets both the staging area and working directory.

⚠️ git reset --hard can permanently remove uncommitted changes. Use it carefully.
