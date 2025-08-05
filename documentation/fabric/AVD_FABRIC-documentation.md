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
| AVD_FABRIC | super-spine | CORE1 | 192.168.4.61/24 | cEOS-LAB | Provisioned | - |
| AVD_FABRIC | super-spine | CORE2 | 192.168.4.62/24 | cEOS-LAB | Provisioned | - |
| AVD_FABRIC | super-spine | CORE3 | 192.168.4.63/24 | cEOS-LAB | Provisioned | - |
| DC1 | l3leaf | DC1_BORDER_LEAF1 | 192.168.4.21/24 | cEOS-LAB | Provisioned | - |
| DC1 | l3leaf | DC1_BORDER_LEAF2 | 192.168.4.22/24 | cEOS-LAB | Provisioned | - |
| DC1 | l3leaf | DC1_BORDER_LEAF3 | 192.168.4.23/24 | cEOS-LAB | Provisioned | - |
| DC1 | l3leaf | DC1_LEAF1 | 192.168.4.31/24 | cEOS-LAB | Provisioned | - |
| DC1 | l3leaf | DC1_LEAF2 | 192.168.4.32/24 | cEOS-LAB | Provisioned | - |
| DC1 | l3leaf | DC1_LEAF3 | 192.168.4.33/24 | cEOS-LAB | Provisioned | - |
| DC1 | l3leaf | DC1_LEAF4 | 192.168.4.34/24 | cEOS-LAB | Provisioned | - |
| DC1 | spine | DC1_SPINE1 | 192.168.4.11/24 | cEOS-LAB | Provisioned | - |
| DC1 | spine | DC1_SPINE2 | 192.168.4.12/24 | cEOS-LAB | Provisioned | - |
| DC1 | spine | DC1_SPINE3 | 192.168.4.13/24 | cEOS-LAB | Provisioned | - |
| DC2 | l3leaf | DC2_BORDER_LEAF1 | 192.168.4.121/24 | cEOS-LAB | Provisioned | - |
| DC2 | l3leaf | DC2_BORDER_LEAF2 | 192.168.4.122/24 | cEOS-LAB | Provisioned | - |
| DC2 | l3leaf | DC2_BORDER_LEAF3 | 192.168.4.123/24 | cEOS-LAB | Provisioned | - |
| DC2 | l3leaf | DC2_LEAF1 | 192.168.4.131/24 | cEOS-LAB | Provisioned | - |
| DC2 | l3leaf | DC2_LEAF2 | 192.168.4.132/24 | cEOS-LAB | Provisioned | - |
| DC2 | l3leaf | DC2_LEAF3 | 192.168.4.133/24 | cEOS-LAB | Provisioned | - |
| DC2 | l3leaf | DC2_LEAF4 | 192.168.4.134/24 | cEOS-LAB | Provisioned | - |
| DC2 | spine | DC2_SPINE1 | 192.168.4.111/24 | cEOS-LAB | Provisioned | - |
| DC2 | spine | DC2_SPINE2 | 192.168.4.112/24 | cEOS-LAB | Provisioned | - |
| DC2 | spine | DC2_SPINE3 | 192.168.4.113/24 | cEOS-LAB | Provisioned | - |

> Provision status is based on Ansible inventory declaration and do not represent real status from CloudVision.

### Fabric Switches with inband Management IP

| POD | Type | Node | Management IP | Inband Interface |
| --- | ---- | ---- | ------------- | ---------------- |

## Fabric Topology

