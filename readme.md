# CanaryHunter Package
- CanaryHunter to detect canaries, scan the network stealthily, and identify traffic, callbacks, and tripwires, including in ports.
- Network File Share Scanner to detect tripwires in network shares.

# NG-CanaryHunter 
- It is an advanced assessment network scanning tool designed for security professionals to detect and interact with canary devices, such as Thinkst Canary and T-Pot while minimizing the risk of detection.

# Features of NG-CanaryHunter 
- Advanced Scanning Techniques: Utilizes sophisticated methods like IPv6 extension header scans, custom payload TCP scans, fingerprinting, timing analysis, and protocol anomaly detection.
- Stealth Mode: Operates in an invisible mode using encrypted payloads to blend with legitimate traffic, reducing the chances of detection.
- Flexible Targeting: Supports single IPs, CIDR notation, multiple IPs, and domain resolution.
- Harmless Simulation: Includes a harmless mode to simulate benign user behavior.
- Hunting Capabilities: Option to hunt for secrets and tripwires after detection.

# Scanning Detection of Canary as Preliminary Step
- NG-CanaryHunter uses very unsual method to scan and generate legitimate network traffic.
- NG-CanaryHunter provides security professionals with a powerful and discreet tool for identifying security traps and tripwires in a network.
- Its advanced techniques and stealth capabilities ensure thorough and undetected security assessments, enhancing the overall security posture.

# Algorithms to Deafeat Canaries such as Thinkst Canary and T-Pot
- Dynamic Payload Generation: Use more complex, dynamically changing payloads that are less likely to be fingerprinted by defensive systems.
- Random Timing Delays: Introduce random timing delays between packet sends to mimic human behavior and evade rate-based detection systems.
- Packet Fragmentation: Use packet fragmentation to sneak past simple packet inspection systems that do not properly reassemble packets.
- Polymorphic Code: Change the code structure dynamically, making the scanning activity harder to detect via static signatures.
- Protocol Obfuscation: Implement techniques to modify protocol headers in ways that are still compliant but might confuse security devices.
- Stealth by Confusion: Use decoy traffic that appears legitimate to distract from the scanning activities.
- Encrypted Payloads: Fernet encryption before sending which Uses the cryptography library to generate a key and encrypt the payloads

# Invisible Method with --invisible flag
- Canary devices may not directly process encrypted payloads because they are designed to detect and respond to specific patterns in traffic. When payloads are encrypted, the canary device cannot easily analyze them, making it less likely to detect the scan. Therefore, using encrypted payloads can help in remaining undetected, which is why it is termed "invisible."

# More Information on Invisible Mode
- Invisible mode encrypts the payloads using a unique key, making them difficult for canary devices to analyze. By encrypting the traffic, the scan appears as harmless or regular encrypted communication, reducing the likelihood of detection. This stealth technique ensures that the payloads are only interpretable by the intended operating system, not by the security traps.

# Finding Tokens and Confirming Tripwires for T-Pot and Thinkst Canary:
- The script sends special messages (payloads) to the target computer to see how it reacts.
- It uses methods to send these messages and look for specific responses that indicate a token or tripwire.
- It looks for patterns in the responses that match common token formats using regex (a tool for finding patterns in text).
- Any detected tokens or unusual responses are saved in a database to keep a record.
- The hunt_for_secrets function sends specific requests to find hidden secrets or tokens on the target.

# Sending Spoofed Requests to Appear Outside the Network for T-Pot and Thinkst Canary:
- The script can send messages that look like they come from a different computer.
- It creates a packet with a fake source IP address and sends it to the target.
- This makes the message appear as if it is coming from outside the network, which can trick the target into thinking it is being attacked from a different location.

