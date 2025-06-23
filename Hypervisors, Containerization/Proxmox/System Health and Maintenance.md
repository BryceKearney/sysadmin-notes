These commands help you ensure the system is stable, up-to-date, and free of issues.

------------
View recent system logs for hardware or kernel errors

```
dmesg | tail -n 20
```
- Look for errors (e.g., disk failures, CPU issues).
- **Tip**: Use dmesg --level=err,crit to filter critical errors.

--------------
View system logs (systemd journal) for troubleshooting.

```
journalctl -xe
```
- Scroll with arrow keys, q to quit.
- Filter by service: journalctl -u pve-cluster.service (for Proxmox-specific issues).
- **Real-Time Logs**: journalctl -f (like tail -f).

------------------
Update and upgrade system packages. No more to it.
```
apt update
apt upgrade -y
```
- Run regularly to apply security patches.
- **Proxmox Note**: For Proxmox, ensure you’re subscribed to the appropriate repository (free or enterprise). Check /etc/apt/sources.list.d/pve-enterprise.list or use the no-subscription repo.
- **Caution**: Always back up critical VMs before upgrading.

-------------
Clean up unused packages and cache.

```
apt autoremove
apt autoclean
```
* Frees disk space and keeps the system tidy.
* Make a backup first
