
Easy way is to use disk-part to turn the USB offline, if you use set-disk it will give you error below

You **cannot pass through USB devices like dongles, HID devices (keyboard/mouse), or specialty hardware directly** to a Hyper-V VM without a workaround (like RDP or USB over IP software).

-----------

The more advanced way is installing a vhdx on the USB, and adding it as a share to your PC, and adding it to Hyper-V as a virtual disk

Use Powershell:
New-VHD -Path "E:\VMDisks\MyDrive.vhdx" -SizeBytes 20GB -Dynamic

Mount-VHD -Path "E:\VMDisks\MyDrive.vhdx"
Initialize-Disk -Number # -PartitionStyle GPT
Then format it
If lazy, use this to format "New-Partition -UseMaximumSize -AssignDriveLetter |
  Format-Volume -FileSystem NTFS -NewFileSystemLabel "USBVHD"

Open Hyper-v
Add Hard drive > use phyiscal Hard disk
![[Pasted image 20250523104051.png]]
You can now access it in Hyper-V, and on your disk