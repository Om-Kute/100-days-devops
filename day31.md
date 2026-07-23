Day 31 – Loops in Bash
🎯 Objective

Learn how to use loops in Bash to automate repetitive tasks and improve script efficiency.

What are Loops?

Loops allow a block of code to execute repeatedly until a specified condition is met. They are widely used in Linux administration, automation, and DevOps workflows.

1. for Loop

The for loop is used when the number of iterations is known.

Syntax
for variable in list
do
    commands
done
Example
for i in {1..5}
do
    echo "Number: $i"
done
Output
Number: 1
Number: 2
Number: 3
Number: 4
Number: 5
