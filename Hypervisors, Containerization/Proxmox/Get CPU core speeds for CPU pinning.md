
There are multiple commands to check the processor cores, here are a few and I'll give quick descriptions.

```
lscpu | grep MHz
```
Most basic, only gives fastest cores speed not good for if you have cores with different speeds.

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