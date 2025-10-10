# Secure-Multi-Section-Network-Design
This is a three section network design in packet tracer, consist of three routers, three switches and several pcs per vlan and the topology is interconnected in triangle design.
# Network Topology Diagram
<img width="831" height="410" alt="topology diagram" src="https://github.com/user-attachments/assets/072b7eab-08dc-4ce5-a40b-1a3877036c85" />

# Switch S0 Vlan Segmentation
Switch>en.\
Switch#conf t.\
Switch(config)#hostname S0.\
S0(config)#no ip domain-lookup.\
S0(config)#vlan 10.\
S0(config-vlan)#name Management.\
S0(config-vlan)#exit.\
S0(config)#vlan 20.\
S0(config-vlan)#name Users.\
S0(config-vlan)#exit.\
S0(config)#vlan 30.\
S0(config-vlan)#name Guests.\
S0(config-vlan)#exit.\
S0(config)#int f0/1.\
S0(config-if)#switchport mode access.\ 
S0(config-if)#switchport access vlan 10.\
S0(config-if)#description PC)-Management.\
S0(config-if)#exit.\
S0(config)#int r f0/2-4.\
S0(config-if-range)#switchport mode access.\
S0(config-if-range)#switchport access vlan 20.\
S0(config-if-range)#description PC1-Users.\
S0(config-if-range)#exit.\
S0(config)#int r f0/5-7.\
S0(config-if-range)#switchport mode access.\ 
S0(config-if-range)#switchport access vlan 30.\
S0(config-if-range)#description PC2-Guests.\
S0(config-if-range)#exit.\
S0(config)#int g0/1.\
S0(config-if)#switchport mode trunk.\
S0(config-if)#switchport trunk allowed vlan 10,20,30.\
S0(config-if)#description trunk to R0.\
S0(config-if)#exit.\
S0(config)#int r f0/8-24, g0/2.\
S0(config-if-range)#sh.

