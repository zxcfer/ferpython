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

last reboot  # Show system reboot history
watch -n.1 'cat /proc/interrupts'  # Watch changeable data continuously

uname -a # Show kernel version and system architecture
head -n1 /etc/issue # Show name and version of distribution
cat /proc/partitions # Show all partitions registered on the system
grep MemTotal /proc/meminfo # Show RAM total seen by the system
grep "model name" /proc/cpuinfo # Show CPU(s) info
lspci -tv # Show PCI info
lsusb -tv # Show USB info
mount | column -t # List mounted filesystems on the system (and align output)
grep -F capacity: /proc/acpi/battery/BAT0/info # Show state of cells in laptop battery

dmidecode -q | less # Display SMBIOS/DMI information
#
smartctl -A /dev/sda | grep Power_On_Hours
How long has this disk (system) been powered on in total
#
hdparm -i /dev/sda           # Show info about disk sda
hdparm -tT /dev/sda          # Do a read speed test on disk sda
badblocks -s /dev/sda        # Test for unreadable blocks on disk sda

interactive (see also linux keyboard shortcuts)

alias hd='od -Ax -tx1z -v'
Handy hexdump. (usage e.g.: • hd /proc/self/cmdline | less)

touch -c -t 0304050607 file # Set file timestamp (YYMMDDhhmm)

sed -i 's/",/",\n/g'
```
