# Network Traffic Flow Analysis with Wireshark

## Objective
The purpose of this project is to capture and analyze network traffic at various layers of the OSI model using Wireshark. This lab demonstrates the fundamental flow of web traffic: **DNS → TCP → TLS → HTTP/HTTPS**.

## Tools Used
*   **Kali Linux** (Virtual Machine)
*   **Wireshark** (Network Protocol Analyzer)
*   **Command Line Tools** (curl, ping)

## Core Phases Analysed
1. **DNS Traffic:** Observed how a domain name resolves to an IP address via Standard Queries and Responses.
2. **TCP Traffic:** Captured the TCP 3-Way Handshake (`SYN`, `SYN-ACK`, `ACK`) and followed the connection streams.
3. **HTTP Traffic:** Extracted unencrypted payloads (HTML code) by analyzing plaintext streams.
4. **TLS Traffic:** Analyzed secure TLS handshakes, Cipher Suite negotiations, and Server Certificates.

---

<details>
<summary><strong>📁 Click Here to Expand: Full Step-by-Step Lab Execution & Screenshots</strong></summary>

### Step 1 to 5: Initial Setup & Capture
![Exercise 1](Screenshots/ASSIGNMENT1.png)
![Exercise 2](Screenshots/ASSIGNMENT2.png)
![Exercise 3](Screenshots/Assignment%203.png)
![Exercise 4](Screenshots/Assignment4.png)
![Exercise 5](Screenshots/Assignment%205.png)

### Step 6 to 10: TCP 3-Way Handshake
![Exercise 6](Screenshots/Assignment6.png)
![Exercise 7](Screenshots/Assignment7.png)
![Exercise 8](Screenshots/Assignment8.png)
![Exercise 9](Screenshots/Assignment9.png)
![Exercise 10](Screenshots/Assignment10.png)

### Step 11 to 15: Analyzing Unencrypted HTTP Traffic
![Exercise 11](Screenshots/Assignment11.png)
![Exercise 12](Screenshots/Assignment12.png)
![Exercise 13](Screenshots/Assignment13.png)
![Exercise 14](Screenshots/Assignment14.png)
![Exercise 15](Screenshots/Assignment15.png)

### Step 16 to 21: Analyzing Encrypted TLS Traffic
![Exercise 16](Screenshots/Assignment16.png)
![Exercise 17](Screenshots/Assignment17.png)
![Exercise 18](Screenshots/Assignment18.png)
![Exercise 19](Screenshots/Assignment19.png)
![Exercise 20](Screenshots/Assignmet20.png)
![Exercise 21](Screenshots/Assignment21.png)

</details>

---

## Conclusion: HTTP vs. TLS Comparison
By comparing the traffic streams, the security benefits of TLS are highly visible:
*   **HTTP Traffic (Unencrypted):** Following the stream revealed the payload in **plaintext**. The exact HTML code, headers, and website content were perfectly readable to anyone monitoring the network.
*   **TLS Traffic (Encrypted):** The payload was classified as **Encrypted Application Data**. Instead of readable code, the packet only contained random, scrambled ciphertext. Because the data is locked behind the Cipher Suite agreed upon during the handshake, a network eavesdropper cannot read or manipulate the actual contents of the communication.