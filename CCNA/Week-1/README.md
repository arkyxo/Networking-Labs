# CCNA Week 1 – Task 1: Static Routing Configuration

## 1. Overview

This lab demonstrates the configuration of two Cisco routers connected through an inter-router network. Static routes were configured to enable communication between two separate LANs.

**Objectives:**
- Configure router interfaces with IPv4 addresses.
- Establish connectivity between two routers.
- Configure static routing.
- Verify end-to-end connectivity using ICMP ping tests.
- Inspect routing tables and interface status.

## 2. Network Topology

The network consists of:
- 2 Cisco 2911 routers (R1 and R2)
- 2 Cisco 2960 switches
- 4 end devices (PC0, PC1, PC2, PC3)

### IP Addressing Scheme

| Device | Interface | IP Address | Subnet Mask |
|---|---|---|---|
| R1 | G0/0 | 10.0.0.1 | 255.255.255.252 |
| R1 | G0/1 | 192.168.1.1 | 255.255.255.0 |
| R2 | G0/1 | 10.0.0.2 | 255.255.255.252 |
| R2 | G0/0 | 192.168.2.1 | 255.255.255.0 |
| PC0 | NIC | 192.168.1.10 | 255.255.255.0 |
| PC1 | NIC | 192.168.1.11 | 255.255.255.0 |
| PC2 | NIC | 192.168.2.10 | 255.255.255.0 |
| PC3 | NIC | 192.168.2.11 | 255.255.255.0 |

Default gateways:
- LAN 1: 192.168.1.1
- LAN 2: 192.168.2.1

## 3. Router Configuration

### Router 1 (R1)

```cisco
enable
configure terminal

interface gigabitEthernet 0/0
ip address 10.0.0.1 255.255.255.252
no shutdown
exit

interface gigabitEthernet 0/1
ip address 192.168.1.1 255.255.255.0
no shutdown
exit

ip route 192.168.2.0 255.255.255.0 10.0.0.2

end
write memory
```

### Router 2 (R2)

```cisco
enable
configure terminal

interface gigabitEthernet 0/0
ip address 192.168.2.1 255.255.255.0
no shutdown
exit

interface gigabitEthernet 0/1
ip address 10.0.0.2 255.255.255.252
no shutdown
exit

ip route 192.168.1.0 255.255.255.0 10.0.0.1

end
write memory
```

## 4. Verification and Testing

The following commands were used to verify the router configuration:

```cisco
show ip interface brief
show ip route
show running-config
```

Both routers showed active interfaces with their assigned IP addresses.

The routing tables confirmed the presence of:
- Directly connected networks.
- Local interface routes.
- Static routes pointing to the opposite LAN.

### Ping Testing

Connectivity was tested between devices on both LANs.

| Source | Destination | Result |
|---|---|---|
| PC0 | 192.168.1.11 | Successful |
| PC0 | 192.168.2.11 | Successful |
| PC0 | 192.168.2.10 | Successful |
| PC3 | 192.168.1.10 | Successful |
| PC3 | 192.168.1.11 | Successful |
| PC3 | 192.168.2.10 | Successful |

**Observation:** Initial ping attempts experienced packet loss while connectivity and address resolution were being established. Subsequent tests returned successful replies with 0% packet loss.

## 5. Conclusion

The static routing lab was successfully completed. Both routers were configured with the appropriate interface addresses and static routes, allowing devices from different LANs to communicate.

The successful ping tests confirmed end-to-end connectivity across the two networks.

**Tools Used:** Cisco Packet Tracer 9.0.0  
**Topics:** IPv4 Addressing, Static Routing, Router Configuration, ICMP, Network Troubleshooting.
