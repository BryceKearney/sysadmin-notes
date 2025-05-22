TLDR: good for maintaining, auditing, troubleshooting, use CMTrace for Intunes.

https://learn.microsoft.com/en-us/intune/configmgr/core/support/tools

The Configuration Manager tools primarily include [client-based](https://learn.microsoft.com/en-us/intune/configmgr/core/support/tools#client-tools) and [server-based tools](https://learn.microsoft.com/en-us/intune/configmgr/core/support/tools#server-tools). Use these tools to help support and troubleshoot your Configuration Manager infrastructure.

These tools are in the `ClientTools` subfolder:

- [Client Spy](https://learn.microsoft.com/en-us/intune/configmgr/core/support/clispy): Troubleshoot issues related to software distribution, inventory, and metering
    
- [Deployment Monitoring Tool](https://learn.microsoft.com/en-us/intune/configmgr/core/support/deployment-monitoring-tool): Troubleshoot applications, updates, and baseline deployments
    
- [Policy Spy](https://learn.microsoft.com/en-us/intune/configmgr/core/support/policy-spy): View policy assignments
    
- [Power Viewer Tool](https://learn.microsoft.com/en-us/intune/configmgr/core/support/power-viewer-tool): View status of power management feature
    
- [Send Schedule Tool](https://learn.microsoft.com/en-us/intune/configmgr/core/support/send-schedule-tool): Trigger schedules and evaluations of configuration baselines'
-

## More tools in the folder

The following tools are in the `CD.Latest\SMSSETUP\TOOLS` folder on the site server:

- [CMTrace](https://learn.microsoft.com/en-us/intune/configmgr/core/support/cmtrace): View, monitor, and analyze Configuration Manager log files.
    
- [Content Library Explorer](https://learn.microsoft.com/en-us/intune/configmgr/core/support/content-library-explorer): View contents of the content library single instance store
    
- [Content Library Transfer](https://learn.microsoft.com/en-us/intune/configmgr/core/support/content-library-transfer): Transfers content library between drives
    
- [Content Ownership Tool](https://learn.microsoft.com/en-us/intune/configmgr/core/support/content-ownership-tool): Changes ownership of orphaned packages. These packages exist in the site without an owning site server.
    
- [Role-based Administration and Auditing Tool](https://learn.microsoft.com/en-us/intune/configmgr/core/support/rbaviewer): Helps administrators audit roles configuration
    
- [CMPivot](https://learn.microsoft.com/en-us/intune/configmgr/core/servers/manage/cmpivot): Use the standalone version of this tool to query real-time data from clients.
    
- [Update reset tool](https://learn.microsoft.com/en-us/intune/configmgr/core/servers/manage/update-reset-tool): Fix issues when in-console updates have problems downloading or replicating.
    
- [Configuration Manager group policy administrative template](https://learn.microsoft.com/en-us/intune/configmgr/core/clients/deploy/deploy-clients-to-windows-computers#configure-and-assign-client-installation-properties-by-using-a-group-policy-object): Configure and assign client installation properties by using a group policy object.
    
- [Content library cleanup tool](https://learn.microsoft.com/en-us/intune/configmgr/core/plan-design/hierarchy/content-library-cleanup-tool): Remove orphaned content from a distribution point.
    
- [Extend and migrate on-premises site to Microsoft Azure](https://learn.microsoft.com/en-us/intune/configmgr/core/support/azure-migration-tool): Helps you to programmatically create Azure virtual machines (VMs) for Configuration Manager.
    
- [Synchronize Microsoft 365 Apps updates from a disconnected software update point](https://learn.microsoft.com/en-us/intune/configmgr/sum/get-started/synchronize-office-updates-disconnected) (OfflineUpdateExporter): Import Microsoft 365 Apps updates from an internet connected WSUS server into a disconnected Configuration Manager environment.
    
- [Configure client communication ports](https://learn.microsoft.com/en-us/intune/configmgr/core/clients/deploy/configure-client-communication-ports): Reconfigure the port numbers for existing clients.
    
- [Service Connection Tool](https://learn.microsoft.com/en-us/intune/configmgr/core/servers/manage/hierarchy-maintenance-tool-preinst.exe): Keep your site up to date when your service connection point is offline.
    
- [Support Center](https://learn.microsoft.com/en-us/intune/configmgr/core/support/support-center): Gather information from clients for easier analysis when troubleshooting.
- [DP Job Queue Manager](https://learn.microsoft.com/en-us/intune/configmgr/core/support/dp-job-manager): Troubleshoots content distribution jobs to distribution points
    
- [Collection Evaluation Viewer](https://learn.microsoft.com/en-us/intune/configmgr/core/support/ceviewer): View collection evaluation details
    
* ***OneTrace** is a modern log viewer with Support Center. It works similarly to CMTrace, with improvements. For more information, see [Support Center OneTrace](https://learn.microsoft.com/en-us/intune/configmgr/core/support/support-center-onetrace).
* 