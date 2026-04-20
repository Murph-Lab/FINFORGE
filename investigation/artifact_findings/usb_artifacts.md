# Artifact Category 2: USB Device Artifacts

**Status:** Complete
**Date:** April 14, 2026
**Examiner:** Tom Murphy

---

## What This Artifact Is

Every time a USB storage device connects to a Windows machine, the OS writes registry entries to track it. This is a device management function, not a security feature. The relevant registry hives are `SYSTEM\CurrentControlSet\Enum\USBSTOR` (device class, vendor, product ID, serial number) and per-user `ntuser.dat` under `MountPoints2` (user-to-device mapping). Autopsy's Recent Activity module parses these and surfaces them under Data Artifacts → USB Device Attached.

USB artifacts record that a device connected, when it first connected, and its serial number. They do not record what files were transferred. Proving file movement requires cross-reference with LNK files, shellbags, and MFT timeline entries.

---

## Summary

16 USB Device Attached entries recovered. After deduplication (Autopsy pulls records from both the live SYSTEM hive and the RegBack backup hive, producing duplicate entries for each device), the actual unique device count is 4: two VMware virtual devices, two ROOT_HUB controller entries, and two distinct SanDisk Cruzer Fit flash drives. The VMware and ROOT_HUB entries are artifacts of the virtualized environment and are not forensically relevant. The two SanDisk drives are the only entries of investigative significance.

---

## Findings

| Device | Device ID | Date/Time Connected | Source Hive |
|---|---|---|---|
| SanDisk Cruzer Fit #1 | 4C530012450531101593 | 2015-03-24 06:38:00 PDT | SYSTEM + RegBack |
| SanDisk Cruzer Fit #2 | 4C530012550531106501 | 2015-03-24 12:38:09 PDT | SYSTEM + RegBack |
| VMware Virtual USB Hub | 68b77da92&0&2 | 2015-03-25 06:05:36 PDT | SYSTEM + RegBack |
| VMware Virtual Mouse | 7&2a7d3009&0&0000 | 2015-03-25 06:05:36 PDT | SYSTEM + RegBack |

Note: ROOT_HUB and ROOT_HUB20 entries (internal USB controller records) also present — not forensically relevant.

---

## Case Relevance

Two distinct SanDisk Cruzer Fit flash drives were connected to the workstation on 2015-03-24 — the day immediately following the suspect's browser research into data exfiltration methods, cloud storage options, and anti-forensic tools. The six-hour gap between connections suggests either two separate transfer sessions or two drives used in sequence. The Cruzer Fit is a nano-sized form factor designed to sit flush with the USB port and is easily concealed — a practical choice for someone attempting to move data without drawing attention.

USB artifacts confirm that physical removable storage was connected during the relevant activity window, consistent with the exfiltration hypothesis. However, USB registry artifacts establish only that the devices connected — they do not prove files were copied. Confirmation of actual file transfer requires cross-referencing with LNK files, shellbags, and MFT timeline entries.

---

## Open Questions

- Do LNK files show recently accessed files on a removable drive (E:\) around 2015-03-24?
- Do shellbags show folder browsing activity on a removable drive on the same date?
- Is there MFT evidence of file access or copy operations timed to the USB connection windows?
- Were CCleaner or Eraser actually downloaded or executed after the USB activity? (Cross-reference: Prefetch)
