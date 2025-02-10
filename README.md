# VLANs Overview and Basic Requirements

## What is VLAN?

A Virtual Local Area Network (VLAN) is a logically segmented network within a switch, allowing devices to communicate as if they are on the same physical network. VLANs enhance network security, improve performance, and simplify management by isolating traffic.

## What is DHCP?

Dynamic Host Configuration Protocol (DHCP) is a network protocol that dynamically assigns IP addresses to devices on a network. This reduces manual configuration efforts and ensures efficient IP address management.

### Types of DHCP Allocations:

1. **Dynamic Allocation** - Automatically assigns IP addresses for a set lease time.
2. **Static Allocation** - Assigns a predefined IP address to a specific device based on its MAC address.
3. **Automatic Allocation** - Permanently assigns an IP address to a device the first time it connects.

## What is an Access Control List (ACL)?

An Access Control List (ACL) is a set of rules that control incoming and outgoing network traffic based on defined security policies.

### Types of ACLs:

1. **Standard ACLs** - Filter traffic based only on source IP addresses.
2. **Extended ACLs** - Filter traffic based on source/destination IP, port numbers, and protocols.
3. **Named ACLs** - Allow custom-named ACLs for better organization and management.

ACLs help secure VLANs by restricting unauthorized communication between network segments.

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

