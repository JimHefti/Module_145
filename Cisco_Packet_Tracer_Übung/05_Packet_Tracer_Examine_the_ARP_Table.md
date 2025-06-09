# Packet Tracer – Examine the ARP Table

---

## Addressing Table

| Device        | Interface | MAC Address      | Switch Interface |
|---------------|-----------|------------------|------------------|
| Router0       | G0/0      | 0001.6458.2501   | G0/1             |
| Router0       | S0/0/0    | N/A              | N/A              |
| Router1       | G0/0      | 00E0.F7B1.8901   | G0/1             |
| Router1       | S0/0/0    | N/A              | N/A              |
| 10.10.10.2    | Wireless  | 0060.2F84.4AB6   | F0/2             |
| 10.10.10.3    | Wireless  | 0060.4706.572B   | F0/2             |
| 172.16.31.2   | F0        | 000C.85CC.1DA7   | F0/1             |
| 172.16.31.3   | F0        | 0060.7036.2849   | F0/2             |
| 172.16.31.4   | G0        | 0002.1640.8D75   | F0/3             |

---

## Part 1: Examine an ARP Request

**Question:** Is this address listed in the table above?  
✔️ Yes, this MAC address belongs to 172.16.31.3, so it's already part of the given addressing table.

**Question:** How many copies of the PDU did Switch1 make?  
✔️ The switch forwarded the ARP request to all devices on different ports — three in total.

**Question:** What is the IP address of the device that accepted the PDU?  
✔️ The target IP that accepted the ARP broadcast was 172.16.31.3.

**Question:** What happened to the source and destination MAC addresses?  
✔️ The sender's MAC address was included as the source, and the destination was set to broadcast (FF:FF:FF:FF:FF:FF) so all hosts receive it.

**Question:** How many copies of the PDU did the switch make during the ARP reply?  
✔️ Just one, since the reply is unicast and directed specifically to the requester.

---

**Step 2: Examine the ARP table.**

**Question:** Do the MAC addresses of the source and destination align with their IP addresses?  
✔️ Yes, the MAC addresses match the respective IPs, as expected after the ARP resolution.

**Question:** To what IP address does the MAC address entry correspond?  
✔️ The MAC address in question is now mapped to IP 172.16.31.3.

**Question:** In general, when does an end device issue an ARP request?  
✔️ Devices send ARP requests when they don’t yet know the MAC address needed to deliver data to an IP.

---

## Part 2: Examine a Switch MAC Address Table

**Question:** How many replies were sent and received?  
✔️ There were a total of four replies — each ping generated two ICMP replies.

**Question:** Do the entries on Switch1 correspond to those in the table above?  
✔️ Yes, the MAC table on Switch1 matches the expected MAC-port mappings from the addressing table.

**Question:** Do the entries on Switch0 correspond to those in the table above?  
✔️ They do — all listed MAC addresses are correctly assigned to their respective interfaces.

**Question:** Why are two MAC addresses associated with one port?  
✔️ That usually happens when multiple end devices connect via a hub or wireless access point that is linked to a single switch port.

---

## Part 3: Examine the ARP Process in Remote Communications

**Question:** What is the IP address of the new ARP table entry?  
✔️ The new entry typically shows the gateway address, most likely 172.16.31.1.

**Question:** How many PDUs appear?  
✔️ Two are visible: the ARP request and the ICMP packet waiting for the MAC resolution.

**Question:** What is the target destination IP address of the ARP request?  
✔️ The ARP request targets 172.16.31.1, which is the local gateway IP.

**Question:** Why?  
✔️ Because communication with a remote network requires forwarding through the default gateway, and its MAC address must be known first.

---

**Step 2: Examine the ARP table on Router1.**

**Question:** How many MAC addresses are in the table? Why?  
✔️ Usually one or two, depending on recent traffic — routers only store MAC entries for directly reachable devices.

**Question:** Is there an entry for 172.16.31.2?  
✔️ Yes, assuming it has recently sent a packet through the router.

**Question:** What happens to the first ping in a situation where the router responds to the ARP request?  
✔️ The initial ping may be lost or delayed due to ARP resolution time, but later pings go through without issue.

---

**✅ End of Document**
