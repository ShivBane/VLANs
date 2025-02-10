# VLANs Overview and Basic Requirements

## What is VLAN?
A Virtual Local Area Network (VLAN) is a logically segmented network within a switch, allowing devices to communicate as if they are on the same physical network. VLANs enhance network security, improve performance, and simplify management by isolating traffic.

## VLAN Basic Requirements
1. **Network Devices:**
   - Layer 2 and Layer 3 switches
   - Routers (for inter-VLAN routing)
   - PCs or other end devices

2. **Key Configurations:**
   - VLAN creation on switches
   - Assigning VLANs to switch ports
   - Configuring trunk ports for inter-switch communication
   - Setting up inter-VLAN routing (if needed)
   - Implementing DHCP for dynamic IP allocation
   - Applying Access Control Lists (ACLs) for security

## Summary of VLAN Implementations
- **Simple VLAN Configuration:**
  - Layer 3 switch connects multiple VLANs
  - PCs are grouped based on departments (e.g., HR, IT, Finance, Interns)

- **VLAN with ACLs and DHCP:**
  - Router assigns dynamic IPs
  - ACLs restrict unauthorized VLAN communication

- **Layer 2 VLAN-only Setup:**
  - Only same VLAN devices can communicate
  - Switches are interconnected using trunk ports

VLANs help in better network segmentation, control, and performance optimization, making them essential for efficient enterprise networking.