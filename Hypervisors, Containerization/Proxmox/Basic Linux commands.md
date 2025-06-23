Some easy Linux commands.

These are foundational commands for navigating, managing files, and understanding the system.

- **ls**: List directory contents.
    
    bash
    
    CollapseWrapRun
    
    Copy
    
    `ls -lah`
    
    - -l: Long format, -a: Show hidden files, -h: Human-readable sizes.
- **cd**: Change directory.
    
    bash
    
    CollapseWrapRun
    
    Copy
    
    `cd /var/log cd .. # Go up one directory`
    
- **pwd**: Print working directory.
    
    bash
    
    CollapseWrapRun
    
    Copy
    
    `pwd`
    
    - Shows your current location (e.g., /root).
- **cat and less**: View file contents.
    
    bash
    
    CollapseWrapRun
    
    Copy
    
    `cat /etc/hosts less /var/log/syslog`
    
    - cat: Prints entire file, less: Paginates (use q to quit).
- **grep**: Search text in files.
    
    bash
    
    CollapseWrapRun
    
    Copy
    
    `grep "error" /var/log/syslog`
    
    - Case-insensitive: grep -i "error".
    - Recursive search: grep -r "string" /path.
- **find**: Locate files/directories.
    
    bash
    
    CollapseWrapRun
    
    Copy
    
    `find / -name "config.txt"`
    
    - Search by size: find / -size +100M (files > 100MB).
- **cp, mv, rm**: Copy, move, and delete files.
    
    bash
    
    CollapseWrapRun
    
    Copy
    
    `cp file.txt /backup/ mv file.txt /new/location/ rm -r /old/directory/`
    
    - **Caution**: rm -rf / deletes everything—double-check commands!
- **chmod and chown**: Change file permissions and ownership.
    
    bash
    
    CollapseWrapRun
    
    Copy
    
    `chmod 644 file.txt chown user:group file.txt`
    
    - 644: Read/write for owner, read-only for others.
    - **Example Use**: Fix Proxmox config file permissions.
- **ps aux**: List running processes.
    
    bash
    
    CollapseWrapRun
    
    Copy
    
    `ps aux | grep qemu`
    
    - Find VM processes (qemu is Proxmox’s VM engine).
- **kill**: Terminate processes by PID.
    
    bash
    
    CollapseWrapRun
    
    Copy
    
    `kill 1234 kill -9 1234 # Force kill`
    
    - Find PID with ps aux or top.
- **ip a**: Show network interfaces and IP addresses.
    
    bash
    
    CollapseWrapRun
    
    Copy
    
    `ip a`
    
    - Check Proxmox’s network config (e.g., eth0 or vmbr0).
- **systemctl**: Manage services.
    
    bash
    
    CollapseWrapRun
    
    Copy
    
    `systemctl status pve-cluster systemctl restart pve-cluster systemctl enable sshd`
    
    - **Example Use**: Restart Proxmox’s web UI:
        
        bash
        
        CollapseWrapRun
        
        Copy
        
        `systemctl restart pveproxy`
        
- **who and w**: See logged-in users.
    
    bash
    
    CollapseWrapRun
    
    Copy
    
    `who w`
    
    - Useful for tracking SSH sessions.