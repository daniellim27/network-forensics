# Network Forensics Investigation Report

> **Case ID:** NF-20260105-001  
> **Investigator:** jonathanleewin  
> **Date:** January 5, 2026

## 📋 Project Overview

This repository contains a comprehensive network forensics investigation conducted on captured network traffic from a controlled laboratory environment. The investigation identified multiple attack vectors including SQL Injection, Cross-Site Scripting (XSS), Directory Traversal, and Command Injection attacks.

## 📁 Repository Contents

```
netfor/
├── capture_final.pcap       # Primary evidence file (916 KB)
├── capture_final.txt        # Text export of packet capture (13 MB)
├── capture_metadata.txt     # Capture session metadata
├── packet.csv              # Packet data in CSV format (454 KB)
├── report.tex              # LaTeX forensic report
├── makesure.md             # Investigation requirements & guidelines
└── README.md               # This file
```

## 🔍 Investigation Details

### Evidence Information

- **Evidence ID:** NF-20260105-001
- **File Name:** `capture_final.pcap`
- **File Size:** 896 KB
- **Packets Captured:** 3,487
- **Capture Duration:** 15 minutes (900 seconds)
- **Capture Method:** tcpdump on loopback interface
- **Integrity Hashes:**
  - **MD5:** `5d56ae74f1cf234e2843bdd289bf2928`
  - **SHA-256:** `9a8e2f4d7dfb244460ccabbbf86275c869cce5aaafe4aa22a7a7843246df737f`

### Technical Environment

- **OS:** Debian GNU/Linux 11 (Bullseye)
- **Kernel:** Linux 5.10.0-36-cloud-amd64
- **Platform:** Google Cloud Platform (GCP) - e2-medium instance
- **Services:**
  - Apache HTTP Server 2.4.x (Port 80)
  - vsftpd 3.x (Port 21)
- **Capture Time:** 2026-01-05 02:36:53 UTC to 02:51:53 UTC

## 🎯 Key Findings

### Attack Categories

| Attack Type | Count | Severity | Description |
|------------|-------|----------|-------------|
| SQL Injection | 7 | Critical | Authentication bypass, UNION SELECT, DROP TABLE attempts |
| Cross-Site Scripting (XSS) | 4 | High | Script tags, event handlers, SVG, iframe injection |
| Directory Traversal | 4 | High | /etc/passwd, /etc/shadow, Apache logs access |
| Command Injection | 2 | Critical | Command chaining via semicolon and pipe |
| Reconnaissance | Multiple | Medium | Directory enumeration, sensitive file probing |

### Attack Timeline

The attack consisted of 6 distinct phases over 15 minutes:

1. **Reconnaissance** (0:00 - 2:00) - Directory scanning and mapping
2. **Vulnerability Scanning** (2:00 - 4:00) - Endpoint probing
3. **SQL Injection** (4:00 - 8:00) - Database exploitation attempts
4. **XSS/Command Injection** (8:00 - 11:00) - Script and command injection
5. **Local File Inclusion** (11:00 - 13:00) - System file access attempts
6. **Persistence** (13:00 - 15:00) - Backdoor and FTP brute force

## 🛠️ Tools Used

- **Capture:** tcpdump 4.99.0
- **Analysis:** Wireshark
- **Documentation:** LaTeX (report.tex)
- **Data Processing:** CSV export for statistical analysis

## 📊 Analysis Workflow

### 1. Evidence Collection

```bash
sudo timeout 900 tcpdump -i lo -w ~/capture_final.pcap -v
```

### 2. Hash Verification

```bash
# MD5
md5sum capture_final.pcap

# SHA-256
sha256sum capture_final.pcap
```

### 3. Wireshark Analysis

Display filters used for attack detection:

```
# SQL Injection
http.request.uri contains "OR" or http.request.uri contains "UNION"

# Cross-Site Scripting
http.request.uri contains "script" or http.request.uri contains "alert"

# Directory Traversal
http.request.uri contains "../" or http.request.uri contains "etc/passwd"

# FTP Authentication
ftp.request.command == "USER" or ftp.request.command == "PASS"
```

### 4. Generate LaTeX Report

```bash
pdflatex report.tex
pdflatex report.tex  # Run twice for TOC
```

## 📖 Documentation

The complete forensic report is available in `report.tex` and includes:

- Executive Summary
- Case Information
- Technical Environment
- Methodology and Chain of Custody
- Detailed Attack Findings (17 documented attacks)
- Attack Timeline Reconstruction
- Impact Assessment
- Recommendations

For investigation requirements and guidelines, see `makesure.md`.

## 🔐 Chain of Custody

| Date/Time | Action | Person | Location | Hash Verified |
|-----------|--------|--------|----------|---------------|
| 2026-01-05 02:36:53 | Evidence Captured | jonathanleewin | forensics-lab (GCP) | N/A |
| 2026-01-05 02:39:46 | Hashes Generated | jonathanleewin | forensics-lab (GCP) | Initial |
| 2026-01-05 [TIME] | Analysis Commenced | jonathanleewin | Local Workstation | ✓ Verified |

## 📝 Compliance & Standards

This investigation follows:

- **RFC 3227** - Guidelines for Evidence Collection and Archiving
- **NIST SP 800-86** - Guide to Integrating Forensic Techniques into Incident Response
- **ISO/IEC 27037** - Guidelines for digital evidence preservation

## ⚠️ Legal Notice

**CONFIDENTIAL - FORENSIC EVIDENCE**

This repository contains forensic evidence collected for educational purposes only. All activities were performed on self-owned infrastructure with proper authorization. No third-party systems were accessed, and no personally identifiable information (PII) was compromised.

- Educational use only
- No malicious intent
- Following academic integrity policies
- Controlled test environment

## 🚀 Quick Start

### Prerequisites

- Wireshark or tshark for packet analysis
- LaTeX distribution (TeX Live, MiKTeX) for report compilation
- Basic understanding of network protocols (HTTP, FTP, TCP/IP)

### Analyzing the Capture

1. Open `capture_final.pcap` in Wireshark
2. Apply display filters (see Analysis Workflow above)
3. Review findings documented in `report.tex`
4. Cross-reference with `packet.csv` for statistical analysis

### Generating the Report

```bash
# Compile LaTeX report
pdflatex report.tex
pdflatex report.tex

# View the PDF
# Output: report.pdf
```

## 📚 Learning Resources

This investigation demonstrates:

- Packet capture techniques using tcpdump
- Network traffic analysis with Wireshark
- Identification of common web application attacks
- Proper forensic evidence handling and chain of custody
- Professional documentation and reporting

## 📧 Contact

**Investigator:** jonathanleewin  
**Location:** forensics-lab  
**Institution:** [Your Institution/Organization]

---

**Note:** This is an educational project demonstrating network forensics techniques in a controlled environment. All attacks were simulated for learning purposes.
