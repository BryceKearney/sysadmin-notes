
https://help.ui.com/hc/en-us/articles/204909754-Remote-Adoption-Layer-3

To Connect the Router to the Cloudkey at other site first do this

Connect to it via ip > log in > you'll see all the others are grayed out > go to manually log in
---------------------

SSH into the device, default username and password usually is UBNT for both.

Then just run command twice, you may need to port forward.

I highly recommend running this command twice, and then adopting the device

set-inform http://PUBLICIP:8080/inform

-------------------------------

If doesn't take UBNT password for switch, hold reset for full minute.

Usually for unifi Switches and routers
Username: ubnt
Password: ubnt

For Unifi UXG
Username: root
Password: ubnt