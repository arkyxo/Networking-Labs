
# Week 1 – Task 3: IOS Command Line, Interfaces and Recovery

Cisco Packet Tracer lab covering basic IOS configuration, SSH access, interface addressing, show commands, configuration saving, and password recovery.

## Lab Topology

- Cisco 1941 Router (R1)
- Cisco 2960 Switch (S1)
- 1 PC (PC0)

## IP Addressing

| Device | Interface | IP Address |
|---|---|---|
| R1 | G0/0 | 192.168.10.1 |
| S1 | VLAN 1 | 192.168.10.2 |
| PC0 | FastEthernet0 | 192.168.10.10 |

Subnet Mask: `255.255.255.0`

## Tasks Completed

- Configured router and switch hostnames, passwords, and banners.
- Assigned IP addresses to network interfaces.
- Configured SSH with local authentication and RSA keys.
- Successfully tested ping connectivity.
- Successfully accessed both devices through SSH.
- Executed `show running-config`, `show ip interface brief`, and `show version`.
- Saved and verified device configurations.
- Demonstrated the initial router password recovery process using configuration register `0x2142`.

## Verification Results

| Test | Result |
|---|---|
| PC to Router Ping | Successful |
| PC to Switch Ping | Successful after initial timeout |
| Router SSH | Successful |
| Switch SSH | Successful |
| Router G0/0 | Up/Up |
| Switch VLAN 1 | Up/Up |
| Configuration Register | Recovery boot demonstrated |

## Password Recovery

Configured the router to use `0x2142` on the next reload:

```bash
configure terminal
config-register 0x2142
end
reload
```

After rebooting, I skipped the initial configuration dialog and successfully reached privileged EXEC mode without the previous enable password.

*Note: The subsequent restoration of the saved configuration and password replacement were not captured.*

## Screenshots

### Router Configuration and SSH
![Router Configuration](screenshots/01-image(20261115-093905).png)
![Router SSH](screenshots/04-image(20261115-094238).png)

### Switch Configuration and SSH
![Switch Configuration](screenshots/05-image(20261115-094425).png)
![Switch SSH](screenshots/08-image(20261115-094556).png)

### Connectivity Tests
![Router Ping](screenshots/09-image(20261115-094642).png)
![Switch Ping](screenshots/11-image(20261115-094705).png)

### IOS Verification
![Router Interfaces](screenshots/15-image(20261115-094846).png)
![Switch VLAN](screenshots/22-image(20261115-095245).png)

### Password Recovery
![Configuration Register](screenshots/26-image(20261115-095441).png)
![Recovery Boot](screenshots/27-image(20261115-095525).png)

## What I Learned

I learned how to configure Cisco IOS devices, manage network interfaces, establish SSH connections, verify configurations, save device settings, and understand the router password recovery process.