# Switch S1 Vlan Segmentation
Switch>en.\
Switch#conf t.\
Switch(config)#hostname S1.\
S1(config)#no ip domain-lookup.\
S1(config)#vlan 10.\
S1(config-vlan)#name Management.\
S1(config-vlan)#exit.\
S1(config)#vlan 20.\
S1(config-vlan)#name Users.\
S1(config-vlan)#exit.\
S1(config)#vlan 30.\
S1(config-vlan)#name Guests.\
S1(config-vlan)#exit.\
S1(config)#int f0/1.\
S1(config-if)#switchport mode access.\
S1(config-if)#switchport access vlan 10.\
S1(config-if)#description PC3-Management.\
S1(config-if)#exit.\
S1(config)#int r f0/2-4.\
S1(config-if-range)#switchport mode access.\
S1(config-if-range)#switchport access vlan 20.\
S1(config-if-range)#description PC4-Users.\
S1(config-if-range)#exit.\
S1(config)#int r f0/5-7.\
S1(config-if-range)#switchport mode access.\
S1(config-if-range)#switchport access vlan 30.\
S1(config-if-range)#description PC5-Guests.\
S1(config-if-range)#exit.\
S1(config)#int g0/1.\
S1(config-if)#switchport mode trunk.\
S1(config-if)#switchport trunk allowed vlan 10,20,30.\
S1(config-if)#description trunk to R1.\
S1(config-if)#exit.\
S1(config)#int r f0/8-24, g0/2.\
S1(config-if-range)#sh.
# Switch S2 Vlan Segmentation
Switch>en.\
Switch#conf t.\
Switch(config)#hostname S2.\
S2(config)#no ip domain-lookup.\
S2(config)#vlan 10.\
S2(config-vlan)#name Management.\
S2(config-vlan)#exit.\
S2(config)#vlan 20.\
S2(config-vlan)#name Users.\
S2(config-vlan)#exit.\
S2(config)#vlan 30.\
S2(config-vlan)#name Guests.\
S2(config-vlan)#exit.\
S2(config)#int f0/1.\
S2(config-if)#switchport mode access.\
S2(config-if)#switchport access vlan 10.\
S2(config-if)#description PC6-Management.\
S2(config-if)#exit.\
S2(config)#int r f0/2-4.\
S2(config-if-range)#switchport mode access.\
S2(config-if-range)#switchport access vlan 20.\
S2(config-if-range)#description PC7-Users.\
S2(config-if-range)#exit.\
S2(config)#int r f0/5-7.\
S2(config-if-range)#switchport mode access.\
S2(config-if-range)#switchport access vlan 30.\
S2(config-if-range)#description PC8-Guests.\
S2(config-if-range)#exit.\
S2(config)#int g0/1.\
S2(config-if)#switchport mode trunk.\
S2(config-if)#switchport trunk allowed vlan 10,20,30.\
S2(config-if)#description trunk to R2.\
S2(config-if)#exit.\
S2(config)#int r f0/8-24, g0/2.\
S2(config-if-range)#sh
# Switch S0 Security Configuration
S0>en.\
S0#conf t.\
S0(config)#int r f0/1-7.\
S0(config-if-range)#switchport port-security.\
S0(config-if-range)#switchport port-security maximum 1.\
S0(config-if-range)#switchport port-security violation shutdown.\
S0(config-if-range)#switchport port-security mac-address sticky.\
S0(config-if-range)#exit.\
S0(config)#int r f0/1-7.\
S0(config-if-range)#spanning-tree portfast.\
S0(config-if-range)#spanning-tree bpduguard enable.\
S0(config-if-range)#exit.\
S0(config)#ip dhcp snooping.\
S0(config)#ip dhcp snooping vlan 10,20,30.\
S0(config)#int g0/1.\
S0(config-if)#ip dhcp snooping trust.\
S0(config-if)#exit.\
S0(config)#int r f0/8-24,g0/2.\
S0(config-if-range)#sh
# Switch S1 Security Configuration
S1>en.\
S1#conf t.\
S1(config)#int r f0/1-7.\
S1(config-if-range)#switchport port-security.\
S1(config-if-range)#switchport port-security maximum 1.\
S1(config-if-range)#switchport port-security violation shutdown.\
S1(config-if-range)#switchport port-security mac-address sticky.\
S1(config-if-range)#exit.\
S1(config)#int r f0/1-7.\
S1(config-if-range)#spanning-tree portfast.\
S1(config-if-range)#spanning-tree bpduguard enable.\
S1(config-if-range)#exit.\
S1(config)#ip dhcp snooping.\
S1(config)#ip dhcp snooping vlan 10,20,30.\
S1(config)#int g0/1.\
S1(config-if)#ip dhcp snooping trust.
# Switch S2 Security Configuration
S2>en.\
S2#conf t.\
S2(config)#int r f0/1-7.\
S2(config-if-range)#switchport port-security.\
S2(config-if-range)#switchport port-security maximum 1.\
S2(config-if-range)#switchport port-security violation shutdown.\
S2(config-if-range)#switchport port-security mac-address sticky.\
S2(config-if-range)#exit.\
S2(config)#int r f0/1-7.\
S2(config-if-range)#spanning-tree portfast.\
S2(config-if-range)#spanning-tree bpduguard enable.\
S2(config-if-range)#exit.\
S2(config)#ip dhcp snooping.\
S2(config)#ip dhcp snooping vlan 10,20,30.\
S2(config)#int g0/1.\
S2(config-if)#ip dhcp snooping trust.

