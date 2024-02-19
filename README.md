# Packet sniffing with Wireshark

Wireshark is a network protocol analyzer that's open source and used for monitoring and analyzing Network traffic. It's a packet sniffing tool that captures and dissects data packets traveling across a network and it will provide you a detailed and real-time view of communication patterns and in Cybersecurity it's used to detect potential security threats, detect malicious activities, Network vulnerabilities. By looking into the packet's contents you can examine communication protocols and apply filters and uncover anomalies, you can see unauthorized access attempts and signs of malicious software that can be invaluable in things like instant response forensics, vulnerability assessments and enabling cybersecurity practitioners to gain insights into Network behavior and strenghten their defenses.

# The Project: Analyzing HTTP Traffic and Identifying Security Issues

We will capture and analyze HTTP traffic to identify potential security issues such as unencrypted credentials, suspicious URLs or unauthorized access attempts.

We will divide the project into 3 sections:

- Capture: web browsing, logging into websites, access different HTTP based services

- Analyze: understanding the information exchanged between the client and the server

- Report: document your findings and observations (how to potentially fix the vulnerabilities)

Task 1
Install and set up Wireshark on Ubuntu:

● To get the latest stable version of Wireshark on Ubuntu Linux, use the add-apt-repository command: sudo add-apt-repository ppa:wireshark-dev/stable

● Wireshark should not be run as superuser for security reasons.

● The user can be added to the Wireshark group to add packet capture capabilities: sudo usermod -aG wireshark $USER

![Screenshot 2024-02-19 at 14 09 40](https://github.com/redjules/Packet-sniffing/assets/106017493/91313ac8-e8a8-4694-b660-4beece313be9)

![Screenshot 2024-02-19 at 14 10 46](https://github.com/redjules/Packet-sniffing/assets/106017493/1324fbfd-2441-4632-abb2-61bf3bdd1313)

Task 2
Start a packet capture on an ethernet port and save it to file:

● The wired interface includes the ethernet packet capture, which begins with ‘en’ in Wireshark.

● The Wireshark app includes controls to start packet capture, stop capture, save the packets to a file, and load the capture file.

● A capture can only be saved once the capture has stopped.

![Screenshot 2024-02-19 at 14 12 26](https://github.com/redjules/Packet-sniffing/assets/106017493/44d3498c-35c1-44a7-8112-1dda460b9b70)

we start the packet transfer:

![Screenshot 2024-02-19 at 14 21 28](https://github.com/redjules/Packet-sniffing/assets/106017493/0b636ee8-aa91-47a2-9a29-8de618a7bc0e)

and stop it:

![Screenshot 2024-02-19 at 14 22 00](https://github.com/redjules/Packet-sniffing/assets/106017493/89997ec0-0027-42b0-9a73-4a9c9fb6e3c6)

we save the task:

![Screenshot 2024-02-19 at 14 23 13](https://github.com/redjules/Packet-sniffing/assets/106017493/4bdc0628-f9f9-40d7-8895-96bcabf6ab3a)

The capture can only be saved once the capture has stopped.

Task 3
Use a display filter to detect HTTPS packets:

● To display certain packets in an existing packet capture, use a display filter.

● To display only HTTPS traffic, use a filter on TCP port 443: tcp.port == 443

we go to duckduckgo.com:

![Screenshot 2024-02-19 at 14 28 23](https://github.com/redjules/Packet-sniffing/assets/106017493/c86ed858-e62a-4bf5-882b-89d12947053e)


and we start a packet transfer in Wireshark:

![Screenshot 2024-02-19 at 14 27 33](https://github.com/redjules/Packet-sniffing/assets/106017493/2dbcf4dc-5dca-4642-aa3e-77ec2b032842)

and save the task as task3:

![Screenshot 2024-02-19 at 14 28 42](https://github.com/redjules/Packet-sniffing/assets/106017493/242156a2-800f-45da-a893-db6239c28609)


we use now a filter on TCP port 443: tcp.port == 443:

![Screenshot 2024-02-19 at 14 30 56](https://github.com/redjules/Packet-sniffing/assets/106017493/0f2b32d9-394b-47de-84a5-25d193724f75)

and if we copy on the browser that IP address, we get the duckduckgo.com website!:

![Screenshot 2024-02-19 at 14 31 30](https://github.com/redjules/Packet-sniffing/assets/106017493/eb3d2ca8-ae01-4698-bb17-86bde4ada346)

![Screenshot 2024-02-19 at 14 32 12](https://github.com/redjules/Packet-sniffing/assets/106017493/d3b08dca-d051-4d43-ae0b-6375f83db62f)


Task 4
Visit a web page and detect its IP address using a display filter:

● A TLS handshake display filter may be used to detect a website visit in a packet list: tls.handshake.type ==1

● The IP address is used in a filter to obtain packet information for a particular website: ip.addr == 142.251.163.103

we go to Google.com:

![Screenshot 2024-02-19 at 14 36 19](https://github.com/redjules/Packet-sniffing/assets/106017493/3698fef9-ef71-4eaa-87ac-db93345e8aaf)

we go to Wireshark and stop  the packet:

![Screenshot 2024-02-19 at 14 36 35](https://github.com/redjules/Packet-sniffing/assets/106017493/d271e927-6925-401e-a7c6-16015de7a347)

we look for tls.handshake.type ==1:

![Screenshot 2024-02-19 at 14 38 10](https://github.com/redjules/Packet-sniffing/assets/106017493/89d4478c-8758-45d1-aec4-d610f7c77ef0)

and now we look for ip.addr == 142.251.163.103:

![Screenshot 2024-02-19 at 14 39 04](https://github.com/redjules/Packet-sniffing/assets/106017493/44cbda6b-b514-44de-8e08-1a64a31fbecb)


Task 5
Locate all HTTPS packets from a capture not containing a certain IP address:

● A Conditional statement may be used to include and eliminate packets from a Wireshark capture: !(ip.addr == 142.251.163.147) and tcp.port == 443


![Screenshot 2024-02-19 at 14 44 36](https://github.com/redjules/Packet-sniffing/assets/106017493/e32d0ce5-b3c6-439a-94bf-38475d22e768)

● A compound conditional should include parentheses to avoid order of execution errors: !(ip.addr == 142.251.163.147) and (tcp.port == 80 or tcp.port == 443)

![Screenshot 2024-02-19 at 14 45 59](https://github.com/redjules/Packet-sniffing/assets/106017493/30c3fd03-6b55-4edc-9bd0-26a5ac162a64)



