
There are multiple commands to check the processor cores, here are a few and I'll give quick descriptions.

```
apt-get install cpufrequtils
```
```
cpufreq-info
```
My Favorite, gives cores beside it, minimum and maximum, if performance or powersave is available.
Also look

---------------

```
lscpu | grep MHz
```
Most basic, only gives fastest cores speed not good for if you have cores with different speeds.

------------------------

```
cat /sys/devices/system/cpu/cpu*/cpufreq/scaling_max_freq
```
Gives max CPU speeds without installing anything, doesn't put the cores right beside it

-------------

```
cat /proc/cpuinfo
```
Another basic command, doesn't seem seem to give top speeds but gives the minimum.

--------

```
dmidecode -t processor
```
Better info to me than LSCPU

----------------

