# Network Forensics Project - Complete Action Guide

## 🎯 Project Status

### ✅ What You've Completed
- Created GCP VM with Debian 11
- Installed Apache web server and vsftpd FTP server
- Generated realistic attack traffic (6 phases)
- Captured 15 minutes of network traffic
- Generated PCAP file: 3,487 packets (896KB)
- Created chain of custody documentation
- Generated MD5 and SHA256 hashes

### 📋 What You Need to Do Now

---

## Step 1: Download Your Evidence (5 minutes)

**On your LOCAL computer:**

```bash
gcloud compute scp forensics-lab:~/capture_final.pcap . --zone=asia-southeast2-a
gcloud compute scp forensics-lab:~/capture_metadata.txt . --zone=asia-southeast2-a
```

**Verify integrity:**
```bash
md5sum capture_final.pcap
# Should match: 5d56ae74f1cf234e2843bdd289bf2928

sha256sum capture_final.pcap  
# Should match: 9a8e2f4d7dfb244460ccabbbf86275c869cce5aaafe4aa22a7a7843246df737f
```

---

## Step 2: Install and Open Wireshark (10 minutes)

**Install Wireshark:**
- Windows: https://www.wireshark.org/download.html
- Mac: `brew install --cask wireshark`
- Linux: `sudo apt install wireshark`

**Open your PCAP:**
```bash
wireshark capture_final.pcap
```

---

## Step 3: Analyze in Wireshark (3-5 hours)

### Quick Start Analysis

**View capture statistics:**
1. Statistics → Capture File Properties (screenshot this)
2. Statistics → Protocol Hierarchy (screenshot this)
3. Statistics → Conversations (screenshot this)

### Find Attacks Using Filters

**SQL Injection:**
```
http.request.uri contains "OR" or http.request.uri contains "UNION"
```

**XSS:**
```
http.request.uri contains "script" or http.request.uri contains "alert"
```

**Directory Traversal:**
```
http.request.uri contains "../" or http.request.uri contains "etc/passwd"
```

**FTP Traffic:**
```
ftp
```

**All attacks:**
```
http.request.uri contains "OR" or http.request.uri contains "script" or http.request.uri contains "../"
```

### Document Each Finding

For each attack you find, record:
- Packet number (from Wireshark)
- Exact timestamp
- Source → Destination
- Full attack payload
- Take screenshot
- Explain what the attack does
- Explain potential impact

**Minimum: 8-10 different findings**

### Required Screenshots (15-20 total)

- [ ] Capture File Properties window
- [ ] Protocol Hierarchy
- [ ] Conversations view
- [ ] Timeline (Statistics → I/O Graph)
- [ ] SQL injection packet (list view)
- [ ] SQL injection (details expanded)
- [ ] SQL injection (Follow HTTP Stream)
- [ ] XSS packet
- [ ] Directory traversal packet
- [ ] FTP brute force (multiple packets visible)
- [ ] Each major finding (10+ screenshots)

---

## Step 4: Build Your Timeline (1-2 hours)

Create a chronological sequence:

```
Phase 1: Reconnaissance (Minutes 0-2)
- Timestamp: 02:36:53 - 02:38:53
- Activity: Directory scanning, file probing
- Packets: Approximately 1-250

Phase 2: Vulnerability Scanning (Minutes 2-4)  
- Timestamp: 02:38:53 - 02:40:53
- Activity: Testing for SQL, XSS, traversal
- Packets: Approximately 250-500

Phase 3: Exploitation (Minutes 4-8)
- Timestamp: 02:40:53 - 02:44:53  
- Activity: Active attacks deployed
- Packets: Approximately 500-1500

Phase 4: Privilege Escalation (Minutes 8-11)
- Timestamp: 02:44:53 - 02:47:53
- Activity: Admin access attempts
- Packets: Approximately 1500-2200

Phase 5: Data Exfiltration (Minutes 11-13)
- Timestamp: 02:47:53 - 02:49:53
- Activity: FTP brute force, file access
- Packets: Approximately 2200-3000

Phase 6: Persistence (Minutes 13-15)
- Timestamp: 02:49:53 - 02:51:53
- Activity: Backdoor attempts
- Packets: Approximately 3000-3487
```

---

## Step 5: Write Your Report (10-15 hours)

### Report Structure (30-40 pages)

**Section 1: Executive Summary (1 page)**
- Brief overview of incident
- Key findings summary
- Risk level assessment

**Section 2: Introduction (2-3 pages)**
- Case background
- Investigation objectives  
- System environment description

**Section 3: Methodology (3-4 pages)**
- Tools used (tcpdump, Wireshark)
- Investigation approach
- Chain of custody with hashes

**Section 4: Technical Environment (2 pages)**
- System specifications
- Network topology diagram
- Services running

