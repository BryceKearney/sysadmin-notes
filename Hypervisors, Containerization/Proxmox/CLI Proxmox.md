Using CLI for proxmox? Fun! Here is some commands to help you with that

-----------
List all virtual machines
```
qm list
```

--------
Check status of a specific VM.
```
qm status 100
```
* Make sure to change the VMID

-------
Control VMs.
```
qm start 100
qm stop 100
qm reboot 100
```
* Start
* Stop
* Reboot

---------
List LXC containers
```
`pct list`
```

------------------
Check Proxmox version and installed packages.
```
pveversion -v
```

--------------------
pvecm status
```
pvecm status
```

-----
Check storage (ZFS or LVM).
```
zfs list
```

```
lvs
```
- Monitors storage pools used by Proxmox for VM disks.
- **Tip**: If using ZFS, check pool health with zpool status.