Day 39 – GitHub Collaboration
🎯 Objective

Learn how to collaborate using Git and GitHub through remote repositories, push, pull, fetch, forks, branches, and Pull Requests.

🌐 What is GitHub?

GitHub is a cloud-based platform for hosting Git repositories.

It provides features such as:

Remote repository hosting
Team collaboration
Pull Requests
Code reviews
Issues
Project management
CI/CD integration
Open-source collaboration
🔗 1. git remote

The git remote command manages connections between your local repository and remote repositories.

Add a Remote
git remote add origin <repository-url>

Example:

git remote add origin https://github.com/username/project.git
🔍 2. git remote -v

Displays configured remote repositories and their fetch/push URLs.

git remote -v

Example output:

origin  https://github.com/username/project.git (fetch)
origin  https://github.com/username/project.git (push)
⬆️ 3. git push
Uploads local commits to a remote repository.

git push <remote> <branch>

Example:

git push origin main

For the first push:

git push -u origin main

The -u option sets the upstream branch.

After that, you can usually use:

git push

⬇️ 4. git pull

Downloads changes from a remote repository and integrates them into your current branch.

git pull <remote> <branch>

Example:

git pull origin main
📥 5. git fetch

Downloads commits, branches, and other references from a remote repository without automatically integrating them into your current branch.

git fetch

Or:

git fetch origin

You can inspect the downloaded remote-tracking branch:

git log HEAD..origin/main
Conceptually:

git pull = git fetch + integration

⚖️ git fetch vs git pull
git fetch	git pull
Downloads remote changes	Downloads remote changes
Updates remote-tracking branches	Integrates changes into current branch
Lets you inspect changes first	Updates your current branch
Useful when you want more control	Convenient for synchronization
By default, that integration is commonly a merge, although Git can also be configured to rebase.
Here, origin is the conventional name for the remote repository.

🍴 What is a Fork?

A Fork is a GitHub-side copy of another user's repository under your own GitHub account.

Typical use cases:

Open-source contribution
Experimenting with another project
Proposing improvements
Working without direct write access to the original repository
