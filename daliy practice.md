# ✅ Daily Linux Practice Routine (RHCSA Level)

**Goal**: Reinforce key Linux skills with 40–60 minutes of hands-on practice each day.  
**Recommended**: Use a RHEL 9/10 VM or cloud environment.

---

## 🧭 Step 1: File & Directory Management (10 min)

```bash
# Create directory structure
mkdir -p ~/lab/day1/docs ~/lab/day1/logs ~/lab/day1/archive

# Create files
touch ~/lab/day1/docs/file{1..5}.txt

# Copy, move, and rename
cp ~/lab/day1/docs/file1.txt ~/lab/day1/logs/
mv ~/lab/day1/docs/file2.txt ~/lab/day1/docs/file2_renamed.txt
rm ~/lab/day1/docs/file3.txt

# Search for files
find ~/lab -name "*.txt"

# Redirection and piping
echo "Hello Linux World" > ~/lab/day1/logs/greeting.txt
cat /etc/passwd | grep root | tee ~/lab/day1/logs/root_users.txt

# Use history
history
!100  # (replace 100 with actual number)

# Try Bash shortcuts (no command line):
# Ctrl+R, Ctrl+A, Ctrl+E, Ctrl+U

# Variables
export MYNAME="LinuxWarrior"
echo "Welcome, $MYNAME"

# Create and use alias
alias ll='ls -alF'
ll

# View environment
env | less

# (Optional) Edit .bashrc to persist alias/variable
vim ~/.bashrc

# man page practice
man tar

# Discover related commands
apropos user

# Practice with vim
vim ~/lab/day1/docs/notes.txt
# i (insert), write some notes, Esc + :wq (save and exit)

# Create compressed tar archive
tar -czvf ~/lab/day1/archive/docs_backup.tar.gz ~/lab/day1/docs

# List contents of tarball
tar -tzf ~/lab/day1/archive/docs_backup.tar.gz

# Create symbolic link
ln -s ~/lab/day1/docs ~/lab/docs_link
ls -l ~/lab

# Check disk usage
df -h
du -sh ~/lab/day1/*

# View mounted filesystems
mount | grep -i "ext"

# Explore log files (read-only)
less /var/log/messages   # or /var/log/syslog
# Write a simple backup script
vim ~/lab/day1/backup.sh

#!/bin/bash
tar -czf ~/lab/day1/archive/backup_$(date +%F).tar.gz ~/lab/day1/docs

# Make it executable and run it
chmod +x ~/lab/day1/backup.sh
./lab/day1/backup.sh

Repeat this routine daily with different file names and paths to reinforce.

Track your progress in a log file.

Create variations: Use scp, ssh, cron, or user management when ready.

Use man -k or tldr (if installed) to explore unknown commands.

| Mode   | Command        | Action                                   |
| ------ | -------------- | ---------------------------------------- |
| Normal | `i`, `a`       | Enter input mode                         |
| Normal | `o`            | Open new line in input mode              |
| Normal | `Esc`          | Enter command (normal) mode              |
| Normal | `:wq`          | Write and quit                           |
| Normal | `:q!`          | Quit without saving                      |
| Normal | `dd`           | Delete the current line                  |
| Normal | `yy`           | Yank (copy) the current line             |
| Normal | `p`            | Paste the text currently in the buffer   |
| Normal | `v`            | Enter visual mode                        |
| Normal | `u`            | Undo the last operation                  |
| Normal | `Ctrl-r`       | Redo the last operation undone           |
| Normal | `gg`           | Go to the top of the document            |
| Normal | `G`            | Go to the end of the document            |
| Normal | `/text`        | Search forward for "text"                |
| Normal | `?text`        | Search backward for "text"               |
| Normal | `^`            | Move to start of line                    |
| Normal | `$`            | Move to end of line                      |
| Normal | `w`            | Move to the next word                    |
| Normal | `:%s/old/new/g`| Substitute all occurrences of old → new  |
