If you make a change in a hybrid AD environment run this command in PowerShell Administrator to sync changes. Has to be ran on the DC.

Start-ADSyncSyncCycle -PolicyType Delta

---

# Checking sync settings  
Get-ADSyncScheduler  
       - **Purpose**: Retrieves the current configuration and status of the Azure AD Connect synchronization scheduler.
- **Details**: This cmdlet provides information about the synchronization schedule, such as:
    - Whether the scheduler is enabled or disabled.
    - The interval between synchronization cycles (e.g., every 30 minutes by default).
    - The last sync time and the type of sync (Initial or Delta).
    - The status of the next scheduled sync.
# Forcing a sync  
Start-ADSyncSyncCycle Initial  
Start-ADSyncSyncCycle Delta  
       
# Synchronization can be paused or un-paused with the following PowerShell cmdlets.  
Set-ADSyncScheduler –SyncCycleEnabled $False  
Set-ADSyncScheduler –SyncCycleEnabled $True