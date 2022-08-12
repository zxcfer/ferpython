---
layout: post
title: "Linux Network Management"
tags: ["linux", "networks"]
---

sudo lshw -C network

tcpdump not port 22 # Show network traffic except ssh. See also tcpdump_not_me

ifconfig eth0 192.168.1.100 netmask 255.255.255.0 up
route add -net 192.168.0.0 netmask 255.255.255.0 eth0

sudo vi /etc/network/interfaces

- Set default gateway to 1.2.3.254

```bash
ip route add default via 1.2.3.254

tc qdisc add dev lo root handle 1:0 netem delay 20msec		Add 20ms latency to loopback device (for testing)
tc qdisc del dev lo root			Remove latency added above
```

- Lookup DNS ip address for name or vice versa

```bash
host pixelbeat.org
```

- Lookup local ip address (equivalent to host `hostname`)

```bash
hostname -i
```

- Lookup whois info for hostname or ip address

```bash
whois pixelbeat.org

netstat -tupl					List internet services on a system
netstat -tup					List active connections to/from system
windows networking (Note samba is the package that provides all this windows specific networking support)
```


- The primary network interface - use DHCP to find our address

```bash
auto eth0
iface eth0 inet dhcp
```

- The primary network interface

```bash
auto eth0
iface eth0 inet static
address 192.168.3.90
gateway 192.168.3.1
netmask 255.255.255.0
network 192.168.3.0
broadcast 192.168.3.255

sudo /etc/init.d/networking restart

auto eth0:1
iface eth0:1 inet static
address 192.168.1.60
netmask 255.255.255.0
network x.x.x.x
broadcast x.x.x.x
gateway x.x.x.x
```
ethtool eth0

- Show status of ethernet interface eth0

```bash
ethtool --change eth0 autoneg off speed 100 duplex full
```

- Manually set ethernet interface speed

```bash
iwconfig eth1
```

- Show status of wireless interface eth1

```bash
iwconfig eth1 rate 1Mb/s fixed
```

- Manually set wireless interface speed

```bash
iwlist scan
```

- List wireless networks in range

```bash
ip link show
```

- List network interfaces

```bash

ip link set dev eth0 name wan
```
- Rename interface eth0 to wan

```bash

ip link set dev eth0 up
```
- Bring interface eth0 up (or down)

```bash

ip addr show
```
- List addresses for interfaces

```bash

ip addr add 1.2.3.4/24 brd + dev eth0
```
- Add (or del) ip and mask (255.255.255.0)

```bash

ip route show
```
- List routing table

```bash

smbtree
Find windows machines. See also findsmb
 
nmblookup -A 1.2.3.4
Find the windows (netbios) name associated with ip address
```
 
