# Secure-Multi-Section-Network-Design
This is a three section network design in packet tracer, consist of three routers, three switches and several pcs per vlan and the topology is interconnected in triangle design.
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
