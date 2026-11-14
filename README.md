<div align="center">

#  PENETRATION TESTING REPORT
FOOTPRINTING & NETWORK SCANNING PHASES
W2-PM-FINAL | CYBERSECURITY |  NETWORKWALKS

</div>
**Building an isolated virtual lab for penetration testing and ethical hacking practice**


| <br>Pentester Name<br /> Cybersecurity Professional | Rajesh Kadim |
| :---: | :--- |
| Program/Batch | Networkwalks - B084 |
| Date | November 13, 2026 |
| Modules Completed | W2-PM1 (Multiple Kali Tools)W2-PM5 (Zenmap Scanning) |
| Client Target| 1. Networkwalks (secured written permission already)2. My own local LAN Network |
| Permission Secured | Yes |
| Phases Covered |Phase 1: Reconnaissance & Footprinting Phase 2: Scanning & Network Discovery Phase 3-5: In Progress |

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
| WHOIS                | Find domain registration details (owner, dates, name servers).   |
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
To obtain the IP address using the DNS I used nslookup which revealed 

<img width="1280" height="800" alt="nslookup networkwalks com" src="https://github.com/user-attachments/assets/59d09aa1-69e6-4665-93b2-07729d513c4e" />

To obtain the entry points of the domain I read the Http headers which leak the endpoints using the command curl -I.

<img width="1280" height="800" alt="curl -I networkwalks com" src="https://github.com/user-attachments/assets/1841d338-22ca-4694-8492-0b02cccfe1b2" />

To detect whether a web application firewall is protecting the site I used the command "wafw00f networkwalks.com". This told me if the site sits behind a firewall ModSecurity from SpiderLabs.

<img width="1280" height="800" alt="wafwoof networkwalks com" src="https://github.com/user-attachments/assets/097a0abc-fa67-4597-88ba-585612bd450f" />

To map the target's entire DNS footprint such as mail server and DNS software version I used the tool dnsrecon -d networkwalks.com. Each record from this result is a potential foothold that allowed me to understand the domains entire email and hosting setup.
<img width="1280" height="800" alt="dnsrecon" src="https://github.com/user-attachments/assets/26663b7f-ba4a-45ff-84a0-9a7d38ef5ee6" />

### 4.2 Network Scanning with Zenmap
To perform a network scan of my local network I used Zenmap which first required me to identify my local IP address and subnet using ipconfig command in Windows Command Prompt which revealed my local IP address to be 192.168.1.14 and my subnet mask 255.255.255.0.  

<img width="1104" height="637" alt="ipconfig" src="https://github.com/user-attachments/assets/1b0066cf-0721-461b-9552-c29c88d15f76" />
 This indicates my nmap address is 192.168.1.0/24 which revealed my local network has 10 hosts up.

 <img width="1920" height="1034" alt="nmap" src="https://github.com/user-attachments/assets/35bc1c7a-10da-47e8-8c9c-3601c57a1d0e" />


 

I first used the Windows ipconfig command to identify my local IP address and LAN subnet. I then entered the subnet into Zenmap and selected Ping Scan to identify active hosts.
The example results provided in the practical identified four live hosts:
•	10.0.0.1
•	10.0.0.4
•	10.0.0.19
•	10.0.0.5
The example results also included four MAC addresses.
After completing the scan, I opened the Topology section in Zenmap, enabled the legend and saved the network topology in PDF format as required by the practical task.


