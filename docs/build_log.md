# FINFORGE — Project Build Log

**Analyst:** Tom Murphy
**Project:** FINFORGE — Financial Forensics Investigation & Report Generator

---

## Phase 1 — Environment Setup
**Status:** Complete
**Date:** March 2026

### Objective
Establish a complete forensic investigation environment on both a host machine and an isolated virtual machine. This environment will support manual artifact investigation, Python-based triage tool development, and memory forensics analysis for the FINFORGE portfolio project.

### Environment Overview

**Host Machine**
- VirtualBox 7.x — Hypervisor running the isolated forensic lab VM
- Python 3.14 — Runtime for FINFORGE triage script development
- VSCode — Code editor for Python tool development
- python-registry 1.3.1 — Windows Registry hive parsing library
- Jinja2 3.1.6 — HTML report template generation
- Volatility3 2.27.0 — Memory forensics framework

**Virtual Machine (FINFORGE-Lab)**
- Windows 10 Pro — Isolated OS environment for forensic tool operation
- Autopsy — Primary GUI platform for disk image analysis
- FTK Imager 4.7 — Forensic image creation and mounting
- Wireshark — Network traffic capture and analysis

### Setup Procedure

**Step 1 — Hypervisor Installation**
Downloaded and installed VirtualBox on host machine. Extension Pack also installed to enable USB passthrough for future evidence acquisition scenarios.

**Step 2 — Virtual Machine Creation**
Created a new VM in VirtualBox with the following specifications:
- Name: FINFORGE-Lab
- OS: Windows 10 Pro (64-bit)
- RAM: 4096 MB
- CPU: 2 cores
- Storage: 80 GB dynamically allocated VDI

**Step 3 — Windows 10 Installation**
Attached Windows 10 ISO obtained from Microsoft's official Media Creation Tool. Completed standard Windows installation. Created local account (no Microsoft account) with username Analyst.

**Step 4 — VirtualBox Guest Additions**
Installed Guest Additions via Devices menu inside the running VM. Enables proper screen resolution, shared clipboard, and improved mouse integration between host and VM.

**Step 5 — Forensic Tool Installation (VM)**
Inside the VM, installed the following tools with default settings:
- Autopsy (Windows 64-bit installer, includes The Sleuth Kit)
- FTK Imager 4.7.3.81 (obtained via Exterro registration portal)
- Wireshark (with Npcap for live capture support)

**Step 6 — Python Environment (Host Machine)**
Confirmed Python 3.14 installed on host. Installed required libraries via pip: python-registry, jinja2, and volatility3.

Note: prefetch-parser skipped due to libscca-python build failure requiring Microsoft C++ Build Tools. Prefetch parsing will be handled via an alternative method in Phase 4.

**Step 7 — Volatility3 Verification**
Confirmed Volatility3 2.27.0 installed and operational. Full plugin list verified including all Windows, Linux, and Mac memory forensics modules.

Note: vol.exe not added to system PATH — full executable path used for all Volatility commands.

### Snapshots Taken

| Snapshot Name | Taken After |
|---------------|-------------|
| Clean Windows Install | Windows setup complete, before any tools installed |
| Forensic Tools Installed | Autopsy, FTK Imager, and Wireshark confirmed installed |

### Issues Encountered & Resolutions

| Issue | Resolution |
|-------|------------|
| prefetch-parser failed to build — missing Microsoft C++ Build Tools | Skipped package; will use alternative prefetch parsing method in Phase 4 |
| vol -h returned path error after pip install | PATH variable not updating correctly; resolved by using full executable path |

**Phase 1 Status: Complete**
All tools confirmed installed and operational. Environment is ready for Phase 2 — Case Scenario Design.

---

## Phase 2 — Scenario Design
**Status:** Complete
**Date:** April 2026

### Objective
Design the fictional financial crime case scenario, select and verify the forensic evidence image, and produce all Phase 2 documentation.

### Work Completed

**Step 1 — Evidence Image Selection**
Selected the NIST CFReDS Data Leakage Case as the forensic image source. Chosen for its insider threat scenario, Windows 7 workstation image, and artifact categories directly relevant to the FINFORGE investigation scope (browser history, LNK files, USB artifacts, prefetch, MFT timeline).

Source: https://cfreds-archive.nist.gov/data_leakage_case/data-leakage-case.html

**Step 2 — Evidence Image Acquisition**
Downloaded the PC DD image (three compressed .7z parts, total 5.05 GB compressed). Extracted using 7-Zip to produce cfreds_2015_data_leakage_pc.dd (approximately 20 GB extracted).

**Step 3 — Hash Verification**
Loaded the extracted DD image in FTK Imager 4.7 and ran hash verification. SHA1 generated: afe5c9ab487bd47a8a9856b1371c2384d44fd7. Note: NIST's published hash list covers the compressed .7z parts only, not the extracted .dd file. No read errors reported on load.

**Step 4 — Shared Folder Configuration**
Configured a read-only shared folder in VirtualBox to make the evidence image accessible from inside the FINFORGE-Lab VM without copying the file into the VM or modifying it. This preserves forensic integrity throughout analysis.

**Step 5 — Documentation Produced**
Three documents written and pushed to the GitHub repository:
- investigation/scenario_brief.md — fictional case brief including suspect profile, firm background, alleged offenses, and investigation scope
- investigation/methodology.md — forensic methodology document covering guiding principles, analysis environment, artifact categories, and documentation approach
- resources/evidence_sources.md — evidence provenance record including source, file details, hash verification notes, and usage disclaimer

**Phase 2 Status: Complete**
Forensic image acquired and verified. Case scenario designed. All Phase 2 documentation committed to GitHub. Environment is ready for Phase 3 — Manual Investigation.
