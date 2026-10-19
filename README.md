# System Hacking Methodologies

Hands-on cybersecurity lab exploring Active Directory enumeration, credential reuse, privilege escalation, file exfiltration, and detection avoidance in a controlled training environment.

## Status

In progress. This README describes the planned exercises and learning objectives. Results and screenshots will be added as the lab is completed.

## Portfolio Documentation

- [Exercise 1, Task 1 — Active Directory Enumeration and Account Correlation](exercises/exercise-01-task-01.md): analysis of supplied reference evidence, with professional figure labels and findings. 
- [Exercise 1, Task 2 — Identify Credential Reuse](exercises/exercise-01-task-02.md): unsuccessful GordonB login and confirmed credential reuse through Pablo's user-level WinRM session.

- [Exercise 2, Task 1 — Enumerate Active Directory](exercises/exercise-02-task-01.md): BloodHound-Python data collection and domain object findings; graph analysis pending.

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
