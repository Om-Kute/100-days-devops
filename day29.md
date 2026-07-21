Day 29 – Bash Operators
Objective

Learn the different types of Bash operators used for calculations, comparisons, logical decisions, string handling, and file testing.

1. Arithmetic Operators

Used for mathematical calculations.

Operator	Description
+	Addition
-	Subtraction
*	Multiplication
/	Division
%	Modulus
**	Exponentiation

2. Relational Operators

Used to compare numeric values.

Operator	Description
-eq	Equal
-ne	Not Equal
-gt	Greater Than
-lt	Less Than
-ge	Greater Than or Equal
-le	Less Than or Equal

Example:

if [ $a -lt $b ]; then
    echo "a is less than b"
fi


3. Logical Operators

Used to combine conditions.

Operator	Description
-a	AND
-o	OR
!	NOT

Example:

if [ $a -gt 5 -a $b -lt 30 ]; then
    echo "Condition is true"
fi

4. String Operators

Used for comparing strings.

Operator	Description
=	Equal
!=	Not Equal
-z	String is empty
-n	String is not empty

Example:

name="DevOps"

if [ "$name" = "DevOps" ]; then
    echo "Strings match"
fi

5. File Operators

Used to check file and directory properties.

Operator	Description
-e	File exists
-f	Regular file
-d	Directory exists
-r	Read permission
-w	Write permission
-x	Execute permission
-s	File is not empty

Example:

if [ -f script.sh ]; then
    echo "File exists"
fi