| Type | Node | Node Interface | Peer Type | Peer Node | Peer Interface |
| ---- | ---- | -------------- | --------- | ----------| -------------- |
| super-spine | CORE1 | Ethernet1 | l3leaf | DC1_BORDER_LEAF1 | Ethernet4 |
| super-spine | CORE1 | Ethernet2 | l3leaf | DC1_BORDER_LEAF2 | Ethernet4 |
| super-spine | CORE1 | Ethernet3 | l3leaf | DC1_BORDER_LEAF3 | Ethernet4 |
| super-spine | CORE1 | Ethernet4 | l3leaf | DC2_BORDER_LEAF1 | Ethernet4 |
| super-spine | CORE1 | Ethernet5 | l3leaf | DC2_BORDER_LEAF2 | Ethernet4 |
| super-spine | CORE1 | Ethernet6 | l3leaf | DC2_BORDER_LEAF3 | Ethernet4 |
| super-spine | CORE2 | Ethernet1 | l3leaf | DC1_BORDER_LEAF1 | Ethernet5 |
| super-spine | CORE2 | Ethernet2 | l3leaf | DC1_BORDER_LEAF2 | Ethernet5 |
| super-spine | CORE2 | Ethernet3 | l3leaf | DC1_BORDER_LEAF3 | Ethernet5 |
| super-spine | CORE2 | Ethernet4 | l3leaf | DC2_BORDER_LEAF1 | Ethernet5 |
| super-spine | CORE2 | Ethernet5 | l3leaf | DC2_BORDER_LEAF2 | Ethernet5 |
| super-spine | CORE2 | Ethernet6 | l3leaf | DC2_BORDER_LEAF3 | Ethernet5 |
| super-spine | CORE3 | Ethernet1 | l3leaf | DC1_BORDER_LEAF1 | Ethernet6 |
| super-spine | CORE3 | Ethernet2 | l3leaf | DC1_BORDER_LEAF2 | Ethernet6 |
| super-spine | CORE3 | Ethernet3 | l3leaf | DC1_BORDER_LEAF3 | Ethernet6 |
| super-spine | CORE3 | Ethernet4 | l3leaf | DC2_BORDER_LEAF1 | Ethernet6 |
| super-spine | CORE3 | Ethernet5 | l3leaf | DC2_BORDER_LEAF2 | Ethernet6 |
| super-spine | CORE3 | Ethernet6 | l3leaf | DC2_BORDER_LEAF3 | Ethernet6 |
| l3leaf | DC1_BORDER_LEAF1 | Ethernet1 | spine | DC1_SPINE1 | Ethernet5 |
| l3leaf | DC1_BORDER_LEAF1 | Ethernet2 | spine | DC1_SPINE2 | Ethernet5 |
| l3leaf | DC1_BORDER_LEAF1 | Ethernet3 | spine | DC1_SPINE3 | Ethernet5 |
| l3leaf | DC1_BORDER_LEAF2 | Ethernet1 | spine | DC1_SPINE1 | Ethernet6 |
| l3leaf | DC1_BORDER_LEAF2 | Ethernet2 | spine | DC1_SPINE2 | Ethernet6 |
| l3leaf | DC1_BORDER_LEAF2 | Ethernet3 | spine | DC1_SPINE3 | Ethernet6 |
| l3leaf | DC1_BORDER_LEAF3 | Ethernet1 | spine | DC1_SPINE1 | Ethernet7 |
| l3leaf | DC1_BORDER_LEAF3 | Ethernet2 | spine | DC1_SPINE2 | Ethernet7 |
| l3leaf | DC1_BORDER_LEAF3 | Ethernet3 | spine | DC1_SPINE3 | Ethernet7 |
| l3leaf | DC1_LEAF1 | Ethernet1 | spine | DC1_SPINE1 | Ethernet1 |
| l3leaf | DC1_LEAF1 | Ethernet2 | spine | DC1_SPINE2 | Ethernet1 |
| l3leaf | DC1_LEAF1 | Ethernet3 | spine | DC1_SPINE3 | Ethernet1 |
| l3leaf | DC1_LEAF2 | Ethernet1 | spine | DC1_SPINE1 | Ethernet2 |
| l3leaf | DC1_LEAF2 | Ethernet2 | spine | DC1_SPINE2 | Ethernet2 |
| l3leaf | DC1_LEAF2 | Ethernet3 | spine | DC1_SPINE3 | Ethernet2 |
| l3leaf | DC1_LEAF3 | Ethernet1 | spine | DC1_SPINE1 | Ethernet3 |
| l3leaf | DC1_LEAF3 | Ethernet2 | spine | DC1_SPINE2 | Ethernet3 |
| l3leaf | DC1_LEAF3 | Ethernet3 | spine | DC1_SPINE3 | Ethernet3 |
| l3leaf | DC1_LEAF4 | Ethernet1 | spine | DC1_SPINE1 | Ethernet4 |
| l3leaf | DC1_LEAF4 | Ethernet2 | spine | DC1_SPINE2 | Ethernet4 |
| l3leaf | DC1_LEAF4 | Ethernet3 | spine | DC1_SPINE3 | Ethernet4 |
| l3leaf | DC2_BORDER_LEAF1 | Ethernet1 | spine | DC2_SPINE1 | Ethernet5 |
| l3leaf | DC2_BORDER_LEAF1 | Ethernet2 | spine | DC2_SPINE2 | Ethernet5 |
| l3leaf | DC2_BORDER_LEAF1 | Ethernet3 | spine | DC2_SPINE3 | Ethernet5 |
| l3leaf | DC2_BORDER_LEAF2 | Ethernet1 | spine | DC2_SPINE1 | Ethernet6 |
| l3leaf | DC2_BORDER_LEAF2 | Ethernet2 | spine | DC2_SPINE2 | Ethernet6 |
| l3leaf | DC2_BORDER_LEAF2 | Ethernet3 | spine | DC2_SPINE3 | Ethernet6 |
| l3leaf | DC2_BORDER_LEAF3 | Ethernet1 | spine | DC2_SPINE1 | Ethernet7 |
| l3leaf | DC2_BORDER_LEAF3 | Ethernet2 | spine | DC2_SPINE2 | Ethernet7 |
| l3leaf | DC2_BORDER_LEAF3 | Ethernet3 | spine | DC2_SPINE3 | Ethernet7 |
| l3leaf | DC2_LEAF1 | Ethernet1 | spine | DC2_SPINE1 | Ethernet1 |
| l3leaf | DC2_LEAF1 | Ethernet2 | spine | DC2_SPINE2 | Ethernet1 |
| l3leaf | DC2_LEAF1 | Ethernet3 | spine | DC2_SPINE3 | Ethernet1 |
| l3leaf | DC2_LEAF2 | Ethernet1 | spine | DC2_SPINE1 | Ethernet2 |
| l3leaf | DC2_LEAF2 | Ethernet2 | spine | DC2_SPINE2 | Ethernet2 |
| l3leaf | DC2_LEAF2 | Ethernet3 | spine | DC2_SPINE3 | Ethernet2 |
| l3leaf | DC2_LEAF3 | Ethernet1 | spine | DC2_SPINE1 | Ethernet3 |
| l3leaf | DC2_LEAF3 | Ethernet2 | spine | DC2_SPINE2 | Ethernet3 |
| l3leaf | DC2_LEAF3 | Ethernet3 | spine | DC2_SPINE3 | Ethernet3 |
| l3leaf | DC2_LEAF4 | Ethernet1 | spine | DC2_SPINE1 | Ethernet4 |
| l3leaf | DC2_LEAF4 | Ethernet2 | spine | DC2_SPINE2 | Ethernet4 |
| l3leaf | DC2_LEAF4 | Ethernet3 | spine | DC2_SPINE3 | Ethernet4 |

