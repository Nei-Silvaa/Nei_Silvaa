# Linux User Management

## Objective
Manage the full lifecycle of an employee account on a Linux system — creation, file ownership, group membership, and removal — for a new employee (`researcher9`) joining an organization.

## Tools used
<div>
    <img src="https://img.shields.io/badge/-Linux-FCC624?style=for-the-badge&logo=Linux&logoColor=black" />
    <img src="https://img.shields.io/badge/-Bash-4EAA25?style=for-the-badge&logo=GNU_Bash&logoColor=white" />
    <img src="https://img.shields.io/badge/-sudo-2C3E50?style=for-the-badge" />
</div>

## Summary
A new employee, `researcher9`, joined the organization and needed a fully managed Linux account: created with the correct primary group, given ownership of a project file, added to a secondary group for cross-team access, and later fully removed from the system — including cleaning up a leftover group that `userdel` did not remove automatically.

## Process

### 1. Add the new employee
Created the user account and set their primary group to `research_team` using `useradd` followed by `usermod -g`.

### 2. Change ownership of a file
Used `chown` (run with `sudo`, since changing ownership is a superuser-level action) to make `researcher9` the owner of `project_r.txt`.

### 3. Add the employee to a secondary group
Used `usermod -a -G` to add `researcher9` to the `sales_team` group as a **secondary** group — the lowercase `-a` (append) and uppercase `-G` (secondary groups) flags matter here, since Linux commands are case-sensitive and using the wrong case would overwrite rather than append group membership.

### 4. Delete the employee from the system
Ran `sudo userdel researcher9` to remove the user. The system returned a warning that the group `researcher9` was not removed automatically, since it was not the user's primary group. Ran `sudo groupdel researcher9` separately to clean up that leftover group, completing the offboarding process.

## Key commands

```bash
sudo useradd researcher9                       # create the new user
sudo usermod -g research_team researcher9      # set primary group
sudo chown researcher9 /home/researcher2/projects/project_r.txt   # transfer file ownership
sudo usermod -a -G sales_team researcher9      # add to a secondary group
sudo userdel researcher9                       # remove the user
sudo groupdel researcher9                      # remove leftover group manually
```

## Key takeaways
- `usermod -g` sets a **primary** group while `usermod -a -G` appends a **secondary** group — mixing these up (or forgetting `-a`) can unintentionally strip a user's existing group memberships.
- `userdel` does not automatically remove a group unless it was that user's primary group — offboarding isn't complete until leftover groups are checked and cleaned up with `groupdel`.
- Linux command flags are case-sensitive; a lowercase vs. uppercase flag (`-a` vs `-A`, `-g` vs `-G`) can produce a completely different result.

## Files
- [Full report (PDF)](./add-and-manage-users-with-linux-commands.pdf) — original write-up
