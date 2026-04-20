# Artifact Category 4: Prefetch Files

**Status:** Complete
**Date:** April 15, 2026
**Examiner:** Tom Murphy

---

## What This Artifact Is

Every time a program executes on Windows, the OS creates a prefetch file for it. Prefetch is a performance feature — Windows analyzes what files a program needs at startup and caches that information so the next launch is faster. Prefetch files live in `C:\Windows\Prefetch\` and are named after the executable (e.g., `CCLEANER.EXE-AB1234CD.pf`).

Each prefetch file records the executable name, its full path, how many times it has been run (run count), and the last execution timestamp. On Windows 8 and later, up to the last eight execution timestamps are stored. Run count is particularly valuable — it distinguishes between a program that existed on the machine and one that was actively used. Autopsy surfaces these under Data Artifacts → Run Programs.

Prefetch proves execution. It does not prove what the program did during that execution.

---

## Summary

95 prefetch entries recovered. The majority are routine Windows system processes. Seven entries are forensically significant: the installation and execution of Eraser and CCleaner on 2015-03-25, the subsequent uninstallation of CCleaner on the same morning, and the execution of GoogleDriveSync. This artifact category directly answers the open questions carried forward from browser history and shellbag analysis — both anti-forensic tools researched on 2015-03-23 and 2015-03-25 were not only downloaded but installed, executed, and in CCleaner's case, uninstalled in a single concentrated window on the morning of March 25.

---

## Key Findings

| Program | Path | Date/Time | Run Count | Significance |
|---|---|---|---|---|
| CCSETUP504.EXE | /USERS/INFORMANT/DESKTOP/DOWNLOAD | 2015-03-25 07:57:56 PDT | 1 | CCleaner installer executed from Downloads — installation confirmed |
| CCLEANER64.EXE | /PROGRAM FILES/CCLEANER | 2015-03-25 08:15:50 PDT | 2 | CCleaner executed twice after installation |
| UNINST.EXE | /PROGRAM FILES/CCLEANER | 2015-03-25 08:18:29 PDT | 1 | CCleaner uninstalled — deliberate removal of the cleaning tool itself |
| ERASER 6.2.0.2962.EXE | /USERS/INFORMANT/DESKTOP/DOWNLOAD | 2015-03-25 07:50:14 PDT | 1 | Eraser installer executed from Downloads — installation confirmed |
| ERASER.EXE | /PROGRAM FILES/ERASER | 2015-03-25 08:13:30 PDT | 2 | Eraser executed twice after installation |
| GOOGLEDRIVESYNC.EXE | /PROGRAM FILES (X86)/GOOGLE/DRIVE | 2015-03-25 08:21:31 PDT | 2 | Google Drive sync client executed — active cloud sync confirmed |
| DOTNETFX40_FULL_SETUP.EXE | /USERS/INFORMANT/APPDATA/LOCAL/TEMP/ERASE... | 2015-03-25 07:50:15 PDT | 1 | .NET framework installer triggered by Eraser as dependency |

---

## Reconstructed Execution Timeline — 2015-03-25 Morning

| Time (PDT) | Event |
|---|---|
| 07:50 | Eraser installer runs from Desktop Downloads |
| 07:50 | .NET Framework 4 installer triggered as Eraser dependency |
| 07:57 | CCleaner installer runs from Desktop Downloads |
| 08:13 | Eraser.exe executed from Program Files — run count 2 |
| 08:15 | CCleaner64.exe executed from Program Files — run count 2 |
| 08:18 | CCleaner uninstaller executed — CCleaner removed from system |
| 08:21 | GoogleDriveSync.exe executed — Google Drive sync client active |

---

## Case Relevance

Prefetch files confirm the complete anti-forensic sequence on the morning of 2015-03-25. Both tools researched on 2015-03-23 and 2015-03-25 via browser search were downloaded, installed, and executed within a 31-minute window. The immediate uninstallation of CCleaner following its execution is a significant indicator of deliberate concealment — the suspect attempted to remove evidence of the tool used to destroy evidence. Run counts of 2 for both CCleaner and Eraser confirm these were not accidental single launches. The execution of GoogleDriveSync at 08:21 PDT — immediately following the anti-forensic activity — corroborates the shellbag evidence of a local Google Drive folder and raises the possibility that cloud sync was used as a secondary exfiltration channel or to preserve copies of exfiltrated data after local traces were wiped. All installer paths (`/USERS/INFORMANT/DESKTOP/DOWNLOAD`) tie activity directly to the "informant" user account.

---

## Open Questions

- Does the MFT timeline show file deletion events correlated with the CCleaner and Eraser execution window?
- What files were present in the Downloads folder prior to the anti-forensic activity that may no longer exist?
- Does GoogleDriveSync execution correlate with any network activity or file upload events recoverable from other artifacts?
- Do Web Downloads entries show the CCleaner and Eraser installers being downloaded prior to execution?
