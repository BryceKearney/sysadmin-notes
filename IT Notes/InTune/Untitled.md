Powershell - IntuneAutoEnroll
Auto enrolls the device into Intune MDM
### Potential Considerations

- **User vs. Device Enrollment**: If your MDM policy targets user-based enrollment, the user must be logged in with their Azure AD credentials when the task runs. For device-based enrollment, the device’s Azure AD identity is sufficient, and no user login is required.
- **Multiple Users**: If multiple users log into the device, the enrollment typically binds to the first user’s credentials or the device’s identity, depending on your MDM configuration.
- **Non-Intune MDM**: If you’re using a different MDM provider (e.g., VMware Workspace ONE), confirm that it supports Azure AD-based enrollment and whether additional registry settings or an enrollment URL are needed.

### What You Need to Ensure

You don’t need to modify the script to specify AAD credentials, but you should verify:

1. **Azure AD Join/Registration**:
    - Ensure the device is Azure AD-joined (AzureAdJoined : YES in dsregcmd /status) or registered.
    - For user-based enrollment, the logged-in user must have a valid Azure AD account.
2. **MDM Configuration**:
    - In your MDM provider (e.g., Intune), ensure automatic MDM enrollment is enabled for Azure AD devices/users. For Intune, this is configured under **Devices > Enroll devices > Automatic Enrollment**.
    - Verify the MDM discovery URL (e.g., https://enrollment.manage.microsoft.com/enrollmentserver/discovery.svc for Intune) is correctly set up in Azure AD.
3. **MDMApplicationId** (if applicable):
    - The script sets MDMApplicationId to an empty string (""), which works for Intune. If your MDM provider requires a specific ID (e.g., a GUID), update the MDMApplicationId value in the script, as noted in my previous response.
4. **Timing of Enrollment**:
    - The scheduled task runs 5 minutes after the script executes. Ensure a user is logged in (or the device is Azure AD-joined) at that time for user-based or device-based enrollment to proceed.


1. #*=============================================================================
    
2. #* SCRIPT BODY
    
3. #*=============================================================================
    

4. # Main Script Logic
    
5. try {
    

6. #### Local Machine Reg Section ####
    
7. #Reg Paths LM
    
8. $RegPoliciesLM = "HKLM:\SOFTWARE\Policies"
    
9. $RegMSLM = "$RegPoliciesLM\Microsoft"
    
10. $RegWINLM = "$RegMSLM\Windows"
    
11. $RegCVLM = "$RegWINLM\CurrentVersion"
    
12. $RegMDMLM = "$RegCVLM\MDM"
    

13. #Test Reg Locations and create if needed LM
    
14. $TestPoliciesLM = Test-Path $RegPoliciesLM
    
15. If ($TestPoliciesLM -eq $False){New-Item -Path "HKLM:\SOFTWARE" -Name "Policies" -Force}
    
16. $MSTestLM = Test-Path $RegMSLM
    
17. If ($MSTestLM -eq $False){New-Item -Path "$RegPoliciesLM" -Name "Microsoft" -Force}
    
18. $WINTestLM = Test-Path $RegWINLM
    
19. If ($WINTestLM -eq $False){New-Item -Path "$RegMSLM" -Name "Windows" -Force}
    
20. $CVTestLM = Test-Path $RegCVLM
    
21. If ($CVTestLM -eq $False){New-Item -Path "$RegWINLM" -Name "CurrentVersion" -Force}
    
22. $MDMTestLM = Test-Path $RegMDMLM
    
23. If ($MDMTestLM -eq $False){New-Item -Path "$RegCVLM" -Name "MDM" -Force}
    

24. #Test MDM LM
    
25. $MDMOldLM = Get-ItemProperty -Path "$RegMDMLM" -ErrorAction SilentlyContinue
    

26. If($MDMOldLM -eq $null) {
    
27. New-ItemProperty -Path "$RegMDMLM" -Name "AutoEnrollMDM" -PropertyType DWORD -Value "1" -Force
    
28. New-ItemProperty -Path "$RegMDMLM" -Name "UseAADCredentialType" -PropertyType DWORD -Value "1" -Force
    
29. New-ItemProperty -Path "$RegMDMLM" -Name "MDMApplicationId" -PropertyType String -Value "" -Force
    
30. }
    

31. $MDMAPPIDLM = Get-ItemProperty -Path "$RegMDMLM" -Name "MDMApplicationId" -ErrorAction SilentlyContinue
    

32. If (($MDMAPPIDLM -eq $Null) -or ($MDMAPPIDLM.'MDMApplicationId' -ne ""))
    
33. {
    
34. If ((Get-ItemProperty -Path $RegMDMLM -Name "MDMApplicationId" -ErrorAction SilentlyContinue) -eq $null) {
    
35. New-ItemProperty -Path "$RegMDMLM" -Name "MDMApplicationId" -PropertyType String -Value "" -Force}
    
36. Else {Set-ItemProperty -Path "$RegMDMLM" -Name "MDMApplicationId" -Value "" -Force}
    

37. If ((Get-ItemProperty -Path $RegMDMLM -Name "AutoEnrollMDM" -ErrorAction SilentlyContinue) -eq $null) {
    
38. New-ItemProperty -Path "$RegMDMLM" -Name "AutoEnrollMDM" -PropertyType DWORD -Value "1" -Force}
    
39. Else {Set-ItemProperty -Path "$RegMDMLM" -Name "AutoEnrollMDM" -Value "1" -Force}
    

40. If ((Get-ItemProperty -Path $RegMDMLM -Name "UseAADCredentialType" -ErrorAction SilentlyContinue) -eq $null) {
    
41. New-ItemProperty -Path "$RegMDMLM" -Name "UseAADCredentialType" -PropertyType DWORD -Value "1" -Force}
    
42. Else {Set-ItemProperty -Path "$RegMDMLM" -Name "UseAADCredentialType" -Value "1" -Force}
    

43. }
    

44. ###Setup Scheduled Task
    
45. $RunTime = (Get-Date).AddMinutes(5)
    
46. $STPrin = New-ScheduledTaskPrincipal -UserID "NT AUTHORITY\SYSTEM" -LogonType S4U -RunLevel Highest
    
47. $Stset = New-ScheduledTaskSettingsSet -RunOnlyIfNetworkAvailable -DontStopOnIdleEnd -ExecutionTimeLimit (New-TimeSpan -Hours 1)
    
48. $actionUpdate = New-ScheduledTaskAction -Execute %windir%\system32\deviceenroller.exe -Argument "/c /AutoEnrollMDM"
    
49. $triggerUpdate = New-ScheduledTaskTrigger -Once -At $RunTime
    

50. Register-ScheduledTask -Trigger $triggerUpdate -Action $actionUpdate -Settings $Stset -TaskName "MDMAutoEnroll" -Principal $STPrin -Force
    

51. $TargetTask = Get-ScheduledTask -TaskName "MDMAutoEnroll"
    
52. $TargetTask.Triggers[0].StartBoundary = $RunTime.ToString("yyyy-MM-dd'T'HH:mm:ss")
    
53. $TargetTask.Triggers[0].EndBoundary = $RunTime.AddMinutes(10).ToString("yyyy-MM-dd'T'HH:mm:ss")
    
54. $TargetTask.Settings.DeleteExpiredTaskAfter = "PT0S"
    
55. $TargetTask | Set-ScheduledTask
    

56. } catch [System.Exception] {
    
57. Write-Log $_ -PrependText "FATAL: An unhandled exception was caught. The script will now exit as failed."
    
58. Exit-Script -ReturnCode -999
    
59. Return
    
60. }
    

61. Exit-Script -ReturnCode 0 # End successfully
    

62. #*=============================================================================
    
63. #* END OF SCRIPT
    
64. #*=============================================================================