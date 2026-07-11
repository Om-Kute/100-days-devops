# Day 19 - Linux Job Scheduling Commands

## Commands

crontab -e
# Edit current user's cron jobs

crontab -l
# List current user's cron jobs

crontab -r
# Remove all cron jobs

crontab -u username -l
# List another user's cron jobs

crontab -u username -e
# Edit another user's cron jobs

systemctl status cron
# Check Cron service status

systemctl start cron
# Start Cron service

systemctl stop cron
# Stop Cron service

systemctl restart cron
# Restart Cron service

at 10:30
# Schedule a one-time job


