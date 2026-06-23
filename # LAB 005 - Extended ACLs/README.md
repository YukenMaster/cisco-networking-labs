# LAB 005 - Extended ACLs

## Objective

Configure an Extended Access Control List (ACL) to block HTTP traffic from the Guest network to the Web Server while still allowing other network communications.

---

## Topology

Admin PC ----- Switch0 ----- Router 2911 ----- Switch1 ----- Guest PC
                     |
                 Web Server

### Network Diagram

![Topology](topology.png)

---

## IP Addressing

### Admin PC

| Parameter | Value |
|------------|------------|
| IP Address | 192.168.10.10 |
| Subnet Mask | 255.255.255.0 |
| Default Gateway | 192.168.10.1 |

### Web Server

| Parameter | Value |
|------------|------------|
| IP Address | 192.168.10.100 |
| Subnet Mask | 255.255.255.0 |
| Default Gateway | 192.168.10.1 |

### Guest PC

| Parameter | Value |
|------------|------------|
| IP Address | 192.168.20.10 |
| Subnet Mask | 255.255.255.0 |
| Default Gateway | 192.168.20.1 |

### Router

| Interface | IP Address |
|------------|------------|
| G0/0 | 192.168.10.1 |
| G0/1 | 192.168.20.1 |

### Verification

![IP Addressing](ip-addressing.png)

---

## Router Interface Configuration

Router interfaces were configured to provide Layer 3 connectivity between both networks.

### Verification

![Router Interface Configuration](router-interface-configuration.png)

---

## Web Server Configuration

The HTTP service was enabled on the Packet Tracer server.

### Verification

![Server HTTP Enabled](server-http-enabled.png)

---

## Connectivity Test Before ACL

The Guest PC successfully reached the Web Server before any filtering was applied.

### Ping Test

![Connectivity Before ACL](http-connectivity-before-acl.png)

### HTTP Access

![Web Access Before ACL](web-server-access-before-acl.png)

### Result

- Guest PC successfully reached the Web Server
- HTTP service was accessible
- Routing operated correctly

---

## Extended ACL Configuration

An Extended ACL was created to deny HTTP traffic originating from the Guest network while permitting all other traffic.

```cisco
access-list 101 deny tcp 192.168.20.0 0.0.0.255 host 192.168.10.100 eq 80
access-list 101 permit ip any any

interface GigabitEthernet0/1
 ip access-group 101 in
```

### Verification

![Extended ACL Configuration](extended-acl-configuration.png)

---

## ACL Validation

Connectivity tests were repeated after applying the ACL.

### Ping Test

The Guest PC was still able to reach the Web Server using ICMP.

![Ping After ACL](ping-after-acl.png)

### HTTP Test

The HTTP service became inaccessible.

![HTTP Blocked After ACL](http-blocked-after-acl.png)

---

## Results

- Guest PC could still ping the Web Server
- HTTP traffic was successfully blocked
- ACL filtered only TCP port 80 traffic
- Other protocols remained operational
- Extended ACL behavior was validated

---

## Security Concepts

This laboratory demonstrates:

- Extended Access Control Lists (ACLs)
- Protocol-based filtering
- Port-based filtering
- Traffic control
- Cisco IOS security features
- Layer 3 traffic filtering
- Network segmentation
- Principle of least privilege

---

## Skills Practiced

- Cisco IOS
- Extended ACL Configuration
- Router Configuration
- Packet Filtering
- HTTP Traffic Control
- Layer 3 Routing
- Network Security
- Connectivity Testing
- Troubleshooting
- Cisco Packet Tracer

---

## Conclusion

An Extended ACL was successfully implemented and validated. The laboratory demonstrated how Extended ACLs provide granular traffic filtering by allowing control based on protocol type, source address, destination address, and port number. Unlike Standard ACLs, Extended ACLs offer precise traffic management and are widely used in real-world network security environments.
