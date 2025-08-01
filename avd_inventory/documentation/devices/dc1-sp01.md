# dc1-sp01

## Table of Contents

- [Management](#management)
  - [Management Interfaces](#management-interfaces)
  - [DNS Domain](#dns-domain)
  - [IP Name Servers](#ip-name-servers)
  - [NTP](#ntp)
  - [Management API HTTP](#management-api-http)
- [Authentication](#authentication)
  - [Local Users](#local-users)
  - [AAA Authorization](#aaa-authorization)
- [Monitoring](#monitoring)
  - [TerminAttr Daemon](#terminattr-daemon)
- [Spanning Tree](#spanning-tree)
  - [Spanning Tree Summary](#spanning-tree-summary)
  - [Spanning Tree Device Configuration](#spanning-tree-device-configuration)
- [Internal VLAN Allocation Policy](#internal-vlan-allocation-policy)
  - [Internal VLAN Allocation Policy Summary](#internal-vlan-allocation-policy-summary)
  - [Internal VLAN Allocation Policy Device Configuration](#internal-vlan-allocation-policy-device-configuration)
- [Interfaces](#interfaces)
  - [Ethernet Interfaces](#ethernet-interfaces)
  - [Loopback Interfaces](#loopback-interfaces)
- [Routing](#routing)
  - [Service Routing Protocols Model](#service-routing-protocols-model)
  - [IP Routing](#ip-routing)
  - [IPv6 Routing](#ipv6-routing)
  - [Static Routes](#static-routes)
  - [Router BGP](#router-bgp)
- [BFD](#bfd)
  - [Router BFD](#router-bfd)
- [Filters](#filters)
  - [Prefix-lists](#prefix-lists)
  - [Route-maps](#route-maps)
- [VRF Instances](#vrf-instances)
  - [VRF Instances Summary](#vrf-instances-summary)
  - [VRF Instances Device Configuration](#vrf-instances-device-configuration)
- [EOS CLI Device Configuration](#eos-cli-device-configuration)

## Management

### Management Interfaces

#### Management Interfaces Summary

##### IPv4

| Management Interface | Description | Type | VRF | IP Address | Gateway |
| -------------------- | ----------- | ---- | --- | ---------- | ------- |
| Management0 | oob_management | oob | MGMT | 111.1.1.1/8 | 172.16.1.1 |

##### IPv6

| Management Interface | Description | Type | VRF | IPv6 Address | IPv6 Gateway |
| -------------------- | ----------- | ---- | --- | ------------ | ------------ |
| Management0 | oob_management | oob | MGMT | - | - |

#### Management Interfaces Device Configuration

```eos
!
interface Management0
   description oob_management
   no shutdown
   vrf MGMT
   ip address 111.1.1.1/8
```

### DNS Domain

DNS domain: orlen.mgmt

#### DNS Domain Device Configuration

```eos
dns domain orlen.mgmt
!
```

### IP Name Servers

#### IP Name Servers Summary

| Name Server | VRF | Priority |
| ----------- | --- | -------- |
| 8.8.8.8 | MGMT | - |

#### IP Name Servers Device Configuration

```eos
ip name-server vrf MGMT 8.8.8.8
```

### NTP

#### NTP Summary

##### NTP Local Interface

| Interface | VRF |
| --------- | --- |
| Management0 | MGMT |

##### NTP Servers

| Server | VRF | Preferred | Burst | iBurst | Version | Min Poll | Max Poll | Local-interface | Key |
| ------ | --- | --------- | ----- | ------ | ------- | -------- | -------- | --------------- | --- |
| time.apple.com | MGMT | - | - | - | - | - | - | - | - |
| time.google.com | MGMT | - | - | - | - | - | - | - | - |
| time.windows.com | MGMT | - | - | - | - | - | - | - | - |

#### NTP Device Configuration

```eos
!
ntp local-interface vrf MGMT Management0
ntp server vrf MGMT time.apple.com
ntp server vrf MGMT time.google.com
ntp server vrf MGMT time.windows.com
```

### Management API HTTP

#### Management API HTTP Summary

| HTTP | HTTPS | Default Services |
| ---- | ----- | ---------------- |
| False | True | - |

#### Management API VRF Access

| VRF Name | IPv4 ACL | IPv6 ACL |
| -------- | -------- | -------- |
| MGMT | - | - |

#### Management API HTTP Device Configuration

```eos
!
management api http-commands
   protocol https
   no shutdown
   !
   vrf MGMT
      no shutdown
```

## Authentication

### Local Users

#### Local Users Summary

| User | Privilege | Role | Disabled | Shell |
| ---- | --------- | ---- | -------- | ----- |
| admin | 15 | network-admin | False | - |
| arista | 15 | network-admin | False | - |

#### Local Users Device Configuration

```eos
!
username admin privilege 15 role network-admin nopassword
username arista privilege 15 role network-admin secret sha512 <removed>
```

### AAA Authorization

#### AAA Authorization Summary

| Type | User Stores |
| ---- | ----------- |
| Exec | local |

Authorization for configuration commands is disabled.

#### AAA Authorization Device Configuration

```eos
aaa authorization exec default local
!
```

## Monitoring

### TerminAttr Daemon

#### TerminAttr Daemon Summary

| CV Compression | CloudVision Servers | VRF | Authentication | Smash Excludes | Ingest Exclude | Bypass AAA |
| -------------- | ------------------- | --- | -------------- | -------------- | -------------- | ---------- |
| gzip | apiserver.cv-staging.corp.arista.io:443 | MGMT | token-secure,/mnt/flash/cv-onboarding-token | ale,flexCounter,hardware,kni,pulse,strata | /Sysdb/cell/1/agent,/Sysdb/cell/2/agent | True |

#### TerminAttr Daemon Device Configuration

```eos
!
daemon TerminAttr
   exec /usr/bin/TerminAttr -cvaddr=apiserver.cv-staging.corp.arista.io:443 -cvauth=token-secure,/mnt/flash/cv-onboarding-token -cvvrf=MGMT -disableaaa -smashexcludes=ale,flexCounter,hardware,kni,pulse,strata -ingestexclude=/Sysdb/cell/1/agent,/Sysdb/cell/2/agent -taillogs
   no shutdown
```

## Spanning Tree

### Spanning Tree Summary

STP mode: **none**

### Spanning Tree Device Configuration

```eos
!
spanning-tree mode none
```

## Internal VLAN Allocation Policy

### Internal VLAN Allocation Policy Summary

| Policy Allocation | Range Beginning | Range Ending |
| ------------------| --------------- | ------------ |
| ascending | 1006 | 1199 |

### Internal VLAN Allocation Policy Device Configuration

```eos
!
vlan internal order ascending range 1006 1199
```

## Interfaces

### Ethernet Interfaces

#### Ethernet Interfaces Summary

##### L2

| Interface | Description | Mode | VLANs | Native VLAN | Trunk Group | Channel-Group |
| --------- | ----------- | ---- | ----- | ----------- | ----------- | ------------- |

*Inherited from Port-Channel Interface

##### IPv4

| Interface | Description | Type | Channel Group | IP Address | VRF |  MTU | Shutdown | ACL In | ACL Out |
| --------- | ----------- | -----| ------------- | ---------- | ----| ---- | -------- | ------ | ------- |
| Ethernet1 | P2P_LINK_TO_DC1-LF01_Ethernet1 | routed | - | 10.255.255.0/31 | default | 9214 | False | - | - |
| Ethernet2 | P2P_LINK_TO_DC1-LF02_Ethernet1 | routed | - | 10.255.255.4/31 | default | 9214 | False | - | - |
| Ethernet3 | P2P_LINK_TO_DC1-LF03_Ethernet1 | routed | - | 10.255.255.8/31 | default | 9214 | False | - | - |
| Ethernet4 | P2P_LINK_TO_DC1-LF04_Ethernet1 | routed | - | 10.255.255.12/31 | default | 9214 | False | - | - |
| Ethernet5 | P2P_LINK_TO_DC1-LF05_Ethernet1 | routed | - | 10.255.255.16/31 | default | 9214 | False | - | - |
| Ethernet6 | P2P_LINK_TO_DC1-LF06_Ethernet1 | routed | - | 10.255.255.20/31 | default | 9214 | False | - | - |
| Ethernet7 | P2P_LINK_TO_DC1-LF07_Ethernet1 | routed | - | 10.255.255.24/31 | default | 9214 | False | - | - |
| Ethernet8 | P2P_LINK_TO_DC1-LF08_Ethernet1 | routed | - | 10.255.255.28/31 | default | 9214 | False | - | - |
| Ethernet9 | P2P_LINK_TO_DC1-LF09_Ethernet1 | routed | - | 10.255.255.32/31 | default | 9214 | False | - | - |
| Ethernet10 | P2P_LINK_TO_DC1-LF10_Ethernet1 | routed | - | 10.255.255.36/31 | default | 9214 | False | - | - |
| Ethernet11 | P2P_LINK_TO_DC1-LF11_Ethernet1 | routed | - | 10.255.255.40/31 | default | 9214 | False | - | - |
| Ethernet12 | P2P_LINK_TO_DC1-LF12_Ethernet1 | routed | - | 10.255.255.44/31 | default | 9214 | False | - | - |
| Ethernet13 | P2P_LINK_TO_DC1-LF13_Ethernet1 | routed | - | 10.255.255.48/31 | default | 9214 | False | - | - |
| Ethernet14 | P2P_LINK_TO_DC1-LF14_Ethernet1 | routed | - | 10.255.255.52/31 | default | 9214 | False | - | - |

#### Ethernet Interfaces Device Configuration

```eos
!
interface Ethernet1
   description P2P_LINK_TO_DC1-LF01_Ethernet1
   no shutdown
   mtu 9214
   no switchport
   ip address 10.255.255.0/31
!
interface Ethernet2
   description P2P_LINK_TO_DC1-LF02_Ethernet1
   no shutdown
   mtu 9214
   no switchport
   ip address 10.255.255.4/31
!
interface Ethernet3
   description P2P_LINK_TO_DC1-LF03_Ethernet1
   no shutdown
   mtu 9214
   no switchport
   ip address 10.255.255.8/31
!
interface Ethernet4
   description P2P_LINK_TO_DC1-LF04_Ethernet1
   no shutdown
   mtu 9214
   no switchport
   ip address 10.255.255.12/31
!
interface Ethernet5
   description P2P_LINK_TO_DC1-LF05_Ethernet1
   no shutdown
   mtu 9214
   no switchport
   ip address 10.255.255.16/31
!
interface Ethernet6
   description P2P_LINK_TO_DC1-LF06_Ethernet1
   no shutdown
   mtu 9214
   no switchport
   ip address 10.255.255.20/31
!
interface Ethernet7
   description P2P_LINK_TO_DC1-LF07_Ethernet1
   no shutdown
   mtu 9214
   no switchport
   ip address 10.255.255.24/31
!
interface Ethernet8
   description P2P_LINK_TO_DC1-LF08_Ethernet1
   no shutdown
   mtu 9214
   no switchport
   ip address 10.255.255.28/31
!
interface Ethernet9
   description P2P_LINK_TO_DC1-LF09_Ethernet1
   no shutdown
   mtu 9214
   no switchport
   ip address 10.255.255.32/31
!
interface Ethernet10
   description P2P_LINK_TO_DC1-LF10_Ethernet1
   no shutdown
   mtu 9214
   no switchport
   ip address 10.255.255.36/31
!
interface Ethernet11
   description P2P_LINK_TO_DC1-LF11_Ethernet1
   no shutdown
   mtu 9214
   no switchport
   ip address 10.255.255.40/31
!
interface Ethernet12
   description P2P_LINK_TO_DC1-LF12_Ethernet1
   no shutdown
   mtu 9214
   no switchport
   ip address 10.255.255.44/31
!
interface Ethernet13
   description P2P_LINK_TO_DC1-LF13_Ethernet1
   no shutdown
   mtu 9214
   no switchport
   ip address 10.255.255.48/31
!
interface Ethernet14
   description P2P_LINK_TO_DC1-LF14_Ethernet1
   no shutdown
   mtu 9214
   no switchport
   ip address 10.255.255.52/31
```

### Loopback Interfaces

#### Loopback Interfaces Summary

##### IPv4

| Interface | Description | VRF | IP Address |
| --------- | ----------- | --- | ---------- |
| Loopback0 | EVPN_Overlay_Peering | default | 10.255.0.1/32 |

##### IPv6

| Interface | Description | VRF | IPv6 Address |
| --------- | ----------- | --- | ------------ |
| Loopback0 | EVPN_Overlay_Peering | default | - |

#### Loopback Interfaces Device Configuration

```eos
!
interface Loopback0
   description EVPN_Overlay_Peering
   no shutdown
   ip address 10.255.0.1/32
```

## Routing

### Service Routing Protocols Model

Multi agent routing protocol model enabled

```eos
!
service routing protocols model multi-agent
```

### IP Routing

#### IP Routing Summary

| VRF | Routing Enabled |
| --- | --------------- |
| default | True |
| MGMT | False |

#### IP Routing Device Configuration

```eos
!
ip routing
no ip routing vrf MGMT
```

### IPv6 Routing

#### IPv6 Routing Summary

| VRF | Routing Enabled |
| --- | --------------- |
| default | False |
| MGMT | false |

### Static Routes

#### Static Routes Summary

| VRF | Destination Prefix | Next Hop IP | Exit interface | Administrative Distance | Tag | Route Name | Metric |
| --- | ------------------ | ----------- | -------------- | ----------------------- | --- | ---------- | ------ |
| MGMT | 0.0.0.0/0 | 172.16.1.1 | - | 1 | - | - | - |

#### Static Routes Device Configuration

```eos
!
ip route vrf MGMT 0.0.0.0/0 172.16.1.1
```

### Router BGP

ASN Notation: asplain

#### Router BGP Summary

| BGP AS | Router ID |
| ------ | --------- |
| 65100 | 10.255.0.1 |

| BGP Tuning |
| ---------- |
| no bgp default ipv4-unicast |
| maximum-paths 4 ecmp 4 |

#### Router BGP Peer Groups

##### EVPN-OVERLAY-PEERS

| Settings | Value |
| -------- | ----- |
| Address Family | evpn |
| Next-hop unchanged | True |
| Source | Loopback0 |
| BFD | True |
| Ebgp multihop | 3 |
| Send community | all |
| Maximum routes | 0 (no limit) |

##### IPv4-UNDERLAY-PEERS

| Settings | Value |
| -------- | ----- |
| Address Family | ipv4 |
| Send community | all |
| Maximum routes | 12000 |

#### BGP Neighbors

| Neighbor | Remote AS | VRF | Shutdown | Send-community | Maximum-routes | Allowas-in | BFD | RIB Pre-Policy Retain | Route-Reflector Client | Passive | TTL Max Hops |
| -------- | --------- | --- | -------- | -------------- | -------------- | ---------- | --- | --------------------- | ---------------------- | ------- | ------------ |
| 10.255.0.3 | 65101 | default | - | Inherited from peer group EVPN-OVERLAY-PEERS | Inherited from peer group EVPN-OVERLAY-PEERS | - | Inherited from peer group EVPN-OVERLAY-PEERS | - | - | - | - |
| 10.255.0.4 | 65102 | default | - | Inherited from peer group EVPN-OVERLAY-PEERS | Inherited from peer group EVPN-OVERLAY-PEERS | - | Inherited from peer group EVPN-OVERLAY-PEERS | - | - | - | - |
| 10.255.0.5 | 65103 | default | - | Inherited from peer group EVPN-OVERLAY-PEERS | Inherited from peer group EVPN-OVERLAY-PEERS | - | Inherited from peer group EVPN-OVERLAY-PEERS | - | - | - | - |
| 10.255.0.6 | 65104 | default | - | Inherited from peer group EVPN-OVERLAY-PEERS | Inherited from peer group EVPN-OVERLAY-PEERS | - | Inherited from peer group EVPN-OVERLAY-PEERS | - | - | - | - |
| 10.255.0.7 | 65105 | default | - | Inherited from peer group EVPN-OVERLAY-PEERS | Inherited from peer group EVPN-OVERLAY-PEERS | - | Inherited from peer group EVPN-OVERLAY-PEERS | - | - | - | - |
| 10.255.0.8 | 65106 | default | - | Inherited from peer group EVPN-OVERLAY-PEERS | Inherited from peer group EVPN-OVERLAY-PEERS | - | Inherited from peer group EVPN-OVERLAY-PEERS | - | - | - | - |
| 10.255.0.9 | 65107 | default | - | Inherited from peer group EVPN-OVERLAY-PEERS | Inherited from peer group EVPN-OVERLAY-PEERS | - | Inherited from peer group EVPN-OVERLAY-PEERS | - | - | - | - |
| 10.255.0.10 | 65108 | default | - | Inherited from peer group EVPN-OVERLAY-PEERS | Inherited from peer group EVPN-OVERLAY-PEERS | - | Inherited from peer group EVPN-OVERLAY-PEERS | - | - | - | - |
| 10.255.0.11 | 65109 | default | - | Inherited from peer group EVPN-OVERLAY-PEERS | Inherited from peer group EVPN-OVERLAY-PEERS | - | Inherited from peer group EVPN-OVERLAY-PEERS | - | - | - | - |
| 10.255.0.12 | 65110 | default | - | Inherited from peer group EVPN-OVERLAY-PEERS | Inherited from peer group EVPN-OVERLAY-PEERS | - | Inherited from peer group EVPN-OVERLAY-PEERS | - | - | - | - |
| 10.255.0.13 | 65111 | default | - | Inherited from peer group EVPN-OVERLAY-PEERS | Inherited from peer group EVPN-OVERLAY-PEERS | - | Inherited from peer group EVPN-OVERLAY-PEERS | - | - | - | - |
| 10.255.0.14 | 65112 | default | - | Inherited from peer group EVPN-OVERLAY-PEERS | Inherited from peer group EVPN-OVERLAY-PEERS | - | Inherited from peer group EVPN-OVERLAY-PEERS | - | - | - | - |
| 10.255.0.15 | 65113 | default | - | Inherited from peer group EVPN-OVERLAY-PEERS | Inherited from peer group EVPN-OVERLAY-PEERS | - | Inherited from peer group EVPN-OVERLAY-PEERS | - | - | - | - |
| 10.255.0.16 | 65114 | default | - | Inherited from peer group EVPN-OVERLAY-PEERS | Inherited from peer group EVPN-OVERLAY-PEERS | - | Inherited from peer group EVPN-OVERLAY-PEERS | - | - | - | - |
| 10.255.255.1 | 65101 | default | - | Inherited from peer group IPv4-UNDERLAY-PEERS | Inherited from peer group IPv4-UNDERLAY-PEERS | - | - | - | - | - | - |
| 10.255.255.5 | 65102 | default | - | Inherited from peer group IPv4-UNDERLAY-PEERS | Inherited from peer group IPv4-UNDERLAY-PEERS | - | - | - | - | - | - |
| 10.255.255.9 | 65103 | default | - | Inherited from peer group IPv4-UNDERLAY-PEERS | Inherited from peer group IPv4-UNDERLAY-PEERS | - | - | - | - | - | - |
| 10.255.255.13 | 65104 | default | - | Inherited from peer group IPv4-UNDERLAY-PEERS | Inherited from peer group IPv4-UNDERLAY-PEERS | - | - | - | - | - | - |
| 10.255.255.17 | 65105 | default | - | Inherited from peer group IPv4-UNDERLAY-PEERS | Inherited from peer group IPv4-UNDERLAY-PEERS | - | - | - | - | - | - |
| 10.255.255.21 | 65106 | default | - | Inherited from peer group IPv4-UNDERLAY-PEERS | Inherited from peer group IPv4-UNDERLAY-PEERS | - | - | - | - | - | - |
| 10.255.255.25 | 65107 | default | - | Inherited from peer group IPv4-UNDERLAY-PEERS | Inherited from peer group IPv4-UNDERLAY-PEERS | - | - | - | - | - | - |
| 10.255.255.29 | 65108 | default | - | Inherited from peer group IPv4-UNDERLAY-PEERS | Inherited from peer group IPv4-UNDERLAY-PEERS | - | - | - | - | - | - |
| 10.255.255.33 | 65109 | default | - | Inherited from peer group IPv4-UNDERLAY-PEERS | Inherited from peer group IPv4-UNDERLAY-PEERS | - | - | - | - | - | - |
| 10.255.255.37 | 65110 | default | - | Inherited from peer group IPv4-UNDERLAY-PEERS | Inherited from peer group IPv4-UNDERLAY-PEERS | - | - | - | - | - | - |
| 10.255.255.41 | 65111 | default | - | Inherited from peer group IPv4-UNDERLAY-PEERS | Inherited from peer group IPv4-UNDERLAY-PEERS | - | - | - | - | - | - |
| 10.255.255.45 | 65112 | default | - | Inherited from peer group IPv4-UNDERLAY-PEERS | Inherited from peer group IPv4-UNDERLAY-PEERS | - | - | - | - | - | - |
| 10.255.255.49 | 65113 | default | - | Inherited from peer group IPv4-UNDERLAY-PEERS | Inherited from peer group IPv4-UNDERLAY-PEERS | - | - | - | - | - | - |
| 10.255.255.53 | 65114 | default | - | Inherited from peer group IPv4-UNDERLAY-PEERS | Inherited from peer group IPv4-UNDERLAY-PEERS | - | - | - | - | - | - |

#### Router BGP EVPN Address Family

##### EVPN Peer Groups

| Peer Group | Activate | Encapsulation |
| ---------- | -------- | ------------- |
| EVPN-OVERLAY-PEERS | True | default |

#### Router BGP Device Configuration

```eos
!
router bgp 65100
   router-id 10.255.0.1
   maximum-paths 4 ecmp 4
   no bgp default ipv4-unicast
   neighbor EVPN-OVERLAY-PEERS peer group
   neighbor EVPN-OVERLAY-PEERS next-hop-unchanged
   neighbor EVPN-OVERLAY-PEERS update-source Loopback0
   neighbor EVPN-OVERLAY-PEERS bfd
   neighbor EVPN-OVERLAY-PEERS ebgp-multihop 3
   neighbor EVPN-OVERLAY-PEERS password 7 <removed>
   neighbor EVPN-OVERLAY-PEERS send-community
   neighbor EVPN-OVERLAY-PEERS maximum-routes 0
   neighbor IPv4-UNDERLAY-PEERS peer group
   neighbor IPv4-UNDERLAY-PEERS password 7 <removed>
   neighbor IPv4-UNDERLAY-PEERS send-community
   neighbor IPv4-UNDERLAY-PEERS maximum-routes 12000
   neighbor 10.255.0.3 peer group EVPN-OVERLAY-PEERS
   neighbor 10.255.0.3 remote-as 65101
   neighbor 10.255.0.3 description dc1-lf01
   neighbor 10.255.0.4 peer group EVPN-OVERLAY-PEERS
   neighbor 10.255.0.4 remote-as 65102
   neighbor 10.255.0.4 description dc1-lf02
   neighbor 10.255.0.5 peer group EVPN-OVERLAY-PEERS
   neighbor 10.255.0.5 remote-as 65103
   neighbor 10.255.0.5 description dc1-lf03
   neighbor 10.255.0.6 peer group EVPN-OVERLAY-PEERS
   neighbor 10.255.0.6 remote-as 65104
   neighbor 10.255.0.6 description dc1-lf04
   neighbor 10.255.0.7 peer group EVPN-OVERLAY-PEERS
   neighbor 10.255.0.7 remote-as 65105
   neighbor 10.255.0.7 description dc1-lf05
   neighbor 10.255.0.8 peer group EVPN-OVERLAY-PEERS
   neighbor 10.255.0.8 remote-as 65106
   neighbor 10.255.0.8 description dc1-lf06
   neighbor 10.255.0.9 peer group EVPN-OVERLAY-PEERS
   neighbor 10.255.0.9 remote-as 65107
   neighbor 10.255.0.9 description dc1-lf07
   neighbor 10.255.0.10 peer group EVPN-OVERLAY-PEERS
   neighbor 10.255.0.10 remote-as 65108
   neighbor 10.255.0.10 description dc1-lf08
   neighbor 10.255.0.11 peer group EVPN-OVERLAY-PEERS
   neighbor 10.255.0.11 remote-as 65109
   neighbor 10.255.0.11 description dc1-lf09
   neighbor 10.255.0.12 peer group EVPN-OVERLAY-PEERS
   neighbor 10.255.0.12 remote-as 65110
   neighbor 10.255.0.12 description dc1-lf10
   neighbor 10.255.0.13 peer group EVPN-OVERLAY-PEERS
   neighbor 10.255.0.13 remote-as 65111
   neighbor 10.255.0.13 description dc1-lf11
   neighbor 10.255.0.14 peer group EVPN-OVERLAY-PEERS
   neighbor 10.255.0.14 remote-as 65112
   neighbor 10.255.0.14 description dc1-lf12
   neighbor 10.255.0.15 peer group EVPN-OVERLAY-PEERS
   neighbor 10.255.0.15 remote-as 65113
   neighbor 10.255.0.15 description dc1-lf13
   neighbor 10.255.0.16 peer group EVPN-OVERLAY-PEERS
   neighbor 10.255.0.16 remote-as 65114
   neighbor 10.255.0.16 description dc1-lf14
   neighbor 10.255.255.1 peer group IPv4-UNDERLAY-PEERS
   neighbor 10.255.255.1 remote-as 65101
   neighbor 10.255.255.1 description dc1-lf01_Ethernet1
   neighbor 10.255.255.5 peer group IPv4-UNDERLAY-PEERS
   neighbor 10.255.255.5 remote-as 65102
   neighbor 10.255.255.5 description dc1-lf02_Ethernet1
   neighbor 10.255.255.9 peer group IPv4-UNDERLAY-PEERS
   neighbor 10.255.255.9 remote-as 65103
   neighbor 10.255.255.9 description dc1-lf03_Ethernet1
   neighbor 10.255.255.13 peer group IPv4-UNDERLAY-PEERS
   neighbor 10.255.255.13 remote-as 65104
   neighbor 10.255.255.13 description dc1-lf04_Ethernet1
   neighbor 10.255.255.17 peer group IPv4-UNDERLAY-PEERS
   neighbor 10.255.255.17 remote-as 65105
   neighbor 10.255.255.17 description dc1-lf05_Ethernet1
   neighbor 10.255.255.21 peer group IPv4-UNDERLAY-PEERS
   neighbor 10.255.255.21 remote-as 65106
   neighbor 10.255.255.21 description dc1-lf06_Ethernet1
   neighbor 10.255.255.25 peer group IPv4-UNDERLAY-PEERS
   neighbor 10.255.255.25 remote-as 65107
   neighbor 10.255.255.25 description dc1-lf07_Ethernet1
   neighbor 10.255.255.29 peer group IPv4-UNDERLAY-PEERS
   neighbor 10.255.255.29 remote-as 65108
   neighbor 10.255.255.29 description dc1-lf08_Ethernet1
   neighbor 10.255.255.33 peer group IPv4-UNDERLAY-PEERS
   neighbor 10.255.255.33 remote-as 65109
   neighbor 10.255.255.33 description dc1-lf09_Ethernet1
   neighbor 10.255.255.37 peer group IPv4-UNDERLAY-PEERS
   neighbor 10.255.255.37 remote-as 65110
   neighbor 10.255.255.37 description dc1-lf10_Ethernet1
   neighbor 10.255.255.41 peer group IPv4-UNDERLAY-PEERS
   neighbor 10.255.255.41 remote-as 65111
   neighbor 10.255.255.41 description dc1-lf11_Ethernet1
   neighbor 10.255.255.45 peer group IPv4-UNDERLAY-PEERS
   neighbor 10.255.255.45 remote-as 65112
   neighbor 10.255.255.45 description dc1-lf12_Ethernet1
   neighbor 10.255.255.49 peer group IPv4-UNDERLAY-PEERS
   neighbor 10.255.255.49 remote-as 65113
   neighbor 10.255.255.49 description dc1-lf13_Ethernet1
   neighbor 10.255.255.53 peer group IPv4-UNDERLAY-PEERS
   neighbor 10.255.255.53 remote-as 65114
   neighbor 10.255.255.53 description dc1-lf14_Ethernet1
   redistribute connected route-map RM-CONN-2-BGP
   !
   address-family evpn
      neighbor EVPN-OVERLAY-PEERS activate
   !
   address-family ipv4
      no neighbor EVPN-OVERLAY-PEERS activate
      neighbor IPv4-UNDERLAY-PEERS activate
```

## BFD

### Router BFD

#### Router BFD Multihop Summary

| Interval | Minimum RX | Multiplier |
| -------- | ---------- | ---------- |
| 300 | 300 | 3 |

#### Router BFD Device Configuration

```eos
!
router bfd
   multihop interval 300 min-rx 300 multiplier 3
```

## Filters

### Prefix-lists

#### Prefix-lists Summary

##### PL-LOOPBACKS-EVPN-OVERLAY

| Sequence | Action |
| -------- | ------ |
| 10 | permit 10.255.0.0/27 eq 32 |

#### Prefix-lists Device Configuration

```eos
!
ip prefix-list PL-LOOPBACKS-EVPN-OVERLAY
   seq 10 permit 10.255.0.0/27 eq 32
```

### Route-maps

#### Route-maps Summary

##### RM-CONN-2-BGP

| Sequence | Type | Match | Set | Sub-Route-Map | Continue |
| -------- | ---- | ----- | --- | ------------- | -------- |
| 10 | permit | ip address prefix-list PL-LOOPBACKS-EVPN-OVERLAY | - | - | - |

#### Route-maps Device Configuration

```eos
!
route-map RM-CONN-2-BGP permit 10
   match ip address prefix-list PL-LOOPBACKS-EVPN-OVERLAY
```

## VRF Instances

### VRF Instances Summary

| VRF Name | IP Routing |
| -------- | ---------- |
| MGMT | disabled |

### VRF Instances Device Configuration

```eos
!
vrf instance MGMT
```

## EOS CLI Device Configuration

```eos
!
interface Management0
  no lldp receive
  no lldp transmit

```
