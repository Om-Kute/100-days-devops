Day 33 – Arrays & String Manipulation in Bash
🎯 Objective

Learn how to use arrays and perform string manipulation to build more efficient and dynamic Bash scripts.

What are Arrays?

An array is a collection of multiple values stored under a single variable name. Arrays make it easier to manage lists of data in Bash scripts.
Declare an Array
fruits=("Apple" "Banana" "Mango" "Orange")
Access Elements
echo ${fruits[0]}
echo ${fruits[2]}
Output
Apple
Mango
Print All Elements
echo ${fruits[@]}
Array Length
echo ${#fruits[@]}
