# Artifact Category 1: Browser History

**Status:** Complete
**Date:** April 12, 2026
**Examiner:** Tom Murphy

---

## What This Artifact Is

Browser history artifacts include two sub-categories: web search queries and visited URLs. Windows stores these records inside browser-specific SQLite databases and the Windows Search index. Autopsy's Recent Activity ingest module parses these automatically and surfaces them under Data Artifacts → Web Search and Web History.

---

## Web Search History

### Summary

63 search queries recovered across Google Chrome, Microsoft Edge, and Internet Explorer. The majority of forensically significant searches occurred on 2015-03-23 via Chrome and Edge. Search terms cluster into four categories: exfiltration method research, anti-forensics tool research, investigative awareness research, and cloud storage access. The anti-forensics cluster is the most significant — searches for CCleaner and Eraser on 2015-03-25 suggest the suspect was aware of forensic investigation risk and actively researching how to destroy evidence.

### Key Findings

| Timestamp (PDT) | Search Term | Browser | Significance |
|---|---|---|---|
| 2015-03-23 11:02:09 | data leakage methods | Chrome | Exfiltration method research |
| 2015-03-23 11:02:44 | leaking confidential information | Chrome | Exfiltration intent research |
| 2015-03-23 11:03:40 | information leakage cases | Chrome | Repeated 15+ times — legal exposure research |
| 2015-03-23 18:08:23 | file sharing and tethering | Edge | Exfiltration method research |
| 2015-03-23 18:08:31 | DLP DRM | Edge | Awareness of corporate monitoring systems |
| 2015-03-23 18:08:54 | e-mail investigation | Edge | Investigative awareness |
| 2015-03-23 18:10:03 | Forensic Email Investigation | Edge | Direct research into forensic methodology |
| 2015-03-23 18:10:27 | what is windows system artifact | Edge | Researching what traces Windows leaves |
| 2015-03-23 18:11:50 | investigation on windows machine | Edge | Researching forensic investigation process |
| 2015-03-23 18:12:35 | windows event logs | Edge | Researching what logs investigators use |
| 2015-03-23 18:13:20 | cd burning method | Edge | Exfiltration method — physical media |
| 2015-03-23 18:13:37 | cd burning method in windows | Edge | Specific Windows implementation |
| 2015-03-23 18:14:11 | external device and forensics | Edge | Researching how external devices are traced |
| 2015-03-23 20:43:52 | external device and forensics | Edge | Repeated search — elevated significance |
| 2015-03-25 14:46:44 | anti-forensic tools | Edge | Direct evidence of cover-up intent |
| 2015-03-25 14:46:54 | eraser | Edge | Eraser is a file wiping tool |
| 2015-03-25 14:47:51 | ccleaner | Edge | CCleaner used for trace removal |
| 2015-03-23 12:55:09 | apple icloud | Chrome | Cloud storage access research |
| 2015-03-23 12:56:04 | google drive | Chrome | Cloud storage access research |

### Case Relevance

The search history establishes a clear behavioral pattern across two days. On 2015-03-23 the suspect researched both exfiltration methods (file sharing, CD burning) and the forensic investigation process itself — indicating awareness that these actions could be traced. On 2015-03-25 the suspect searched specifically for anti-forensic tools including file wiping software. The searches for Apple iCloud and Google Drive on 2015-03-23 suggest personal cloud storage was being considered as an exfiltration channel. Taken together, this search history supports the allegation that Forsythe researched, planned, and attempted to conceal a deliberate data exfiltration.

---

## Web History (Visited URLs)

### Summary

1,611 URL visits recovered. Filtered for forensically significant entries. Key findings confirm that search activity translated into actual visits — the suspect did not just search for exfiltration methods and anti-forensics tools, he visited the relevant pages. Cloud storage comparison, iCloud setup, Google Drive download, and ForensicsWiki anti-forensic techniques pages were all visited on 2015-03-23. The suspect also visited an FBI intellectual property theft page and read about a data leakage settlement, suggesting awareness of legal exposure.

### Key Findings

| Timestamp (PDT) | URL / Page Title | Browser | Significance |
|---|---|---|---|
| 2015-03-23 11:05:28 | Google To Settle 'Data Leakage' Case For $8.5 Million | Chrome | Researching legal consequences |
| 2015-03-23 11:05:55 | FBI — Intellectual Property Theft | Chrome | Visited FBI IP theft page — consciousness of guilt |
| 2015-03-23 11:06:01 | Intellectual Property — Wikipedia | Chrome | Research into IP theft definitions |
| 2015-03-23 11:15:32 | 7 Best Cloud Storage 2015: Dropbox vs Google Drive vs OneDrive vs iCloud | Chrome | Actively comparing cloud storage options |
| 2015-03-23 11:15:49 | Digital Forensics — Wikipedia | Chrome | Researching forensic investigation methodology |
| 2015-03-23 11:17:19 | Anti-Forensic Techniques — ForensicsWiki | Chrome | Direct evidence of cover-up research |
| 2015-03-23 11:19:17 | List of Data Recovery Software — Wikipedia | Chrome | Researching data recovery tools |
| 2015-03-23 11:19:21 | Tools:Data Recovery — ForensicsWiki | Chrome | Second ForensicsWiki visit |
| 2015-03-23 12:55:34 | icloud.com/icloudcontrolpanel | Chrome | Visited iCloud control panel setup page — active configuration |
| 2015-03-23 12:56:xx | Download Google Drive — Free Cloud Storage | Chrome | Visited Google Drive download page |

### Case Relevance

Web history confirms that search queries translated into deliberate visits. The suspect visited iCloud setup pages and the Google Drive download page on 2015-03-23, indicating active exploration of cloud-based exfiltration channels. The visit to the FBI Intellectual Property Theft page and the data leakage settlement article on the same date establishes awareness of criminal exposure. ForensicsWiki was visited twice for anti-forensic techniques, corroborating the later CCleaner and Eraser searches on 2015-03-25.

---

## Open Questions

- Were Google Drive or iCloud actually installed or used for file transfer? (Cross-reference: Prefetch, Shellbags)
- Did the suspect visit any file transfer service URLs directly (WeTransfer, Dropbox, SendSpace)?
- Do Web Downloads show any tool actually downloaded from these pages?
- Do USB artifact timestamps correlate with the 2015-03-23 activity window?
