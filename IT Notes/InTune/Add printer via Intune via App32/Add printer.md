Youtube video: https://www.youtube.com/watch?v=8glLCjBytIA - Brett Benson
A good guide: [How to install Printer Drivers and Printers from Intune using Win32 apps and PowerShell - MSEndpointMgr](https://msendpointmgr.com/2022/01/03/install-network-printers-intune-win32apps-powershell/)

Go to printer driver folder
Find .Cat and .inf file, if you none you need to enable show extensions at end of name. The type names are Security catalog and setup information as well.![[Pasted image 20250402161527.png]]
Pick the main driver, this one is the HPOnedrive_v4
You need it's pre-requisites, to find those right click the .inf and open with notepad and go to [SourceDisksNames]
For this driver it needs
So it needs the \x64 folder![[Pasted image 20250402161310.png]]
Grab the .cat, .inf, and the prerequisites and put them into a folder, I recommend a folder on C:\Temp:\name of driver
Create the Powershell scripts, make notepads, change name to Install-Printer.ps1 and Remove-Printer.ps1 and add the github scripts in https://github.com/MSEndpointMgr/Intune/blob/master/Windows%2010/Install-Printer.ps1
Install https://github.com/Microsoft/Microsoft-Win32-Content-Prep-Tool to make a Win32app
Use the Make Win32 app tool in the temp\(driver name) directory and run this script IntuneWinAppUtil.exe -c C:\Temp\(driver name) -s C:\Temp\(driver name)\install.ps1 -o C:\Temp\Output -q
Go to Intune, apps, create new app, use the win32 app from C:\Temp\output
make the [[Execution Script]](Called Install command in intune), change this to your settings  `powershell.exe -ExecutionPolicy Bypass -File .\Install-Printer.ps1 -PortName "10.10.10.254" -PrinterIP "10.10.10.254" -PrinterName "Receiving HP Copier" -DriverName "HP Smart Universal Printing" -INFFile "HPOneDriver_V4_x64.inf"`
Make uninstall command   
`powershell.exe -ExecutionPolicy Bypass -File .\Remove-Printer.ps1 -PrinterName "Receiving HP Copier"`
Add detection rule for Registry key HKEY_LOCAL_MACHINE\Software\Microsoft\Windows NT\CurrentVersion\Print\Printers\Receiving HP Copier

