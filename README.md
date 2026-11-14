<div align="center">

#  PENETRATION TESTING REPORT
FOOTPRINTING & NETWORK SCANNING PHASES
W2-PM-FINAL | CYBERSECURITY |  NETWORKWALKS

</div>

| <br>Pentester Name<br /> Cybersecurity Professional | Rajesh Kadim |
| :---: | :--- |
| Program/Batch | Networkwalks - B084 |
| Date | November 14, 2026 |
| Modules Completed |  W2-PM1 (Multiple Kali Tools) <br>W2-PM5 (Zenmap Scanning) <br />|
| Client Target| 1. Networkwalks (secured written permission already) <br> 2. My own local LAN Network |
| Permission Secured | Yes |
| Phases Covered |Phase 1: Reconnaissance & Footprinting  <br> Phase 2: Scanning & Network Discovery <br>Phase 3-5: In Progress <br />|

## 1. Liability Disclaimer
The activities performed on these devices were performed with secured written permission using my own permitted devices. Please do not repeat any of the steps below without written permission as unauthorized access can lead to criminal charges.

## 2. Introduction
Reconnaissance which is also called as footprinting is the first step to any attack. Before touching a target, an attacker quietly collects as much public information about the target as possible. This report covers footprinting of the domain networkwalks.com using Kali Linux tools whois, whatweb, nslookup, curl -l, wafw00f, dnsrecon and scanning my own network with Zenmap.

## 3. Tools Used
The table below lists each tool used in this report and its purpose.
<div align="center">

| **Tool**             | **Purpose**                                                      |
| -------------------- | ---------------------------------------------------------------- |
| Kali Linux & Windows | Operating systems used for reconnaissance activities             |
| whois                | Find domain registration details (owner, dates, name servers).   |
| whatweb              | Fingerprint web technologies (server, CMS, plugins, IP).         |
| nslookup             | Resolve the domain name to its IP address using DNS.             |
| curl -I              | Read the HTTP response headers of the website.                   |
| wafw00f              | Detect whether a Web Application Firewall protects the site.     |
| dnsrecon             | Enumerate all DNS records (NS, MX, SPF, TXT, SRV).               |
| Zenmap (Nmap GUI)    | Scan the local subnet to find live hosts, IPs and MAC addresses. |
| Windows CMD          | Local IP and MAC address identification                          |
</div>

## 4. Activities Performed
### 4.1 Footprinting & Reconnaissance

I performed reconnaissance against the networkwalks.com domain using six Kali Linux tools namely whois, whatweb, nslookup, curl -I, wafw00f and dnsrecon. 

To obtain the registration details of the domain I used the Linux tool whois which gave me details such as when it was created, who is the domains registrar,  where it is located, etc.

<img width="1280" height="800" alt="whois networkwalks com" src="https://github.com/user-attachments/assets/406ee397-af3d-41c9-b44a-d719e83b42d6" />

Next to find out what type of software and version the domain uses I performed the command $whatweb networkwalks.com on Kali Linux. I found out the domain's Http Server runs on Apache, it uses Bootstrap[7.1.4]
, and WordPress[7.1.4] to name a few.
<img width="1280" height="800" alt="whatweb networkwalks com" src="https://github.com/user-attachments/assets/f6ec47f3-e5cb-4551-9493-469e0d05d2fa" />
To obtain the IP address using the DNS I used nslookup which it revealed. 

<img width="1280" height="800" alt="nslookup networkwalks com" src="https://github.com/user-attachments/assets/59d09aa1-69e6-4665-93b2-07729d513c4e" />

To obtain the entry points of the domain I read the Http headers which leak the endpoints using the command curl -I.

<img width="1280" height="800" alt="curl -I networkwalks com" src="https://github.com/user-attachments/assets/1841d338-22ca-4694-8492-0b02cccfe1b2" />

To detect whether a web application firewall is protecting the site I used the command "wafw00f networkwalks.com". This told me the site sits behind a firewall ModSecurity from SpiderLabs.

<img width="1280" height="800" alt="wafwoof networkwalks com" src="https://github.com/user-attachments/assets/097a0abc-fa67-4597-88ba-585612bd450f" />

To map the target's entire DNS footprint such as mail server and DNS software version I used the tool dnsrecon -d networkwalks.com. Each record from this result is a potential foothold that allowed me to understand the domains entire email and hosting setup.
<img width="1280" height="800" alt="dnsrecon" src="https://github.com/user-attachments/assets/26663b7f-ba4a-45ff-84a0-9a7d38ef5ee6" />

### 4.2 Network Scanning with Zenmap
To perform a network scan of my local network I used Zenmap which first required me to identify my local IP address and subnet using ipconfig command in Windows Command Prompt which revealed my local IP address to be 192.168.1.14 and my subnet mask 255.255.255.0.  

<img width="1104" height="637" alt="ipconfig" src="https://github.com/user-attachments/assets/1b0066cf-0721-461b-9552-c29c88d15f76" />
 This indicates my nmap address is 192.168.1.0/24 with Ping scan which revealed my local network has 10 hosts up.

 <img width="1920" height="1034" alt="nmap" src="https://github.com/user-attachments/assets/35bc1c7a-10da-47e8-8c9c-3601c57a1d0e" />

This resulted in providing ten live hosts with a IP addresses:

•	192.168.1.1
<br>•	192.168.1.3
<br>•	192.168.1.4
<br>•	192.168.1.5
<br>•	192.168.1.6
<br>•	192.168.1.7
<br>•	192.168.1.9
<br>•	192.168.1.10
<br>•	192.168.1.11
<br>•	192.168.1.14

After completing the scan, I opened the Topology section in Zenmap, enabled the legend and saved the network topology in PDF format as required by the practical task.

<img width="1920" height="993" alt="Topology" src="https://github.com/user-attachments/assets/f93c6a02-4baf-4c86-9ee7-7ac66c4384c1" />


[nmap topology .pdf](https://github.com/user-attachments/files/34843043/nmap.topology.pdf)

## 5. Risk Analysis
Based on what I observed during the footprinting and network scanning I identified the following potential risks. When performing reconnaissance using six Kali Linux tools, I found that the "whois" tool shows complete registration details of a domain, which attackers can use to create a similar-looking fraudulent site. The "whatweb" tool reveals the exact software version, allowing attackers to find vulnerabilities and gain access. The "nslookup" tool provides the site's actual IP address, highlighting other domains that might have weak points. The "curl -I" tool shows endpoints for information access. The "wafw00f" tool identifies the firewall software, which attackers can try to bypass. Lastly, "dnsrecon" reveals the domain's structure. While gaining this information is possible, actual access still requires significant effort. The recommendation is to stay alert about vulnerabilities and keep security updates current.

## 6. Conclusion
During Week 2 of my Cybersecurity & Ethical Hacking internship, I engaged in practical activities focused on footprinting, reconnaissance, and network scanning. I utilized six Kali Linux tools to gather domain information, including whois, whatweb, nslookup, curl -I, wafw00f, and dnsrecon. Using Zenmap, I identified my local network setup and discovered active hosts, gathering IP and MAC addresses to create a network topology. This experience highlighted the importance of information gathering in cybersecurity and the need for clear documentation in reports. Furthermore, I learned that such activities should always be conducted within an authorized scope.