## Fabric IP Allocation

### Fabric Point-To-Point Links

| Uplink IPv4 Pool | Available Addresses | Assigned addresses | Assigned Address % |
| ---------------- | ------------------- | ------------------ | ------------------ |
| 172.31.10.0/24 | 256 | 42 | 16.41 % |
| 172.31.20.0/24 | 256 | 42 | 16.41 % |

### Point-To-Point Links Node Allocation

| Node | Node Interface | Node IP Address | Peer Node | Peer Interface | Peer IP Address |
| ---- | -------------- | --------------- | --------- | -------------- | --------------- |
| CORE1 | Ethernet1 | 172.16.30.61/31 | DC1_BORDER_LEAF1 | Ethernet4 | 172.16.30.60/31 |
| CORE1 | Ethernet2 | 172.16.30.67/31 | DC1_BORDER_LEAF2 | Ethernet4 | 172.16.30.66/31 |
| CORE1 | Ethernet3 | 172.16.30.73/31 | DC1_BORDER_LEAF3 | Ethernet4 | 172.16.30.72/31 |
| CORE1 | Ethernet4 | 172.16.30.81/31 | DC2_BORDER_LEAF1 | Ethernet4 | 172.16.30.80/31 |
| CORE1 | Ethernet5 | 172.16.30.87/31 | DC2_BORDER_LEAF2 | Ethernet4 | 172.16.30.86/31 |
| CORE1 | Ethernet6 | 172.16.30.93/31 | DC2_BORDER_LEAF3 | Ethernet4 | 172.16.30.92/31 |
| CORE2 | Ethernet1 | 172.16.30.63/31 | DC1_BORDER_LEAF1 | Ethernet5 | 172.16.30.62/31 |
| CORE2 | Ethernet2 | 172.16.30.69/31 | DC1_BORDER_LEAF2 | Ethernet5 | 172.16.30.68/31 |
| CORE2 | Ethernet3 | 172.16.30.75/31 | DC1_BORDER_LEAF3 | Ethernet5 | 172.16.30.74/31 |
| CORE2 | Ethernet4 | 172.16.30.83/31 | DC2_BORDER_LEAF1 | Ethernet5 | 172.16.30.82/31 |
| CORE2 | Ethernet5 | 172.16.30.89/31 | DC2_BORDER_LEAF2 | Ethernet5 | 172.16.30.88/31 |
| CORE2 | Ethernet6 | 172.16.30.95/31 | DC2_BORDER_LEAF3 | Ethernet5 | 172.16.30.94/31 |
| CORE3 | Ethernet1 | 172.16.30.65/31 | DC1_BORDER_LEAF1 | Ethernet6 | 172.16.30.64/31 |
| CORE3 | Ethernet2 | 172.16.30.71/31 | DC1_BORDER_LEAF2 | Ethernet6 | 172.16.30.70/31 |
| CORE3 | Ethernet3 | 172.16.30.77/31 | DC1_BORDER_LEAF3 | Ethernet6 | 172.16.30.76/31 |
| CORE3 | Ethernet4 | 172.16.30.85/31 | DC2_BORDER_LEAF1 | Ethernet6 | 172.16.30.84/31 |
| CORE3 | Ethernet5 | 172.16.30.91/31 | DC2_BORDER_LEAF2 | Ethernet6 | 172.16.30.90/31 |
| CORE3 | Ethernet6 | 172.16.30.97/31 | DC2_BORDER_LEAF3 | Ethernet6 | 172.16.30.96/31 |
| DC1_BORDER_LEAF1 | Ethernet1 | 172.31.10.61/31 | DC1_SPINE1 | Ethernet5 | 172.31.10.60/31 |
| DC1_BORDER_LEAF1 | Ethernet2 | 172.31.10.63/31 | DC1_SPINE2 | Ethernet5 | 172.31.10.62/31 |
| DC1_BORDER_LEAF1 | Ethernet3 | 172.31.10.65/31 | DC1_SPINE3 | Ethernet5 | 172.31.10.64/31 |
| DC1_BORDER_LEAF2 | Ethernet1 | 172.31.10.67/31 | DC1_SPINE1 | Ethernet6 | 172.31.10.66/31 |
| DC1_BORDER_LEAF2 | Ethernet2 | 172.31.10.69/31 | DC1_SPINE2 | Ethernet6 | 172.31.10.68/31 |
| DC1_BORDER_LEAF2 | Ethernet3 | 172.31.10.71/31 | DC1_SPINE3 | Ethernet6 | 172.31.10.70/31 |
| DC1_BORDER_LEAF3 | Ethernet1 | 172.31.10.73/31 | DC1_SPINE1 | Ethernet7 | 172.31.10.72/31 |
| DC1_BORDER_LEAF3 | Ethernet2 | 172.31.10.75/31 | DC1_SPINE2 | Ethernet7 | 172.31.10.74/31 |
| DC1_BORDER_LEAF3 | Ethernet3 | 172.31.10.77/31 | DC1_SPINE3 | Ethernet7 | 172.31.10.76/31 |
| DC1_LEAF1 | Ethernet1 | 172.31.10.79/31 | DC1_SPINE1 | Ethernet1 | 172.31.10.78/31 |
| DC1_LEAF1 | Ethernet2 | 172.31.10.81/31 | DC1_SPINE2 | Ethernet1 | 172.31.10.80/31 |
| DC1_LEAF1 | Ethernet3 | 172.31.10.83/31 | DC1_SPINE3 | Ethernet1 | 172.31.10.82/31 |
| DC1_LEAF2 | Ethernet1 | 172.31.10.85/31 | DC1_SPINE1 | Ethernet2 | 172.31.10.84/31 |
| DC1_LEAF2 | Ethernet2 | 172.31.10.87/31 | DC1_SPINE2 | Ethernet2 | 172.31.10.86/31 |
| DC1_LEAF2 | Ethernet3 | 172.31.10.89/31 | DC1_SPINE3 | Ethernet2 | 172.31.10.88/31 |
| DC1_LEAF3 | Ethernet1 | 172.31.10.91/31 | DC1_SPINE1 | Ethernet3 | 172.31.10.90/31 |
| DC1_LEAF3 | Ethernet2 | 172.31.10.93/31 | DC1_SPINE2 | Ethernet3 | 172.31.10.92/31 |
| DC1_LEAF3 | Ethernet3 | 172.31.10.95/31 | DC1_SPINE3 | Ethernet3 | 172.31.10.94/31 |
| DC1_LEAF4 | Ethernet1 | 172.31.10.97/31 | DC1_SPINE1 | Ethernet4 | 172.31.10.96/31 |
| DC1_LEAF4 | Ethernet2 | 172.31.10.99/31 | DC1_SPINE2 | Ethernet4 | 172.31.10.98/31 |
| DC1_LEAF4 | Ethernet3 | 172.31.10.101/31 | DC1_SPINE3 | Ethernet4 | 172.31.10.100/31 |
| DC2_BORDER_LEAF1 | Ethernet1 | 172.31.20.121/31 | DC2_SPINE1 | Ethernet5 | 172.31.20.120/31 |
| DC2_BORDER_LEAF1 | Ethernet2 | 172.31.20.123/31 | DC2_SPINE2 | Ethernet5 | 172.31.20.122/31 |
| DC2_BORDER_LEAF1 | Ethernet3 | 172.31.20.125/31 | DC2_SPINE3 | Ethernet5 | 172.31.20.124/31 |
| DC2_BORDER_LEAF2 | Ethernet1 | 172.31.20.127/31 | DC2_SPINE1 | Ethernet6 | 172.31.20.126/31 |
| DC2_BORDER_LEAF2 | Ethernet2 | 172.31.20.129/31 | DC2_SPINE2 | Ethernet6 | 172.31.20.128/31 |
| DC2_BORDER_LEAF2 | Ethernet3 | 172.31.20.131/31 | DC2_SPINE3 | Ethernet6 | 172.31.20.130/31 |
| DC2_BORDER_LEAF3 | Ethernet1 | 172.31.20.133/31 | DC2_SPINE1 | Ethernet7 | 172.31.20.132/31 |
| DC2_BORDER_LEAF3 | Ethernet2 | 172.31.20.135/31 | DC2_SPINE2 | Ethernet7 | 172.31.20.134/31 |
| DC2_BORDER_LEAF3 | Ethernet3 | 172.31.20.137/31 | DC2_SPINE3 | Ethernet7 | 172.31.20.136/31 |
| DC2_LEAF1 | Ethernet1 | 172.31.20.139/31 | DC2_SPINE1 | Ethernet1 | 172.31.20.138/31 |
| DC2_LEAF1 | Ethernet2 | 172.31.20.141/31 | DC2_SPINE2 | Ethernet1 | 172.31.20.140/31 |
| DC2_LEAF1 | Ethernet3 | 172.31.20.143/31 | DC2_SPINE3 | Ethernet1 | 172.31.20.142/31 |
| DC2_LEAF2 | Ethernet1 | 172.31.20.145/31 | DC2_SPINE1 | Ethernet2 | 172.31.20.144/31 |
| DC2_LEAF2 | Ethernet2 | 172.31.20.147/31 | DC2_SPINE2 | Ethernet2 | 172.31.20.146/31 |
| DC2_LEAF2 | Ethernet3 | 172.31.20.149/31 | DC2_SPINE3 | Ethernet2 | 172.31.20.148/31 |
| DC2_LEAF3 | Ethernet1 | 172.31.20.151/31 | DC2_SPINE1 | Ethernet3 | 172.31.20.150/31 |
| DC2_LEAF3 | Ethernet2 | 172.31.20.153/31 | DC2_SPINE2 | Ethernet3 | 172.31.20.152/31 |
| DC2_LEAF3 | Ethernet3 | 172.31.20.155/31 | DC2_SPINE3 | Ethernet3 | 172.31.20.154/31 |
| DC2_LEAF4 | Ethernet1 | 172.31.20.157/31 | DC2_SPINE1 | Ethernet4 | 172.31.20.156/31 |
| DC2_LEAF4 | Ethernet2 | 172.31.20.159/31 | DC2_SPINE2 | Ethernet4 | 172.31.20.158/31 |
| DC2_LEAF4 | Ethernet3 | 172.31.20.161/31 | DC2_SPINE3 | Ethernet4 | 172.31.20.160/31 |

