Locks down IOS devices fully, enabling no one outside the company to use them. Not a MDM, but can connect to one. Usually Intune.

Make sure to connect your VPP token to Intune, and that if you have phone provider like Verizon or T-Mobile that they point it to your MDM servers in ABP.

https://business.apple.com/#/main

You may need to add the apps you need in ABP for the licenses, which you can then add the app in Intune

You really cannot do anything software wise in ABP, besides remove devices in ABP which will FULLY disconnect it from your org. Please don't do.

