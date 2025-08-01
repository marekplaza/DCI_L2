# FABRIC

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
| FABRIC | l3leaf | dc1-lf01 | 111.1.2.1/8 | cEOS | Provisioned | - |
| FABRIC | l3leaf | dc1-lf02 | 111.1.2.2/8 | cEOS | Provisioned | - |
| FABRIC | l3leaf | dc1-lf03 | 111.1.2.3/8 | cEOS | Provisioned | - |
| FABRIC | l3leaf | dc1-lf04 | 111.1.2.4/8 | cEOS | Provisioned | - |
| FABRIC | l3leaf | dc1-lf05 | 111.1.2.5/8 | cEOS | Provisioned | - |
| FABRIC | l3leaf | dc1-lf06 | 111.1.2.6/8 | cEOS | Provisioned | - |
| FABRIC | l3leaf | dc1-lf07 | 111.1.2.7/8 | cEOS | Provisioned | - |
| FABRIC | l3leaf | dc1-lf08 | 111.1.2.8/8 | cEOS | Provisioned | - |
| FABRIC | l3leaf | dc1-lf09 | 111.1.2.9/8 | cEOS | Provisioned | - |
| FABRIC | l3leaf | dc1-lf10 | 111.1.2.10/8 | cEOS | Provisioned | - |
| FABRIC | l3leaf | dc1-lf11 | 111.1.2.11/8 | cEOS | Provisioned | - |
| FABRIC | l3leaf | dc1-lf12 | 111.1.2.12/8 | cEOS | Provisioned | - |
| FABRIC | l3leaf | dc1-lf13 | 111.1.2.13/8 | cEOS | Provisioned | - |
| FABRIC | l3leaf | dc1-lf14 | 111.1.2.14/8 | cEOS | Provisioned | - |
| FABRIC | spine | dc1-sp01 | 111.1.1.1/8 | cEOS | Provisioned | - |
| FABRIC | spine | dc1-sp02 | 111.1.1.2/8 | cEOS | Provisioned | - |
| FABRIC | l3leaf | dc2-lf01 | 111.2.2.1/8 | cEOS | Provisioned | - |
| FABRIC | l3leaf | dc2-lf02 | 111.2.2.2/8 | cEOS | Provisioned | - |
| FABRIC | l3leaf | dc2-lf03 | 111.2.2.3/8 | cEOS | Provisioned | - |
| FABRIC | l3leaf | dc2-lf04 | 111.2.2.4/8 | cEOS | Provisioned | - |
| FABRIC | l3leaf | dc2-lf05 | 111.2.2.5/8 | cEOS | Provisioned | - |
| FABRIC | l3leaf | dc2-lf06 | 111.2.2.6/8 | cEOS | Provisioned | - |
| FABRIC | spine | dc2-sp01 | 111.2.1.1/8 | cEOS | Provisioned | - |
| FABRIC | spine | dc2-sp02 | 111.2.1.2/8 | cEOS | Provisioned | - |

> Provision status is based on Ansible inventory declaration and do not represent real status from CloudVision.

### Fabric Switches with inband Management IP

| POD | Type | Node | Management IP | Inband Interface |
| --- | ---- | ---- | ------------- | ---------------- |

## Fabric Topology

