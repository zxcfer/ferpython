---
layout: post
title: "Linux Memory Management"
tags: ["linux", "memory"]
---


```bash
ps -e -o pcpu,cpu,nice,state,cputime,args --sort pcpu | sed '/^ 0.0 /d' # List processes by % cpu usage
ps -e -orss=,args= | sort -b -k1,1n | pr -TW$COLUMNS # List processes by mem (KB) usage. See also ps_mem.py
ps -C firefox-bin -L -o pid,tid,pcpu,state  # List all threads for a particular process
ps -p 1,2    # List info for particular process IDs

uname -a # Show kernel version and system architecture
head -n1 /etc/issue # Show name and version of distribution
grep MemTotal /proc/meminfo # Show RAM total seen by the system
grep "model name" /proc/cpuinfo # Show CPU(s) info

lspci -tv # Show PCI info
lsusb -tv # Show USB info

mount | column -t # List mounted filesystems on the system (and align output)
grep -F capacity: /proc/acpi/battery/BAT0/info # Show state of cells in laptop battery

```
