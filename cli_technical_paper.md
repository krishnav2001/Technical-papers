# Comprehensive Linux CLI & System Administration Guide

This technical paper contains the important concepts of cli like the Processes & ports, Managing software,
File Permissions,
Pipes and Redirection


---




## 1. Processes and Process Management

A process is an instance of an executing program. Every process in Linux is assigned a unique **Process ID (PID)**.

### Key Commands

*   **`ps`** – It basically gives a snapshot of the current processes.
    ```bash
    ps aux                  # Display all running processes for all users
    ps -ef                  # Full-format process listing
    ps aux | grep nginx     # Search for a specific process (e.g., nginx)
    ```

*   **`top` & `htop`** – It gives a dynamic real-time view of running processes.
    ```bash
    top                     # Default interactive process monitor
    htop                    # Enhanced interactive process viewer (requires installation)
    ```

*   **`pgrep` & `pkill`** – Look up or signal processes by name.
    ```bash
    pgrep -l python         # List PIDs and names of processes matching "python"
    pkill -f python         # Send termination signal to all processes matching "python"
    ```

*   **`kill` & `killall`** – It Terminate processes using PID or name.
    ```bash
    kill 1234               # Send SIGTERM (15) to PID 1234 (Graceful shutdown)
    kill -9 1234            # Send SIGKILL (9) to PID 1234 (Force kill)
    killall node            # Terminate all processes named "node"
    ```



---

## 2. Ports and Networking

Ports are virtual endpoints for network communication. Network sockets consist of an IP address and a port number (e.g., `127.0.0.1:8080`).

### Viewing Open Ports & Connections

*   **`ss`** – Utility to investigate sockets (replaces legacy `netstat`).
    ```bash
    ss -tuln                # List TCP (-t) and UDP (-u) listening (-l) numeric (-n) ports
    ss -tulnp               # Include process information (-p) (Requires sudo)
    ```

*   **`lsof`** – List open files and the processes using network ports.
    ```bash
    lsof -i :8080           # Find which process is listening on port 8080
    lsof -i TCP:1-1024      # Show open TCP ports in range 1–1024
    ```

*   **`netstat`** (Legacy)
    ```bash
    netstat -tulnp          # Show listening ports and programs
    ```

### Network Troubleshooting
```bash
ping google.com             # Test network connectivity to a host
curl -I https://example.com # Fetch HTTP headers of a website
nc -zv 192.168.1.1 22       # Netcat port scan on a specific host and port
```

---

## 3. File Permissions and Access Control

Linux utilizes a multi-user permission model divided into three categories: **Owner (u)**, **Group (g)**, and **Others (o)**.

### Permission Structure

| Permission | Symbol | Numeric Value | Meaning (File) | Meaning (Directory) |
| :--- | :---: | :---: | :--- | :--- |
| **Read** | `r` | `4` | View contents | List directory contents |
| **Write** | `w` | `2` | Modify contents | Add/delete files in directory |
| **Execute** | `x` | `1` | Run as executable | Enter (`cd`) into directory |

A file with `-rwxr-xr--` means:
*   **Owner:** `rwx` (7)
*   **Group:** `r-x` (5)
*   **Others:** `r--` (4)

### Commands

*   **`chmod`** – Change file access permissions.
    ```bash
    # Numeric (Octal) Notation
    chmod 755 script.sh     # rwxr-xr-x (Owner: full, Group/Others: read+exec)
    chmod 600 secret.txt    # rw------- (Owner: read/write, Group/Others: none)

    # Symbolic Notation
    chmod u+x script.sh     # Add execute permission to User
    chmod g-w file.txt      # Remove write permission from Group
    chmod -R 755 /var/www   # Apply permissions recursively
    ```

*   **`chown`** – Change file owner and group.
    ```bash
    chown john file.txt           # Change owner to "john"
    chown john:developers file.txt# Change owner to "john" and group to "developers"
    chown -R john:www-data /var/www# Change ownership recursively
    ```

---

## 4. Pipes and I/O Redirection

Every Linux process uses three standard I/O streams:
*   `stdin` (Standard Input - File Descriptor `0`)
*   `stdout` (Standard Output - File Descriptor `1`)
*   `stderr` (Standard Error - File Descriptor `2`)

### Redirection Operators

```bash
# Redirecting Output
command > output.txt        # Overwrite stdout to output.txt
command >> output.txt       # Append stdout to output.txt

# Redirecting Error
command 2> error.log        # Direct stderr to error.log
command > output.txt 2>&1   # Redirect both stdout and stderr to output.txt
command &> output.txt       # Shorthand for redirecting stdout and stderr

# Discarding Output
command > /dev/null 2>&1    # Suppress all output completely

# Redirecting Input
command < input.txt         # Pass file contents as stdin to command
```

### Pipelines (`|`)

Pipes connect the `stdout` of one command directly to the `stdin` of another.

```bash
# Search for specific running processes
ps aux | grep "nginx"

# Count total line entries matching a log pattern
cat access.log | grep "404" | wc -l

# Sort and find unique entries
cat names.txt | sort | uniq

# Real-time monitoring and saving to a file simultaneously using `tee`
echo "System Update Executed" | tee -a deployment.log
```

---

## 5. Managing Software (Package Managers)

Linux distributions rely on package managers to install, update, and remove software.

### Ubuntu / Debian (`apt`)
```bash
sudo apt update                   # Refresh package repository indices
sudo apt upgrade                  # Upgrade all installed packages
sudo apt install nginx -y         # Install a package without prompting

```

### RHEL / CentOS / Fedora (`dnf` / `yum`)
```bash
sudo dnf check-update             # Check for available updates
sudo dnf upgrade                  # Upgrade packages

```

### Arch Linux (`pacman`)
```bash
sudo pacman -Sy                   # Update package lists
sudo pacman -Syu                  # Update entire system

```

---

## 6. Environment Variables & Shell Configs

Environment variables store system configurations and user preferences accessed by processes.

```bash
# Viewing Variables
env                               # Print all environment variables
echo $PATH                        # Print PATH variable (lookup path for binaries)
echo $USER                        # Show current logged-in user

# Setting Variables
export APP_ENV="production"       # Set an environment variable for the session


```

---

## 7. System Monitoring & Disk Usage

Command-line utilities for tracking hardware resources and storage utilization.

```bash
# Disk Space & Usage
df -h                             # Human-readable summary of disk filesystem usage
du -sh /var/log/*                 # Human-readable summary of directory space usage

# Memory & CPU
free -h                           # Display used and free RAM/Swap memory
uptime                            # Show how long the system has been running + load average


```
---

#  Command Cheat Sheet

| Task | Command |
|---|---|
| Current directory | `pwd` |
| List files | `ls` |
| Detailed list | `ls -l` |
| Hidden files | `ls -la` |
| Change directory | `cd` |
| Home directory | `cd ~` |
| Create directory | `mkdir` |
| Create file | `touch` |
| Copy | `cp` |
| Move/rename | `mv` |
| Delete | `rm` |
| Read file | `cat` |
| First lines | `head` |
| Last lines | `tail` |
| Search text | `grep` |
| Find files | `find` |
| Process list | `ps` |
| Process monitor | `top` / `htop` |
| Kill process | `kill PID` |
| Disk space | `df -h` |
| Directory size | `du -sh` |
| IP information | `ip addr` |
| Network test | `ping` |
| Listening ports | `ss -tulnp` |
| Current user | `whoami` |
| Kernel/system info | `uname -a` |
| Command location | `which` / `command -v` |
| Manual | `man` |
| Superuser command | `sudo` |
| Install package | `sudo apt install` |

---
