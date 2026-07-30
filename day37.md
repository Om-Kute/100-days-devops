Day 37 – Basic Git Commands
🎯 Objective

Learn the most commonly used Git commands to manage repositories, track changes, and maintain project history.

📂 1. git init

Initializes a new Git repository in the current directory.

Syntax
git init

Example

mkdir my-project
cd my-project
git init

📥 2. git clone

Creates a copy of an existing remote repository.

Syntax
git clone <repository-url>

Example

git clone https://github.com/username/project.git

📋 3. git status

Displays the current state of your working directory and staging area.

Syntax
git status

➕ 4. git add

Stages files before committing them.

Syntax
git add file.txt

Stage all files:

git add .

Use Cases

Check modified files
View staged changes
Identify untracked files

💾 5. git commit

Saves staged changes to the local repository.

Syntax
git commit -m "Your commit message"

Example

git commit -m "Add login page"

📜 6. git log

Displays commit history.

Syntax
git log

Compact view:

git log --oneline