### Loopback Interfaces (BGP EVPN Peering)

| Loopback Pool | Available Addresses | Assigned addresses | Assigned Address % |
| ------------- | ------------------- | ------------------ | ------------------ |
| 10.255.10.0/24 | 256 | 10 | 3.91 % |
| 10.255.20.0/24 | 256 | 10 | 3.91 % |
| 10.255.30.0/24 | 256 | 3 | 1.18 % |

### Loopback0 Interfaces Node Allocation

| POD | Node | Loopback0 |
| --- | ---- | --------- |
| AVD_FABRIC | CORE1 | 10.255.30.61/32 |
| AVD_FABRIC | CORE2 | 10.255.30.62/32 |
| AVD_FABRIC | CORE3 | 10.255.30.63/32 |
| DC1 | DC1_BORDER_LEAF1 | 10.255.10.11/32 |
| DC1 | DC1_BORDER_LEAF2 | 10.255.10.12/32 |
| DC1 | DC1_BORDER_LEAF3 | 10.255.10.13/32 |
| DC1 | DC1_LEAF1 | 10.255.10.14/32 |
| DC1 | DC1_LEAF2 | 10.255.10.15/32 |
| DC1 | DC1_LEAF3 | 10.255.10.16/32 |
| DC1 | DC1_LEAF4 | 10.255.10.17/32 |
| DC1 | DC1_SPINE1 | 10.255.10.1/32 |
| DC1 | DC1_SPINE2 | 10.255.10.2/32 |
| DC1 | DC1_SPINE3 | 10.255.10.3/32 |
| DC2 | DC2_BORDER_LEAF1 | 10.255.20.21/32 |
| DC2 | DC2_BORDER_LEAF2 | 10.255.20.22/32 |
| DC2 | DC2_BORDER_LEAF3 | 10.255.20.23/32 |
| DC2 | DC2_LEAF1 | 10.255.20.24/32 |
| DC2 | DC2_LEAF2 | 10.255.20.25/32 |
| DC2 | DC2_LEAF3 | 10.255.20.26/32 |
| DC2 | DC2_LEAF4 | 10.255.20.27/32 |
| DC2 | DC2_SPINE1 | 10.255.20.4/32 |
| DC2 | DC2_SPINE2 | 10.255.20.5/32 |
| DC2 | DC2_SPINE3 | 10.255.20.6/32 |

