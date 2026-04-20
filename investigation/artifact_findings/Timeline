# Artifact Category 5: MFT Timeline

**Status:** Complete
**Date:** April 15, 2026
**Examiner:** Tom Murphy

---

## What This Artifact Is

Every file on an NTFS volume has an entry in the Master File Table (MFT). The MFT is a database tracking every file and folder on the drive, with each entry containing four timestamps per file: Created, Modified, MFT Modified, and Accessed — stored in both the `$STANDARD_INFORMATION` attribute (user-visible, can be manipulated) and the `$FILE_NAME` attribute (kernel-written, harder to tamper with). Discrepancies between these two sets of timestamps on the same file can indicate timestomping — a known anti-forensic technique.

The MFT timeline reconstructs file system activity across the entire volume in chronological order: every file created, modified, accessed, or deleted. Autopsy surfaces timeline data via the Timeline Editor (top toolbar), which allows filtering by date range, event type, and keyword.

---

## Summary

109,724 file system events recovered across the March 22–25, 2015 window. The MFT timeline corroborates and sequences every finding from prior artifact categories at the file level. Key findings include the full installation and execution sequence for Eraser and CCleaner, Recycle Bin entries appearing immediately after Eraser execution, Outlook data file modification during the anti-forensic window, and Google Drive sync client activation following the cleanup sequence.

---

## Reconstructed Event Sequence — 2015-03-25 Morning

| Time (PDT) | Event | MFT Evidence | Significance |
|---|---|---|---|
| 07:50 | Eraser installed | `/Program Files/Eraser/` files created: `Eraser.exe`, `Eraser.Shell.dll`, plugins | Full installation footprint confirmed |
| 07:50 | .NET Framework 4 installed as dependency | Setup logs in Temp, ASP.NET registration events | Corroborates `DOTNETFX40_FULL_SETUP.EXE` prefetch entry |
| 07:54 | .NET compilation completes | NGEN compilation events, NativeImages assembly created | Normal post-install behavior |
| 07:57 | CCleaner installation begins | `CCSETUP504.EXE` prefetch created, installer temp files in `$OrphanFiles` | Installation confirmed |
| 07:58 | CCleaner pings network during install | `PING.EXE` runs at 07:58:34 | Normal installer behavior — active network connection confirmed |
| 07:58 | CCleaner fully installed | `/Program Files/CCleaner/CCleaner.exe`, `CCleaner64.exe`, `uninst.exe` created | Full installation footprint confirmed |
| 08:11 | Outlook data file modified | `/Users/informant/AppData/Local/Microsoft/Outlook/iaman.informant@nist.gov.ost` | Outlook active during anti-forensic window |
| 08:12 | Eraser prefetch updated | `ERASER.EXE-CE61944A.pf` modified | Confirms Eraser execution |
| 08:13 | Eraser executes | `Program Run: ERASER.EXE` at 08:13:30 | Execution confirmed |
| 08:13 | Recycle Bin entries created | `$R508CBB.jpg`, `$RI3FM2A.jpg`, `$RKXD1U3.jpg` in `$Recycle.Bin` | Files deleted during or after Eraser execution — may be recoverable |
| 08:13 | Windows Burn folder files present | `Desert.jpg`, `Hydrangeas.jpg`, `Chrysanthemum.jpg`, `Jellyfish.jpg` | Corroborates CD burning research from 2015-03-23 |
| 08:15 | CCleaner executes | `CCleaner64.exe` and language DLLs showing modified events | Execution confirmed |
| 08:15 | CCleaner contacts licensing server | `app_cc_pro_trialkey[1].htm` created in IE Temp Internet Files | Confirms CCleaner actually ran, not just installed |
| 08:18 | CCleaner uninstalled | `uninst.exe` events, CCleaner directory modified | Deliberate removal of cleaning tool |
| 08:16 | Google Update runs | `GOOGLEUPDATE.EXE` prefetch, Windows Task files created | Google Drive update mechanism active |
| 08:21 | Google Drive sync executes | `GOOGLEDRIVESYNC.EXE` prefetch confirmed | Cloud sync client active immediately after cleanup |

---

## Additional Observations

### Recycle Bin entries after Eraser execution
Files appearing in `$Recycle.Bin` immediately after Eraser runs suggests Eraser did not successfully wipe all targeted files — some were deleted normally and may be recoverable. The `$R` prefixed entries represent actual file content and may be accessible via Autopsy's Deleted Files view.

### Outlook OST file modification
The `iaman.informant@nist.gov.ost` file modification during the anti-forensic window is notable. This is the local Outlook data cache for the informant account. Activity during this window could indicate email deletion, drafting, or sending — a potential secondary exfiltration or cover-up channel not fully explored in this investigation.

### Windows Burn folder
Sample image files present in the Windows Burn staging folder corroborate the March 23 browser searches for CD burning methods. The Burn folder is where Windows stages files before writing to optical media. Presence of files here is consistent with CD burning activity on or around March 24.

### MFT event type codes observed
- `_C_` — File Changed (MFT entry modified)
- `AC__` — File Accessed and Created
- `_C_M` — File Changed, MFT entry modified
- `A_BM` — File Accessed, Born timestamp set, MFT modified
- `Program Run` — Execution event from prefetch

---

## Evidentiary Gap

USB artifacts and LNK/shellbag data prove access and device connection. MFT proves file system activity. No artifact category directly captures a file copy operation — it cannot be proven with certainty what files left the machine and where they ended up. The CD burning gap is the sharpest version of this limitation: the Burn folder had files staged, browser history shows CD burning research, but there is no confirmation the disc was written or what it contained. This limitation is documented and does not diminish the overall findings — it represents the boundary of what the available artifacts can establish.

---

## Case Relevance

The MFT timeline provides the chronological backbone connecting all five artifact categories into a single coherent sequence. File system events confirm the installation and execution of both anti-forensic tools on the morning of March 25 — the day after USB drives connected and two days after the suspect researched exfiltration methods. The immediate uninstallation of CCleaner following execution, combined with Recycle Bin deletions timed to Eraser's run, demonstrates a deliberate multi-tool cleanup effort. The activation of Google Drive sync immediately following the cleanup sequence raises the possibility that cloud storage was used as a secondary exfiltration channel or as a backup mechanism after local traces were removed. Taken across all five artifact categories, the MFT timeline completes a documented chain of events consistent with deliberate data exfiltration followed by an organized anti-forensic cleanup.

---

## Open Questions

- Are the Recycle Bin `$R` entries recoverable via Autopsy's Deleted Files view?
- Does the Outlook OST modification represent email deletion, sending, or routine background sync?
- Do the Windows Burn folder contents match any files identified on the E:\ USB drive or network share?
- Is there MFT evidence of the CCleaner and Eraser installers being deleted from the Downloads folder after use?
