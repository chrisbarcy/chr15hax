---
date: '2026-11-13T08:03:27-08:00'
draft: false
title: 'Initial Enumeration'
---

# Initial Enumeration

---

## Service Enumeration

### Nmap, single target
Recommend using environment variables to reference IP
```bash
TARGET={ip}
```

#### Simple port scan (top 1000), one target:
```bash
sudo nmap -sC -sV $TARGET
```

#### Full port scan, one target:
Find all open ports

```bash
sudo nmap -p- --min-rate 2000 $TARGET
```

Then, service scan just the open ports:

```bash
sudo nmap -sC -sV -p <port1>,<port2>,<etc> $TARGET
```

### Nmap, multiple targets
Recommend using targets.txt file, one IP per line

#### Simple port scan (top 1000), many targets:
```bash
sudo nmap -sC -sV -iL targets.txt --min-rate 2000
```
### Saving output to file
For a simple, readable file that you can easily `cat`:
```bash
-oN results.nmap
```
For all file formats:
```bash
-oA scans/<scan-name>
``` 

### Extra info
- Sometimes hosts appear down when they actually are not because firewalls are blocking ICMP traffic. Adding ```-Pn``` flag treats hosts as online
- The ```-sU``` flag can be used to perform UDP scans

---

### Found Nothing
If all standard TCP ports look locked down or empty:
- [ ] Verify the full `-p-` TCP scan finished completely
- [ ] Check the UDP scan output (`nmap-udp.txt`)
- [ ] Check for virtual host routing on HTTP (`ffuf` Host header fuzzing) -> [Scenario: Stuck on Initial Foothold](scenarios/no-foothold.md)
