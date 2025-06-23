Commands to monitor Linux including resources, temperature, and more

```
apt-get install htop
```
Install htop
```
htop
```
Favorite command, shows Memory, CPU, time, and processes. If you go into settings F2, can also add CPU frequency's, and CPU temperatures (install Libsensors)

-------

```
apt-get update 
apt-get install lm-sensors
```
Install it
```
sensors-detect
```
Answer prompts
```
watch -n 1 sensors
```
Watch sensors in real time
Monitor temperatures dedicated

---------
```
top
```
Basic, and works without installing anything.
- Shows CPU usage, memory, and running processes.
- Press q to quit, k to kill a process (enter PID), or 1 to toggle per-CPU core view.
- **Pro Tip**: Use Shift+P to sort by CPU usage or Shift+M for memory.

--------------------
```
free -h
```
Basic, and works without installing anything.
* Looks at available for actual free RAM.

----------------