| Type | Node | Node Interface | Peer Type | Peer Node | Peer Interface |
| ---- | ---- | -------------- | --------- | ----------| -------------- |
| l3leaf | dc1-lf01 | Ethernet1 | spine | dc1-sp01 | Ethernet1 |
| l3leaf | dc1-lf01 | Ethernet2 | spine | dc1-sp02 | Ethernet1 |
| l3leaf | dc1-lf02 | Ethernet1 | spine | dc1-sp01 | Ethernet2 |
| l3leaf | dc1-lf02 | Ethernet2 | spine | dc1-sp02 | Ethernet2 |
| l3leaf | dc1-lf03 | Ethernet1 | spine | dc1-sp01 | Ethernet3 |
| l3leaf | dc1-lf03 | Ethernet2 | spine | dc1-sp02 | Ethernet3 |
| l3leaf | dc1-lf03 | Ethernet6 | l3leaf | dc2-lf03 | Ethernet6 |
| l3leaf | dc1-lf04 | Ethernet1 | spine | dc1-sp01 | Ethernet4 |
| l3leaf | dc1-lf04 | Ethernet2 | spine | dc1-sp02 | Ethernet4 |
| l3leaf | dc1-lf04 | Ethernet6 | l3leaf | dc2-lf04 | Ethernet6 |
| l3leaf | dc1-lf05 | Ethernet1 | spine | dc1-sp01 | Ethernet5 |
| l3leaf | dc1-lf05 | Ethernet2 | spine | dc1-sp02 | Ethernet5 |
| l3leaf | dc1-lf06 | Ethernet1 | spine | dc1-sp01 | Ethernet6 |
| l3leaf | dc1-lf06 | Ethernet2 | spine | dc1-sp02 | Ethernet6 |
| l3leaf | dc1-lf07 | Ethernet1 | spine | dc1-sp01 | Ethernet7 |
| l3leaf | dc1-lf07 | Ethernet2 | spine | dc1-sp02 | Ethernet7 |
| l3leaf | dc1-lf08 | Ethernet1 | spine | dc1-sp01 | Ethernet8 |
| l3leaf | dc1-lf08 | Ethernet2 | spine | dc1-sp02 | Ethernet8 |
| l3leaf | dc1-lf09 | Ethernet1 | spine | dc1-sp01 | Ethernet9 |
| l3leaf | dc1-lf09 | Ethernet2 | spine | dc1-sp02 | Ethernet9 |
| l3leaf | dc1-lf10 | Ethernet1 | spine | dc1-sp01 | Ethernet10 |
| l3leaf | dc1-lf10 | Ethernet2 | spine | dc1-sp02 | Ethernet10 |
| l3leaf | dc1-lf11 | Ethernet1 | spine | dc1-sp01 | Ethernet11 |
| l3leaf | dc1-lf11 | Ethernet2 | spine | dc1-sp02 | Ethernet11 |
| l3leaf | dc1-lf12 | Ethernet1 | spine | dc1-sp01 | Ethernet12 |
| l3leaf | dc1-lf12 | Ethernet2 | spine | dc1-sp02 | Ethernet12 |
| l3leaf | dc1-lf13 | Ethernet1 | spine | dc1-sp01 | Ethernet13 |
| l3leaf | dc1-lf13 | Ethernet2 | spine | dc1-sp02 | Ethernet13 |
| l3leaf | dc1-lf14 | Ethernet1 | spine | dc1-sp01 | Ethernet14 |
| l3leaf | dc1-lf14 | Ethernet2 | spine | dc1-sp02 | Ethernet14 |
| l3leaf | dc2-lf01 | Ethernet1 | spine | dc2-sp01 | Ethernet1 |
| l3leaf | dc2-lf01 | Ethernet2 | spine | dc2-sp02 | Ethernet1 |
| l3leaf | dc2-lf02 | Ethernet1 | spine | dc2-sp01 | Ethernet2 |
| l3leaf | dc2-lf02 | Ethernet2 | spine | dc2-sp02 | Ethernet2 |
| l3leaf | dc2-lf03 | Ethernet1 | spine | dc2-sp01 | Ethernet3 |
| l3leaf | dc2-lf03 | Ethernet2 | spine | dc2-sp02 | Ethernet3 |
| l3leaf | dc2-lf04 | Ethernet1 | spine | dc2-sp01 | Ethernet4 |
| l3leaf | dc2-lf04 | Ethernet2 | spine | dc2-sp02 | Ethernet4 |
| l3leaf | dc2-lf05 | Ethernet1 | spine | dc2-sp01 | Ethernet5 |
| l3leaf | dc2-lf05 | Ethernet2 | spine | dc2-sp02 | Ethernet5 |
| l3leaf | dc2-lf06 | Ethernet1 | spine | dc2-sp01 | Ethernet6 |
| l3leaf | dc2-lf06 | Ethernet2 | spine | dc2-sp02 | Ethernet6 |

## Fabric IP Allocation

### Fabric Point-To-Point Links

| Uplink IPv4 Pool | Available Addresses | Assigned addresses | Assigned Address % |
| ---------------- | ------------------- | ------------------ | ------------------ |
| 10.255.255.0/26 | 64 | 56 | 87.5 % |
| 10.255.255.64/26 | 64 | 24 | 37.5 % |

### Point-To-Point Links Node Allocation

