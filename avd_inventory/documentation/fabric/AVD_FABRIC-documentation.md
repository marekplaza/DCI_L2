# AVD_FABRIC

## Table of Contents

- [Fabric Switches and Management IP](#fabric-switches-and-management-ip)
  - [Fabric Switches with inband Management IP](#fabric-switches-with-inband-management-ip)
- [Fabric Topology](#fabric-topology)
- [Fabric IP Allocation](#fabric-ip-allocation)
  - [Fabric Point-To-Point Links](#fabric-point-to-point-links)
  - [Point-To-Point Links Node Allocation](#point-to-point-links-node-allocation)
  - [Loopback Interfaces (BGP EVPN Peering)](#loopback-interfaces-bgp-evpn-peering)
  - [Loopback0 Interfaces Node Allocation](#loopback0-interfaces-node-allocation)
  - [VTEP Loopback VXLAN Tunnel Source Interfaces (VTEPs Only)](#vtep-loopback-vxlan-tunnel-source-interfaces-vteps-only)
  - [VTEP Loopback Node allocation](#vtep-loopback-node-allocation)

## Fabric Switches and Management IP

| POD | Type | Node | Management IP | Platform | Provisioned in CloudVision | Serial Number |
| --- | ---- | ---- | ------------- | -------- | -------------------------- | ------------- |
| AVD_FABRIC | l3leaf | l01 | 10.0.2.1/16 | cEOS | Provisioned | - |
| AVD_FABRIC | l3leaf | l02 | 10.0.2.2/16 | cEOS | Provisioned | - |
| AVD_FABRIC | spine | s01 | 10.0.1.1/16 | cEOS | Provisioned | - |
| AVD_FABRIC | spine | s02 | 10.0.1.2/16 | cEOS | Provisioned | - |

> Provision status is based on Ansible inventory declaration and do not represent real status from CloudVision.

### Fabric Switches with inband Management IP

| POD | Type | Node | Management IP | Inband Interface |
| --- | ---- | ---- | ------------- | ---------------- |

## Fabric Topology

| Type | Node | Node Interface | Peer Type | Peer Node | Peer Interface |
| ---- | ---- | -------------- | --------- | ----------| -------------- |
| l3leaf | l01 | Ethernet1 | spine | s01 | Ethernet1 |
| l3leaf | l01 | Ethernet2 | spine | s02 | Ethernet1 |
| l3leaf | l02 | Ethernet1 | spine | s01 | Ethernet2 |
| l3leaf | l02 | Ethernet2 | spine | s02 | Ethernet2 |

## Fabric IP Allocation

### Fabric Point-To-Point Links

| Uplink IPv4 Pool | Available Addresses | Assigned addresses | Assigned Address % |
| ---------------- | ------------------- | ------------------ | ------------------ |
| 100.65.0.0/24 | 256 | 8 | 3.13 % |

### Point-To-Point Links Node Allocation

| Node | Node Interface | Node IP Address | Peer Node | Peer Interface | Peer IP Address |
| ---- | -------------- | --------------- | --------- | -------------- | --------------- |
| l01 | Ethernet1 | 100.65.0.1/31 | s01 | Ethernet1 | 100.65.0.0/31 |
| l01 | Ethernet2 | 100.65.0.3/31 | s02 | Ethernet1 | 100.65.0.2/31 |
| l02 | Ethernet1 | 100.65.0.5/31 | s01 | Ethernet2 | 100.65.0.4/31 |
| l02 | Ethernet2 | 100.65.0.7/31 | s02 | Ethernet2 | 100.65.0.6/31 |

### Loopback Interfaces (BGP EVPN Peering)

| Loopback Pool | Available Addresses | Assigned addresses | Assigned Address % |
| ------------- | ------------------- | ------------------ | ------------------ |
| 100.64.255.0/24 | 256 | 2 | 0.79 % |
| 100.65.255.0/24 | 256 | 2 | 0.79 % |

### Loopback0 Interfaces Node Allocation

| POD | Node | Loopback0 |
| --- | ---- | --------- |
| AVD_FABRIC | l01 | 100.65.255.3/32 |
| AVD_FABRIC | l02 | 100.65.255.4/32 |
| AVD_FABRIC | s01 | 100.64.255.1/32 |
| AVD_FABRIC | s02 | 100.64.255.2/32 |

### VTEP Loopback VXLAN Tunnel Source Interfaces (VTEPs Only)

| VTEP Loopback Pool | Available Addresses | Assigned addresses | Assigned Address % |
| --------------------- | ------------------- | ------------------ | ------------------ |
| 100.65.254.0/24 | 256 | 2 | 0.79 % |

### VTEP Loopback Node allocation

| POD | Node | Loopback1 |
| --- | ---- | --------- |
| AVD_FABRIC | l01 | 100.65.254.3/32 |
| AVD_FABRIC | l02 | 100.65.254.4/32 |
