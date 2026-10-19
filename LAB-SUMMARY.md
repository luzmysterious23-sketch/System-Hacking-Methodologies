# System Hacking Methodologies — Portfolio Summary

## Project Overview

This guided lab explores how application credential exposure can connect to domain access, how Active Directory relationships can reveal privilege risks, and how steganography can be used to simulate file exfiltration. The final exercise examines cleanup actions and the evidence they may leave behind.

All activities described belong to an authorized training environment. The file used for the exfiltration exercise contains Lorem Ipsum placeholder text.

## Exercise Coverage

| Exercise | Focus | Documentation coverage |
| --- | --- | --- |
| 1 — Exploit Active Directory | Prior enumeration, username correlation, credential reuse | Supplied screenshots support username matches and contrasting WinRM login outcomes |
| 2 — Exfiltrate a Sensitive File | BloodHound analysis, privilege change, OpenStego, simulated transfer and recovery | Collection and graph screenshots reviewed; later outcomes documented from instructions |
| 3 — Detection Avoidance | History, tool removal, local logs, privilege rollback | Supplied instructions documented; execution screenshots pending |

## Key Findings

1. **Username overlap is not password-reuse proof.** The enumeration output identifies Pablo and GordonB as domain principals, but the successful Pablo WinRM session supplies the stronger credential-reuse evidence.
2. **Graph relationships need precise interpretation.** The instructions describe GenericAll delegation, while the supplied graph labels the relevant group connection MemberOf. These are different mechanisms and should not be reported interchangeably.
3. **File transfer and external exfiltration are distinct.** The SMB stage moves an image between lab machines; external receipt is simulated separately in the instructions.
4. **Cleanup has limits.** History changes, application removal, and clearing a local log do not establish that all evidence is gone.
5. **Direct membership is only part of access.** Removing Pablo from the Domain Admins listing does not resolve existing sessions, nested memberships, or the underlying delegation issue.

## Tools and Technologies

Kali Linux, Windows Server 2019, Windows 10 Pro, Nmap, saved SQLmap results, Evil-WinRM, PowerShell, BloodHound-Python, BloodHound, Neo4j, Python HTTP server, OpenStego, SMB, and Windows Event Viewer.

## Portfolio Evidence Still to Add

- Privilege-change output and the resulting Domain Admins listing.
- OpenStego installation completion.
- Image creation, successful transfer, extraction, and recovered placeholder text.
- Exercise 3 cleanup results and the post-cleanup membership check.
- Embedded screenshots: the current entries contain captions and source filenames, not uploaded image assets.

## Conclusion

The lab links account exposure, domain relationships, and data handling into one investigation. Its strongest lesson is the need to separate an intended procedure from an observed result and to support each security conclusion with the correct evidence.

[Return to project overview](README.md)
