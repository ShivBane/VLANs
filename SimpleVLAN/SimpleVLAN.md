# SimpleVLAN Network Configuration

## Description

This network consists of two VLANs: VLAN 1 and VLAN 2. Each VLAN has two PCs and a unique subnet. A Layer 3 switch is used for inter-VLAN routing, allowing communication between VLANs. The setup ensures efficient network segmentation and improved security.

## VLAN Details

- **VLAN 1**

  - Network: 10.0.0.0/24
  - Default Gateway: 10.0.0.1
  - Devices: 2 PCs

- **VLAN 2**

  - Network: 20.0.0.0/24
  - Default Gateway: 20.0.0.1
  - Devices: 2 PCs

- **Layer 3 Switch**

  - Connects both VLANs and provides inter-VLAN routing.

## Required Configuration

### 1. VLAN Configuration on the Layer 3 Switch

```sh
configure terminal
vlan 1
name VLAN1
exit

vlan 2
name VLAN2
exit
```

### 2. Assign VLANs to Ports

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
switchport access vlan 2
exit
```

### 3. Configure Inter-VLAN Routing

```sh
interface Vlan1
ip address 10.0.0.1 255.255.255.0
no shutdown
exit

interface Vlan2
ip address 20.0.0.1 255.255.255.0
no shutdown
exit

ip routing
```

### 4. Configure PC IP Addresses

#### VLAN 1 PCs:

- **PC1**: IP: 10.0.0.2, Subnet: 255.255.255.0, Gateway: 10.0.0.1
- **PC2**: IP: 10.0.0.3, Subnet: 255.255.255.0, Gateway: 10.0.0.1

#### VLAN 2 PCs:

- **PC3**: IP: 20.0.0.2, Subnet: 255.255.255.0, Gateway: 20.0.0.1
- **PC4**: IP: 20.0.0.3, Subnet: 255.255.255.0, Gateway: 20.0.0.1

### 5. Verify Configuration

```sh
show vlan brief
show ip interface brief
show ip route
ping 20.0.0.2 source 10.0.0.2
```

This configuration ensures proper VLAN segmentation and enables communication between VLANs through inter-VLAN routing.