# Router R0 Subinterface and dhcp configuration
Router>en\
Router#conf t\
Router(config)#int g0/0\
Router(config-if)#no sh\
Router(config-if)#hostname R0\
R0(config)#no ip domain-lookup\
R0(config)#int g0/0.10\
R0(config-subif)#encapsulation dot1q 10\
R0(config-subif)#ip address 10.0.1.1 255.255.255.0\
R0(config-subif)#description Management-VLAN\
R0(config-subif)#exit\
R0(config)#int g0/0.20\
R0(config-subif)#encapsulation dot1q 20\
R0(config-subif)#ip address 10.0.2.1 255.255.255.0\
R0(config-subif)#description Users-VLAN\
R0(config-subif)#exit\
R0(config)#int g0/0.30\
R0(config-subif)#encapsulation dot1q 30\
R0(config-subif)#ip address 10.0.3.1 255.255.255.0\
R0(config-subif)#description Guests-VLAN\
R0(config)#ip dhcp excluded-address 10.0.1.1 10.0.1.12\
R0(config)#ip dhcp excluded-address 10.0.2.1 10.0.2.12\
R0(config)#ip dhcp excluded-address 10.0.3.1 10.0.3.12\
R0(config)#ip dhcp pool Management-VLAN\
R0(dhcp-config)#network 10.0.1.0 255.255.255.0\
R0(dhcp-config)#default-router 10.0.1.1\
R0(dhcp-config)#dns-server 8.8.8.8\
R0(dhcp-config)#exit\
R0(config)#ip dhcp pool Users-VLAN\
R0(dhcp-config)#network 10.0.2.0 255.255.255.0\
R0(dhcp-config)#default-router 10.0.2.1\
R0(dhcp-config)#dns-server 8.8.8.8\
R0(dhcp-config)#exit\
R0(config)#ip dhcp pool Guests-VLAN\
R0(dhcp-config)#network 10.0.3.0 255.255.255.0\
R0(dhcp-config)#default-router 10.0.3.1\
R0(dhcp-config)#dns-server 8.8.8.8

# Router R1 Subinterface and dhcp configuration
Router>\
Router>en\
Router#conf t\
Router(config)#int g0/0\
Router(config-if)#no sh\
Router(config-if)#hostname R1\
R1(config)#no ip domain-lookup\
R1(config)#int g0/0.10\
R1(config-subif)#encapsulation dot1q 10\
R1(config-subif)#ip address 10.1.1.1 255.255.255.0\
R1(config-subif)#description Management-VLAN\
R1(config-subif)#exit\
R1(config)#int g0/0.20\
R1(config-subif)#encapsulation dot1q 20\
R1(config-subif)#ip address 10.1.2.1 255.255.255.0\
R1(config-subif)#description Users-VLAN\
R1(config-subif)#exit\
R1(config)#int g0/0.30\
R1(config-subif)#encapsulation dot1q 30\
R1(config-subif)#ip address 10.1.3.1 255.255.255.0\
R1(config-subif)#description Guests-VLAN\
R1(config)#ip dhcp excluded-address 10.1.1.1 10.1.1.12\
R1(config)#ip dhcp excluded-address 10.1.2.1 10.1.2.12\
R1(config)#ip dhcp excluded-address 10.1.3.1 10.1.3.12\
R1(config)#ip dhcp pool Management-VLAN\
R1(dhcp-config)#network 10.1.1.0 255.255.255.0\
R1(dhcp-config)#default-router 10.1.1.1\
R1(dhcp-config)#dns-server 8.8.8.8\
R1(dhcp-config)#exit\
R1(config)#ip dhcp pool Users-VLAN\
R1(dhcp-config)#network 10.1.2.0 255.255.255.0\
R1(dhcp-config)#default-router 10.1.2.1\
R1(dhcp-config)#dns-server 8.8.8.8\
R1(dhcp-config)#exit\
R1(config)#ip dhcp pool Guests-VLAN\
R1(dhcp-config)#network 10.1.3.0 255.255.255.0\
R1(dhcp-config)#default-router 10.1.3.1\
R1(dhcp-config)#dns-server 8.8.8.8

