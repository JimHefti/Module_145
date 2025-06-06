# 04_Packet Tracer - Identify MAC and IP Addresses
Objectives
Part 1: Gather PDU Information for Local Network Communication

Part 2: Gather PDU Information for Remote Network Communication

Background
This activity is optimized for viewing PDUs. The devices are already configured. You will gather PDU information in simulation mode and answer a series of questions about the data you collect.

Instructions

## Part 1: Gather PDU Information for Local Network Communication
Note: Review the Reflection Questions in Part 3 before proceeding with Part 1. It will give you an idea of the type of information you will need to gather.Gather PDU information as a packet travels from 172.16.31.5 to 172.16.31.2.


### Ping from 172.16.31.5 to 172.16.31.2

 At Device     | Dest. MAC       | Src MAC         | Src IPv4       | Dest IPv4      |
|---------------|------------------|------------------|----------------|----------------|
| 172.16.31.5   | 000:FF:FF:FF:FF:FF | 00D0:D311:C2F5   | 172.16.31.5    | 172.16.31.2    |
| Switch1       | FF:FF:FF:FF:FF:FF | 00D0:D311:C2F5   | 172.16.31.5    | 172.16.31.2    |

e.     Click Capture / Forward (the right arrow followed by a vertical bar) to move the PDU to the next device. Gather the same information from Step 1d. Repeat this process until the PDU reaches its destination. Record the PDU information you gathered into a spreadsheet using a format like the table shown below:





Step 2: Gather additional PDU information from other pings.
Repeat the process in Step 1 and gather the information for the following tests:

·         Ping 172.16.31.2 from 172.16.31.3.

·         Ping 172.16.31.4 from 172.16.31.5.

Return to Realtime mode.

## Part 2: Gather PDU Information for Remote Network Communication
In order to communicate with remote networks, a gateway device is necessary. Study the process that takes place to communicate with devices on the remote network. Pay close attention to the MAC addresses used.

Step 1: Gather PDU information as a packet travels from 172.16.31.5 to 10.10.10.2.
a.     Click 172.16.31.5 and open the Command Prompt.

b.     Enter the ping 10.10.10.2 command.

c.     Switch to simulation mode and repeat the ping 10.10.10.2 command. A PDU appears next to 172.16.31.5.

d.     Click the PDU and note the following information from the Outbound PDU Layer tab:

·         Destination MAC Address: 00D0:BA8E:741A

·         Source MAC Address: 00D0:D311:C788

·         Source IP Address: 172.16.31.5

·         Destination IP Address: 10.10.10.2

·         At Device: 172.16.31.5

Question:
What device has the destination MAC that is shown?

e.     Click Capture / Forward (the right arrow followed by a vertical bar) to move the PDU to the next device. Gather the same information from Step 1d. Repeat this process until the PDU reaches its destination. Record the PDU information you gathered from pinging 172.16.31.5 to 10.10.10.2 into a spreadsheet using a format like the sample table shown below:

At Device



## Reflection Questions
Answer the following questions regarding the captured data:

1. Were there different types of cables/media used to connect devices?

2. Did the cables change the handling of the PDU in any way?

3. Did the Hub lose any of the information that it received?

4. What does the Hub do with MAC addresses and IP addresses?

5. Did the wireless Access Point do anything with the information given to it?

6. Was any MAC or IP address lost during the wireless transfer?

7. What was the highest OSI layer that the Hub and Access Point used?

8. Did the Hub or Access Point ever replicate a PDU that was rejected with a red “X”?

9. When examining the PDU Details tab, which MAC address appeared first, the source or the destination?

10. Why would the MAC addresses appear in this order?

11. Was there a pattern to the MAC addressing in the simulation?

12. Did the switches ever replicate a PDU that was rejected with a red “X”?

13. Every time that the PDU was sent between the 10 network and the 172 network, there was a point where the MAC addresses suddenly changed. Where did that occur?

14. Which device uses MAC addresses that start with 00D0:BA?

15. What devices did the other MAC addresses belong to?

16. Did the sending and receiving IPv4 addresses change fields in any of the PDUs?

17. When you follow the reply to a ping, sometimes called a pong, do you see the sending and receiving IPv4 addresses switch?

18. What is the pattern to the IPv4 addressing used in this simulation?

19. Why do different IP networks need to be assigned to different ports of a router?

20. If this simulation was configured with IPv6 instead of IPv4, what would be different?

