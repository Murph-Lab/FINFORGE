# Investigative Methodology

## Overview

This document describes the forensic methodology applied throughout the FINFORGE investigation. All procedures are modeled after standard digital forensics practice and are consistent with methods used in professional forensic consulting engagements.

---

## Guiding Principles

**Forensic Soundness** — Evidence is never modified. All analysis is performed on forensic images, not original media. Write-blocking procedures are observed where applicable.

**Documentation First** — Every action taken during the investigation is logged before, during, and after execution. Undocumented analysis has no evidentiary value.

**Chain of Custody** — The origin, handling, and integrity of all evidence items is tracked and recorded in the Evidence Sources document.

**Reproducibility** — Analysis steps are documented in sufficient detail that another analyst could reproduce the findings independently.

---

## Evidence Acquisition

The forensic image used in this investigation was obtained from the NIST CFReDS Data Leakage Case — a publicly available forensic training dataset. The image was downloaded, extracted, and verified in FTK Imager 4.7 prior to any analysis.

Hash verification was performed on load. See `resources/evidence_sources.md` for full acquisition details.

---

## Analysis Environment

| Component | Tool | Version |
|-----------|------|---------|
| Disk image analysis | Autopsy | Latest |
| Image mounting & verification | FTK Imager | 4.7.3.81 |
| Memory forensics | Volatility3 | 2.27.0 |
| Network traffic analysis | Wireshark | Latest |
| Triage automation | Python (triage_generator.py) | 3.14 |

All manual analysis is performed inside an isolated Windows 10 VM (FINFORGE-Lab) running in VirtualBox. The forensic image is accessed via a read-only shared folder — it is never copied into the VM or modified.

---

## Artifact Categories & Approach

### Browser History
**Tool:** Autopsy  
**Purpose:** Identify web-based exfiltration activity — cloud storage uploads, webmail use, file sharing services  
**Artifacts:** Chrome and IE browsing history, cached files, download records

### LNK Files & Shellbags
**Tool:** Autopsy  
**Purpose:** Establish what files and folders the suspect accessed, and reconstruct access patterns  
**Artifacts:** Windows shortcut (.lnk) files, shellbag registry entries

### Prefetch Files
**Tool:** Autopsy  
**Purpose:** Identify what programs were executed on the workstation and when  
**Artifacts:** Windows Prefetch files (`C:\Windows\Prefetch\`)

### USB Device Artifacts
**Tool:** Autopsy  
**Purpose:** Identify external storage devices connected to the workstation  
**Artifacts:** USBSTOR registry key, setupapi logs, device serial numbers

### MFT Timeline
**Tool:** Autopsy  
**Purpose:** Reconstruct file system activity in the 72 hours prior to the suspect's resignation  
**Artifacts:** Master File Table ($MFT), file creation/modification/access timestamps

---

## Documentation Approach

Findings from each artifact category are recorded in individual markdown files under `investigation/artifact_findings/`. Each file captures:

- What was found
- What tool and method was used to find it
- What the finding means in the context of the investigation
- How it connects to the investigative question

All findings feed into the Final Case Report (`investigation/CASE_REPORT.pdf`), produced in Phase 5.

---

## Investigative Question

*Did Daniel Forsythe access, copy, or transmit confidential client data from his Hargrove Wealth Partners workstation prior to his resignation, and if so, what methods did he use?*

All analysis is scoped to answer this question. Artifacts that do not bear on this question are noted but not analyzed in depth.