# Router R2 Subinterface and dhcp configuration
Router>en\
Router#conf t\
Router(config)#hostname R2\
R2(config)#no ip domain-lookup\
R2(config)#int g0/0.10\
R2(config-subif)#encapsulation dot1q 10\
R2(config-subif)#ip address 10.2.1.1 255.255.255.0\
R2(config-subif)#description Management-VLAN\
R2(config-subif)#exit\
R2(config)#int g0/0.20\
R2(config-subif)#encapsulation dot1q 20\
R2(config-subif)#ip address 10.2.2.1 255.255.255.0\
R2(config-subif)#description Users-VLAN\
R2(config-subif)#exit\
R2(config)#int g0/0.30\
R2(config-subif)#encapsulation dot1q 30\
R2(config-subif)#ip address 10.2.3.1 255.255.255.0\
R2(config-subif)#description Guests-VLAN\
R2(config-subif)#exit\
R2(config)#ip dhcp excluded-address 10.2.1.1 10.2.1.12\
R2(config)#ip dhcp excluded-address 10.2.2.1 10.2.2.12\
R2(config)#ip dhcp excluded-address 10.2.3.1 10.2.3.12\
R2(config)#ip dhcp pool Management-VLAN\
R2(dhcp-config)#network 10.2.1.0 255.255.255.0\
R2(dhcp-config)#default-router 10.2.1.1\
R2(dhcp-config)#dns-server 8.8.8.8\
R2(dhcp-config)#exit\
R2(config)#ip dhcp pool Users-VLAN\
R2(dhcp-config)#network 10.2.2.0 255.255.255.0\
R2(dhcp-config)#default-router 10.2.2.1\
R2(dhcp-config)#dns-server 8.8.8.8\
R2(config)#ip dhcp pool Guest-VLAN\
R2(dhcp-config)#network 10.2.3.0 255.255.255.0\
R2(dhcp-config)#default-router 10.2.3.1\
R2(dhcp-config)#dns-server 8.8.8.8

# Router R0 OSPF configuration
R0>en\
R0#conf t\
R0(config)#int g0/1\
R0(config-if)#ip address 192.168.10.1 255.255.255.252\
R0(config-if)#no sh\
R0(config-if)#exit\
R0(config)#int g0/2\
R0(config-if)#ip address 192.168.11.1 255.255.255.252\
R0(config-if)#no sh\
R0(config-if)#router ospf 1\
R0(config-router)#router-id 1.1.1.1\
R0(config-router)#network 10.0.1.0 0.0.0.255 area 0\
R0(config-router)#network 10.0.2.0 0.0.0.255 area 0\
R0(config-router)#network 10.0.3.0 0.0.0.255 area 0\
R0(config-router)#network 192.168.10.0 0.0.0.3 area 0\
R0(config-router)#network 192.168.11.0 0.0.0.3 area 0\
R0(config-router)#passive-interface g0/0.10\
R0(config-router)#passive-interface g0/0.20\
R0(config-router)#passive-interface g0/0.30\
R0(config-router)#end\
R0#copy running-config startup-config

# Router R1 OSPF configuration
R1>en\
R1#conf t\
R1(config)#int g0/1\
R1(config-if)#ip address 192.168.10.2 255.255.255.252\
R1(config-if)#no sh\
R1(config-if)#int g0/2\
R1(config-if)#ip address 192.168.22.1 255.255.255.252\
R1(config-if)#no sh\
R1(config-if)#router ospf 1\
R1(config-router)#router-id 2.2.2.2\
R1(config-router)#network 10.1.1.0 0.0.0.255 area 0\
R1(config-router)#network 10.1.2.0 0.0.0.255 area 0\
R1(config-router)#network 10.1.3.0 0.0.0.255 area 0\
R1(config-router)#network 192.168.10.0 0.0.0.3 area 0\
R1(config-router)#network 192.168.10.0 0.0.0.3 area 0\
R1(config-router)#network 192.168.22.0 0.0.0.3 area 0\
R1(config-router)#passive-interface g0/0.10\
R1(config-router)#passive-interface g0/0.20\
R1(config-router)#passive-interface g0/0.30\
R1(config-router)#end\
R1#copy running-config startup-config

# Router R2 OSPF configuration
R2>en\
R2#conf t\
R2(config)#int g0/1\
R2(config-if)#ip address 192.168.11.2 255.255.255.252\
R2(config-if)#no sh\
R2(config-if)#int g0/2\
R2(config-if)#ip address 192.168.22.2 255.255.255.252\
R2(config-if)#no sh\
R2(config-if)#router ospf 1\
R2(config-router)#router-id 3.3.3.3\
R2(config-router)#network 10.2.1.0 0.0.0.255 area 0\
R2(config-router)#network 10.2.2.0 0.0.0.255 area 0\
R2(config-router)#network 10.2.3.0 0.0.0.255 area 0\
R2(config-router)#network 192.168.11.0 0.0.0.3 area 0\
R2(config-router)#network 192.168.22.0 0.0.0.3 area 0\
R2(config-router)#passive-interface g0/0.10\
R2(config-router)#passive-interface g0/0.20\
R2(config-router)#passive-interface g0/0.30\
R2(config-router)#end\
R2#copy running-config startup-config

