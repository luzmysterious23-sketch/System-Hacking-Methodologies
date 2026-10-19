# Exercise 2 — Exfiltrate a Sensitive File

## Task 3 — Install Steganography Tool

**Environment:** Authorized Practice Labs training environment  
**Evidence status:** Workflow documented from the supplied instructions; installation screenshots have not been supplied.

## Objective

Prepare PLABWIN10 for the lab's steganography demonstration by transferring and installing OpenStego in Pablo's user account.

## Workflow

1. Open a new local terminal tab on PLABKALI and start the temporary file server from the directory containing the installer:
   ```bash
   python3 -m http.server
   ```
2. Sign in to PLABWIN10 using Pablo's lab account.
3. Use Windows PowerShell to retrieve the installer from the Kali host:
   ```powershell
   Invoke-WebRequest -Uri "http://192.168.0.5:8000/OpenStego.exe" -Outfile "C:\Users\pablo\Desktop\OpenStego.exe"
   ```
4. Launch the downloaded installer:
   ```powershell
   C:\Users\pablo\Desktop\OpenStego.exe
   ```
5. Select **Install for me only**, accept the license agreement, continue through the setup options, and finish the installation.

The supplied instructions identify OpenStego version 0.8.4 for this lab.

## Technical Clarification

The HTTP command uses port **8000**, which matches the download URL. The note referring to port 8080 is inconsistent with those commands. Python serves the current directory; the installer must be located in that served directory.

PowerShell is a native Windows tool used for the download. OpenStego is an added application. These are distinct parts of the workflow.

## Portfolio Evidence Labels

| Label | Evidence to capture |
| --- | --- |
| Temporary Lab File Server Started | Kali terminal showing the HTTP server and port |
| OpenStego Installer Transferred to PLABWIN10 | Download result and installer location |
| OpenStego Installation Completed | Installer completion screen |

## Outcome Described by the Lab

OpenStego is installed for Pablo on PLABWIN10, preparing the workstation for Task 4. This is the instructed outcome; completion is not independently verified by the materials supplied so far.

[Previous: Task 2](exercise-02-task-02.md) | [Next: Task 4](exercise-02-task-04.md)
