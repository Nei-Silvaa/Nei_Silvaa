# Linux File Permissions

## Objective
Audit and correct file and directory permissions in `/home/researcher2/projects` — including hidden files — to enforce the principle of least privilege for the user `researcher2` (member of the `research_team` group).

## Tools used
<div>
    <img src="https://img.shields.io/badge/-Linux-FCC624?style=for-the-badge&logo=Linux&logoColor=black" />
    <img src="https://img.shields.io/badge/-Bash-4EAA25?style=for-the-badge&logo=GNU_Bash&logoColor=white" />
    <img src="https://img.shields.io/badge/-chmod-2C3E50?style=for-the-badge" />
</div>

## Summary
Given a directory with several project files, I audited the existing user/group/other permissions — including a hidden file — and identified cases where **other** had unauthorized write access. I used `chmod` to remove that excess access on both a regular file and a hidden file, and corrected a directory permission as well, following least-privilege principles throughout.

## Process

### 1. Check file and directory details
Ran `ls -l` and `ls -la` inside `/home/researcher2/projects` to list all files, including the hidden file `.project_x.txt` and the `drafts` subdirectory, and read the 10-character permission string on each entry.

### 2. Describe the permissions string
Documented existing permissions for all five files and the `drafts` subdirectory. Notable findings:
- `project_k.txt` — user: rw, group: rw, **other: rw** ⚠️ (other should not have write access)
- `project_m.txt` — user: rw, group: r, other: none
- `project_r.txt` — user: rw, group: rw, other: r
- `project_t.txt` — user: rw, group: rw, other: r
- `.project_x.txt` (hidden) — user: rw, group: w, other: none
- `drafts` (directory) — user: rwx, group: x, other: none

### 3. Change file permissions
Removed write access for **other** on `project_k.txt`, and reduced `project_m.txt` group access to remove read as well, per the requirement that "other" should never have write access to any file.

### 4. Change permissions on the hidden file
On `.project_x.txt`, removed write access from **user** and **group**, and added read access to **group**, ensuring no one has write access to that file while user and group retain read access.

### 5. Change directory permissions
While updating the `drafts` directory, I initially forgot to prefix the command with `chmod`, causing a `command not found` error. I caught the mistake, corrected it, and removed execute access for **group** on the directory.

## Key commands

```bash
ls -la                              # list all files, including hidden ones, with permissions
chmod o-w project_k.txt             # remove write access from "other"
chmod g-r project_m.txt             # remove read access from "group"
chmod u-w,g-w,g+r .project_x.txt    # remove write from user/group, add read to group (hidden file)
chmod g-x drafts                    # remove execute access from "group" on a directory
```

## Key takeaways
- Hidden files (prefixed with `.`) are easy to overlook but must be audited with the same rigor as regular files — `ls -la` is essential, not `ls -l`.
- Least privilege means checking every file individually rather than assuming a directory-wide policy is being followed; each file in this project had a different permission gap.
- A single missing keyword (`chmod`) is enough to break a command — reviewing commands before executing them, especially with `sudo`-level changes, prevents avoidable errors.

## Files
- [Full report (PDF)](./file-permissions-in-linux.pdf) — original write-up
