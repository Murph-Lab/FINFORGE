# Artifact Category 3: LNK Files and Shellbags

**Status:** Complete
**Date:** April 15, 2026
**Examiner:** Tom Murphy

---

## What These Artifacts Are

### LNK Files
LNK files are Windows shortcut files created automatically every time a user opens a file. Windows generates them silently in the background as a convenience feature for the Recent Items list. They live in `C:\Users\[username]\AppData\Roaming\Microsoft\Windows\Recent\` and store the full path to the target file, timestamps (first opened, last opened), volume information, and the drive serial number. If a file was opened from a removable drive, the LNK file will reflect the removable media volume type. LNK files can persist after the target file is deleted — an LNK pointing to a missing file is itself significant. Autopsy surfaces these under Data Artifacts → Recent Documents.

### Shellbags
Shellbags are registry entries Windows creates to remember folder window preferences (size, position, view). As a side effect, a shellbag entry is written every time a user opens a folder — including folders on removable drives and network shares. They live in the user's `ntuser.dat` under `Software\Microsoft\Windows\Shell\BagMRU`. Shellbags persist after the device is removed and after files are deleted. They prove folder navigation, not file access — but combined with LNK files they establish both what folders were browsed and what files within them were opened. Autopsy surfaces these under Data Artifacts → Shell Bags.

---

## LNK File Findings

### Summary

46 LNK file entries recovered. Key entries confirm that confidential project files were opened from both a removable drive (E:\) and a secured network share (\\10.11.11.128\secured_drive) during the investigative window. The user account attributed across all entries is **"informant"** (confirmed via source file path: `Users/informant/AppData/Roaming/Microsoft/Windows/Recent/`).

### Key Findings

| File | Path | Date Accessed | Significance |
|---|---|---|---|
| [secret_project]_proposal.docx | E:\RM#1\Secret Project Data\proposal\ | 2015-03-23 11:37:20 PDT | Confidential project file accessed from removable drive |
| [secret_project]_proposal.LNK | E:\RM#1\Secret Project Data\proposal\ | 2015-03-23 11:37:54 PDT | Corroborating entry |
| [secret_project]_design_concept.ppt | E:\RM#1\Secret Project Data\design\ | 2015-03-23 11:38:21 PDT | Confidential design file accessed from removable drive |
| [secret_project]_design_concept.LNK | E:\RM#1\Secret Project Data\design\ | 2015-03-23 11:38:23 PDT | Corroborating entry |
| [secret_project]_final_meeting.pptx | \\10.11.11.128\secured_drive\Secret Project Data\final\ | 2015-03-23 13:27:33 PDT | Confidential presentation accessed from secured network share |
| [secret_project]_final_meeting.pptx.LNK | \\10.11.11.128\secured_drive\Secret Project Data\final\ | 2015-03-23 13:27:37 PDT | Corroborating entry |
| pricing decision.lnk | \\10.11.11.128\SECURED_DRIVE\Secret Project Data\ | 2015-03-23 13:26:54 PDT | Pricing document accessed from secured network share |
| [secret_project]_pricing_decision.xlsx | \\10.11.11.128\SECURED_DRIVE\Secret Project Data\ | 2015-03-23 13:26:53 PDT | Financial document accessed from secured network share |
| secret.lnk | No preferred path found | 2015-03-23 11:37:20 PDT | Target file missing — possible deletion after access |
| winter_whether_advisory.zip | D:\de\winter_whether_advisory.zip | 2015-03-24 07:01:23 PDT | Archive accessed from optical drive |
| CD Drive (2).lnk | D:\ | 2015-03-24 14:01:11 PDT | Optical drive accessed — corroborates CD burning research |
| Resignation_Letter_(laman_Informant).docx | C:\Users\informant\Desktop\ | 2015-03-24 11:48:41 PDT | Resignation letter present on desktop during activity window |

### Notes

The `secret.lnk` entry returning "No preferred path found" indicates the target file no longer exists — consistent with deliberate deletion. The timestamp discrepancy between E:\ LNK entries (2015-03-23) and USB registry entries (2015-03-24) requires MFT cross-reference to resolve — the E:\ drive may have been connected on both days, or LNK timestamps may reflect file metadata carried over from the drive itself.

---

## Shellbag Findings

### Summary

118 shellbag entries recovered. Key entries confirm systematic folder navigation on the E:\ removable drive, the secured network share, and a D:\ optical drive — all during the March 23–24 activity window. A local Google Drive folder appearing in shellbags on 2015-03-25 corroborates the browser history visit to the Google Drive download page on 2015-03-23.

### Key Findings

| Path Browsed | Last Write | Significance |
|---|---|---|
| My Computer\E:\ | — | Removable drive root browsed |
| My Computer\E:\RM#\Secret Project Dat | 2015-03-24 13:38:31 PDT | Deliberate folder navigation into confidential project data on USB drive |
| My Computer\E:\RM#\Secret Project Dat\desig | 2015-03-24 13:38:52 PDT | Design subfolder browsed on USB drive |
| My Computer\E:\Secret Project Dat | 2015-03-24 14:00:19 PDT | Second E:\ path structure — possible second USB drive |
| My Computer\E:\Secret Project Dat\technical revie | — | Technical review subfolder browsed |
| My Computer\E:\Secret Project Dat\proposa | — | Proposal subfolder browsed |
| My Computer\E:\Secret Project Dat\progres | 2015-03-24 20:54:07 PDT | Progress subfolder browsed — evening activity |
| My Computer\E:\Secret Project Dat\pricing decisio | — | Pricing decision subfolder browsed |
| My Computer\E:\Secret Project Dat\desig\winter_whe... | 2015-03-24 14:01:29 PDT | Specific file location browsed |
| My Computer\D:\ | — | Optical drive root browsed |
| My Computer\D:\d\winter_whether_advisory.zi | 2015-03-24 19:54:43 PDT | Archive file location browsed on optical drive |
| My Computer\D:\d\winter_whether_advisory.zi\Unkn... | 2015-03-24 19:54–20:44 PDT | Contents of archive examined |
| My Network Places\10.11.11.128 | 2015-03-23 20:23:28 PDT | Network share host browsed |
| My Network Places\10.11.11.128\\secured_drive | 2015-03-23 20:23–20:28 PDT | Secured network share browsed |
| S dat\Secret Project Dat | 2015-03-24 13:40:13 PDT | Truncated path — unresolved storage location, identical folder structure to E:\ and network share |
| S dat\Secret Project Dat\design | 2015-03-24 13:52:05 PDT | Design subfolder browsed at unresolved location |
| Users\Google Driv | 2015-03-25 15:20:59 PDT | Local Google Drive folder browsed — confirms Google Drive installed by March 25 |

---

## Case Relevance

LNK files and shellbags together establish that the suspect did not merely research exfiltration methods — he actively accessed confidential project files across multiple storage locations during a concentrated two-day window. On 2015-03-23, specific files including pricing decisions, a final meeting presentation, and project proposals were accessed from a secured network share. The same categories of files appear on the E:\ removable drive, consistent with files being copied from the network share to a USB drive. Shellbags confirm systematic folder navigation rather than incidental file access — the suspect browsed multiple subfolders of Secret Project Data deliberately. The appearance of a local Google Drive folder on 2015-03-25 corroborates the browser history visit to the Google Drive download page two days earlier. The resignation letter on the desktop on 2015-03-24 places all of this activity in the context of an impending departure.

---

## Open Questions

- Does the MFT timeline show file copy operations from the network share to E:\ on 2015-03-23?
- Does the "S dat" truncated shellbag path resolve to a mapped network drive or a third removable device?
- Is there evidence Google Drive was actively used for file sync or upload on 2015-03-25?
- Does the secret.lnk missing target correlate with any deletion events in the MFT?
- Do prefetch files show Google Drive, CCleaner, or Eraser execution during the activity window?