| Node | Node Interface | Node IP Address | Peer Node | Peer Interface | Peer IP Address |
| ---- | -------------- | --------------- | --------- | -------------- | --------------- |
| dc1-lf01 | Ethernet1 | 10.255.255.1/31 | dc1-sp01 | Ethernet1 | 10.255.255.0/31 |
| dc1-lf01 | Ethernet2 | 10.255.255.3/31 | dc1-sp02 | Ethernet1 | 10.255.255.2/31 |
| dc1-lf02 | Ethernet1 | 10.255.255.5/31 | dc1-sp01 | Ethernet2 | 10.255.255.4/31 |
| dc1-lf02 | Ethernet2 | 10.255.255.7/31 | dc1-sp02 | Ethernet2 | 10.255.255.6/31 |
| dc1-lf03 | Ethernet1 | 10.255.255.9/31 | dc1-sp01 | Ethernet3 | 10.255.255.8/31 |
| dc1-lf03 | Ethernet2 | 10.255.255.11/31 | dc1-sp02 | Ethernet3 | 10.255.255.10/31 |
| dc1-lf03 | Ethernet6 | 172.16.100.0/31 | dc2-lf03 | Ethernet6 | 172.16.100.1/31 |
| dc1-lf04 | Ethernet1 | 10.255.255.13/31 | dc1-sp01 | Ethernet4 | 10.255.255.12/31 |
| dc1-lf04 | Ethernet2 | 10.255.255.15/31 | dc1-sp02 | Ethernet4 | 10.255.255.14/31 |
| dc1-lf04 | Ethernet6 | 172.16.100.2/31 | dc2-lf04 | Ethernet6 | 172.16.100.3/31 |
| dc1-lf05 | Ethernet1 | 10.255.255.17/31 | dc1-sp01 | Ethernet5 | 10.255.255.16/31 |
| dc1-lf05 | Ethernet2 | 10.255.255.19/31 | dc1-sp02 | Ethernet5 | 10.255.255.18/31 |
| dc1-lf06 | Ethernet1 | 10.255.255.21/31 | dc1-sp01 | Ethernet6 | 10.255.255.20/31 |
| dc1-lf06 | Ethernet2 | 10.255.255.23/31 | dc1-sp02 | Ethernet6 | 10.255.255.22/31 |
| dc1-lf07 | Ethernet1 | 10.255.255.25/31 | dc1-sp01 | Ethernet7 | 10.255.255.24/31 |
| dc1-lf07 | Ethernet2 | 10.255.255.27/31 | dc1-sp02 | Ethernet7 | 10.255.255.26/31 |
| dc1-lf08 | Ethernet1 | 10.255.255.29/31 | dc1-sp01 | Ethernet8 | 10.255.255.28/31 |
| dc1-lf08 | Ethernet2 | 10.255.255.31/31 | dc1-sp02 | Ethernet8 | 10.255.255.30/31 |
| dc1-lf09 | Ethernet1 | 10.255.255.33/31 | dc1-sp01 | Ethernet9 | 10.255.255.32/31 |
| dc1-lf09 | Ethernet2 | 10.255.255.35/31 | dc1-sp02 | Ethernet9 | 10.255.255.34/31 |
| dc1-lf10 | Ethernet1 | 10.255.255.37/31 | dc1-sp01 | Ethernet10 | 10.255.255.36/31 |
| dc1-lf10 | Ethernet2 | 10.255.255.39/31 | dc1-sp02 | Ethernet10 | 10.255.255.38/31 |
| dc1-lf11 | Ethernet1 | 10.255.255.41/31 | dc1-sp01 | Ethernet11 | 10.255.255.40/31 |
| dc1-lf11 | Ethernet2 | 10.255.255.43/31 | dc1-sp02 | Ethernet11 | 10.255.255.42/31 |
| dc1-lf12 | Ethernet1 | 10.255.255.45/31 | dc1-sp01 | Ethernet12 | 10.255.255.44/31 |
| dc1-lf12 | Ethernet2 | 10.255.255.47/31 | dc1-sp02 | Ethernet12 | 10.255.255.46/31 |
| dc1-lf13 | Ethernet1 | 10.255.255.49/31 | dc1-sp01 | Ethernet13 | 10.255.255.48/31 |
| dc1-lf13 | Ethernet2 | 10.255.255.51/31 | dc1-sp02 | Ethernet13 | 10.255.255.50/31 |
| dc1-lf14 | Ethernet1 | 10.255.255.53/31 | dc1-sp01 | Ethernet14 | 10.255.255.52/31 |
| dc1-lf14 | Ethernet2 | 10.255.255.55/31 | dc1-sp02 | Ethernet14 | 10.255.255.54/31 |
| dc2-lf01 | Ethernet1 | 10.255.255.105/31 | dc2-sp01 | Ethernet1 | 10.255.255.104/31 |
| dc2-lf01 | Ethernet2 | 10.255.255.107/31 | dc2-sp02 | Ethernet1 | 10.255.255.106/31 |
| dc2-lf02 | Ethernet1 | 10.255.255.109/31 | dc2-sp01 | Ethernet2 | 10.255.255.108/31 |
| dc2-lf02 | Ethernet2 | 10.255.255.111/31 | dc2-sp02 | Ethernet2 | 10.255.255.110/31 |
| dc2-lf03 | Ethernet1 | 10.255.255.113/31 | dc2-sp01 | Ethernet3 | 10.255.255.112/31 |
| dc2-lf03 | Ethernet2 | 10.255.255.115/31 | dc2-sp02 | Ethernet3 | 10.255.255.114/31 |
| dc2-lf04 | Ethernet1 | 10.255.255.117/31 | dc2-sp01 | Ethernet4 | 10.255.255.116/31 |
| dc2-lf04 | Ethernet2 | 10.255.255.119/31 | dc2-sp02 | Ethernet4 | 10.255.255.118/31 |
| dc2-lf05 | Ethernet1 | 10.255.255.121/31 | dc2-sp01 | Ethernet5 | 10.255.255.120/31 |
| dc2-lf05 | Ethernet2 | 10.255.255.123/31 | dc2-sp02 | Ethernet5 | 10.255.255.122/31 |
| dc2-lf06 | Ethernet1 | 10.255.255.125/31 | dc2-sp01 | Ethernet6 | 10.255.255.124/31 |
| dc2-lf06 | Ethernet2 | 10.255.255.127/31 | dc2-sp02 | Ethernet6 | 10.255.255.126/31 |

