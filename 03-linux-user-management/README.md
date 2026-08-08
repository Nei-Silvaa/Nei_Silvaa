# Linux User Management

## Objective
Create, modify, and manage user accounts and privileges on a Linux system using command-line tools — complementing file-permission work with the identity side of access control (IAM fundamentals).

## Tools used
<div>
    <img src="https://img.shields.io/badge/-Linux-FCC624?style=for-the-badge&logo=Linux&logoColor=black" />
    <img src="https://img.shields.io/badge/-Bash-4EAA25?style=for-the-badge&logo=GNU_Bash&logoColor=white" />
</div>

## Summary
*(Replace with a short summary: which user-management scenarios you worked through — adding users, assigning groups, setting privileges, deleting/locking accounts.)*

## Process
1. **Adding users** — commands used (`useradd`, `adduser`) and configuration choices
2. **Managing groups & privileges** — `usermod`, `groupadd`, `sudo` access
3. **Verifying and auditing** — how you confirmed accounts were configured correctly

## Key commands

```bash
# example — replace with the actual commands from your lab
useradd -m -s /bin/bash newuser
usermod -aG sudo newuser
passwd newuser
```

## Key takeaways
- *(1–2 lessons learned about account management or security implications)*

## Files
- `add-and-manage-users-with-linux-commands.pdf` — full write-up *(export your Google Doc as PDF and place it here)*
