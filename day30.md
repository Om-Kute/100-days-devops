Day 30 – Conditional Statements in Bash
📖 Objective

Learn how Bash scripts make decisions using conditional statements.

What are Conditional Statements?

Conditional statements allow a script to execute different blocks of code depending on whether a condition is true or false.

They are essential for creating intelligent and dynamic automation scripts.

1. if Statement

Executes code only when the specified condition is true.

Syntax
if [ condition ]; then
    commands
fi
Example
age=20

if [ $age -ge 18 ]; then
    echo "Eligible to vote"
fi

2. if...else Statement

Executes one block when the condition is true and another when it is false.

Syntax
if [ condition ]; then
    commands
else
    commands
fi
Example
marks=45

if [ $marks -ge 50 ]; then
    echo "Pass"
else
    echo "Fail"
fi