# Stealth Promiscuous Mode 
- It aims to enable packet sniffing while minimizing the likelihood of detection by canary devices. 
- Selective Filtering: Instead of capturing all packets, apply filters to capture only specific traffic (e.g., TCP packets on certain ports like 80 and 443). This reduces the volume of captured traffic and makes the monitoring less obvious.
- Randomized Intervals: Capture packets at randomized intervals rather than continuously. This reduces the chance of the monitoring pattern being detected.
Stealthy Packet Handling: Avoid sending out packets that might be used to detect the presence of promiscuous mode. This includes avoiding ARP requests or any other traffic that might be generated by the network interface in response to received packets.
- Reduced Network Footprint: Keep the network interface's interaction with the network minimal. This can include not responding to broadcasts or other typical network traffic that might indicate the presence of an active network interface.
- Network Timing and Response: By carefully timing the sniffing sessions and limiting the duration and volume of captured traffic, the script minimizes the network footprint, making it harder for canary devices to detect the presence of a monitoring interface.
- Handling Stealthy Packet Analysis: The script uses a callback function packet_callback to process packets in real-time. This avoids storing large volumes of captured data, further reducing the likelihood of detection.

# Hunting for Secrets
- It hunt_for_secrets function to sniff network traffic and detect tokens and secrets with an option for stealth mode.

# Changing OSI to defeat Canary
- Dynamic OSI Layer Manipulation:
The script auto-detects the best OSI layer (Layer 3 or 7) for stealth operations.

# Old School Scripts to Next Level Performance
- Run custom tools such as nikto.pl and pass it's payload fully encrypted and advance format to reach the target, bypassing Canaries.
 - You can run any custom tool with this script

# Usage
```bash
sudo python NG-CanaryHunter.py --target_ip <target_ip> --methods <method1> <method2> --invisible --hunt
```

# Polymorpic Decoy
```bash
sudo python NG-CanaryHunter.py --target_ip 192.168.1.10 --methods polymorphic decoy --hunt
```

# The Great Invisible Hunt
```bash
python script.py --target_ip 192.168.1.10 --methods obfuscation --invisible --hunt
```

# Output
```bash
$ python ng-canaryhunter.py --target_ip 192.168.1.11 --methods ipv6 custom_payload fingerprinting timing protocol non_standard_ports --hunt --invisible --interface eth0 --crawl --tripwire --stealth --customtool /home/haroon/Downloads/nikto.pl --spoofip 192.168.1.1 --auto_osi


Starting canary detection phase...
IPv6 Extension Header Scan on 192.168.1.11
Sent IPv6 Extension Header Scan to 192.168.1.11
Sent Custom Payload TCP Scan to 192.168.1.11:80
Possible canary device detected at 192.168.1.11 (Fingerprint: TTL=50, Window=8192)
High latency detected (1.5 seconds), 192.168.1.11 may be a canary device
Protocol anomaly detected in 192.168.1.11's response
Response from 192.168.1.11 on non-standard port 9999, potential canary device
Detected token: http://canarytokens.org/unique-token
Detected secret: secret_key=abc123

Using dynamic OSI layer manipulation and encrypted payloads to enhance custom tool performance...

Starting custom tool scan using /home/haroon/Downloads/nikto.pl on 192.168.1.11:80 with spoofed IP 192.168.1.1
Auto-detected best OSI layer: Layer 7 (Application Layer)
- Nikto v2.1.6
---------------------------------------------------------------------------
+ Target IP:          192.168.1.11
+ Target Hostname:    haroontesterserver
+ Target Port:        80
+ Start Time:         2024-08-07 16:00:00
---------------------------------------------------------------------------
+ Server: Apache/2.4.41 (Ubuntu)
+ The X-XSS-Protection header is not defined. This header can hint to the user-agent to protect against some forms of XSS.
+ Uncommon header 'x-backend-server' found, with contents: haroontesterserver
+ Allowed HTTP Methods: GET, HEAD, POST, OPTIONS 
+ OSVDB-3092: /admin: This might be interesting...
+ OSVDB-3092: /phpmyadmin: This might be interesting...
+ OSVDB-3268: /phpMyAdmin/scripts/setup.php: phpMyAdmin setup script found.
+ 100 requests: 0 error(s) and 4 item(s) reported on remote host
+ End Time:           2024-08-07 16:02:00 (120 seconds)
---------------------------------------------------------------------------
Scan completed with enhanced stealth techniques: Layer 7 manipulation, encrypted payloads, and randomized options.

```

# Bonus - Network File Share Scanner for Canary
- Use network_scanner_canary.py to identify which machine is the canary and how much share access, such as tokens or tripwires, is implemented.
- Identify the tripwires.
- Use a public-facing IP with spoofing.
- Enjoy your legitimate presence in the network.

