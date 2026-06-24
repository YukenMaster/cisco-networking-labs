# LAB-008 - Switch Port Security

## Objective

Configure Port Security on a Cisco Switch to restrict access to a single authorized device using Sticky MAC Address learning and validate the security violation protection mechanism.

---

## Network Diagram

![Topology](topology\(7\).png)

---

## IP Addressing

### PC1

| Parameter   | Value         |
| ----------- | ------------- |
| IP Address  | 192.168.1.10  |
| Subnet Mask | 255.255.255.0 |

![PC1 IP Configuration](pc1-ip-configuration\(1\).png)

### PC2

| Parameter   | Value         |
| ----------- | ------------- |
| IP Address  | 192.168.1.20  |
| Subnet Mask | 255.255.255.0 |

![PC2 IP Configuration](pc2-ip-configuration\(1\).png)

---

## Port Security Configuration

Port Security was configured on interface FastEthernet0/1 to allow only one device and automatically learn its MAC address using the Sticky feature.

```cisco
interface FastEthernet0/1
 switchport mode access
 switchport port-security
 switchport port-security mac-address sticky
```

The configuration was verified using:

```cisco
show port-security interface fa0/1
```

![Port Security Configuration](port-security-configuration\(1\).png)

---

## Sticky MAC Learning

After connecting the authorized device, the switch dynamically learned and stored the MAC address as a Secure Sticky entry.

Verification command:

```cisco
show port-security address
```

![Secure MAC Address Table](secure-mac-address\(1\).png)

The learned MAC address became permanently associated with the protected interface.

---

## Port Security Status Verification

The operational status of Port Security was verified after the Sticky MAC address was learned.

```cisco
show port-security interface fa0/1
```

The output confirms:

* Port Security enabled
* Secure-Up state
* Maximum of one MAC address allowed
* Sticky MAC learning active
* No security violations detected

![Port Security Status](port-security-status\(1\).png)

---

## Security Violation Test

To validate the protection mechanism, the authorized device was disconnected and a different host was connected to the protected interface.

The switch detected a MAC address violation and automatically placed the interface into a Secure-Shutdown state.

Verification command:

```cisco
show port-security interface fa0/1
```

Output highlights:

* Port Status: Secure-shutdown
* Violation Mode: Shutdown
* Security Violation Count: 1

![Security Violation](security-violation\(1\).png)

---

## Security Violation Topology

The following topology illustrates the result after the unauthorized device triggered the Port Security violation.

The protected interface was automatically disabled by the switch, preventing network access from the unauthorized host.

![Security Violation Topology](topology_security-violation\(2\).png)

---

## Skills Demonstrated

* Cisco Switch Security Configuration
* Port Security Implementation
* Sticky MAC Address Learning
* MAC Address Restriction
* Switch Access Control
* Cisco IOS CLI Administration
* Layer 2 Security
* Security Violation Detection
* Secure Port Shutdown Operation
* Network Access Protection

---

## Conclusion

In this lab, Cisco Port Security was successfully implemented on a switch access port using Sticky MAC Address learning.

The switch dynamically learned the MAC address of the authorized device and restricted access to a single endpoint. When an unauthorized device attempted to connect to the protected interface, the switch immediately detected the violation and transitioned the port into a Secure-Shutdown state.

This exercise demonstrates an important Layer 2 security control commonly used in enterprise environments to prevent unauthorized access, MAC spoofing attempts, and rogue device connections.

The lab reinforces practical skills related to switch hardening, access control, network security monitoring, and Cisco IOS administration.

---

## Files

* LAB-008-Port-Security.pkt
* README.md
* topology(7).png
* pc1-ip-configuration(1).png
* pc2-ip-configuration(1).png
* port-security-configuration(1).png
* secure-mac-address(1).png
* port-security-status(1).png
* security-violation(1).png
* topology_security-violation(2).png
