# Day 11 - Linux Group Management

groupadd devops
# Create new group

gpasswd -M user1,user2 devops
# Add multiple users to group

groupmod devops
# Modify group settings

gpasswd devops
# Manage group password/members

groups username
# Show user groups

grpck
# Verify group files

grpconv
# Convert to shadow group passwords

groupmod -g 1050 devops
# Change group ID