# Router R0 ACL and Security Configuration
R0>en\
R0#conf t\
R0(config)#ip access-list extended GUEST_ACL\
R0(config-ext-nacl)#permit icmp 10.0.3.0 0.0.0.255 10.0.0.0 0.0.255.255 echo-reply\
R0(config-ext-nacl)#permit icmp 10.0.3.0 0.0.0.255 10.1.0.0 0.0.255.255 echo-reply\
R0(config-ext-nacl)#permit icmp 10.0.3.0 0.0.0.255 10.2.0.0 0.0.255.255 echo-reply\
R0(config-ext-nacl)#deny ip 10.0.3.0 0.0.0.255 10.0.0.0 0.0.255.255\
R0(config-ext-nacl)#deny ip 10.0.3.0 0.0.0.255 10.1.0.0 0.0.255.255\
R0(config-ext-nacl)#deny ip 10.0.3.0 0.0.0.255 10.2.0.0 0.0.255.255\
R0(config-ext-nacl)#permit ip any any\
R0(config-ext-nacl)#exit\
R0(config)#ip access-list extended USER_ACL\
R0(config-ext-nacl)#permit icmp 10.0.2.0 0.0.0.255 10.0.1.0 0.0.0.255 echo-reply\
R0(config-ext-nacl)#permit icmp 10.0.2.0 0.0.0.255 10.1.1.0 0.0.0.255 echo-reply\
R0(config-ext-nacl)#permit icmp 10.0.2.0 0.0.0.255 10.2.1.0 0.0.0.255 echo-reply\
R0(config-ext-nacl)#deny ip 10.0.2.0 0.0.0.255 10.0.1.0 0.0.0.255\
R0(config-ext-nacl)#deny ip 10.0.2.0 0.0.0.255 10.1.1.0 0.0.0.255\
R0(config-ext-nacl)#deny ip 10.0.2.0 0.0.0.255 10.2.1.0 0.0.0.255\
R0(config-ext-nacl)#permit ip any any\
R0(config-ext-nacl)#exit\
R0(config)# ip access-list extended MGMT_ACL\
R0(config-ext-nacl)#permit ip 10.0.1.0 0.0.0.255 any\
R0(config-ext-nacl)#permit ip 10.1.1.0 0.0.0.255 any\
R0(config-ext-nacl)#permit ip 10.2.1.0 0.0.0.255 any\
R0(config-ext-nacl)#exit\
R0(config)#int g0/0.30\
R0(config-subif)#ip access-group GUEST_ACL in\
R0(config-subif)#exit\
R0(config)#int g0/0.20\
R0(config-subif)#ip access-group USER_ACL in\
R0(config-subif)#int g0/0.10\
R0(config-subif)#ip access-group MGMT_ACL in\
R0(config-subif)#exit\
R0(config)#ip domain-name greywan.com\
R0(config)#crypto key generate rsa modulus 2048\
R0(config)#username wantech privilege 15 secret Greym@nw@n1\
*Mar 1 0:41:0.349: %SSH-5-ENABLED: SSH 1.99 has been enabled\
R0(config)#ip access-list standard MGMT_ACCESS\
R0(config-std-nacl)#permit 10.0.1.0 0.0.0.255\
R0(config-std-nacl)#permit 10.1.1.0 0.0.0.255\
R0(config-std-nacl)#permit 10.2.1.0 0.0.0.255\
R0(config-std-nacl)#exit\
R0(config)#line vty 0 4\
R0(config-line)#access-class MGMT_ACCESS in\
R0(config-line)#transport input ssh\
R0(config-line)#login local\
R0(config-line)#exec-timeout 5 0\
R0(config-line)#exit\
R0(config)#ip ssh version 2\
R0(config)#service password-encryption\

