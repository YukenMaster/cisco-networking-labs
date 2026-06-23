# LAB 005 - Extended ACLs

## Objective

Configure an Extended Access Control List (ACL) to block HTTP traffic from the Guest network to the Web Server while still allowing other network communications.

---

## Network Diagram

![Topology](topology.png)

---

## IP Addressing

### Admin PC

| Parameter       | Value         |
| --------------- | ------------- |
| IP Address      | 192.168.10.10 |
| Subnet Mask     | 255.255.255.0 |
| Default Gateway | 192.168.10.1  |

![Admin PC IP Configuration](admin-pc-ip-configuration.png)

### Web Server

| Parameter       | Value          |
| --------------- | -------------- |
| IP Address      | 192.168.10.100 |
| Subnet Mask     | 255.255.255.0  |
| Default Gateway | 192.168.10.1   |

![Web Server IP Configuration](web-server-ip-configuration.png)

### Guest PC

| Parameter       | Value         |
| --------------- | ------------- |
| IP Address      | 192.168.20.10 |
| Subnet Mask     | 255.255.255.0 |
| Default Gateway | 192.168.20.1  |

![Guest PC IP Configuration](guest-pc-ip-configuration.png)

### Router Interfaces

| Interface          | IP Address   |
| ------------------ | ------------ |
| GigabitEthernet0/0 | 192.168.10.1 |
| GigabitEthernet0/1 | 192.168.20.1 |

![Router IP Addressing](router-ip-addressing.png)

---

## HTTP Service Configuration

The HTTP service was enabled on the Web Server before applying the ACL.

![HTTP Service Enabled](server-http-enabled.png)

---

## Verification Before ACL

The Guest PC was able to access the Web Server through HTTP before the ACL was applied.

![Web Server Access Before ACL](web-server-access-before-acl.png)

---

## Extended ACL Configuration

The following Extended ACL was configured on the router:

```cisco
access-list 101 deny tcp 192.168.20.0 0.0.0.255 host 192.168.10.100 eq 80
access-list 101 permit ip any any

interface GigabitEthernet0/1
 ip access-group 101 in
```

![Extended ACL Configuration](extended-acl-configuration.png)

---

## Verification After ACL

After applying the ACL, HTTP access from the Guest network to the Web Server was successfully blocked.

![HTTP Blocked After ACL](http-blocked-after-acl.png)

ICMP traffic (ping) remained functional, confirming that only HTTP traffic was filtered.

![Ping After ACL](ping-after-acl.png)

---

## Skills Demonstrated

* Extended ACL implementation
* Traffic filtering and access control
* HTTP service restriction
* Router security configuration
* Network troubleshooting
* Connectivity validation
* Cisco IOS command-line configuration

---

## Conclusion

In this lab, an Extended ACL was implemented to control traffic between network segments. The solution successfully prevented Guest users from accessing the Web Server through HTTP while maintaining normal network connectivity for other protocols.

This exercise reinforces important networking and cybersecurity concepts, including traffic filtering, access control enforcement, router-based security policies, and network verification techniques. These skills are essential for network administrators, cybersecurity analysts, and SOC professionals.

---

## Files

* LAB-005-Extended-ACLs.pkt
* README.md

```
```
