# VLAN Configuration

## Description
This network consists of two Layer 2 switches and eight PCs, organized into three VLANs: Accounting, HR, and Admission. All VLANs operate on the same network (10.0.0.0/24). A crossover cable connects the switches, and communication is restricted to devices within the same VLAN.

## Devices
- **2 Layer 2 Switches** (Cisco 2960-24TT)
- **8 PCs** (Connected to VLANs as per the topology)

## VLAN Details
- **VLAN 1 - Accounting**  
  - IP Range: 10.0.0.2, 10.0.0.3, 10.0.0.6, 10.0.0.7  

- **VLAN 2 - HR**  
  - IP Range: 10.0.0.1, 10.0.0.5  

- **VLAN 3 - Admission**  
  - IP Range: 10.0.0.4, 10.0.0.8  

## Connection Setup
- Both switches are connected via a crossover cable.
- **Switch 1:**
  - VLAN 1 (Accounting): PC1 (10.0.0.2), PC2 (10.0.0.3)
  - VLAN 2 (HR): PC3 (10.0.0.1)
  - VLAN 3 (Admission): PC4 (10.0.0.4)
- **Switch 2:**
  - VLAN 1 (Accounting): PC5 (10.0.0.6), PC6 (10.0.0.7)
  - VLAN 2 (HR): PC7 (10.0.0.5)
  - VLAN 3 (Admission): PC8 (10.0.0.8)

## VLAN Configuration on Switches

### 1. Create VLANs
```sh
configure terminal
vlan 1
name Accounting
exit

vlan 2
name HR
exit

vlan 3
name Admission
exit
```

### 2. Assign VLANs to Ports on Switch 1
```sh
interface FastEthernet0/1
switchport mode access
switchport access vlan 1
exit

interface FastEthernet0/2
switchport mode access
switchport access vlan 1
exit

interface FastEthernet0/3
switchport mode access
switchport access vlan 2
exit

interface FastEthernet0/4
switchport mode access
switchport access vlan 3
exit
```

### 3. Assign VLANs to Ports on Switch 2
```sh
interface FastEthernet0/1
switchport mode access
switchport access vlan 1
exit

interface FastEthernet0/2
switchport mode access
switchport access vlan 1
exit

interface FastEthernet0/3
switchport mode access
switchport access vlan 2
exit

interface FastEthernet0/4
switchport mode access
switchport access vlan 3
exit
```

### 4. Configure Trunk Port for Switch Interconnection
```sh
interface FastEthernet0/24
switchport mode trunk
exit
```

## Verification
```sh
show vlan brief
show mac address-table
ping 10.0.0.6 source 10.0.0.2
```

This configuration ensures that devices within the same VLAN can communicate while restricting inter-VLAN communication.