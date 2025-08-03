---
title: at.deny
aliases:
  - at.deny
draft: false
tags:
  - AZ-104
  - Cloud
author:
  - Sarthak Chandajkar
---
The **at.deny** file is a system configuration file in Unix-like operating systems, used to control access to the `at` command, which schedules jobs for one-time execution at a specified time. It lists users who are explicitly **denied** from using `at` (and related commands like `batch`) to submit jobs, complementing the **at.allow** file. This note details its purpose, configuration, and usage in the context of job scheduling, with backlinks to related concepts.

## Purpose

The `at.deny` file restricts access to the `at` command, ensuring that only authorized users can schedule jobs. It is part of a two-file access control system:

- **at.allow**: If present, only users listed in this file can use `at`. The `at.deny` file is ignored.
- **at.deny**: If `at.allow` does not exist, users listed in `at.deny` are denied access, while all others are allowed.

This mechanism provides system administrators with fine-grained control over job scheduling, enhancing security by preventing unauthorized users from running potentially resource-intensive or malicious tasks.

> [!NOTE] Access Control Logic  
> If `at.allow` exists, it takes precedence, and `at.deny` is irrelevant. If only `at.deny` exists, it specifies users to exclude, implicitly allowing all others.

## Configuration

The `at.deny` file is typically located at `/etc/at.deny`. It contains a list of usernames, one per line, without additional syntax or comments. For example:

```
guest
user123
testuser
```

### Key Points

- **Default Behavior**: On many systems, `at.deny` exists by default and may include low-privilege users (e.g., `guest`, `nobody`) to prevent them from scheduling jobs.
- **Empty File**: An empty `at.deny` allows all users to use `at` (unless `at.allow` exists).
- **Permissions**: The file is owned by `root` and should have restricted permissions (e.g., `600`) to prevent unauthorized modifications.
- **Location**: Path may vary by system (e.g., `/etc/at.deny` on Linux, `/usr/lib/cron/at.deny` on some BSD systems).

### Real-World Example

On a university server, administrators add student accounts like `student01` to `/etc/at.deny` to prevent them from scheduling resource-heavy jobs that could disrupt research computations. Faculty accounts, not listed, can use `at` freely.

## Usage

The `at` command schedules jobs for later execution. For example:

```bash
at 10pm
echo "Backup started" > /var/log/backup.log
tar -czf /backup/data.tar.gz /data
<Ctrl+D>
```

If a user is listed in `at.deny`, they receive an error:

```
at: you are not authorized to use at. Sorry.
```

### Checking Access

Administrators can verify `at` access by:

1. Checking if `/etc/at.allow` exists (takes precedence).
2. If not, inspecting `/etc/at.deny` for denied users.
3. Testing with `at -l` (lists scheduled jobs) as a user.

### Modifying at.deny

To deny a user (e.g., `user123`):

```bash
sudo sh -c 'echo "user123" >> /etc/at.deny'
```

To allow a previously denied user, remove their name from `at.deny` using a text editor or command like:

```bash
sudo sed -i '/user123/d' /etc/at.deny
```

> [!TIP] Practical Tip  
> Regularly audit `at.deny` and `at.allow` to ensure only authorized users can schedule jobs, especially on shared systems. Use `ls -l /etc/at.*` to check file permissions and ownership.

## Integration with Job Schedulers

While `at` is for one-time jobs, `at.deny` contrasts with more complex schedulers like SLURM or Sun Grid Engine (SGE), which use scripts and directives (e.g., `#SBATCH` or `#$`) for batch job submission (see,). Unlike `at.deny`, these systems often rely on user permissions or queue configurations for access control.[](https://www.bu.edu/tech/support/research/system-usage/running-jobs/submitting-jobs/)[](https://vsoch.github.io/lessons/sherlock-jobs/)

### Real-World Example

In a high-performance computing (HPC) cluster, `at.deny` prevents non-admin users from scheduling lightweight `at` jobs, while SLURM manages heavy computational tasks (e.g., training [[Neural Networks]]) via `sbatch` scripts, ensuring resource allocation aligns with project priorities.

## Challenges

1. **Precedence Confusion**: If `at.allow` exists, `at.deny` is ignored, which can lead to misconfigured access.
    - **Solution**: Clearly document which file controls access and avoid creating both unnecessarily.
2. **Limited Granularity**: `at.deny` only restricts users, not specific commands or resources.
    - **Solution**: Use more advanced schedulers like SLURM for fine-grained control.
3. **System Variability**: File location and behavior may differ across Unix-like systems (e.g., Linux vs. BSD).
    - **Solution**: Check system documentation (e.g., `man at`).

## Implementation Example

Below is a Bash script to check if a user is denied `at` access:

```bash
#!/bin/bash
USER=$1
if [ -f /etc/at.allow ]; then
    if grep -Fx "$USER" /etc/at.allow > /dev/null; then
        echo "$USER is allowed to use at."
    else
        echo "$USER is denied by at.allow."
    fi
elif [ -f /etc/at.deny ]; then
    if grep -Fx "$USER" /etc/at.deny > /dev/null; then
        echo "$USER is denied by at.deny."
    else
        echo "$USER is allowed to use at."
    fi
else
    echo "$USER is allowed to use at (no at.deny or at.allow)."
fi
```

Run with:

```bash
./check_at_access.sh user123
```

This script checks `at.allow` first, then `at.deny`, reflecting the system’s access control logic.