# Router R1 ACL and Security Configuration
R1>en\
R1#conf t\
R1(config)#ip access-list extended Guests_ACL\
R1(config-ext-nacl)#permit icmp 10.1.3.0 0.0.0.255 10.0.0.0 0.0.255.255 echo-reply\
R1(config-ext-nacl)#permit icmp 10.1.3.0 0.0.0.255 10.1.0.0 0.0.255.255 echo-reply\
R1(config-ext-nacl)#permit icmp 10.1.3.0 0.0.0.255 10.2.0.0 0.0.255.255 echo-reply\
R1(config-ext-nacl)#deny ip 10.1.3.0 0.0.0.255 10.0.0.0 0.0.255.255\
R1(config-ext-nacl)#deny ip 10.1.3.0 0.0.0.255 10.1.0.0 0.0.255.255\
R1(config-ext-nacl)#deny ip 10.1.3.0 0.0.0.255 10.2.0.0 0.0.255.255\
R1(config-ext-nacl)#permit ip any any\
R1(config-ext-nacl)#exit\
R1(config)#int g0/0.30\
R1(config-subif)#ip access-group Guests_ACL in\
R1(config-subif)#exit\
R1(config)#ip access-list extended Users_ACL\
R1(config-ext-nacl)#permit icmp 10.1.2.0 0.0.0.255 10.0.1.0 0.0.0.255 echo-reply\
R1(config-ext-nacl)#permit icmp 10.1.2.0 0.0.0.255 10.1.1.0 0.0.0.255 echo-reply\
R1(config-ext-nacl)#permit icmp 10.1.2.0 0.0.0.255 10.2.1.0 0.0.0.255 echo-reply\
R1(config-ext-nacl)#deny ip 10.1.2.0 0.0.0.255 10.0.1.0 0.0.0.255\
R1(config-ext-nacl)#deny ip 10.1.2.0 0.0.0.255 10.1.1.0 0.0.0.255\
R1(config-ext-nacl)#deny ip 10.1.2.0 0.0.0.255 10.2.1.0 0.0.0.255\
R1(config-ext-nacl)#permit ip any any\
R1(config-ext-nacl)#exit\
R1(config)#int g0/0.20\
R1(config-subif)#ip access-group Users_ACL in\
R1(config)#ip access-list extended Management_ACL\
R1(config-ext-nacl)#permit ip 10.0.1.0 0.0.0.255 any\
R1(config-ext-nacl)#permit ip 10.1.1.0 0.0.0.255 any\
R1(config-ext-nacl)#permit ip 10.2.1.0 0.0.0.255 any\
R1(config-ext-nacl)#exit\
R1(config)#int g0/0.10\
R1(config-subif)#ip access-group Management_ACL in\
R1(config-subif)#exit\
R1(config)#ip domain-name greywan.com\
R1(config)#crypto key generate rsa modulus 2048\
R1(config)#username wantech secret Greym@nw@n1\
R1(config)#ip access-list standard Management_ACCESS\
R1(config-std-nacl)#permit 10.0.1.0 0.0.0.255\
R1(config-std-nacl)#permit 10.1.1.0 0.0.0.255\
R1(config-std-nacl)#permit 10.2.1.0 0.0.0.255\
R1(config-std-nacl)#exit\
R1(config)#line vty 0 4\
R1(config-line)#access-class Management_ACCESS in\
R1(config-line)#transport input ssh\
R1(config-line)#login local\
R1(config-line)#exec-timeout 5 0\
R1(config-line)#exit\
R1(config)#ip ssh version 2\
R1(config)#service password-encryption\
R1(config)#exit

