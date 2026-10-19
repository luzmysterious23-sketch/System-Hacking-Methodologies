# System Hacking Methodologies

Hands-on cybersecurity lab exploring Active Directory enumeration, credential reuse, privilege escalation, file exfiltration, and detection avoidance in a controlled training environment.

## Status

Documentation covers all three exercises. Supplied screenshots support the early enumeration, login, and BloodHound analysis stages; later procedures are documented from lab instructions with result evidence pending. Screenshot captions are included; image assets are not yet embedded.

## Portfolio Documentation

- [Exercise 1, Task 1 — Active Directory Enumeration and Account Correlation](exercises/exercise-01-task-01.md): analysis of supplied reference evidence, with professional figure labels and findings. 
- [Exercise 1, Task 2 — Identify Credential Reuse](exercises/exercise-01-task-02.md): unsuccessful GordonB login and confirmed credential reuse through Pablo's user-level WinRM session.

- [Exercise 2, Task 1 — Enumerate Active Directory](exercises/exercise-02-task-01.md): BloodHound collection, JSON import, and graph analysis, including the relationship-label discrepancy.

- [Exercise 2, Task 2 — Escalate User Privileges](exercises/exercise-02-task-02.md): prescribed membership validation; result evidence pending.
- [Exercise 2, Task 3 — Install Steganography Tool](exercises/exercise-02-task-03.md): OpenStego preparation workflow; result evidence pending.
- [Exercise 2, Task 4 — Simulated File Exfiltration](exercises/exercise-02-task-04.md): embedding, transfer, and recovery of lab placeholder data; result evidence pending.

- [Exercise 3 — Detection Avoidance](exercises/exercise-03-detection-avoidance.md): all four cleanup tasks, evidence interpretation, and privilege-rollback limits.
- [Final Lab Summary](LAB-SUMMARY.md): findings, tools, and evidence coverage.

## Objective

Develop an understanding of system hacking phases and attack techniques through guided exercises using the devices provided in the practice lab.

## Exercises

### Exercise 1 — Exploit Active Directory (AD)

- Review previous enumeration findings.
- Identify credential reuse.

### Exercise 2 — Exfiltrate a Sensitive File

- Enumerate Active Directory with BloodHound-Python.
- Analyze potential privilege escalation paths.

- Install a steganography tool.
- Practice exfiltrating a lab-provided sensitive file within the training environment.

### Exercise 3 — Detection Avoidance

- Examine PowerShell history deletion and tool removal.
- Explore clearing logs on the lab target.
- Restore user-level privileges.

## Learning Focus

The module covers system hacking phases and attack techniques, including how credential reuse and privilege escalation can affect system security and how detection avoidance can affect evidence available to defenders.

## Scope

All activities are limited to the authorized practice lab and its provided devices and files.
