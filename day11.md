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
