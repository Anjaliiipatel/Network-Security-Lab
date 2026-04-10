# Network Security & Protocol Analysis Lab
This project explores the vulnerabilities within the TCP/IP stack and evaluates the effectiveness of various security mechanisms. Using a controlled VM environment, I performed network reconnaissance, eavesdropping attacks, and protocol-level disruptions to understand how "baked-in" security compares to "bolt-on" security.

# Tools Used
Packet Analysis: Wireshark

Reconnaissance: Nmap

Exploitation: hping3, Telnet, Slowloris (Python)

Secure Communications: SSH, PuTTY (Port Forwarding)

Environment: Linux (Ubuntu/Debian VMs), Apache Web Server

# Investigation Highlights
1. Network Reconnaissance & Filtering
I conducted traffic analysis to distinguish between standard network operations and potential security threats.

ARP/DNS Analysis: Investigated address resolution and domain queries to identify spoofing risks.

<img width="781" height="340" alt="image" src="https://github.com/user-attachments/assets/b8c4e2ff-6d33-46aa-8f66-14a3e582142f" />

                                    Figure 1: ARP Protocols Analysis 

<img width="782" height="489" alt="image" src="https://github.com/user-attachments/assets/c4ec2c56-15ab-4cdc-878a-08af60b604ee" />

                                    Figure 2: DNS Protocols Analysis 

Capture vs. Display Filters: > Refining the data stream: Capture filters reduce CPU load by discarding packets at the NIC level, while Display filters allow for deep-dive analysis of a saved trace.

# 2. Eavesdropping: Telnet vs. SSH
A comparative study of plaintext vs. encrypted protocols.

<img width="777" height="523" alt="Screenshot 2026-04-09 233939" src="https://github.com/user-attachments/assets/5010640c-974e-470c-af2a-5581b29bdafc" />

                                    Figure 3: ARP Protocols Analysis 


The Vulnerability: Using Wireshark, I successfully intercepted a Telnet session and recovered the plaintext username and password.
<img width="780" height="670" alt="image" src="https://github.com/user-attachments/assets/6b76ed35-2370-44e7-9297-598036538909" />

                                    Figure 4: ARP Protocols Analysis 

<img width="770" height="425" alt="image" src="https://github.com/user-attachments/assets/534d39a6-f517-4b16-ab55-91c6fce8369f" />

                                    Figure 5: ARP Protocols Analysis 

The Solution: Analyzed SSH handshakes, identifying the Diffie-Hellman key exchange and the symmetric encryption (AES) used to secure the tunnel.

<img width="776" height="416" alt="image" src="https://github.com/user-attachments/assets/a7c0ad25-27cd-4384-9476-a283dedf5e20" />

                                    Figure 6: ARP Protocols Analysis 

# 3. SSH Port Forwarding (Tunneling)
I implemented a "poor man's VPN" by tunneling insecure HTTP traffic through an encrypted SSH connection.

Mechanism: Forwarded local port 7777 to the remote web server on port 80.
<img width="780" height="443" alt="image" src="https://github.com/user-attachments/assets/7ff8c1fb-15f8-4a9e-9dcb-9be0ddb2eef1" />


Security Insight: This demonstrates how attackers can create backdoors or bypass firewalls, but also how admins can secure legacy plaintext applications.

# 4. TCP RST (Reset) Attack
I performed a Denial of Service (DoS) attack by injecting spoofed TCP packets with the RST flag set.

Process: Using hping3, I monitored the sequence numbers of an active Telnet session and injected a reset packet to force-close the connection.
<img width="777" height="255" alt="Screenshot 2026-04-09 234518" src="https://github.com/user-attachments/assets/651ffcbf-2e7e-4cdb-8ca4-f77bd1d9fdf5" />


Result: The connection was instantly terminated, demonstrating the inherent trust vulnerabilities in the TCP protocol.

# 5. "Low and Slow" DoS: Slowloris
(If you completed the extra credit)

Tested the Apache server against a Slowloris attack, which exhausts the server's connection pool by keeping HTTP headers open indefinitely.

<img width="782" height="441" alt="image" src="https://github.com/user-attachments/assets/5910e5bc-8120-4d33-a9bd-a00a16ecc4df" />

The lab confirms that security must be integrated at the protocol design level. Transitioning from Telnet to SSH, and understanding the mechanics of a TCP Reset attack, highlights that encryption is only one piece of the puzzle—protocol logic and state management are equally vital.


