# NETWORKWALKS CYBERSECURITY INTERNSHIP — BATCH B084

# WEEK 2: FOOTPRINTING, RECONNAISSANCE & NETWORK SCANNING REPORT

**Prepared by:** Samuel Miracle
**Programme:** NetworkWalks Cybersecurity Internship
**Batch:** B084
**Practical Exercises:** W2-PM1 and W2-PM5

---

## 1. LIABILITY DISCLAIMER

This report documents practical cybersecurity exercises carried out as part of the NetworkWalks Cybersecurity Internship.

The activities were conducted for educational purposes and within the intended testing scope. Domain reconnaissance was directed at the specified training target, while network discovery was performed on my local network.

All findings and observations presented in this report are based on the practical activities and evidence collected. The results should not be interpreted as confirmation of vulnerabilities unless independently verified.

## 2. INTRODUCTION

Footprinting, reconnaissance, and network scanning are important stages of a cybersecurity assessment. They help security professionals gather information about a target, identify exposed technologies, understand network configurations, and discover active devices.

This week's practical exercises focused on two areas:

- **W2-PM1 – Multiple Kali Linux Tools:** Using different reconnaissance tools to gather domain information, identify web technologies, inspect HTTP headers, and perform DNS enumeration.
- **W2-PM5 – Network Scanning with Zenmap:** Discovering devices on a local network, verifying active hosts, identifying available MAC address information, and inspecting network topology.

The exercises provided hands-on experience with commonly used cybersecurity tools and techniques.

## 3. TOOLS USED

| Tool                   | Purpose                                  |
| ---------------------- | ---------------------------------------- |
| Kali Linux             | Testing environment                      |
| WHOIS                  | Domain registration information          |
| WhatWeb                | Web technology identification            |
| Nslookup               | DNS information gathering                |
| cURL                   | HTTP response header inspection          |
| WAFW00F                | Web Application Firewall detection       |
| DNSRecon               | DNS enumeration                          |
| Zenmap                 | Graphical network scanning interface     |
| Nmap                   | Network discovery and scanning           |
| Windows Command Prompt | Network configuration and ARP inspection |

## 4. ACTIVITIES PERFORMED

### 4.1 FOOTPRINTING & RECONNAISSANCE (W2-PM1)

**Target Domain:** `networkwalks.com`

The following tools were used to gather information about the specified domain.

#### 4.1.1 WHOIS networkwalks.com

**Command:**

```bash
whois networkwalks.com
```

**Purpose:** Retrieve available domain registration information.

**Evidence – WHOIS&#x20;**&#x6E;etworkwalks.com



*Insert WHOIS screenshot here.*

#### 4.1.2 Web Technology Identification

**Command:**

```bash
whatweb https://networkwalks.com
```

**Purpose:** Identify technologies and web components exposed by the website.

**Evidence – WhatWeb**



*Insert WhatWeb screenshot here.*

#### 4.1.3 DNS Lookup

**Command:**

```bash
nslookup networkwalks.com
```

**Purpose:** Query DNS and retrieve available name resolution information.

**Evidence – Nslookup**



*Insert Nslookup screenshot here.*

#### 4.1.4 HTTP Response Header Inspection

**Command:**

```bash
curl -I https://networkwalks.com
```

**Purpose:** Retrieve HTTP response headers and inspect information returned by the web server.

**Evidence – curl -I**



*Insert cURL screenshot here.*

#### 4.1.5 Web Application Firewall Detection

**Command:**

```bash
wafw00f https://networkwalks.com
```

**Purpose:** Check for indications of Web Application Firewall protection.

**Evidence – WAFW00F**



*Insert WAFW00F screenshot here.*

#### 4.1.6 DNS Enumeration

**Command:**

```bash
dnsrecon -d networkwalks.com
```

**Purpose:** Gather additional DNS-related information about the specified domain.

**Evidence – dnsrecon -d**



*Insert DNSRecon screenshot here.*

**Observations:**

The tools provided different perspectives on the target domain, including registration information, web technology fingerprints, DNS records, HTTP response headers, and possible WAF identification.

The actual outputs and findings will be interpreted based on the collected evidence.

### 4.2 NETWORK SCANNING WITH ZENMAP (W2-PM5)

**Objective:** Discover devices on my local network, verify their availability, inspect IP-to-MAC address information, and examine network topology.

#### 4.2.1 Local Network Configuration

I used the Windows Command Prompt to identify my local network configuration.

**Command:**

```cmd
ipconfig
```

**Network Details:**

| Parameter          | Value             |
| ------------------ | ----------------- |
| Local IPv4 Address | `192.168.34.115`  |
| Subnet Mask        | `255.255.255.0`   |
| Default Gateway    | `192.168.34.148`  |
| Network Range      | `192.168.34.0/24` |

#### 4.2.2 Initial Network Discovery

I opened Zenmap, selected the **Ping Scan** profile, and entered my local network range.

**Command:**

```bash
nmap -sn 192.168.34.0/24
```

The initial scan reported 256 hosts as up. However, further verification did not establish that 256 individual devices were active. Therefore, this result was treated as inconclusive.

#### 4.2.3 Individual Host Verification

To verify the known devices, I performed individual scans.

**Default Gateway:**

```bash
nmap -sn 192.168.34.148
```

**Result:** Host reported as up.

**Evidence – Gateway Scan**



*Insert gateway scan screenshot here.*

**Local Windows Computer:**

```bash
nmap -sn 192.168.34.115
```