# Thinkst Canary and T-Pot
- Included SMB Callpacket Packets to detect tripwires
- Include MD5 and SHA1 remote detection method to detect tripwires

# Sample Usage
Normal Scan Without Spoofing or Normal User Simulation
sudo python network_scanner_canary.py -s 192.168.1.0/24 -m normal

# Stealth Scan with Spoofing Enabled
sudo python network_scanner_canary.py -s 192.168.1.0/24 -m stealth --spoof

# Stealth Scan with Normal User Simulation
sudopython network_scanner_canary.py -s 192.168.1.0/24 -m stealth --normal-user

# Stealth Scan with Both Spoofing and Normal User Simulation
sudo python network_scanner_canary.py -s 192.168.1.0/24 -m stealth --spoof --normal-user

# Stealth Scan with Spoofing from a Custom IP Address
sudo python network_scanner_canary.py -s 192.168.1.0/24 -m stealth --spoof --spoof-ip 203.0.113.5


``` bash
Sample Output: Normal Scan Without Spoofing or Normal User Simulation
Scanning subnet: 192.168.1.0/24 in normal mode with spoofing disabled
Simulated normal user activity from \\192.168.1.5\finance\safe_file.txt
Simulated normal user activity from \\192.168.1.6\tripwire\safe_file.txt
Simulated normal user activity from \\192.168.1.7\engineering\safe_file.txt
...
Canary token detected in \\192.168.1.5\finance\token.txt
Canary token detected in \\192.168.1.6\tripwire\alert.log
...

Stealth Scan with Spoofing Enabled
Scanning subnet: 192.168.1.0/24 in stealth mode with spoofing enabled
Spoofing IP: 192.168.1.100 to access 192.168.1.5
Spoofing IP: 192.168.1.101 to access 192.168.1.6
Spoofing IP: 192.168.1.102 to access 192.168.1.7
...
Canary token detected in \\192.168.1.5\finance\token.txt
Canary token detected in \\192.168.1.6\tripwire\alert.log
...

Stealth Scan with Normal User Simulation
Scanning subnet: 192.168.1.0/24 in stealth mode with spoofing disabled
Simulated normal user activity from \\192.168.1.5\finance\safe_file.txt
Simulated normal user activity from \\192.168.1.6\tripwire\safe_file.txt
Simulated normal user activity from \\192.168.1.7\engineering\safe_file.txt
...
Canary token detected in \\192.168.1.5\finance\token.txt
Canary token detected in \\192.168.1.6\tripwire\alert.log
...

Stealth Scan with Both Spoofing and Normal User Simulation
Scanning subnet: 192.168.1.0/24 in stealth mode with spoofing enabled
Spoofing IP: 192.168.1.100 to access 192.168.1.5
Simulated normal user activity from \\192.168.1.5\finance\safe_file.txt
Spoofing IP: 192.168.1.101 to access 192.168.1.6
Simulated normal user activity from \\192.168.1.6\tripwire\safe_file.txt
Spoofing IP: 192.168.1.102 to access 192.168.1.7
Simulated normal user activity from \\192.168.1.7\engineering\safe_file.txt
...
Canary token detected in \\192.168.1.5\finance\token.txt
Canary token detected in \\192.168.1.6\tripwire\alert.log
...

Scanning subnet: 192.168.1.0/24 in stealth mode with spoofing enabled
Spoofing IP: 203.0.113.5 to access 192.168.1.5
Simulated normal user activity: accessed \\192.168.1.5\finance\quarterly_report.xlsx
Spoofing IP: 203.0.113.5 to access 192.168.1.6
Simulated normal user activity: accessed \\192.168.1.6\tripwire\system_logs.log
Spoofing IP: 203.0.113.5 to access 192.168.1.7
Simulated normal user activity: accessed \\192.168.1.7\engineering\design_specifications.docx
...
Canary token detected in \\192.168.1.5\finance\token.txt
Canary token detected in \\192.168.1.6\tripwire\alert.log
...
```


# Company
Cyber Zeus

# Contact
Haroon Ahmad Awan

# Email
haroon@cyberzeus.pk
