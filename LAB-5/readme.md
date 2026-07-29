# Day 5 - OSPF (Open Shortest Path First) Dynamic Routing Practical

## Overview

This lab demonstrates the implementation of OSPF (Open Shortest Path First), a Link-State Dynamic Routing Protocol, using Cisco Packet Tracer.

Unlike Static Routing, OSPF automatically discovers neighboring routers, exchanges routing information, calculates the best path using cost, and dynamically updates the routing table whenever network changes occur.

This practical was performed using three Cisco routers and two end devices to establish communication between two different LAN networks.

---

# Objective

- Understand the working of OSPF.
- Configure OSPF between three routers.
- Establish neighbor relationships.
- Learn route advertisement.
- Verify dynamically learned routes.
- Test end-to-end communication.

---

# Network Topology

```
PC1 -------- R1 -------- R2 -------- R3 -------- PC2
```

---

# Devices Used

- Cisco Packet Tracer
- 3 × Cisco 1941 Routers
- 2 × PCs
- Copper Straight Through Cable
- Copper Cross Over Cable (or Auto)

---

# IP Addressing Scheme

## Router 1

| Interface | IP Address | Subnet Mask |
|-----------|------------|-------------|
| G0/0 | 192.168.1.1 | 255.255.255.0 |
| G0/1 | 10.0.0.1 | 255.255.255.252 |

---

## Router 2

| Interface | IP Address | Subnet Mask |
|-----------|------------|-------------|
| G0/0 | 10.0.0.2 | 255.255.255.252 |
| G0/1 | 20.0.0.1 | 255.255.255.252 |

---

## Router 3

| Interface | IP Address | Subnet Mask |
|-----------|------------|-------------|
| G0/0 | 20.0.0.2 | 255.255.255.252 |
| G0/1 | 192.168.2.1 | 255.255.255.0 |

---

## End Devices

### PC1

- IP Address : 192.168.1.2
- Subnet Mask : 255.255.255.0
- Default Gateway : 192.168.1.1

### PC2

- IP Address : 192.168.2.2
- Subnet Mask : 255.255.255.0
- Default Gateway : 192.168.2.1

---

# Configuration Procedure

## Step 1

Configured IP addresses on all router interfaces.

---

## Step 2

Enabled all interfaces using

```
no shutdown
```

---

## Step 3

Verified interface status

```
show ip interface brief
```

All interfaces reached **UP/UP** state.

---

## Step 4

Verified direct connectivity using Ping.

- R1 → R2
- R2 → R3
- PC → Gateway

All direct connections were successful.

---

## Step 5

Configured OSPF.

```
router ospf 1
```

Created OSPF Process ID 1.

---

## Step 6

Enabled OSPF on required interfaces using Network Statements.

Example

```
network 192.168.1.0 0.0.0.255 area 0

network 10.0.0.0 0.0.0.3 area 0
```

The wildcard mask was used to identify the interfaces that should participate in OSPF.

---

## Step 7

Verified Neighbor Relationship

```
show ip ospf neighbor
```

Neighbor State

```
FULL
```

This indicates successful database synchronization between neighboring routers.

---

## Step 8

Verified Routing Table

```
show ip route
```

Observed:

- Connected Routes (C)
- Local Routes (L)
- OSPF Learned Routes (O)

Example

```
O 192.168.2.0/24
```

This confirms that Router 1 dynamically learned the remote LAN from Router 3.

---

## Step 9

Verified only OSPF Routes

```
show ip route ospf
```

Displayed only routes learned through OSPF.

---

## Step 10

Performed End-to-End Connectivity Test

```
PC1

↓

R1

↓

R2

↓

R3

↓

PC2
```

Ping from PC1 to PC2 was successful.

---

# OSPF Commands Used

```
router ospf 1

network x.x.x.x wildcard-mask area 0
```

---

# Verification Commands

```
show ip interface brief

show ip ospf neighbor

show ip route

show ip route ospf

show running-config
```

---

# Important Concepts Learned

- Dynamic Routing
- Link-State Routing Protocol
- OSPF Process ID
- Router ID
- Hello Packet
- Neighbor Discovery
- Area 0
- Wildcard Mask
- Route Advertisement
- OSPF Cost
- Administrative Distance
- Routing Table
- OSPF Neighbor States
- Dynamic Route Learning

---

# Advantages of OSPF

- Fast convergence
- Automatic route updates
- Scalable for large enterprise networks
- Supports VLSM and CIDR
- Loop-free routing
- Efficient path selection using Cost Metric

---

# Verification Results

| Test | Status |
|------|--------|
| Interface Status | Successful |
| Neighbor Formation | Successful |
| OSPF Route Learning | Successful |
| Routing Table Update | Successful |
| End-to-End Ping | Successful |

---

# Conclusion

This lab successfully demonstrated the implementation of OSPF Dynamic Routing using three Cisco routers. Neighbor relationships were established successfully, routing information was exchanged automatically, and dynamic routes were added to the routing table. Communication between two different LAN networks was successfully achieved without using Static Routing.