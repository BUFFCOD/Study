# 🧾 RHCSA Text Processing & Regular Expression Practice

**Goal:** Strengthen your ability to analyze, search, and edit text files using Linux command-line utilities — essential for RHCSA success.  
**Focus Tools:** `head`, `tail`, `grep`, `awk`, `sed`, and regex fundamentals.  
**Environment:** Practice inside a RHEL 9/10 VM or container.

---

## 🔹 1. Quick Reference: Common Text Tools

| Command | Purpose | Example |
|----------|----------|----------|
| `head` | Show first lines of a file | `head -n 5 /etc/passwd` |
| `tail` | Show last lines of a file | `tail -n 10 /var/log/messages` |
| `sed` | Stream editor — print, delete, or replace text | `sed -n 5p /etc/passwd` |
| `awk` | Field processor and formatter | `awk -F: '{print $1}' /etc/passwd` |
| `grep` | Search text using patterns or regex | `grep root /etc/passwd` |

---

## 🔹 2. Practice Lab: Working with `/etc/passwd`

### 🧩 Basic Line Extraction
```bash
# Show the fifth line using head and tail
head -n 5 /etc/passwd | tail -n 1

# Show the fifth line using sed
sed -n 5p /etc/passwd
```

### 🧩 Filtering Fields with awk
```bash
# Show the last column from ps aux output
ps aux | awk '{print $NF}'

# Print username and shell neatly aligned
awk -F: '{printf "%-15s %s\n", $1, $7}' /etc/passwd

# Find all users whose shell is /bin/bash
awk -F: '$7 == "/bin/bash" {print $1}' /etc/passwd
```

### 🧩 Searching with grep
```bash
# Show files in /etc containing the word 'root'
grep -rw '\<root\>' /etc

# Show lines with exactly three characters
grep -rx '^...$' /etc/* 2>/dev/null

# Find “alex” but exclude “alexander”
grep -rw 'alex' /etc | grep -v 'alexander'
```

---

## 🔹 3. Regular Expression Reference (for grep, awk, sed)

| Symbol | Meaning | Example | Matches |
|---------|----------|----------|----------|
| `^` | Start of line | `^anna` | Lines beginning with *anna* |
| `$` | End of line | `bash$` | Lines ending with *bash* |
| `.` | Any single character | `r.t` | *rat*, *rot*, *rut* |
| `*` | Zero or more of the preceding character | `ab*c` | *ac*, *abc*, *abbc* |
| `+` | One or more (extended) | `ab+c` | *abc*, *abbc* (requires `-E` or `egrep`) |
| `?` | Zero or one | `colou?r` | *color*, *colour* |
| `[abc]` | One character from set | `gr[ae]y` | *gray*, *grey* |
| `[^abc]` | Any character not in set | `[^0-9]` | Any non-digit |
| `(abc)` | Grouping | `(foo|bar)` | *foo* or *bar* |

**Note:** Always quote regex:  
```bash
grep '^root' /etc/passwd
```

---

## 🔹 4. sed Essentials (Editing Streams)

| Task | Example |
|------|----------|
| Show a specific line | `sed -n 5p /etc/passwd` |
| Replace “bash” with “zsh” | `sed 's/bash/zsh/g' /etc/passwd` |
| In-place replacement | `sed -i 's/bash/zsh/g' /etc/passwd` |
| Delete a line | `sed -i '2d' ~/myfile` |
| Delete multiple ranges | `sed -i -e '2d;20,25d' ~/myfile` |

💡 **Safety Tip:** Always back up before in-place edits:
```bash
cp /etc/passwd ~/passwd.bak
```

---

## 🔹 5. RHCSA-Level Challenge Tasks

| Objective | Command Hint |
|------------|---------------|
| Show 5th line of `/etc/passwd` using head/tail | `head -n5 /etc/passwd \| tail -n1` |
| Display same line using sed | `sed -n 5p /etc/passwd` |
| Filter last column of ps aux | `ps aux \| awk '{print $NF}'` |
| List files in /etc containing word “root” | `grep -rw '\<root\>' /etc` |
| Find “alex” but not “alexander” | `grep -rw 'alex' /etc \| grep -v 'alexander'` |
| Delete line 10 of a test file | `sed -i '10d' test.txt` |
| Print usernames with bash shell | `awk -F: '$7~/bash$/ {print $1}' /etc/passwd` |
| Replace “PermitRootLogin no” with “yes” in sshd_config | `sudo sed -i 's/^PermitRootLogin no/PermitRootLogin yes/' /etc/ssh/sshd_config` |
| Show non-comment lines of /etc/fstab | `grep -v '^#' /etc/fstab` |
| Search recursively for IP addresses | `grep -Ero '([0-9]{1,3}\.){3}[0-9]{1,3}' /etc` |

---

## 🔹 6. Why It Matters for RHCSA

Red Hat tests your ability to:
- Search and extract information from system text files (`grep`, `awk`).
- Edit configuration files quickly (`sed`, `vim`, or `nano`).
- Use regex in administrative tasks.
- Automate small one-liners for troubleshooting or file updates.

Expect tasks such as:
- Filtering `/etc/passwd`, `/etc/group`, or `/etc/fstab`.
- Editing configuration lines under `/etc/ssh/` or `/etc/sysconfig/`.
- Extracting service or process data using `ps`, `awk`, and `grep` pipelines.

---

## ⚙️ 7. Optional Practice Extensions

- Build a daily script that:
  1. Extracts users with `/bin/bash`.
  2. Saves results to `~/lab/day2/users_bash.txt`.
  3. Replaces “bash” with “zsh” using `sed`.
  4. Displays number of matches using `grep -c`.

```bash
#!/bin/bash
awk -F: '$7~/bash$/ {print $1}' /etc/passwd > ~/lab/day2/users_bash.txt
sed -i 's/bash/zsh/g' ~/lab/day2/users_bash.txt
grep -c 'zsh' ~/lab/day2/users_bash.txt
```

---

✅ **Tip:** For the RHCSA exam, always practice your one-liners until they’re muscle memory.  
If you can confidently use `grep`, `awk`, and `sed` in pipelines, you’ll breeze through the text-analysis and troubleshooting sections.
