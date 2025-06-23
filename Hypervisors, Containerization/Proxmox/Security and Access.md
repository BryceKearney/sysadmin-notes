Basic security commands to protect your server.

- **passwd**: Change your password.
    
    bash
    
    CollapseWrapRun
    
    Copy
    
    `passwd`
    
    - Set a strong root password.
- **ufw**: Simple firewall management.
    
    bash
    
    CollapseWrapRun
    
    Copy
    
    `apt-get install ufw ufw allow 8006 # Allow Proxmox web UI ufw allow ssh ufw enable ufw status`
    
    - **Proxmox Note**: Open ports 8006 (web UI), 22 (SSH), and VM-specific ports.
- **fail2ban**: Protect against brute-force attacks.
    
    bash
    
    CollapseWrapRun
    
    Copy
    
    `apt-get install fail2ban systemctl status fail2ban`
    
    - Configures bans for repeated failed logins (e.g., SSH).
- **adduser and deluser**: Manage users.
    
    bash
    
    CollapseWrapRun
    
    Copy
    
    `adduser newuser deluser newuser`
    
    - Avoid using root for daily tasks; create a user with sudo access.

---

### 6. Beginner Tips and Best Practices

- **Backups**: Use Proxmox’s built-in backup tool (vzdump) or configure external backups. Check backups with:
    
    bash
    
    CollapseWrapRun
    
    Copy
    
    `ls /var/lib/vz/dump/`
    
- **Snapshots**: Take VM/container snapshots before changes:
    
    bash
    
    CollapseWrapRun
    
    Copy
    
    `qm snapshot 100 snap1`
    
- **Logs**: Regularly check /var/log/syslog or /var/log/messages for issues.
- **Documentation**: Keep a notepad with commands and server details (IPs, ports, VM IDs).
- **Test Commands**: Use --dry-run or test on a non-critical system to avoid mistakes.
- **Learn man**: Read command manuals (e.g., man ls).
- **Cron Jobs**: Automate tasks (e.g., updates) with crontab -e:
    
    bash
    
    CollapseWrapRun
    
    Copy
    
    `0 2 * * * apt update && apt upgrade -y`
    
    - Runs updates daily at 2 AM.