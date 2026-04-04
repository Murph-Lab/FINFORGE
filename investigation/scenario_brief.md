# Scenario Brief — FINFORGE Investigation

## Case Reference
**Case ID:** FINFORGE-001  
**Date of Brief:** April 2026  
**Analyst:** Thomas Murphy  
**Status:** Active Investigation

---

## Fictional Organization

**Firm:** Hargrove Wealth Partners  
**Industry:** Wealth Management / Private Client Advisory  
**Size:** Mid-size regional firm, approximately 120 employees  
**Description:** Hargrove Wealth Partners provides investment advisory, portfolio management, and financial planning services to high-net-worth individuals and small institutional clients. The firm maintains strict confidentiality obligations with all clients under its advisory agreements.

---

## Suspect Profile

**Name:** Daniel Forsythe (fictional)  
**Title:** Senior Portfolio Analyst  
**Tenure:** 4 years at Hargrove Wealth Partners  
**Access Level:** Elevated — authorized access to client portfolio data, internal pricing models, and proprietary investment research stored on secured network drives  

---

## Alleged Offenses

Forsythe is suspected of two related offenses in the weeks prior to his resignation:

1. **Data Exfiltration** — Copying confidential client records, portfolio holdings, and proprietary investment models to unauthorized external storage devices for delivery to a competitor firm.

2. **Expense Report Fraud** — Submitting falsified expense reports during the same period, potentially as a secondary source of financial gain or as cover activity during the exfiltration window.

---

## Circumstances

Forsythe submitted his resignation on March 25, 2015. Prior to his final day, the firm's IT security team flagged unusual file access patterns on his workstation — large volumes of data being accessed outside of normal business hours and activity consistent with bulk file copying.

His workstation was seized and forensically imaged before he was permitted to leave the building. Removable media found in his possession was also seized and imaged.

---

## Evidence Preserved

| Item | Description | Source |
|------|-------------|--------|
| PC Image | Forensic DD image of Forsythe's Windows 7 workstation | NIST CFReDS Data Leakage Case (cfreds-archive.nist.gov) |
| RM#2 | Forensic image of unauthorized USB drive found in suspect's possession | NIST CFReDS Data Leakage Case |

**Note:** Evidence images were sourced from the NIST CFReDS Data Leakage Case, a publicly available forensic training dataset. The fictional scenario was constructed around the artifact categories present in these images. No proprietary or real case data is used in this project.

---

## Scope of Investigation

This investigation focuses on the following artifact categories from the PC image:

- **Browser history and cached files** — evidence of cloud uploads, webmail use, or research into exfiltration methods
- **LNK files and shellbags** — what files and folders were accessed, and when
- **Prefetch files** — what programs were executed on the workstation
- **USB device artifacts** — registry evidence of external storage connections
- **MFT timeline** — reconstructing file system activity in the 72 hours prior to resignation

---

## Investigative Question

*Did Daniel Forsythe access, copy, or transmit confidential client data from his Hargrove Wealth Partners workstation prior to his resignation, and if so, what methods did he use?*

---

## Notes

- This is a portfolio project simulating a real-world forensic investigation. All people, firms, and circumstances are fictional.
- The forensic image used is a publicly available training dataset published by NIST.
- Findings from this investigation will be documented in the Case Investigation Log and compiled into a final professional case report.
