Day 34 – File Handling & Automation Scripts in Bash
🎯 Objective

Learn how to perform file operations and create automation scripts using Bash to simplify Linux administration tasks.

What is File Handling?

File handling refers to performing operations such as reading, writing, appending, copying, moving, and deleting files. These operations form the foundation of automation in Bash scripting.
1. Reading Files
Display File Content
cat file.txt
Read Line by Line
while IFS= read -r line
do
    echo "$line"
done < file.txt
Read First 5 Lines
head -n 5 file.txt
Read Last 5 Lines
tail -n 5 file.txt
2. Writing to Files
Create or Overwrite a File
echo "Hello DevOps" > file.txt
3. Appending Data
Append a Single Line
echo "New Entry" >> file.txt
Append Multiple Lines
cat >> file.txt << EOF
Line 4
Line 5
EOF
Write Multiple Lines
cat > file.txt << EOF
Line 1
Line 2
Line 3
EOF
4. Copy, Move & Delete Files
Copy
cp source.txt backup.txt
Move or Rename
mv old.txt new.txt
Delete
rm file.txt
