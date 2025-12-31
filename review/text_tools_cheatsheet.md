# Text Tools Cheat Sheet (RHCSA)

Memorize these patterns; drill 10 minutes daily.

## Lines
- 5th line: `sed -n 5p /etc/passwd` or `head -n5 file | tail -n1`
- First/last N: `head -n 3 file`, `tail -n 20 file`

## Search
- Simple: `grep pattern file`
- Regex: `grep -E '^root' /etc/passwd`
- Recursive: `grep -R pattern /etc`
- Exclude: `grep -v pattern file`
- Context: `grep -C2 pattern file`  # 2 lines before/after

## Replace (sed)
- In-place: `sed -i 's/old/new/' file`
- With slash in pattern: `sed -i 's|/etc/|/srv/|' file`
- Print only match lines: `sed -n '/pattern/p' file`

## Fields (awk)
- First field of passwd: `awk -F: '{print $1}' /etc/passwd`
- Users with bash: `awk -F: '$7=="/bin/bash" {print $1}' /etc/passwd`
- Last field of ps: `ps aux | awk '{print $NF}'`
- Conditional: `awk '$3>50 {print $1,$3}' file`  # example on 3rd column

## Combine & filter
- Find files then search: `find /etc -name '*.conf' -exec grep -l pattern {} \;`
- Process tree and filter: `ps fax | grep sshd`
- Journal filter: `journalctl -u sshd | grep Failed`

## Quick picks
- Count matches: `grep -c pattern file`
- Unique sorted: `awk '{print $1}' file | sort -u`
- Show columns: `cut -d: -f1,7 /etc/passwd`

## Daily drill (pick 3)
1) Show bash users; save to `/tmp/bash_users.txt`.
2) Replace a token in a temp file with `sed -i`.
3) Find files under `/etc` containing “PermitRootLogin”.
4) Print last column of `ps aux` and count unique commands.
5) Extract 5th line of `/etc/passwd` two ways.

## Extra challenges (rotate weekly)
- Log scrape: Count SSH failures today.
  ```bash
  journalctl -u sshd --since today | grep -c 'Failed password'
  ```
- Config edit: Flip `PermitRootLogin no` to `yes` safely.
  ```bash
  sudo sed -i 's/^PermitRootLogin no/PermitRootLogin yes/' /etc/ssh/sshd_config
  ```
- Field math: Show usernames + UIDs > 1000.
  ```bash
  awk -F: '$3>1000 {printf "%s %s\n", $1, $3}' /etc/passwd
  ```
- Multi-file search: List files in `/etc` that mention `SELINUX=enforcing`.
  ```bash
  grep -R "^SELINUX=enforcing" /etc
  ```
- Replace with backup: Swap `foo`→`bar` keeping `.bak`.
  ```bash
  sed -i.bak 's/foo/bar/g' /tmp/test.txt
  ```
- Extract and sort: Unique shells in `/etc/passwd`.
  ```bash
  awk -F: '{print $7}' /etc/passwd | sort -u
  ```
- Find + exec: Remove blank lines from every `.conf` under `/tmp/conf.d`.
  ```bash
  find /tmp/conf.d -name '*.conf' -exec sed -i '/^$/d' {} \;
  ```
- Mix grep/sed/awk: Show service names and states from `systemctl list-units --type=service`.
  ```bash
  systemctl list-units --type=service --no-pager | awk 'NR>1 {print $1, $4}'
  ```