### VTEP Loopback VXLAN Tunnel Source Interfaces (VTEPs Only)

| VTEP Loopback Pool | Available Addresses | Assigned addresses | Assigned Address % |
| --------------------- | ------------------- | ------------------ | ------------------ |
| 10.255.11.0/24 | 256 | 7 | 2.74 % |
| 10.255.21.0/24 | 256 | 7 | 2.74 % |

### VTEP Loopback Node allocation

| POD | Node | Loopback1 |
| --- | ---- | --------- |
| DC1 | DC1_BORDER_LEAF1 | 10.255.11.11/32 |
| DC1 | DC1_BORDER_LEAF2 | 10.255.11.12/32 |
| DC1 | DC1_BORDER_LEAF3 | 10.255.11.13/32 |
| DC1 | DC1_LEAF1 | 10.255.11.14/32 |
| DC1 | DC1_LEAF2 | 10.255.11.15/32 |
| DC1 | DC1_LEAF3 | 10.255.11.16/32 |
| DC1 | DC1_LEAF4 | 10.255.11.17/32 |
| DC2 | DC2_BORDER_LEAF1 | 10.255.21.21/32 |
| DC2 | DC2_BORDER_LEAF2 | 10.255.21.22/32 |
| DC2 | DC2_BORDER_LEAF3 | 10.255.21.23/32 |
| DC2 | DC2_LEAF1 | 10.255.21.24/32 |
| DC2 | DC2_LEAF2 | 10.255.21.25/32 |
| DC2 | DC2_LEAF3 | 10.255.21.26/32 |
| DC2 | DC2_LEAF4 | 10.255.21.27/32 |
