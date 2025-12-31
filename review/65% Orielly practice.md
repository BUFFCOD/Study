# RHCSA LONG REVIEW & PRACTICE GUIDE
Built from ALL notes, labs, and files you provided

This is a full-scope RHCSA execution guide.
Not theory. Not summaries. This is how you pass.

==================================================

## HOW TO USE THIS GUIDE

• Study 45–90 minutes per day  
• Always practice on a real VM  
• Man pages are allowed (use them)  
• Repeat the cycle weekly  
• If it feels boring → you are ready  

==================================================

## DAILY WARM-UP (DO THIS EVERY DAY – 10 MINUTES)

Purpose: speed, accuracy, muscle memory

sed -n 5p /etc/passwd
head -n 5 /etc/passwd | tail -n 1

awk -F: '$7=="/bin/bash" {print $1}' /etc/passwd

journalctl -u sshd --since today | grep -c Failed

==================================================

# WEEKLY PRACTICE CYCLE (RHCSA EXECUTION MODE)

==================================================

## DAY 1 – USERS, GROUPS, DEFAULTS, SUDO

Goal: control access safely and correctly

useradd analyst1
passwd analyst1
groupadd audit
usermod -aG audit analyst1
id analyst1

usermod -L analyst1
chage -l analyst1

usermod -aG wheel analyst1
visudo

sudo sh -c "ls /root > /tmp/root.lst"
sudo ls /root | sudo tee /tmp/root.lst > /dev/null

==================================================

## DAY 2 – PERMISSIONS, OWNERSHIP, SPECIAL BITS

mkdir /data/share
chgrp audit /data/share
chmod 2770 /data/share

chmod 1777 /data/share

find / -perm -4000 -type f 2>/dev/null

==================================================

## DAY 3 – PACKAGES, RPM, DNF, REPOSITORIES

dnf search vim
dnf install vim-enhanced
dnf remove vim-enhanced
dnf provides /usr/bin/ssh
dnf repolist
dnf history

rpm -qi bash
rpm -ql bash
rpm -qf /bin/bash

==================================================

## DAY 4 – JOBS, PROCESSES, SIGNALS, PRIORITY

sleep 300 &
jobs
bg %1
fg %1

ps aux
ps -ef
ps fax

kill -15 PID
kill -9 PID
kill -STOP PID
kill -CONT PID

nice -n 10 yes > /dev/null &
renice -n 5 -p PID

==================================================

## DAY 5 – SYSTEMD, LOGGING, TIMERS

systemctl status sshd
systemctl start sshd
systemctl stop sshd
systemctl enable --now sshd
systemctl disable sshd

systemctl edit sshd
systemctl mask sshd
systemctl unmask sshd

journalctl
journalctl -u sshd
journalctl -p 3
journalctl --since today
journalctl -f

systemctl list-timers

==================================================

## DAY 6 – STORAGE: PARTITIONS, FILESYSTEMS, MOUNTS

fdisk /dev/sdb
mkfs.xfs /dev/sdb1
mount /dev/sdb1 /mnt

blkid
vim /etc/fstab
mount -a
findmnt --verify

==================================================

## DAY 7 – LVM

pvcreate /dev/sdb1
vgcreate vgdata /dev/sdb1
lvcreate -L 5G -n lvdata vgdata
mkfs.xfs /dev/vgdata/lvdata
mount /dev/vgdata/lvdata /data

lvextend -r -L +2G /dev/vgdata/lvdata

==================================================

## STRATIS

dnf install stratis-cli stratisd
systemctl enable --now stratisd

stratis pool create mypool /dev/sdc
stratis fs create mypool myfs

==================================================

## BOOT PROCESS & RECOVERY

UEFI
GRUB
Kernel
initramfs
systemd
target

systemctl get-default
systemctl set-default multi-user.target
systemctl isolate rescue.target

==================================================

FINAL NOTE:
Repeat until boring.
Then pass.
