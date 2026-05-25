# Day 10 - Linux Permissions & Links

chmod 444 file.txt
# Read-only permission

chmod 111 file.txt
# Execute-only permission

chmod 222 file.txt
# Write-only permission

chmod 754 file.txt
# Custom permissions

chmod u+r file.txt
# Add read permission to user

ln file.txt hardlink.txt
# Create hard link

ln -s file.txt softlink.txt
# Create soft link

chown user file.txt
# Change owner

chgrp group file.txt
# Change group



