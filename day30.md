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

3. if...elif...else Statement

Used when multiple conditions need to be checked.

Syntax
if [ condition1 ]; then
    commands
elif [ condition2 ]; then
    commands
else
    commands
fi
Example
marks=82

if [ $marks -ge 90 ]; then
    echo "Grade A"
elif [ $marks -ge 75 ]; then
    echo "Grade B"
elif [ $marks -ge 60 ]; then
    echo "Grade C"
else
    echo "Grade D"
fi

4. Nested if Statement

An if statement inside another if statement.

Example
age=22
citizen="yes"

if [ $age -ge 18 ]; then
    if [ "$citizen" = "yes" ]; then
        echo "Eligible to vote"
5. case Statement

Used when checking one variable against multiple possible values.

Syntax
case variable in
    pattern1)
        commands
        ;;
    pattern2)
        commands
        ;;
    *)
        default_command
        ;;
esac
Example
day="Sun"

case $day in
    Mon)
        echo "Start of the week"
        ;;
    Fri)
        echo "Weekend is near"
        ;;
    Sat|Sun)
        echo "Weekend"
        ;;
    *)
        echo "Regular day"
        ;;
esac

        
    else
        echo "Citizenship required"
    fi
else
    echo "Not eligible"
fi
