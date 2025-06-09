# Packet Tracer – Identify MAC and IP Addresses

---

## Objectives

- Part 1: Gather PDU Information for Local Network Communication  
- Part 2: Gather PDU Information for Remote Network Communication  
- Part 3: Answer Reflection Questions

---

## Part 1: Local Network PDU Data Collection

### Ping from 172.16.31.5 to 172.16.31.2

| At Device   | Dest. MAC        | Src MAC         | Src IPv4     | Dest IPv4    |
|------------|------------------|------------------|--------------|--------------|
| 172.16.31.5 | 000C:85CC:1DA7   | 00D0:D311:C788   | 172.16.31.5  | 172.16.31.2  |
| Switch1     | 000C:85CC:1DA7   | 00D0:D311:C788   | 172.16.31.5  | 172.16.31.2  |
| 172.16.31.2 | 00D0:D311:C788   | 000C:85CC:1DA7   | 172.16.31.2  | 172.16.31.5  |

### Ping from 172.16.31.3 to 172.16.31.2

| At Device   | Dest. MAC        | Src MAC         | Src IPv4     | Dest IPv4    |
|------------|------------------|------------------|--------------|--------------|
| 172.16.31.3 | 000C:85CC:1DA7   | 00D0:588C:2401   | 172.16.31.3  | 172.16.31.2  |
| Switch1     | 000C:85CC:1DA7   | 00D0:588C:2401   | 172.16.31.3  | 172.16.31.2  |
| 172.16.31.2 | 00D0:588C:2401   | 000C:85CC:1DA7   | 172.16.31.2  | 172.16.31.3  |

### Ping from 172.16.31.5 to 172.16.31.4

| At Device   | Dest. MAC        | Src MAC         | Src IPv4     | Dest IPv4    |
|------------|------------------|------------------|--------------|--------------|
| 172.16.31.5 | 00D0:234C:1FA1   | 00D0:D311:C788   | 172.16.31.5  | 172.16.31.4  |
| Switch1     | 00D0:234C:1FA1   | 00D0:D311:C788   | 172.16.31.5  | 172.16.31.4  |
| 172.16.31.4 | 00D0:D311:C788   | 00D0:234C:1FA1   | 172.16.31.4  | 172.16.31.5  |

---

## Part 2: Remote Network PDU Data Collection

### Ping from 172.16.31.5 to 10.10.10.2

| At Device    | Dest. MAC       | Src MAC         | Src IPv4     | Dest IPv4    |
|-------------|------------------|------------------|--------------|--------------|
| 172.16.31.5  | 00D0:BA8E:741A   | 00D0:D311:C788   | 172.16.31.5  | 10.10.10.2   |
| Switch1      | 00D0:BA8E:741A   | 00D0:D311:C788   | 172.16.31.5  | 10.10.10.2   |
| Router       | 0060:2F84:4AB6   | 00D0:BA8E:741A   | 172.16.31.5  | 10.10.10.2   |
| Switch0      | 0060:2F84:4AB6   | 00D0:588C:2401   | 172.16.31.5  | 10.10.10.2   |
| Access Point | 0060:2F84:4AB6   | 00D0:588C:2401   | 172.16.31.5  | 10.10.10.2   |
| 10.10.10.2   | 00D0:588C:2401   | 0060:2F84:4AB6   | 10.10.10.2   | 172.16.31.5  |

---

## Part 3: Reflection Questions & Reworded Answers

1. **Were there different types of cables/media used to connect devices?**  
   ✔️ Yes, the setup included both Ethernet cables and wireless links.

2. **Did the cables change the handling of the PDU in any way?**  
   ✔️ No, the format of the PDU remains constant; only the transmission path differs.

3. **Did the Hub lose any of the information that it received?**  
   ✔️ No, a hub doesn’t drop data but sends it to all connected ports.

4. **What does the Hub do with MAC addresses and IP addresses?**  
   ✔️ Hubs don’t analyze addresses—they blindly forward the frames to every port.

5. **Did the wireless Access Point do anything with the information given to it?**  
   ✔️ Yes, it used MAC addressing to forward the frame to the correct wireless client.

6. **Was any MAC or IP address lost during the wireless transfer?**  
   ✔️ No information was lost; both MAC and IP data remained intact.

7. **What was the highest OSI layer that the Hub and Access Point used?**  
   - **Hub:** Layer 1 – Physical  
   - **Access Point:** Layer 2 – Data Link

8. **Did the Hub or Access Point ever replicate a PDU that was rejected with a red “X”?**  
   ✔️ No, neither device duplicated any packet that failed.

9. **When examining the PDU Details tab, which MAC address appeared first, the source or the destination?**  
   ✔️ The destination MAC was shown before the source.

10. **Why would the MAC addresses appear in this order?**  
    ✔️ Because forwarding a frame requires knowing the destination first.

11. **Was there a pattern to the MAC addressing in the simulation?**  
    ✔️ Yes, each device type had similar MAC address prefixes for easier identification.

12. **Did the switches ever replicate a PDU that was rejected with a red “X”?**  
    ✔️ No, switches only forward frames to known destinations based on their MAC tables.

13. **Where did the MAC addresses change during transmission between the 10 and 172 networks?**  
    ✔️ The router acted as a boundary, updating the MAC addresses when crossing subnets.

14. **Which device uses MAC addresses that start with 00D0:BA?**  
    ✔️ That prefix was used by the router’s interface facing the 172.16.31.0 network.

15. **What devices did the other MAC addresses belong to?**  
    ✔️ Each MAC was unique to its device—PCs, switches, routers, and APs all had their own.

16. **Did the sending and receiving IPv4 addresses change in any of the PDUs?**  
    ✔️ No, the IP addresses remained consistent throughout the communication process.

17. **When you follow the reply to a ping (pong), do the sending and receiving IPv4 addresses switch?**  
    ✔️ Yes, the response inverts the source and destination roles.

18. **What is the pattern to the IPv4 addressing used in this simulation?**  
    ✔️ Local systems used the 172.16.31.x range, while remote systems used 10.10.10.x.

19. **Why do different IP networks need to be assigned to different ports of a router?**  
    ✔️ Because each port handles a distinct subnet and the router uses this to route traffic properly.

20. **If this simulation was configured with IPv6 instead of IPv4, what would be different?**  
    ✔️ IPv6 uses a different format: longer addresses, colon separators, and NDP replaces ARP for address resolution.

---

