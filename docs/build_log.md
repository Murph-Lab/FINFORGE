# FINFORGE — Project Build Log

**Analyst:** Tom Murphy
**Project:** FINFORGE — Financial Forensics Investigation & Report Generator
**Phase:** 1 — Environment Setup
**Status:** Complete
**Date:** March 2026

---

## Objective

Establish a complete forensic investigation environment on both a host machine and an isolated virtual machine. This environment will support manual artifact investigation, Python-based triage tool development, and memory forensics analysis for the FINFORGE portfolio project.

---

## Environment Overview

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

---

## Setup Procedure

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

Attached Windows 10 ISO obtained from Microsoft's official Media Creation Tool. Completed standard Windows installation. Created local account (no Microsoft account) with username `Analyst`.

**Step 4 — VirtualBox Guest Additions**

Installed Guest Additions via Devices menu inside the running VM. Enables proper screen resolution, shared clipboard, and improved mouse integration between host and VM.

**Step 5 — Forensic Tool Installation (VM)**

Inside the VM, installed the following tools with default settings:
- Autopsy (Windows 64-bit installer, includes The Sleuth Kit)
- FTK Imager 4.7.3.81 (obtained via Exterro registration portal)
- Wireshark (with Npcap for live capture support)

**Step 6 — Python Environment (Host Machine)**

Confirmed Python 3.14 installed on host. Installed required libraries via pip:

```
pip install python-registry jinja2
pip install volatility3
```

Note: `prefetch-parser` skipped due to `libscca-python` build failure requiring Microsoft C++ Build Tools. Prefetch parsing will be handled via an alternative method in Phase 4.

**Step 7 — Volatility3 Verification**

Confirmed Volatility3 2.27.0 operational via full executable path:

```
C:\Users\tomem\AppData\Local\Python\pythoncore-3.14-64\Scripts\vol.exe -h
```

Full plugin list confirmed. Note: `vol.exe` not added to PATH successfully — use full path for all Volatility commands.

---

## Snapshots Taken

| Snapshot Name | Taken After |
|---|---|
| Clean Windows Install | Windows setup complete, before any tools installed |
| Forensic Tools Installed | Autopsy, FTK Imager, and Wireshark confirmed installed |

---

## Issues Encountered & Resolutions

| Issue | Resolution |
|---|---|
| `prefetch-parser` failed to build — missing Microsoft C++ Build Tools | Skipped package; will use alternative prefetch parsing method in Phase 4 |
| `vol -h` returned path error after pip install | PATH variable not updating correctly; resolved by using full executable path |

---

## Phase 1 Status: Complete

All tools confirmed installed and operational. Environment is ready for Phase 2 — Case Scenario Design.

