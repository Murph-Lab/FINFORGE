# FINFORGE

### Financial Forensics Investigation & Report Generator

**Author:** Tom Murphy
**Status:** In Progress
**Started:** March 2026
**Target Completion:** Summer 2026

---

## Overview

FINFORGE is a digital forensics portfolio project simulating a real-world financial crime investigation. It combines manual artifact analysis using industry-standard forensic tools with a custom Python-based triage automation tool, culminating in a professional case report modeled after deliverables produced by firms like Kroll, FTI Consulting, and Ankura.

The project was built to demonstrate forensic investigative methodology, technical tool-building ability, and professional documentation standards to employers in the digital forensics and financial crime investigation space — before obtaining professional experience in the field.

---

## Scenario

A mid-level employee at a fictional wealth management firm is suspected of submitting falsified expense reports and exfiltrating confidential client data prior to resignation. A forensic image of the suspect's Windows workstation has been preserved following proper chain of custody procedures. This investigation reconstructs the suspect's activity, identifies relevant artifacts, and produces findings in a format suitable for legal and corporate review.

---

## Project Goals

- Demonstrate hands-on proficiency with industry forensic tools: Autopsy, FTK Imager, Volatility3, and Wireshark
- Build a functional Python tool that automates artifact parsing and generates structured triage reports
- Produce professional documentation modeled after real consulting firm deliverables
- Create a forensics-specific portfolio piece targeting financial crime investigation roles

---

## Tools & Technologies

| Tool | Purpose |
|---|---|
| Autopsy | Primary GUI platform for disk image analysis |
| FTK Imager 4.7 | Forensic image mounting and acquisition |
| Volatility3 | Memory forensics and process analysis |
| Wireshark | Network traffic capture and analysis |
| Python 3.14 | Triage automation tool development |
| python-registry | Windows Registry hive parsing |
| Jinja2 | HTML report template generation |
| VSCode | Development environment |

---

## Repository Structure

```
FINFORGE/
├── README.md
├── tool/
│   ├── triage_generator.py
│   ├── artifact_parsers/
│   └── report_template.html
├── investigation/
│   ├── methodology.md
│   ├── scenario_brief.md
│   ├── artifact_findings/
│   │   ├── browser_history.md
│   │   ├── prefetch_analysis.md
│   │   ├── lnk_files.md
│   │   ├── usb_artifacts.md
│   │   └── timeline.md
│   └── CASE_REPORT.pdf
├── docs/
│   └── build_log.md
└── resources/
    └── evidence_sources.md
```

---

## Build Phases

**Phase 1 — Environment Setup**  Complete

Established isolated forensic lab VM, installed all forensic tools, configured Python environment and libraries on host machine.

**Phase 2 — Scenario Design**  Complete

Developing fictional financial crime case brief including suspect profile, alleged offenses, and investigation scope.

**Phase 3 — Manual Investigation** In Progress

Conducting artifact analysis on forensic image using Autopsy and FTK Imager. Documenting findings across browser history, prefetch files, LNK files, USB artifacts, and file system timeline.

**Phase 4 — Python Triage Tool**

Building `triage_generator.py` — a command-line tool that automates artifact collection from a forensic image and outputs a structured HTML triage report using Jinja2 templates.

**Phase 5 — Professional Case Report**

Producing a PDF case report formatted as a consulting firm deliverable. Sections include case overview, investigative methodology, findings by artifact category, activity timeline, and conclusions.

**Phase 6 — Publish & Promote**

Finalizing GitHub repository, writing LinkedIn content series documenting the build process, and adding project to resume.

---

## Evidence Sources

No forensic image files are stored in this repository due to size constraints. See `resources/evidence_sources.md` for information on obtaining the practice image used in this investigation.

---

## About

Built as part of a cybersecurity portfolio while completing a Bachelor of Interdisciplinary Studies with certificates in Cybersecurity, Data Analytics, and Group Communication & Leadership. Career focus: digital forensics, with a long-term target in financial crime investigation.
