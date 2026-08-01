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
Here, origin is the conventional name for the remote repository.
