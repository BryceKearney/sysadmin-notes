Make your own office tools with or without ones. You just need to put the XML beside the 

https://config.office.com/deploymentsettings

2. Configure Office Deployment Settings
You'll go through several tabs with settings:

3. Products and releases
Architecture: Choose 64-bit or 32-bit (usually 64-bit).

Office Suite: Select Microsoft 365 Apps for enterprise or business, or another Office version.

Additional Products: Add Visio, Project, etc.

Version: Choose "Latest" or specify a version.

Channel: Choose update channel (Current, Monthly Enterprise, Semi-Annual, etc.).

2. Language
Select primary and any additional languages for the install.

3. Installation
Install behavior: Choose to install for all users or just the current user.

Automatically accept EULA: Usually enabled for silent installs.

Installation path: Optional, can specify custom install location.

4. Update and upgrade
Configure how updates are managed (auto-update, source path, etc.).

5. Licensing and activation
Choose whether to auto-activate with a shared computer license or not.

6. General
Configure Office background, theme, and disable first run experiences (e.g., "Show the Office welcome screen").

7. Application preferences
Configure settings per app (e.g., Outlook profile creation, disable animations in Office, etc.).

8. Export the Configuration
When finished, click "Export" at the top.

Choose "Office Open XML" or JSON format (for Configuration Manager or script-based deployment).

Save the configuration file (usually configuration.xml).

4. Deploy Office Using the Configuration
Download the Office Deployment Tool (ODT) from Microsoft:
 https://www.microsoft.com/en-us/download/details.aspx?id=49117

Place your configuration.xml in the same folder as setup.exe from ODT. Just beside each other.

Run this command to install Office using your custom settings:
setup.exe /configure configuration.xml

It will generate the office 365 install