 # [Ph4nt0m 1ntrud3r](https://play.picoctf.org/practice/challenge/459)

 ## Challenge Information
 - **Category**: Forensics
 - **Difficulty**: Medium
 - **Description**: A digital ghost has breached my defenses, and my sensitive data has been stolen! 😱💻 Your mission is to uncover how this phantom intruder infiltrated my system and retrieve the hidden flag.
To solve this challenge, you'll need to analyze the provided PCAP file and track down the attack method. The attacker has cleverly concealed his moves in well timely manner. Dive into the network traffic, apply the right filters and show off your forensic prowess and unmask the digital intruder!
Find the PCAP file here [Network Traffic PCAP file](https://challenge-files.picoctf.net/c_verbal_sleep/4d25aca04e2409ba0d917d8ed27d49c6fb616ff9603fa3926712cce623a3d7f5/myNetworkTraffic.pcap) and try to get the flag.

 ## Solution Overview
 The attack was executed in a **timely manner**, so time-based analysis is crucial. We analyze network traffic to identify anomalies and extract hidden data.

 ## Hints
 - **Look at the timing of the packets.**
 - **Is there something unusual in the retransmissions?**
 - **Encoding might be the key.**

 ## Detailed Walkthrough

 ### Step 1: Load the PCAP File
 - Open the provided **PCAP** file in **Wireshark**.
 - Scan the network traffic for **suspicious patterns**.

 ### Step 2: Filtering Out Noise
 - Observing the packets, most had a **length of 48**, likely irrelevant traffic.
 - Apply the **Wireshark filter** to remove them:

    ```text
    frame.len != 48
    ```

 - This filter leaves only potentially significant packets.

 ### Step 3: Analyzing the Remaining Packets
 After filtering, the remaining packets are:

 | No. | Time      | Source       | Destination  | Protocol | Length | Info                                     |
 |---- |----------|--------------|-------------|---------|--------|------------------------------------------|
 | 9   | 0.001736 | 192.168.0.2  | 192.168.1.2 | TCP     | 52     | [TCP Out-Of-Order] [Illegal Segments]   |
 | 21  | 0.001964 | 192.168.0.2  | 192.168.1.2 | TCP     | 52     | [TCP Retransmission] SYN 20 → 80        |
 | 17  | 0.002195 | 192.168.0.2  | 192.168.1.2 | TCP     | 52     | [TCP Retransmission] SYN 20 → 80        |
 | 15  | 0.002512 | 192.168.0.2  | 192.168.1.2 | TCP     | 52     | [TCP Retransmission] SYN 20 → 80        |
 | 20  | 0.002749 | 192.168.0.2  | 192.168.1.2 | TCP     | 52     | [TCP Retransmission] SYN 20 → 80        |
 | 13  | 0.002975 | 192.168.0.2  | 192.168.1.2 | TCP     | 52     | [TCP Retransmission] SYN 20 → 80        |
 | 8   | 0.003195 | 192.168.0.2  | 192.168.1.2 | TCP     | 44     | [TCP Retransmission] SYN 20 → 80        |

 - These are multiple **TCP retransmissions** and **out-of-order packets**.
 - Some packets contain **Base64-encoded data**.

 ### Step 4: Extract & Decode Base64 Strings
 - Extracting payloads reveals:

   ```text
   cGljb0NURg==
   ezF0X3c0cw==
   bnRfdGg0dA==
   XzM0c3lfdA==
   YmhfNHJfOA==
   ZTEwZTgzOQ==
   fQ==
   ```

 - Decoding each line:

   ```text
   picoCTF
   {1t_w4s
   nt_th4t
   _34sy_t
   bh_4r_8
   e10e839
   }
   ```

 ### Step 5: Assemble the Flag
 - Combining all parts:

   ```text
   picoCTF{1t_w4snt_th4t_34sy_tbh_4r_8e10e839}
   ```

 ## Tools and Resources Used
 - **Wireshark**: For analyzing network packets.
 - **Base64 decoder**: To decode hidden text.
 - **PCAP filtering**: To isolate relevant data.

 ## Learning Points
 - **Time-based packet analysis can reveal attack patterns.**
 - **TCP retransmissions and out-of-order packets can indicate malicious activity.**
 - **Base64 encoding is commonly used to hide data in network traffic.**

 ## Mitigation Strategies
 To detect and prevent such hidden data leaks in real-world applications:
 - **Monitor TCP retransmissions for unusual activity.**
 - **Use packet filtering to isolate suspicious patterns.**

 ## References
 - [Wireshark Filter Manual Page](https://www.wireshark.org/docs/man-pages/wireshark-filter.html)
 - [Base64 Encoding/Decoding](https://www.base64decode.org/)