**Section 5: Detailed Findings (15-20 pages)** ⭐ MOST IMPORTANT
- Finding #1: SQL Injection (2 pages with screenshot)
- Finding #2: Another SQL variant (2 pages)
- Finding #3: XSS attack (2 pages)
- Finding #4: Directory traversal (2 pages)
- Finding #5: FTP brute force (2 pages)
- Finding #6-10: Continue for all findings

**Each finding must include:**
- Packet number
- Timestamp
- Full payload/attack string
- Technical analysis
- Wireshark screenshot
- Potential impact
- Mitigation recommendation

**Section 6: Timeline (3-4 pages)**
- Chronological event reconstruction
- Visual timeline diagram
- Attack phase breakdown

**Section 7: Root Cause Analysis (2-3 pages)**
- Why vulnerabilities existed
- How attacker exploited them
- Security gaps identified

**Section 8: Impact Assessment (2 pages)**
- What could be compromised
- Business impact
- Data at risk

**Section 9: Recommendations (3-4 pages)**
- Immediate fixes
- Short-term improvements
- Long-term security strategy

**Section 10: Conclusion (1-2 pages)**
- Summary
- Final assessment

**Section 11: Appendices**
- Additional screenshots
- Hash values
- Tool versions

---

## Step 6: Create Presentation (2-3 hours)

### Presentation Outline (10-15 slides)

1. **Title Slide**
   - Project title
   - Your name
   - Date

2. **Executive Summary**
   - Quick overview
   - Key statistics

3. **Attack Scenario**
   - What happened
   - Timeline visual

4. **Technical Environment**
   - System diagram
   - Services involved

5-9. **Key Findings** (5 slides, one per top finding)
   - Attack type
   - Screenshot
   - Impact

10. **Timeline Visualization**
   - Visual timeline
   - 6 phases

11. **Impact Assessment**
   - What was affected
   - Severity

12. **Recommendations**
   - Top 3-5 recommendations

13. **Conclusion**
   - Summary
   - Lessons learned

14. **Q&A**

---

## Step 7: Final Checklist Before Submission

### Document Checklist
- [ ] Report is 30-40 pages
- [ ] All 4 required sections present (Intro, Methodology, Analysis, Conclusion)
- [ ] Minimum 8-10 findings documented
- [ ] Each finding has packet number, timestamp, screenshot
- [ ] Timeline reconstruction included
- [ ] Chain of custody documented
- [ ] Hashes included
- [ ] 15-20 screenshots included
- [ ] Professional formatting
- [ ] No spelling/grammar errors

### Presentation Checklist
- [ ] 10-15 slides created
- [ ] Key findings highlighted
- [ ] Timeline visual included
- [ ] Screenshots included
- [ ] Ready to present in Week 13

### Files to Submit
- [ ] Forensic report (DOC/DOCX)
- [ ] Presentation slides (PPT/PPTX)
- [ ] PCAP file (optional, check requirements)

---

## Grading Breakdown

| Component | Weight | How to Maximize |
|-----------|--------|-----------------|
| **PCAP Quality** | 20% | ✅ You have this - 3,487 packets with attacks |
| **Analysis Depth** | 30% | Find 10+ attacks, explain each thoroughly |
| **Report Quality** | 25% | 30-40 pages, professional, detailed |
| **Timeline** | 15% | Clear chronological reconstruction |
| **Presentation** | 10% | Clear, concise, well-designed |

---

## Time Estimate

| Task | Time Needed |
|------|-------------|
| Download files | 5 minutes |
| Install Wireshark | 10 minutes |
| Analyze PCAP | 3-5 hours |
| Take screenshots | 1 hour |
| Build timeline | 1-2 hours |
| Write report | 10-15 hours |
| Create presentation | 2-3 hours |
| Review & polish | 2-3 hours |
| **TOTAL** | **20-30 hours** |

**Recommended schedule:** 2-3 hours per day over 10 days

---

## Quick Reference: Your Evidence Details

```
File: capture_final.pcap
Size: 896KB
Packets: 3,487
HTTP: 2,414 packets (69%)
FTP: 520 packets (15%)
Duration: 15 minutes
MD5: 5d56ae74f1cf234e2843bdd289bf2928
SHA256: 9a8e2f4d7dfb244460ccabbbf86275c869cce5aaafe4aa22a7a7843246df737f
```

---

## Important Reminders

✅ **Your capture is PERFECT** - Don't recapture!
✅ **Quality > Quantity** - 3,487 packets with clear attacks is excellent
✅ **Focus on analysis** - This is where grades are earned
✅ **Professional presentation** - Format matters
✅ **Due date:** December 19, 2025

---

## Need Help?

**Stuck on Wireshark?** Use the display filters above
**Can't find attacks?** They're there - use: `http.request.uri contains "OR"`
**Report too short?** Expand each finding to 2 pages with detailed analysis
**Timeline confusing?** Use the 6-phase breakdown provided

---

**You have everything you need! The technical work is DONE. Now it's just analysis and documentation!** 📝

**Good luck! You've got this!** 🎯#   n e t w o r k - f o r e n s i c s  
 #   n e t w o r k - f o r e n s i c s  
 