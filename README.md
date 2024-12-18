# PCAP 2

## Objective

I’ll be putting my Wireshark skills to the test

### Skills Learned

- **Packet Capture Analysis:** Learn how to capture and examine network traffic to identify unusual patterns like port scanning.
- **Protocol Dissection:** Gain experience in dissecting various network protocols (e.g., TCP, UDP, ICMP) to analyze specific packet details.
- **Traffic Filtering:** Practice filtering specific IP addresses, ports, and protocols to focus on the relevant traffic for analysis.
- **Anomaly Detection:** Learn how to spot anomalies in traffic patterns, such as unusual frequency or volume of requests.
- **Flow Analysis:** Study communication flows between internal systems to detect unauthorized or suspicious interactions.
- **Evidence Collection:** Collect and interpret network data to support incident investigation and reporting.

### Tools Used

- Wireshark for capturing and examining network traffic to investigate the 'Local to Local Port Scanning' alert.
- Packet Capture File (PCAP) provided for detailed analysis of network communication between internal systems.
- VirtualBox used as the virtual machine platform to simulate the environment for traffic analysis, ensuring a controlled and isolated space for investigation.
- Windows 10 Virtual Machine

## Steps
### 1. What is the WebAdmin password?
- Typed in http in display filter, to check HTTP traffic
  
  <div><img width="510" alt="image" src="https://github.com/user-attachments/assets/7915f345-8ff7-4258-ad56-be967d3784b6" /></div>
- Right click on packet 4121 > followed HTTP stream, because of a GET request for a password.txt, that got my attention
  
  <div><img width="206" alt="image" src="https://github.com/user-attachments/assets/fe2ba775-b453-4931-84a0-40ca2258c1a4" /></div>
<div>Answer: sbt123</div>

### 2. What is the version number of the attacker’s FTP server?
- Based on the previous question, we can infer that the device used to get the password.txt file is the attacker. Type in “ftp and ip.src == 192.168.56.1” in the display filter.
  
  <div><img width="509" alt="image" src="https://github.com/user-attachments/assets/3d9c4a8f-ca47-41a2-a9f1-5a63f7a79676" /></div>
  
- Checked the frame display section of packet 4243.
  <div><img width="250" alt="image" src="https://github.com/user-attachments/assets/aa657e9d-22de-46ef-b7b3-ab969b8419dc" /></div>
  
  <div>A quick google search on pyftpdlib shows that it is a python FTP server library.</div>
<div>Answer: 1.5.5</div>

### 3. Which port was used to gain access to the victim Windows host?
- I decided to look at all the traffic coming from the compromised host 192.168.56.1. Type in “ip.src == 192.168.56.1” in the display filter.
  <div><img width="511" alt="image" src="https://github.com/user-attachments/assets/ea1a7c6a-f876-4025-a3d8-43e7ae12d8cf" /></div>

- I analyzed the results and identified the HTTP traffic where the attacker downloaded the password.txt file. I then examined packet 4128, the first packet following the HTTP traffic.
  <div><img width="483" alt="image" src="https://github.com/user-attachments/assets/c336961a-3ba1-4735-ad8a-f4e0a7cb4d8f" /></div>
  
- I followed the TCP stream by right clicking the packet > Follow > TCP stream.
  <div><img width="275" alt="image" src="https://github.com/user-attachments/assets/f019652c-1351-4a37-a456-ff50feb8a13a" /></div>
  <div><img width="222" alt="image" src="https://github.com/user-attachments/assets/c0246d76-6e08-4842-b8af-f9b6b5b30ad3" /></div>
  <div><img width="211" alt="image" src="https://github.com/user-attachments/assets/0cc9264d-fe57-40aa-a99b-44804a40c881" /></div>
  <div>The attacker accessed the desktop, listed files, created a text file with commands for connecting to a server via anonymous FTP, and downloaded a binary named malware.exe.</div>

- Returned back to the main screen and looked for the destination port
  <div><img width="244" alt="image" src="https://github.com/user-attachments/assets/9fbe5f10-fc44-4b78-965c-3203641511b4" /></div>

<div>Answer: 8081</div>

### 4. What is the name of a confidential file on the Windows host?
- I followed the TCP stream of packet 4128.
- Checked the files in the Desktop directory and found a file called Employee_Information_CONFIDENTIAL.txt.

  <div><img width="283" alt="image" src="https://github.com/user-attachments/assets/73cdab71-6799-47cd-ae19-90e8d557e28d" /></div>
  
<div>Answer: Employee_Information_CONFIDENTIAL.txt</div>

### 5. What is the name of the log file that was created at 4:51 AM on the Windows host?
- Followed the TCP stream of packet 4128. A log file was created on 7/16/2019 at 4:51 AM called LogFile.log.
  
  <div><img width="199" alt="image" src="https://github.com/user-attachments/assets/3699a7e3-820b-4c78-a3b5-f179f2b2be83" /></div>

<div>Answer: LogFile.log</div>