# Router R2 ACL and Security Configuration
R2(config)#ip access-list extended User_ACL\
R2(config-ext-nacl)#permit icmp 10.2.2.0 0.0.0.255 10.0.1.0 0.0.0.255\
R2(config-ext-nacl)#permit icmp 10.2.2.0 0.0.0.255 10.0.1.0 0.0.0.255 echo-reply\
R2(config-ext-nacl)#permit icmp 10.2.2.0 0.0.0.255 10.1.1.0 0.0.0.255 echo-reply\
R2(config-ext-nacl)#permit icmp 10.2.2.0 0.0.0.255 10.2.1.0 0.0.0.255 echo-reply\
R2(config-ext-nacl)#deny ip 10.2.2.0 0.0.0.255 10.0.1.0 0.0.0.255\
R2(config-ext-nacl)#deny ip 10.2.2.0 0.0.0.255 10.1.1.0 0.0.0.255\
R2(config-ext-nacl)#deny ip 10.2.2.0 0.0.0.255 10.2.1.0 0.0.0.255\
R2(config-ext-nacl)#permit ip any any\
R2(config-ext-nacl)#exit\
R2(config)#ip access-list extended Guest_ACL\
R2(config-ext-nacl)#permit icmp 10.2.3.0 0.0.0.255 10.0.0.0 0.0.255.255 echo-reply\
R2(config-ext-nacl)#permit icmp 10.2.3.0 0.0.0.255 10.1.0.0 0.0.255.255 echo-reply\
R2(config-ext-nacl)#permit icmp 10.2.3.0 0.0.0.255 10.2.0.0 0.0.255.255 echo-reply\
R2(config-ext-nacl)#deny ip 10.2.3.0 0.0.0.255 10.0.0.0 0.0.255.255\
R2(config-ext-nacl)#deny ip 10.2.3.0 0.0.0.255 10.1.0.0 0.0.255.255\
R2(config-ext-nacl)#deny ip 10.2.3.0 0.0.0.255 10.2.0.0 0.0.255.255\
R2(config-ext-nacl)#permit ip any any\
R2(config-ext-nacl)#exit\
R2(config)#ip access-list extended Management_ACL\
R2(config-ext-nacl)#permit ip 10.0.1.0 0.0.0.255 any\
R2(config-ext-nacl)#permit ip 10.1.1.0 0.0.0.255 any\
R2(config-ext-nacl)#permit ip 10.2.1.0 0.0.0.255 any\
R2(config-ext-nacl)#exit\
R2(config)#int g0/0.10\
R2(config-subif)#ip access-group Management_ACL in\
R2(config-subif)#exit\
R2(config)#int g0/0.20\
R2(config-subif)#ip access-group User_ACL in\
R2(config-subif)#int g0/0.30\
R2(config-subif)#ip access-group Guest_ACL in\
R2(config-subif)#exit\
R2(config)#int g0/0.30\
R2(config-subif)#ip access-group Guest_ACL in\
R2(config)#ip domain-name greywan.com\
R2(config)#crypto key generate rsa modulus 2048\
R2(config)#username wantech secret Greym@nw@n1\
R2(config)#ip access-list standard Management_ACCESS\
R2(config-std-nacl)#permit 10.0.1.0 0.0.0.255\
R2(config-std-nacl)#permit 10.1.1.0 0.0.0.255\
R2(config-std-nacl)#permit 10.2.1.0 0.0.0.255\
R2(config-std-nacl)#exit\
R2(config)#line vty 0 4\
R2(config-line)#access-class Management_ACCESS in\
R2(config-line)#transport input ssh\
R2(config-line)#login local\
R2(config-line)#exec-timeout 5 0\
R2(config-line)#exit\
R2(config)#ip ssh version 2\
R2(config)#service password-encryption\
R2(config)#exit

# Verification test
# 1 Vlan Segmentation
Before routing on stick the three vlan 10,20,30 could not communicate to each other,after configuration on router on stick communication was successful. Also i configured inter vlan routing using open shortest path first to enable vlans accross the three sections to communicate.\
<img width="1360" height="764" alt="ping pc2 from pc0" src="https://github.com/user-attachments/assets/16d28741-d202-4ad6-8268-ab4bae7b9005" />\
<img width="1359" height="764" alt="ping pc7 from pc6" src="https://github.com/user-attachments/assets/f50ed0b7-3f7c-423e-ab8d-16f85242eb7d" />\
<img width="1366" height="768" alt="Intervlan comm ospf protocol R0 to R1R2" src="https://github.com/user-attachments/assets/ff82c5c3-8602-4f4c-b808-3d363f552b70" />\
# 2 Verify Port Security
I changed the mac address of PC2 on that is connected to switch S0 via interface f0/5 to trigger a a violation and below is a screenshot showing violation
<img width="705" height="455" alt="change pc2 mac" src="https://github.com/user-attachments/assets/5184cb7a-c77c-4e5b-ace7-51f0d1088f2d" />\
<img width="1364" height="765" alt="Port security" src="https://github.com/user-attachments/assets/567ef8b0-62f9-477c-b349-dd37b92bf645" />

# 2 DHCP Verification


