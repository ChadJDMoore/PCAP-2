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

## Steps
### 1. What is the WebAdmin password?
- Typed in http in display filter, to check HTTP traffic
  
  <div><img width="510" alt="image" src="https://github.com/user-attachments/assets/7915f345-8ff7-4258-ad56-be967d3784b6" /></div>
- Right click on packet 4121 > followed HTTP stream, because of a GET request for a password.txt, that got my attention
  
  <div><img width="206" alt="image" src="https://github.com/user-attachments/assets/fe2ba775-b453-4931-84a0-40ca2258c1a4" /></div>
<div>Answer: sbt123</div>

### 2. What is the IP address of the host that was pinged twice?
- Type icmp on the display filter.
  <div><img width="374" alt="image" src="https://github.com/user-attachments/assets/5fdffdb2-99d4-4b1c-9041-91679e74c2b5" /></div>
<div>We can see two ping requests that were sent to 8.8.4.4.</div>
<div>Answer: 8.8.4.4</div>

### 3. How many DNS query response packets were captured?
- Type dns in the display filter. Select the first packet that says “standard query response.”
  <div><img width="511" alt="image" src="https://github.com/user-attachments/assets/67e727c3-6ff2-4e0c-9e9f-685ae94b979f" /></div>

- Go to the frame display on the lower left-hand side of wireshark. Click on Domain Name System > Flags > Right click the entry that says “response: message is a response” > apply as filter > selected.
  <div><img width="253" alt="image" src="https://github.com/user-attachments/assets/14d28c35-c446-482e-8104-8e1ae1e7fbff" /></div>
  
- Check the displayed packets in the lower right-hand side of wireshark. Look for the number next to "Displayed"
  <div><img width="254" alt="image" src="https://github.com/user-attachments/assets/6f6a9683-f812-4f70-bb48-b14d82081f40" /></div>

<div>Answer: 90</div>

### 4. What is the IP address of the host which sent the most number of bytes?
- Go to Statistics > Endpoints > IPv4 > click Tx Bytes (transmit bytes) to display the results in descending order.
  
  <div><img width="374" alt="image" src="https://github.com/user-attachments/assets/1b0c5dc2-24e0-4f6d-b869-dc13e1f9371b" /></div>
  
<div>Answer: 115.178.9.18</div>

