PBX stands for Private Branch Exchange, it's where the VoIP handsets point to

###### **Needed from User** -
What brand VoIP handsets are they?
Are they wired or Wi-Fi
Are calls consistently low quality (e.g., choppy audio, static, delay) or do they randomly cut out? Does this happen for all users or specific ones?
Do you always receive calls, or do they sometimes not go through
Do the buttons turn gray every now and then?
How often does this happen, is it a constant?
Does it fix itself after a certain amount of time
When did it start?
Did anything change around that time?

------------------------

###### **Info needed** -
Comcast Bill / or whoever ISP is
VoIP provider
Their recommended setup from VoIP provider, do they need port forwarding for their PBX

------------------------
###### **Bryce's** **shit** **-**
Double check VLAN
Speedtest
Is QoS enabled?
Does their PBX need portforwarded, probs. /Double check as well
Is SIP disabled
Give them a call and see what it sounds like
Is there a high Jitter?
Run continuous ping overnight checking for high pocket loss or jitter
Get with ISP provider

------------------------

### Summary of Likely Causes and Fixes

|**Issue**|**Possible Cause**|**Fix**|
|---|---|---|
|Low Quality (Choppy Audio)|High jitter, latency, or packet loss|Improve network, enable QoS, check bandwidth|
|Calls Drop Out|Blocked ports, NAT issues, or provider problems|Verify port forwarding, check NAT, contact provider|
|One-Way Audio|NAT traversal or firewall issues|Enable STUN/TURN, check firewall settings|
|Device Issues|Poor hardware or firmware|Update firmware, test different devices|

What