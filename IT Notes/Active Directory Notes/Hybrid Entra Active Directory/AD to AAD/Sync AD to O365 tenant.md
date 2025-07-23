If you make a change in a hybrid AD environment run this command in PowerShell Administrator to sync changes. Has to be ran on the DC.

Start-ADSyncSyncCycle -PolicyType Delta

---

# Checking sync settings  

```
Get-ADSyncScheduler
```
  - **Purpose**: Retrieves the current configuration and status of the Azure AD Connect synchronization scheduler.
- **Details**: This cmdlet provides information about the synchronization schedule, such as:
    - Whether the scheduler is enabled or disabled.
    - The interval between synchronization cycles (e.g., every 30 minutes by default).
    - The last sync time and the type of sync (Initial or Delta).
    - The status of the next scheduled sync.
- **Use Case**: Use this to check the current state of the sync process, troubleshoot issues, or verify sync settings.

-----

# Forcing a sync  

```
Start-ADSyncSyncCycle Initial  
```
- **Purpose**: Triggers a full synchronization cycle.
- **Details**:
    - An **Initial** sync performs a complete synchronization of all objects and attributes from the on-premises AD to Microsoft Entra ID, regardless of whether they have been previously synced.
    - This process is resource-intensive and typically used when setting up Azure AD Connect for the first time, after significant configuration changes, or when a full refresh is needed.
- **Use Case**: Run this when you need to re-sync all data, such as after major AD changes or schema updates.


RUN POWERSHELL AS ADMIN.
```
Start-ADSyncSyncCycle -PolicyType Delta  
```
- **Purpose**: Triggers a delta synchronization cycle. - **RECOMMENDED for minor changes**
- **Details**:
    - A **Delta** sync only processes changes (additions, modifications, or deletions) in AD objects since the last sync.
    - This is less resource-intensive than an Initial sync and is the default mode for regular synchronization cycles.
- **Use Case**: Use this to manually initiate a sync for recent changes without performing a full sync, such as after minor updates to user accounts or groups


----------
       
# Synchronization can be paused or un-paused with the following PowerShell cmdlets.  
Set-ADSyncScheduler –SyncCycleEnabled $False  
Set-ADSyncScheduler –SyncCycleEnabled $True

- **Purpose**: Resumes or enables the synchronization scheduler.
- **Details**:
    - Re-enables the automatic sync schedule, allowing Azure AD Connect to resume syncing at the configured interval (e.g., every 30 minutes).
- **Use Case**: Use this to restore normal sync operations after pausing the scheduler for maintenance or troubleshooting.
