Day 32 – Functions & Positional Parameters in Bash
🎯 Objective

Learn how to write reusable functions and use positional parameters to make Bash scripts modular and dynamic.

What are Functions?

A function is a reusable block of commands that performs a specific task. Functions improve code readability, reduce duplication, and make scripts easier to maintain.

Function Syntax
function_name() {
    commands
}

or

function function_name() {
    commands
}
Example 1 – Simple Function
greet() {
    echo "Hello, DevOps!"
}

greet
Output
Hello, DevOps!
Example 2 – Function with Parameters
add() {
    echo "Sum = $(($1 + $2))"
}

add 15 25
Output
Sum = 40

Example 3 – Function Return Status
check() {
    if [ $1 -gt 0 ]; then
        return 0
    else
        return 1
    fi
}

check 5
echo $?
Output
0
