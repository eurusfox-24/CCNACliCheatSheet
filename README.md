# CCNACliCheatSheet
This repo is a complete list of cisco iso commands found in ccna 200-301

# CCNA CLI Complete Cheat Sheet

---

## 🔹 Modes

| Mode | Command | Prompt |
|-----|---------|--------|
| User EXEC | login | `>` |
| Privileged EXEC | `enable` | `#` |
| Global Config | `configure terminal` | `(config)#` |
| Interface Config | `interface g0/0` | `(config-if)#` |
| Line Config | `line console 0` | `(config-line)#` |
| Router Config | `router rip` | `(config-router)#` |

Exit mode: `exit`  
Return to privileged: `end` or `Ctrl+Z`

---

## 🔹 Basic Device Setup

```
hostname R1
no ip domain-lookup
enable secret class
service password-encryption
banner motd #Unauthorized access prohibited#
```

---

## 🔹 Interface Configuration

```
interface g0/0
ip address 192.168.1.1 255.255.255.0
description LAN Interface
no shutdown
shutdown
```

Check interfaces:
```
show ip interface brief
show interfaces
```

---

## 🔹 Switch VLAN Configuration

Create VLAN:
```
vlan 10
name SALES
```

Assign VLAN to port:
```
interface f0/1
switchport mode access
switchport access vlan 10
```

Trunk port:
```
interface g0/1
switchport mode trunk
```

Check VLANs:
```
show vlan brief
show interfaces trunk
```

---

## 🔹 IP Routing (Static Route)

```
ip route 0.0.0.0 0.0.0.0 10.0.0.2
ip route 192.168.2.0 255.255.255.0 10.0.0.2
```

Routing table:
```
show ip route
```

---

## 🔹 RIP Configuration

```
router rip
version 2
no auto-summary
network 192.168.1.0
network 10.0.0.0
```

---

## 🔹 OSPF Configuration

```
router ospf 1
network 192.168.1.0 0.0.0.255 area 0
network 10.0.0.0 0.0.0.3 area 0
```

Check OSPF:
```
show ip ospf neighbor
show ip protocols
```

---

## 🔹 DHCP Configuration (Router as DHCP Server)

```
ip dhcp excluded-address 192.168.1.1 192.168.1.10

ip dhcp pool LAN
network 192.168.1.0 255.255.255.0
default-router 192.168.1.1
dns-server 8.8.8.8
```

---

## 🔹 SSH Configuration

```
ip domain-name ccna.local
crypto key generate rsa
username admin secret cisco

line vty 0 4
login local
transport input ssh
```

---

## 🔹 Port Security (Switch)

```
interface f0/1
switchport mode access
switchport port-security
switchport port-security maximum 2
switchport port-security violation shutdown
switchport port-security mac-address sticky
```

Check:
```
show port-security
show port-security interface f0/1
```

---

## 🔹 Access Control Lists (ACL)

### Standard ACL
```
access-list 10 permit 192.168.1.0 0.0.0.255
interface g0/0
ip access-group 10 in
```

### Extended ACL
```
access-list 100 permit tcp 192.168.1.0 0.0.0.255 any eq 80
access-list 100 deny ip any any
interface g0/0
ip access-group 100 in
```

---

## 🔹 NAT Configuration

### Static NAT
```
ip nat inside source static 192.168.1.10 200.1.1.10
```

### Dynamic NAT
```
access-list 1 permit 192.168.1.0 0.0.0.255
ip nat pool MYPOOL 200.1.1.1 200.1.1.10 netmask 255.255.255.0
ip nat inside source list 1 pool MYPOOL
```

### PAT (Overload)
```
ip nat inside source list 1 interface g0/1 overload
```

Assign inside/outside:
```
interface g0/0
ip nat inside
interface g0/1
ip nat outside
```

---

## 🔹 STP (Spanning Tree)

```
spanning-tree mode rapid-pvst
spanning-tree vlan 1 priority 4096
```

Check:
```
show spanning-tree
```

---

## 🔹 EtherChannel

```
interface range f0/1 - 2
channel-group 1 mode active
```

Check:
```
show etherchannel summary
```

---

## 🔹 CDP & LLDP

```
show cdp neighbors
no cdp run
show lldp neighbors
```

---

## 🔹 Useful Show Commands

```
show running-config
show startup-config
show version
show ip route
show mac address-table
show arp
show protocols
```

---

## 🔹 Save Configuration

```
copy running-config startup-config
write memory
```

---

## 🔹 Password Recovery / Console

```
line console 0
password cisco
login
logging synchronous
exec-timeout 5 0
```

---

## 🔹 Ping & Traceroute

```
ping 8.8.8.8
traceroute 8.8.8.8
```

---

## 🔹 Reload / Erase

```
reload
erase startup-config
```

---

## 🔹 Interface Ranges

```
interface range f0/1 - 24
shutdown
```

---

## 🔹 Default Gateway (Switch)

```
ip default-gateway 192.168.1.1
```

---

## 🔹 DNS Lookup

```
ip name-server 8.8.8.8
ping google.com
```

---
****
