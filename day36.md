Day 36 – Git Fundamentals & Architecture
🎯 Objective

Learn the fundamentals of Git, understand version control, explore Git architecture, and configure Git for development.
📖 What is Git?

Git is a Distributed Version Control System (DVCS) that tracks changes in source code and allows multiple developers to collaborate efficiently on projects.

Developed by Linus Torvalds in 2005, Git has become the industry standard for version control.
📖 What is Version Control?

Version Control is a system that records changes to files over time, allowing developers to:

Track project history
Restore previous versions
Collaborate safely
Resolve conflicts
Manage releases
⭐ Why Git?
Fast and lightweight
Distributed architecture
Data integrity using SHA hashing
Supports branching and merging
Easy collaboration
Works offline
Open source
🏗 Git Architecture

Git manages changes through four main areas:

Working Directory
        │
    git add
        ▼
Staging Area
        │
   git commit
        ▼
Local Repository
        │
    git push
        ▼
Remote Repository (GitHub)
Working Directory

The folder where you create, edit, and delete project files.

Staging Area

A temporary area where selected changes are prepared before committing.

Local Repository

Centralized vs Distributed Version Control
Centralized VCS	Distributed VCS
Single central server	Every developer has a complete repository
Internet usually required	Can work offline
Single point of failure	More reliable
Examples: SVN, CVS	Example: Git

Stores the complete commit history on your local machine.

Remote Repository

Git vs GitHub
Git	GitHub
Version control software	Cloud hosting platform
Runs locally	Hosts remote repositories
Tracks code changes	Enables collaboration and pull requests

A shared repository hosted on platforms like GitHub for collaboration.