**Result:** Host reported as up.

**Evidence – Local Computer Scan**



*Insert local computer scan screenshot here.*

#### 4.2.4 Combined Host Discovery

I performed a combined scan against both verified IP addresses.

**Command:**

```bash
nmap -sn 192.168.34.115 192.168.34.148
```

Both hosts were reported as up and appeared in the Zenmap Hosts tab.

| IP Address       | Device                 | Status |
| ---------------- | ---------------------- | ------ |
| `192.168.34.115` | Local Windows computer | Up     |
| `192.168.34.148` | Default gateway        | Up     |

**Evidence – Combined Scan**



*Insert combined Hosts tab screenshot here.*

#### 4.2.5 MAC Address Identification

I used the following command to inspect the local ARP table.

**Command:**

```cmd
arp -a
```

The output contained the following dynamic entry:

| IP Address       | MAC Address         | Type    |
| ---------------- | ------------------- | ------- |
| `192.168.34.148` | `7e-2b-88-8b-02-51` | Dynamic |

This identified the MAC address associated with the default gateway in the local ARP table.

**Evidence – ARP Table**



*Insert ARP table screenshot here.*

#### 4.2.6 Network Topology Inspection

I inspected the Topology tab in Zenmap after performing the scans. However, both verified devices were not displayed together in the topology visualization.

The following simplified diagram represents the two verified devices and their network context. It is not a complete physical network map.

```text
             LOCAL NETWORK
            192.168.34.0/24
                    |
             DEFAULT GATEWAY
              192.168.34.148
                    |
             LOCAL COMPUTER
              192.168.34.115
```

**Evidence – Zenmap Topology View**



*Insert Zenmap topology screenshot here.*

The combined scan was also saved in XML format for record keeping.

**Saved file:** `W2-PM5-combined-scan.xml`

## 5. RISK ANALYSIS / IMPACT

The practical exercises demonstrated how reconnaissance and network discovery can support an initial security assessment.

Key observations include:

- Domain registration and DNS information can reveal publicly available infrastructure details.
- Technology fingerprinting can help identify the technologies exposed by a website.
- HTTP response headers can provide useful information about server configuration.
- WAF detection can indicate the presence of web application protection mechanisms.
- Network discovery and ARP inspection can help identify devices and their network information.

The initial network scan produced an anomalous result of 256 hosts reported as up. Further verification confirmed two specific hosts, so the initial count was not treated as a reliable device count.

No exploitable vulnerability is claimed solely from these discovery activities.

## 6. RECOMMENDATIONS

Based on the exercises, the following general security recommendations are relevant:

1. Periodically review publicly exposed domain and DNS information.
2. Keep web technologies and server software updated.
3. Configure appropriate HTTP security headers.
4. Deploy and maintain suitable web application protection mechanisms.
5. Avoid unnecessary exposure of infrastructure information.
6. Maintain an accurate inventory of devices connected to local networks.
7. Validate network scan results before reporting findings.
8. Conduct security assessments only within authorised testing scopes.

## 7. CONCLUSION

The Week 2 practical exercises provided hands-on experience in footprinting, reconnaissance, and local network discovery.

Using Kali Linux utilities, I explored different methods of gathering domain-related information, identifying web technologies, inspecting HTTP headers, and examining DNS information.

Using Zenmap and Nmap, I identified my local network range, performed host discovery, verified two devices, inspected the ARP table, and saved the combined scan results.

The exercises reinforced the importance of selecting appropriate tools, interpreting their outputs carefully, and validating findings before documenting them in a cybersecurity assessment.

## 8. EVIDENCES COLLECTED

All screenshots and supporting files are organised under the repository's `evidence/` directory.

### W2-PM1 – Footprinting & Reconnaissance

| No. | Evidence              | Screenshot                              |
| --- | --------------------- | --------------------------------------- |
| 01  | WHOIS lookup          | [View](evidence/W2-PM1/01-whois.png)    |
| 02  | WhatWeb scan          | [View](evidence/W2-PM1/02-whatweb.png)  |
| 03  | Nslookup results      | [View](evidence/W2-PM1/03-nslookup.png) |
| 04  | cURL response headers | [View](evidence/W2-PM1/04-curl.png)     |
| 05  | WAFW00F results       | [View](evidence/W2-PM1/05-wafw00f.png)  |
| 06  | DNSRecon results      | [View](evidence/W2-PM1/06-dnsrecon.png) |

### W2-PM5 – Network Scanning with Zenmap

| No. | Evidence            | Screenshot / File                                     |
| --- | ------------------- | ----------------------------------------------------- |
| 07  | Gateway scan        | [View](evidence/W2-PM5/07-zenmap-gateway-scan.png)    |
| 08  | Local computer scan | [View](evidence/W2-PM5/08-zenmap-local-host-scan.png) |
| 09  | ARP table           | [View](evidence/W2-PM5/09-arp-mac-address.png)        |
| 10  | Initial topology    | [View](evidence/W2-PM5/10-zenmap-topology.png)        |
| 11  | Combined Hosts tab  | [View](evidence/W2-PM5/11-zenmap-combined-hosts.png)  |
| 12  | Saved scan results  | [View](evidence/W2-PM5/W2-PM5-combined-scan.xml)      |

---

**Prepared by:** Samuel Miracle
**NetworkWalks Cybersecurity Internship — Batch B084**

*Learning through practical exercises, documenting findings, and building cybersecurity skills.*