### Loopback Interfaces (BGP EVPN Peering)

| Loopback Pool | Available Addresses | Assigned addresses | Assigned Address % |
| ------------- | ------------------- | ------------------ | ------------------ |
| 10.255.0.0/27 | 32 | 16 | 50.0 % |
| 10.255.128.0/27 | 32 | 8 | 25.0 % |

### Loopback0 Interfaces Node Allocation

| POD | Node | Loopback0 |
| --- | ---- | --------- |
| FABRIC | dc1-lf01 | 10.255.0.3/32 |
| FABRIC | dc1-lf02 | 10.255.0.4/32 |
| FABRIC | dc1-lf03 | 10.255.0.5/32 |
| FABRIC | dc1-lf04 | 10.255.0.6/32 |
| FABRIC | dc1-lf05 | 10.255.0.7/32 |
| FABRIC | dc1-lf06 | 10.255.0.8/32 |
| FABRIC | dc1-lf07 | 10.255.0.9/32 |
| FABRIC | dc1-lf08 | 10.255.0.10/32 |
| FABRIC | dc1-lf09 | 10.255.0.11/32 |
| FABRIC | dc1-lf10 | 10.255.0.12/32 |
| FABRIC | dc1-lf11 | 10.255.0.13/32 |
| FABRIC | dc1-lf12 | 10.255.0.14/32 |
| FABRIC | dc1-lf13 | 10.255.0.15/32 |
| FABRIC | dc1-lf14 | 10.255.0.16/32 |
| FABRIC | dc1-sp01 | 10.255.0.1/32 |
| FABRIC | dc1-sp02 | 10.255.0.2/32 |
| FABRIC | dc2-lf01 | 10.255.128.13/32 |
| FABRIC | dc2-lf02 | 10.255.128.14/32 |
| FABRIC | dc2-lf03 | 10.255.128.15/32 |
| FABRIC | dc2-lf04 | 10.255.128.16/32 |
| FABRIC | dc2-lf05 | 10.255.128.17/32 |
| FABRIC | dc2-lf06 | 10.255.128.18/32 |
| FABRIC | dc2-sp01 | 10.255.128.11/32 |
| FABRIC | dc2-sp02 | 10.255.128.12/32 |

### VTEP Loopback VXLAN Tunnel Source Interfaces (VTEPs Only)

| VTEP Loopback Pool | Available Addresses | Assigned addresses | Assigned Address % |
| --------------------- | ------------------- | ------------------ | ------------------ |
| 10.255.1.0/27 | 32 | 14 | 43.75 % |
| 10.255.129.64/27 | 32 | 6 | 18.75 % |

### VTEP Loopback Node allocation

| POD | Node | Loopback1 |
| --- | ---- | --------- |
| FABRIC | dc1-lf01 | 10.255.1.3/32 |
| FABRIC | dc1-lf02 | 10.255.1.4/32 |
| FABRIC | dc1-lf03 | 10.255.1.5/32 |
| FABRIC | dc1-lf04 | 10.255.1.6/32 |
| FABRIC | dc1-lf05 | 10.255.1.7/32 |
| FABRIC | dc1-lf06 | 10.255.1.8/32 |
| FABRIC | dc1-lf07 | 10.255.1.9/32 |
| FABRIC | dc1-lf08 | 10.255.1.10/32 |
| FABRIC | dc1-lf09 | 10.255.1.11/32 |
| FABRIC | dc1-lf10 | 10.255.1.12/32 |
| FABRIC | dc1-lf11 | 10.255.1.13/32 |
| FABRIC | dc1-lf12 | 10.255.1.14/32 |
| FABRIC | dc1-lf13 | 10.255.1.15/32 |
| FABRIC | dc1-lf14 | 10.255.1.16/32 |
| FABRIC | dc2-lf01 | 10.255.129.77/32 |
| FABRIC | dc2-lf02 | 10.255.129.78/32 |
| FABRIC | dc2-lf03 | 10.255.129.79/32 |
| FABRIC | dc2-lf04 | 10.255.129.80/32 |
| FABRIC | dc2-lf05 | 10.255.129.81/32 |
| FABRIC | dc2-lf06 | 10.255.129.82/32 |
