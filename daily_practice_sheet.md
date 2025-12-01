# Daily RHCSA Practice (built from your notes)

Spend ~45–60 minutes. Rotate through the days; restart the cycle weekly. Commands are drawn from your existing notes (filenames in backticks for quick lookup).

## Warm-up (10 min, every day)
- Text tools: `grep/awk/sed/head/tail` (`7.1 Common Text Tools.md`, `rhcsa_text_processing.md`).
  - Show 5th line of `/etc/passwd` two ways: `head -n5 /etc/passwd | tail -n1` and `sed -n 5p /etc/passwd`.
  - List bash users: `awk -F: '$7=="/bin/bash" {print $1}' /etc/passwd`.
  - Replace a token in a temp file with `sed -i 's/old/new/' file`.
- Finders: `find`/`which`/`locate` drill (`6.3 Finding files.md`).

## Day 1 – Users, groups, defaults
- Create 2 users, set passwords, lock/unlock, set expiry (`9.6 Limiting User Access.md`).
- Adjust password aging in `/etc/login.defs` and verify with `chage` (`9.4 Manage User Default Settings.md`).
- Add to secondary group; test `newgrp` and `id`.

## Day 2 – Permissions & special bits
- Build a shared dir: `mkdir /data/share && chgrp <grp> /data/share && chmod 2770 /data/share` (`10.2 Changing File Ownership.md`).
- Create files as two users; test sticky bit vs delete rules (also test `chmod 1777`).
- Practice `umask` expectations and `chmod -R X` safe recursion.

## Day 3 – sudo & redirection
- Add a user to `wheel`, enable `%wheel ALL=(ALL) ALL` via `visudo` (`8.4 Managing Sudo Config.md`).
- Test proper redirection: `sudo sh -c "ls /root > /tmp/root.lst"` (`8.3 Performing Administrator Tasks with sudo.md`).
- Create a limited sudo rule in `/etc/sudoers.d/` for a specific command (lab only).

## Day 4 – Packages & repos
- Search/install/remove with `dnf` (`_12.4 Managing packages with dnf.md`).
- Enable/disable a repo (use an existing file), run `dnf repolist`, `dnf history`.
- Query RPM info/files/owner: `rpm -qi/-ql/-qf` (`12.0 Manging Software.md`).

## Day 5 – Processes, signals, priority
- Job control: start `sleep 300 &`, `jobs`, `bg/fg` (`13.1 Exploring jobs and Processes.md`).
- Inspect states with `ps aux`, `ps fax` (`13.3`, `13.4`).
- Send signals: `kill -STOP/-CONT/-TERM` (`14.1 Using signals to Manage Process States.md`).
- Change nice: `nice -n 10 yes > /dev/null &`, then `renice` (`14.2 Manging Process Prioity.md`).

## Day 6 – Networking identity
- Set hostname with `hostnamectl`, verify `/etc/hostname` and `/etc/hosts` (`11.3 understanding nic naming.md`).
- Identify NIC names with `ip a`; note predictable naming patterns.
- (Stretch) Configure a simple `nmcli` connection if you have a lab NIC.

## Day 7 – Tuning & sessions
- List and set a tuned profile; check `tuned.conf` basics (`14.3 Using tuned Profiles.md`).
- Use `loginctl list-users/sessions`, `loginctl terminate-user` in a lab (`Managing user Sessions and utilties.md`).

## Weekly review (30 min)
- Run through the practice exam in `9-14.3 Self study practice and exam.md` under a timer.
- Note any slow steps and add them to the next cycle’s warm-up.

## Off-notes gap (add separately)
Storage (parted/LVM/fstab), SELinux (contexts/restorecon/setsebool), firewalld, systemd units/timers, cron/at, time/chrony. Add brief drills for these since they’re critical but not covered in your current notes.
