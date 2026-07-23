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
2. while Loop

The while loop executes as long as the specified condition is true.

Syntax
while [ condition ]
do
    commands
done
Example
count=1

while [ $count -le 5 ]
do
    echo "Count: $count"
    ((count++))
done
Output
Number: 1
Number: 2
Number: 3
Number: 4
Number: 5


3. until Loop

The until loop executes until the specified condition becomes true.

Syntax
until [ condition ]
do
    commands
done
Example
count=1

4. break Statement

The break statement immediately exits the loop.

Example
for i in {1..5}
do
    if [ $i -eq 3 ]; then
        break
    fi

    echo $i
done
Output
1
2

until [ $count -gt 5 ]
do
    echo "Count: $count"
    ((count++))
done
