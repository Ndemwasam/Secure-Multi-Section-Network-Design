# Secure-Multi-Section-Network-Design

This repository contains a Packet Tracer lab demonstrating a three-section network design (Management / Users / Guests) across three sites. The design covers VLAN segmentation, router‑on‑a‑stick inter‑VLAN routing, OSPF between routers, DHCP pools on routers, switch port security, DHCP snooping, and ACL‑based isolation.

Topology diagram
![topology diagram](https://github.com/user-attachments/assets/072b7eab-08dc-4ce5-a40b-1a3877036c85)

## Summary
- 3 routers (R0, R1, R2)
- 3 switches (S0, S1, S2)
- VLANs: 10 = Management, 20 = Users, 30 = Guests
- Router-on-a-stick for each site (subinterfaces on Gi0/0)
- OSPF for routing between routers
- ACLs to restrict Guest/User access to other internal sections
- Port security + DHCP snooping on switches to limit host spoofing

## Addressing & VLAN table

- VLAN 10 (Management)
  - R0 gateway: 10.0.1.1/24
  - R1 gateway: 10.1.1.1/24
  - R2 gateway: 10.2.1.1/24
- VLAN 20 (Users)
  - R0 gateway: 10.0.2.1/24
  - R1 gateway: 10.1.2.1/24
  - R2 gateway: 10.2.2.1/24
- VLAN 30 (Guests)
  - R0 gateway: 10.0.3.1/24
  - R1 gateway: 10.1.3.1/24
  - R2 gateway: 10.2.3.1/24

Inter-router links (point-to-point /30)
- R0 — R1: 192.168.10.0/30 (R0 .1, R1 .2)
- R0 — R2: 192.168.11.0/30 (R0 .1, R2 .2)
- R1 — R2: 192.168.22.0/30 (R1 .1, R2 .2)

DHCP pools on each router (examples)
- Management: network x.x.1.0/24, default-router x.x.1.1, excluded addresses .1-.12
- Users: network x.x.2.0/24, default-router x.x.2.1, excluded addresses .1-.12
- Guests: network x.x.3.0/24, default-router x.x.3.1, excluded addresses .1-.12

## Cleaned / copy‑ready configuration snippets

Notes:
- I standardized interface names to FastEthernet/GigabitEthernet.
- Remove trailing backslashes and stray periods from commands.
- Replace any real credentials with placeholders in public repos.

Switch S0 VLAN & access ports (example)
```text
enable
configure terminal
hostname S0
no ip domain-lookup

vlan 10
 name Management
exit
vlan 20
 name Users
exit
vlan 30
 name Guests
exit

interface FastEthernet0/1
 switchport mode access
 switchport access vlan 10
 description PC-Management
exit

interface range FastEthernet0/2 - 4
 switchport mode access
 switchport access vlan 20
 description PC-Users
exit

interface range FastEthernet0/5 - 7
 switchport mode access
 switchport access vlan 30
 description PC-Guests
exit

interface GigabitEthernet0/1
 switchport mode trunk
 switchport trunk allowed vlan 10,20,30
 description Trunk to R0
exit
```

Switch S0 security (port-security, STP fast / bpduguard, DHCP snooping)
```text
configure terminal
interface range FastEthernet0/1 - 7
 switchport port-security
 switchport port-security maximum 1
 switchport port-security violation shutdown
 switchport port-security mac-address sticky
 spanning-tree portfast
 spanning-tree bpduguard enable
exit

ip dhcp snooping
ip dhcp snooping vlan 10,20,30

interface GigabitEthernet0/1
 ip dhcp snooping trust
exit
```

(Repeat equivalent S1/S2 configs, changing interface descriptions as needed.)

Router (R0) — subinterfaces and DHCP pools (example)
```text
enable
configure terminal
hostname R0
no ip domain-lookup

interface GigabitEthernet0/0
 no shutdown

interface GigabitEthernet0/0.10
 encapsulation dot1Q 10
 ip address 10.0.1.1 255.255.255.0
 description Management-VLAN
exit

interface GigabitEthernet0/0.20
 encapsulation dot1Q 20
 ip address 10.0.2.1 255.255.255.0
 description Users-VLAN
exit

interface GigabitEthernet0/0.30
 encapsulation dot1Q 30
 ip address 10.0.3.1 255.255.255.0
 description Guests-VLAN
exit

ip dhcp excluded-address 10.0.1.1 10.0.1.12
ip dhcp excluded-address 10.0.2.1 10.0.2.12
ip dhcp excluded-address 10.0.3.1 10.0.3.12

ip dhcp pool Management-VLAN
 network 10.0.1.0 255.255.255.0
 default-router 10.0.1.1
 dns-server 8.8.8.8
exit

ip dhcp pool Users-VLAN
 network 10.0.2.0 255.255.255.0
 default-router 10.0.2.1
 dns-server 8.8.8.8
exit

ip dhcp pool Guests-VLAN
 network 10.0.3.0 255.255.255.0
 default-router 10.0.3.1
 dns-server 8.8.8.8
exit
```

OSPF (R0 example) — include only required networks, remove duplicates
```text
interface GigabitEthernet0/1
 ip address 192.168.10.1 255.255.255.252
 no shutdown
exit

interface GigabitEthernet0/2
 ip address 192.168.11.1 255.255.255.252
 no shutdown
exit

router ospf 1
 router-id 1.1.1.1
 network 10.0.1.0 0.0.0.255 area 0
 network 10.0.2.0 0.0.0.255 area 0
 network 10.0.3.0 0.0.0.255 area 0
 network 192.168.10.0 0.0.0.3 area 0
 network 192.168.11.0 0.0.0.3 area 0
 passive-interface GigabitEthernet0/0.10
 passive-interface GigabitEthernet0/0.20
 passive-interface GigabitEthernet0/0.30
end
copy running-config startup-config
```

ACL approach (R0 example for Guests -> internal networks)
- For clarity in a lab, allow ICMP echo/echo-reply in both directions used for testing, then deny other IP to internal networks, then permit the rest.
```text
ip access-list extended GUEST_ACL
 remark allow icmp echo/echo-reply for testing
 permit icmp 10.0.3.0 0.0.0.255 10.0.0.0 0.0.255.255 echo
 permit icmp 10.0.3.0 0.0.0.255 10.0.0.0 0.0.255.255 echo-reply
 deny   ip 10.0.3.0 0.0.0.255 10.0.0.0 0.0.255.255
 permit ip any any
exit
interface GigabitEthernet0/0.30
 ip access-group GUEST_ACL in
exit
```
Notes:
- If guests originate pings, ensure ACLs permit the ICMP type you expect (echo is type 8; echo-reply is type 0). For general lab testing, you can use `permit icmp <src> <wildcard> <dst> <wildcard> any` during testing, then tighten later.

Management access (replace secrets before publishing)
```text
ip domain-name example.local
crypto key generate rsa modulus 2048
username <admin> privilege 15 secret <YOUR_SECRET>
ip access-list standard MGMT_ACCESS
 permit 10.0.1.0 0.0.0.255
 permit 10.1.1.0 0.0.0.255
 permit 10.2.1.0 0.0.0.255
exit

line vty 0 4
 access-class MGMT_ACCESS in
 transport input ssh
 login local
 exec-timeout 5 0
exit

ip ssh version 2
service password-encryption
```

## Verification / testing checklist
Run these on routers/switches to confirm the design:
- show ip interface brief
- show ip route
- show ip ospf neighbor
- show ip ospf database
- show ip dhcp binding
- show ip dhcp pool
- show ip dhcp snooping
- show mac address-table
- show port-security interface FastEthernet0/1
- show access-lists
- Try pings across VLANs per policy:
  - Management -> Users, Guests (should work)
  - Users -> Management (ICMP allowed per ACL configuration) but restricted as designed
  - Guests -> internal networks (should be denied except allowed ICMP test if configured)

## Security & hygiene notes
- Remove/replace passwords and secrets before publishing or sharing. The README uses placeholders like `<admin>` and `<YOUR_SECRET>`.
- `service password-encryption` is only weak obfuscation; for production use centralized AAA and secure key/cert management.
- `permit ip any any` at the bottom of an ACL lets remaining traffic through — use explicit denies if you want to strictly block traffic.
- For more realistic labs, enable logging, NTP, and more granular service ACLs (e.g., allow only TCP/22 for management).

## What I changed in this README
- Cleaned and reformatted the original command snippets (removed stray characters, normalized interface names).
- Added an addressing/VLAN table for clarity.
- Rewrote ACL examples to be explicit about ICMP types and noted testing caveats.
- Replaced cleartext credentials with placeholders and added security notes.
- Added a concise verification checklist.

## Next steps (I can help)
- I can produce a fully validated, paste-ready set of configs for R0/R1/R2 and S0/S1/S2 (lab-ready), fixing any remaining small IOS/platform differences.
- Or I can create a simplified "How to run this lab in Packet Tracer" step-by-step guide and a checklist of exact commands and expected outputs.

If you'd like, tell me which option you prefer and I will prepare the next artifact.