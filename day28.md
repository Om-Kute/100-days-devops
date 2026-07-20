Day 28 – Shell Scripting Basics
Objective

Learn the fundamentals of Bash Shell Scripting, including script structure, variables, user input, output, and execution.

What is Shell Scripting?

Shell scripting is the process of writing Linux commands in a file and executing them using the Bash shell.

It is widely used to automate repetitive tasks in Linux systems and DevOps workflows.

Basic Script Structure
#!/bin/bash

# This is a comment

echo "Hello, DevOps!"
Components
#!/bin/bash → Shebang (specifies Bash interpreter)
# → Comment
echo → Display output
Variables

Variables store data for later use.

name="Om"
course="Shell Scripting"

echo "Name: $name"
echo "Course: $course"

Output Commands
echo
echo "Hello World"
printf
printf "Name: %s\n" "Om"
Output Redirection

Overwrite file:

echo "Hello" > file.txt

Append to file:

echo "DevOps" >> file.txt
User Input

Read input from the keyboard using read.

read username
echo "Welcome $username"
