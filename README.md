# CCNA CLI Complete Cheat Sheet

This repo is a complete list of cisco iso commands found in ccna 200-301

# 🧠 CCNA Complete CLI Mega Cheat Sheet

---

## 🔹 Navigation & Modes

| Mode | Command | Prompt |
|---|---|---|
| User EXEC | login | `>` |
| Privileged EXEC | `enable` | `#` |
| Global Config | `configure terminal` | `(config)#` |
| Interface | `interface g0/0` | `(config-if)#` |
| Sub-interface | `interface g0/0.10` | `(config-subif)#` |
| Line | `line console 0` | `(config-line)#` |
| Router | `router ospf 1` | `(config-router)#` |

```
end
exit
Ctrl+Z
```

---

## 🔹 Basic Device Hardening

```
hostname R1
no ip domain-lookup
enable secret class
service password-encryption
banner motd #AUTHORIZED USERS ONLY#
login block-for 120 attempts 3 within 60
```

---

## 🔹 Passwords & Console / VTY

```
line console 0
password cisco
login
logging synchronous
exec-timeout 5 0

line vty 0 4
password cisco
login
transport input telnet ssh
```

---

## 🔹 SSH Full Setup

```
ip domain-name ccna.local
crypto key generate rsa modulus 1024
username admin secret cisco

line vty 0 4
login local
transport input ssh
```

Verify:
```
show ip ssh
```

---

## 🔹 Interface Configuration

```
interface g0/0
description LAN
ip address 192.168.1.1 255.255.255.0
no shutdown
shutdown
```

```
show ip interface brief
show interfaces g0/0
```

---

## 🔹 Sub-Interfaces (Router on a Stick)

```
interface g0/0.10
encapsulation dot1Q 10
ip address 192.168.10.1 255.255.255.0
```

---

## 🔹 Switch VLANs

Create VLAN:
```
vlan 10
name SALES
```

Assign Access Port:
```
interface f0/1
switchport mode access
switchport access vlan 10
```

Trunk Port:
```
interface g0/1
switchport trunk encapsulation dot1q
switchport mode trunk
switchport trunk allowed vlan 10,20
```

Verify:
```
show vlan brief
show interfaces trunk
```

---

## 🔹 Inter-VLAN Routing

### Router on a Stick
Use sub-interfaces above.

### Layer 3 Switch
```
ip routing
interface vlan 10
ip address 192.168.10.1 255.255.255.0
no shutdown
```

---

## 🔹 Static Routing

```
ip route 192.168.2.0 255.255.255.0 10.0.0.2
ip route 0.0.0.0 0.0.0.0 10.0.0.2
```

---

## 🔹 RIP v2

```
router rip
version 2
no auto-summary
network 192.168.1.0
```

---

## 🔹 OSPFv2

```
router ospf 1
router-id 1.1.1.1
network 192.168.1.0 0.0.0.255 area 0
passive-interface g0/0
```

Verify:
```
show ip ospf neighbor
show ip route ospf
```

---

## 🔹 DHCP Server (Router)

```
ip dhcp excluded-address 192.168.1.1 192.168.1.10

ip dhcp pool LAN
network 192.168.1.0 255.255.255.0
default-router 192.168.1.1
dns-server 8.8.8.8
domain-name ccna.local
```

---

## 🔹 DHCP Relay

```
interface g0/0
ip helper-address 10.0.0.5
```

---

## 🔹 NAT

### Inside / Outside
```
interface g0/0
ip nat inside
interface g0/1
ip nat outside
```

### Static NAT
```
ip nat inside source static 192.168.1.10 200.1.1.10
```

### PAT
```
access-list 1 permit 192.168.1.0 0.0.0.255
ip nat inside source list 1 interface g0/1 overload
```

Verify:
```
show ip nat translations
show ip nat statistics
```

---

## 🔹 ACLs

### Standard
```
access-list 10 permit 192.168.1.0 0.0.0.255
interface g0/0
ip access-group 10 in
```

### Extended
```
access-list 100 permit tcp 192.168.1.0 0.0.0.255 any eq 80
access-list 100 deny ip any any
interface g0/1
ip access-group 100 out
```

---

## 🔹 Port Security

```
interface f0/1
switchport mode access
switchport port-security
switchport port-security maximum 2
switchport port-security mac-address sticky
switchport port-security violation shutdown
```

Verify:
```
show port-security
```

---

## 🔹 STP

```
spanning-tree mode rapid-pvst
spanning-tree vlan 1 priority 4096
spanning-tree portfast
spanning-tree bpduguard enable
```

---

## 🔹 EtherChannel (LACP)

```
interface range f0/1 - 2
channel-group 1 mode active
```

---

## 🔹 CDP / LLDP

```
show cdp neighbors
no cdp run
show lldp neighbors
```

---

## 🔹 DNS

```
ip name-server 8.8.8.8
ping google.com
```

---

## 🔹 Default Gateway (Switch)

```
ip default-gateway 192.168.1.1
```

---

## 🔹 Syslog & NTP

```
logging host 192.168.1.5
ntp server 192.168.1.10
```

---

## 🔹 Backup & Restore

Save:
```
copy running-config startup-config
write memory
```

Backup to TFTP:
```
copy running-config tftp
```

---

## 🔹 Useful SHOW Commands

```
show running-config
show startup-config
show version
show ip route
show ip protocols
show arp
show mac address-table
show interfaces status
show controllers
show clock
```

---

## 🔹 Troubleshooting

```
ping
traceroute
debug ip routing
undebug all
```

---

## 🔹 Interface Range

```
interface range f0/1 - 24
shutdown
```

---

## 🔹 Reload / Reset

```
reload
erase startup-config
delete vlan.dat
```

---

## 🔹 Time & Clock

```
clock set 10:00:00 6 FEB 2026
```

---

## 🔹 IPv6 Basics

```
ipv6 unicast-routing
interface g0/0
ipv6 address 2001:db8:1::1/64
```

Static IPv6 Route:
```
ipv6 route ::/0 2001:db8:1::2
```

---

## 🔹 Verify Everything Fast

```
show ip interface brief
show vlan brief
show ip route
show ip ospf neighbor
show port-security
show interfaces trunk
```

---
