Want users to be able to change their password at first sign in? Enable this to get fix that pesky problem!

```
Set-ADSyncAADCompanyFeature -ForcePasswordChangeOnLogOn $true
```


- **Purpose**: Enables the synchronization of the "User must change password at next logon" flag from on-premises Active Directory to Microsoft Entra ID.
- **Effect**: When this feature is enabled (set to $true), if a user account in the on-premises AD has the "User must change password at next logon" attribute set, this setting will be synchronized to Microsoft Entra ID. As a result, when the user logs into a Microsoft Entra ID service (e.g., Microsoft 365), they will be prompted to change their password at their next login.

---------

- **Prerequisites**:

- Requires Microsoft Entra Connect version **2.0.3.0 or higher** to support synchronization of temporary passwords.[
    
- Password Hash Synchronization (PHS) and Self-Service Password Reset (SSPR) with Password Writeback should be enabled for full functionality, ensuring password changes in Entra ID are synced back to on-premises AD.

---

**Limitations**:

- This feature primarily applies to scenarios involving **admin-initiated password resets**. Newly created users without a password in Entra ID are automatically prompted to set one, regardless of this setting.[
    
    ![](https://imgs.search.brave.com/ImsDLl-j1sx4E470lOVcJdjxJ_afTjiJ8P5eUDx4tFU/rs:fit:64:0:0:0/g:ce/aHR0cDovL2Zhdmlj/b25zLnNlYXJjaC5i/cmF2ZS5jb20vaWNv/bnMvMmMzNjVjYjk4/NmJkODdmNTU4ZDU1/MGUwNjk0MWFmZWU0/NmYzZjVlYmZjZDIy/MWM4MGMwODc4MDhi/MDM5MmZkYy9sZWFy/bi5taWNyb3NvZnQu/Y29tLw)
    
    ](https://learn.microsoft.com/en-us/entra/identity/hybrid/connect/how-to-connect-password-hash-synchronization)
- The "change password at next logon" prompt does not apply when logging into or unlocking Entra ID-joined workstations; it only affects Entra ID login scenarios (e.g., web-based logins).[
    
    ![](https://imgs.search.brave.com/hggd-Y3QefjSGG7cxRr3V9jYTMm7J0ERolasVJGJzkw/rs:fit:64:0:0:0/g:ce/aHR0cDovL2Zhdmlj/b25zLnNlYXJjaC5i/cmF2ZS5jb20vaWNv/bnMvNWIwYzE4M2Mw/YmNiNWI5NjdjNmIz/ZGE1NmExNDRmN2Q3/MGYxY2NlZTYzYTQ5/ZjU0ZGYzYmFkZjVj/NmM2ZDFhNi9zcGVj/b3Bzc29mdC5jb20v)
    
    ](https://specopssoft.com/blog/user-must-change-password-at-next-login-azure-ad/)
- Requires a subsequent synchronization cycle (e.g., Start-ADSyncSyncCycle -PolicyType Delta) to propagate the change to Entra ID.
