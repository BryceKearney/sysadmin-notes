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

```
apt update
apt upgrade -y
```


-------------
```
dmesg | tail -n 20
```

```
dmesg | tail -n 20
```