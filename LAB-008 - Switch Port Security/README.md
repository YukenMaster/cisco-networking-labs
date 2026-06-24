# LAB-008 - Switch Port Security

## Objective

Configure and validate Port Security on a Cisco Switch to restrict network access based on MAC addresses and protect the network against unauthorized devices.

---

## Network Diagram

![Topology](Topology.png)

---

## IP Addressing

### PC1

| Parameter   | Value        |
| ----------- | ------------ |
| IP Address  | 192.168.1.10 |
| Subnet Mask | 255.255.255.0 |

![PC1 IP Configuration](pc1-ip-configuration.png)

### PC2

| Parameter   | Value        |
| ----------- | ------------ |
| IP Address  | 192.168.1.20 |
| Subnet Mask | 255.255.255.0 |

![PC2 IP Configuration](pc2-ip-configuration.png)

---

## Port Security Configuration

Port Security was configured on interface **FastEthernet0/1** using Sticky MAC learning.

### Configuration Applied

```cisco
enable
configure terminal

interface fastethernet0/1
 switchport mode access
 switchport port-security
 switchport port-security maximum 1
 switchport port-security mac-address sticky
 switchport port-security violation shutdown

end
write memory
```

The configuration was verified using the following command:

```cisco
show port-security interface fa0/1
```

![Port Security Configuration](port-security-configuration.png)

---

## Sticky MAC Address Learning

After connecting the authorized device, the switch dynamically learned and stored the MAC address on the secured port.

Verification was performed using:

```cisco
show port-security address
```

The output confirms that a Sticky Secure MAC Address was successfully learned on FastEthernet0/1.

![Secure MAC Address](secure-mac-address.png)

---

## Security Violation Test

To validate Port Security functionality, the authorized device was disconnected and another device was connected to the protected port.

Since the new device presented a different MAC address than the one previously learned, the switch detected a security violation.

The violation caused the interface to enter the **Secure-Shutdown** state as configured.

Verification command:

```cisco
show port-security interface fa0/1
```

Output highlights:

* Port Security Enabled
* Violation Mode: Shutdown
* Port Status: Secure-shutdown
* Security Violation Count: 1

![Security Violation](security-violation.png)

---

## Topology After Violation

The topology below shows the final state after the unauthorized device triggered the Port Security violation.

The protected port was automatically disabled by the switch, preventing unauthorized network access.

![Topology Security Violation](topology-security-violation.png)

---

## Port Security Operation Summary

### Authorized Device

| Feature | Status |
|----------|---------|
| Port Security Enabled | Yes |
| Sticky MAC Learned | Yes |
| Maximum MAC Addresses | 1 |
| Port Status | Secure-Up |

### Unauthorized Device

| Feature | Status |
|----------|---------|
| Different MAC Address Detected | Yes |
| Security Violation Triggered | Yes |
| Port Shutdown Executed | Yes |
| Secure-Shutdown State | Yes |

---

## Skills Demonstrated

* Cisco Switch Security Configuration
* Port Security Implementation
* Sticky MAC Address Learning
* Secure MAC Address Verification
* Security Violation Detection
* Layer 2 Network Protection
* Cisco IOS CLI Administration
* Switch Port Hardening
* Network Access Control
* Basic Network Security Operations
* Troubleshooting Security Events

---

## Conclusion

In this lab, Port Security was successfully implemented on a Cisco Switch to control access to the network using MAC address-based restrictions.

The switch dynamically learned the authorized device's MAC address through Sticky MAC functionality and enforced a limit of one MAC address on the protected port.

When an unauthorized device attempted to use the secured interface, the switch correctly detected the violation and automatically placed the port into a Secure-Shutdown state according to the configured security policy.

This exercise demonstrates an important Layer 2 security mechanism commonly used in enterprise environments to prevent unauthorized access, rogue devices, and basic network attacks, reinforcing essential Cisco switching and cybersecurity skills.

---

## Files

* LAB-008-Port-Security.pkt
* README.md
* topology.png
* pc1-ip-configuration.png
* pc2-ip-configuration.png
* port-security-configuration.png
* secure-mac-address.png
* security-violation.png
* topology-security-violation.png
