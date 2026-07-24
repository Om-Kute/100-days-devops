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
Positional Parameters

Positional parameters store the arguments passed to a Bash script.

Example
./script.sh Linux DevOps AWS
Parameter	Description	Example Output
$0	Script name	./script.sh
$1	First argument	Linux
$2	Second argument	DevOps
$3	Third argument	AWS
$#	Number of arguments	3
$@	All arguments individually	Linux DevOps AWS
$*	All arguments as one string	Linux DevOps AWS
$$	Current process ID	e.g., 12345
$?	Exit status of last command	0 (success)
