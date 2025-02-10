# VLAN Network Configuration with Access Lists and DHCP

## Description
This network consists of multiple VLANs configured on a Layer 3 switch with DHCP services and Access Control Lists (ACLs) for network security. The setup includes a router, a Layer 3 switch, and multiple Layer 2 switches connecting 12 PCs across four VLANs.

## Devices
- **1 Router** (Cisco 2911)
- **1 Layer 3 Switch** (Cisco 3560-24PS)
- **4 Layer 2 Switches** (Cisco 2960-24TT)
- **12 PCs** (Connected to Layer 2 switches, 3 per switch)

## Network Topology
- PCs connect to Layer 2 switches.
- Layer 2 switches connect to the Layer 3 switch.
- The Layer 3 switch connects to the router for external connectivity.

## VLAN Details
- **VLAN 10 - HR**  
  - Network: 192.168.10.0/24  
  - Default Gateway: 192.168.10.1  

- **VLAN 20 - IT**  
  - Network: 192.168.20.0/24  
  - Default Gateway: 192.168.20.1  

- **VLAN 30 - Finance**  
  - Network: 192.168.30.0/24  
  - Default Gateway: 192.168.30.1  

- **VLAN 40 - Intern**  
  - Network: 192.168.40.0/24  
  - Default Gateway: 192.168.40.1  

## Required Configuration

### 1. VLAN Configuration on the Layer 3 Switch
```sh
configure terminal
vlan 10
name HR
exit

vlan 20
name IT
exit

vlan 30
name Finance
exit

vlan 40
name Intern
exit
```

### 2. Assign VLANs to Ports
```sh
! Trunk Link to Router
interface GigabitEthernet0/1
switchport trunk encapsulation dot1q
switchport mode trunk
switchport trunk allowed vlan 10,20,30,40

! Trunk Links to Access Switches
interface fastEthernet 0/1
switchport trunk encapsulation dot1q
 switchport mode trunk
 switchport trunk allowed vlan 10

interface fastEthernet 0/2
switchport trunk encapsulation dot1q
 switchport mode trunk
 switchport trunk allowed vlan 20

interface fastEthernet 0/3
switchport trunk encapsulation dot1q
 switchport mode trunk
 switchport trunk allowed vlan 30

interface fastEthernet 0/4
switchport trunk encapsulation dot1q
 switchport mode trunk
 switchport trunk allowed vlan 40
exit
```

### 3. Configure Inter-VLAN Routing
```sh
! Create VLAN sub-interfaces
enable 
configure terminal
interface GigabitEthernet0/0
no shutdown

interface GigabitEthernet0/0.10
encapsulation dot1Q 10
ip address 192.168.10.1 255.255.255.0  

interface GigabitEthernet0/0.20
encapsulation dot1Q 20
ip address 192.168.20.1 255.255.255.0  

interface GigabitEthernet0/0.30
encapsulation dot1Q 30
ip address 192.168.30.1 255.255.255.0  

interface GigabitEthernet0/0.40
encapsulation dot1Q 40
ip address 192.168.40.1 255.255.255.0
exit

ip routing
```

### 4. Configure DHCP on Router
```sh
ip dhcp excluded-address 192.168.10.1 192.168.10.10
ip dhcp excluded-address 192.168.20.1 192.168.20.10
ip dhcp excluded-address 192.168.30.1 192.168.30.10
ip dhcp excluded-address 192.168.40.1 192.168.40.10

ip dhcp pool HR
 network 192.168.10.0 255.255.255.0
 default-router 192.168.10.1
 dns-server 8.8.8.8

ip dhcp pool IT
 network 192.168.20.0 255.255.255.0
 default-router 192.168.20.1
 dns-server 8.8.8.8

ip dhcp pool Finance
 network 192.168.30.0 255.255.255.0
 default-router 192.168.30.1
 dns-server 8.8.8.8

ip dhcp pool Intern
 network 192.168.40.0 255.255.255.0
 default-router 192.168.40.1
 dns-server 8.8.8.8```

### 5. Configure Access Control Lists (ACLs)
```sh
enable
configure terminal

! Access Control Lists (ACLs)
access-list 100 deny ip 192.168.40.0 0.0.0.255 192.168.10.0 0.0.0.255
access-list 100 deny ip 192.168.40.0 0.0.0.255 192.168.30.0 0.0.0.255
access-list 100 permit ip any any

access-list 101 deny ip 192.168.20.0 0.0.0.255 192.168.30.0 0.0.0.255
access-list 101 permit ip any any

interface GigabitEthernet0/0.40
 ip access-group 100 in

interface GigabitEthernet0/0.20
 ip access-group 101 in
```

### 6. Verify Configuration
```sh
show vlan brief
show ip interface brief
show ip dhcp binding
show access-lists
show ip route
ping 192.168.30.2 source 192.168.20.2
```