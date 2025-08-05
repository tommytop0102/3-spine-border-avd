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
| DC1_BORDER_LEAF1 | Ethernet1 | 172.31.10.121/31 | DC1_SPINE1 | Ethernet5 | 172.31.10.120/31 |
| DC1_BORDER_LEAF1 | Ethernet2 | 172.31.10.123/31 | DC1_SPINE2 | Ethernet5 | 172.31.10.122/31 |
| DC1_BORDER_LEAF1 | Ethernet3 | 172.31.10.125/31 | DC1_SPINE3 | Ethernet5 | 172.31.10.124/31 |
| DC1_BORDER_LEAF2 | Ethernet1 | 172.31.10.127/31 | DC1_SPINE1 | Ethernet6 | 172.31.10.126/31 |
| DC1_BORDER_LEAF2 | Ethernet2 | 172.31.10.129/31 | DC1_SPINE2 | Ethernet6 | 172.31.10.128/31 |
| DC1_BORDER_LEAF2 | Ethernet3 | 172.31.10.131/31 | DC1_SPINE3 | Ethernet6 | 172.31.10.130/31 |
| DC1_BORDER_LEAF3 | Ethernet1 | 172.31.10.133/31 | DC1_SPINE1 | Ethernet7 | 172.31.10.132/31 |
| DC1_BORDER_LEAF3 | Ethernet2 | 172.31.10.135/31 | DC1_SPINE2 | Ethernet7 | 172.31.10.134/31 |
| DC1_BORDER_LEAF3 | Ethernet3 | 172.31.10.137/31 | DC1_SPINE3 | Ethernet7 | 172.31.10.136/31 |
| DC1_LEAF1 | Ethernet1 | 172.31.10.181/31 | DC1_SPINE1 | Ethernet1 | 172.31.10.180/31 |
| DC1_LEAF1 | Ethernet2 | 172.31.10.183/31 | DC1_SPINE2 | Ethernet1 | 172.31.10.182/31 |
| DC1_LEAF1 | Ethernet3 | 172.31.10.185/31 | DC1_SPINE3 | Ethernet1 | 172.31.10.184/31 |
| DC1_LEAF2 | Ethernet1 | 172.31.10.187/31 | DC1_SPINE1 | Ethernet2 | 172.31.10.186/31 |
| DC1_LEAF2 | Ethernet2 | 172.31.10.189/31 | DC1_SPINE2 | Ethernet2 | 172.31.10.188/31 |
| DC1_LEAF2 | Ethernet3 | 172.31.10.191/31 | DC1_SPINE3 | Ethernet2 | 172.31.10.190/31 |
| DC1_LEAF3 | Ethernet1 | 172.31.10.193/31 | DC1_SPINE1 | Ethernet3 | 172.31.10.192/31 |
| DC1_LEAF3 | Ethernet2 | 172.31.10.195/31 | DC1_SPINE2 | Ethernet3 | 172.31.10.194/31 |
| DC1_LEAF3 | Ethernet3 | 172.31.10.197/31 | DC1_SPINE3 | Ethernet3 | 172.31.10.196/31 |
| DC1_LEAF4 | Ethernet1 | 172.31.10.199/31 | DC1_SPINE1 | Ethernet4 | 172.31.10.198/31 |
| DC1_LEAF4 | Ethernet2 | 172.31.10.201/31 | DC1_SPINE2 | Ethernet4 | 172.31.10.200/31 |
| DC1_LEAF4 | Ethernet3 | 172.31.10.203/31 | DC1_SPINE3 | Ethernet4 | 172.31.10.202/31 |
| DC2_BORDER_LEAF1 | Ethernet1 | 172.31.20.139/31 | DC2_SPINE1 | Ethernet5 | 172.31.20.138/31 |
| DC2_BORDER_LEAF1 | Ethernet2 | 172.31.20.141/31 | DC2_SPINE2 | Ethernet5 | 172.31.20.140/31 |
| DC2_BORDER_LEAF1 | Ethernet3 | 172.31.20.143/31 | DC2_SPINE3 | Ethernet5 | 172.31.20.142/31 |
| DC2_BORDER_LEAF2 | Ethernet1 | 172.31.20.145/31 | DC2_SPINE1 | Ethernet6 | 172.31.20.144/31 |
| DC2_BORDER_LEAF2 | Ethernet2 | 172.31.20.147/31 | DC2_SPINE2 | Ethernet6 | 172.31.20.146/31 |
| DC2_BORDER_LEAF2 | Ethernet3 | 172.31.20.149/31 | DC2_SPINE3 | Ethernet6 | 172.31.20.148/31 |
| DC2_BORDER_LEAF3 | Ethernet1 | 172.31.20.151/31 | DC2_SPINE1 | Ethernet7 | 172.31.20.150/31 |
| DC2_BORDER_LEAF3 | Ethernet2 | 172.31.20.153/31 | DC2_SPINE2 | Ethernet7 | 172.31.20.152/31 |
| DC2_BORDER_LEAF3 | Ethernet3 | 172.31.20.155/31 | DC2_SPINE3 | Ethernet7 | 172.31.20.154/31 |
| DC2_LEAF1 | Ethernet1 | 172.31.20.205/31 | DC2_SPINE1 | Ethernet1 | 172.31.20.204/31 |
| DC2_LEAF1 | Ethernet2 | 172.31.20.207/31 | DC2_SPINE2 | Ethernet1 | 172.31.20.206/31 |
| DC2_LEAF1 | Ethernet3 | 172.31.20.209/31 | DC2_SPINE3 | Ethernet1 | 172.31.20.208/31 |
| DC2_LEAF2 | Ethernet1 | 172.31.20.211/31 | DC2_SPINE1 | Ethernet2 | 172.31.20.210/31 |
| DC2_LEAF2 | Ethernet2 | 172.31.20.213/31 | DC2_SPINE2 | Ethernet2 | 172.31.20.212/31 |
| DC2_LEAF2 | Ethernet3 | 172.31.20.215/31 | DC2_SPINE3 | Ethernet2 | 172.31.20.214/31 |
| DC2_LEAF3 | Ethernet1 | 172.31.20.217/31 | DC2_SPINE1 | Ethernet3 | 172.31.20.216/31 |
| DC2_LEAF3 | Ethernet2 | 172.31.20.219/31 | DC2_SPINE2 | Ethernet3 | 172.31.20.218/31 |
| DC2_LEAF3 | Ethernet3 | 172.31.20.221/31 | DC2_SPINE3 | Ethernet3 | 172.31.20.220/31 |
| DC2_LEAF4 | Ethernet1 | 172.31.20.223/31 | DC2_SPINE1 | Ethernet4 | 172.31.20.222/31 |
| DC2_LEAF4 | Ethernet2 | 172.31.20.225/31 | DC2_SPINE2 | Ethernet4 | 172.31.20.224/31 |
| DC2_LEAF4 | Ethernet3 | 172.31.20.227/31 | DC2_SPINE3 | Ethernet4 | 172.31.20.226/31 |

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
| DC1 | DC1_BORDER_LEAF1 | 10.255.10.21/32 |
| DC1 | DC1_BORDER_LEAF2 | 10.255.10.22/32 |
| DC1 | DC1_BORDER_LEAF3 | 10.255.10.23/32 |
| DC1 | DC1_LEAF1 | 10.255.10.31/32 |
| DC1 | DC1_LEAF2 | 10.255.10.32/32 |
| DC1 | DC1_LEAF3 | 10.255.10.33/32 |
| DC1 | DC1_LEAF4 | 10.255.10.34/32 |
| DC1 | DC1_SPINE1 | 10.255.10.1/32 |
| DC1 | DC1_SPINE2 | 10.255.10.2/32 |
| DC1 | DC1_SPINE3 | 10.255.10.3/32 |
| DC2 | DC2_BORDER_LEAF1 | 10.255.20.24/32 |
| DC2 | DC2_BORDER_LEAF2 | 10.255.20.25/32 |
| DC2 | DC2_BORDER_LEAF3 | 10.255.20.26/32 |
| DC2 | DC2_LEAF1 | 10.255.20.35/32 |
| DC2 | DC2_LEAF2 | 10.255.20.36/32 |
| DC2 | DC2_LEAF3 | 10.255.20.37/32 |
| DC2 | DC2_LEAF4 | 10.255.20.38/32 |
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
| DC1 | DC1_BORDER_LEAF1 | 10.255.11.21/32 |
| DC1 | DC1_BORDER_LEAF2 | 10.255.11.22/32 |
| DC1 | DC1_BORDER_LEAF3 | 10.255.11.23/32 |
| DC1 | DC1_LEAF1 | 10.255.11.31/32 |
| DC1 | DC1_LEAF2 | 10.255.11.32/32 |
| DC1 | DC1_LEAF3 | 10.255.11.33/32 |
| DC1 | DC1_LEAF4 | 10.255.11.34/32 |
| DC2 | DC2_BORDER_LEAF1 | 10.255.21.24/32 |
| DC2 | DC2_BORDER_LEAF2 | 10.255.21.25/32 |
| DC2 | DC2_BORDER_LEAF3 | 10.255.21.26/32 |
| DC2 | DC2_LEAF1 | 10.255.21.35/32 |
| DC2 | DC2_LEAF2 | 10.255.21.36/32 |
| DC2 | DC2_LEAF3 | 10.255.21.37/32 |
| DC2 | DC2_LEAF4 | 10.255.21.38/32 |
