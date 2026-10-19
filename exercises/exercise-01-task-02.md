# Exercise 1 — Exploit Active Directory (AD)

## Task 2 — Identify Credential Reuse

**Environment:** Authorized Practice Labs training environment  
**Tools:** Kali Linux, Evil-WinRM, Windows Remote Management (WinRM)  
**Target:** PLABDC01 (`192.168.0.1`)

## Objective

Test whether application credentials associated with the domain usernames identified in Task 1 also allow remote access to the domain controller.

## Methodology

The two candidate accounts were tested with Evil-WinRM using the credentials from the earlier SQLmap results. Passwords are replaced with placeholders in this public documentation.

```bash
evil-winrm -i 192.168.0.1 -u gordonb -p '<LAB_PASSWORD>'
evil-winrm -i 192.168.0.1 -u pablo -p '<LAB_PASSWORD>'
```

The `-i` parameter specifies the remote host, `-u` specifies the account, and `-p` supplies its password. Each placeholder represents that account's own lab password.

## Results and Evidence

### Figure 5 — Unsuccessful WinRM Access Attempt for GordonB

**Source:** `image(20261019-163132).png`  
**Caption:** The login attempt for `gordonb` returns `WinRM::WinRMAuthorizationError` and exits with code 1. No remote shell is established.

This result does not confirm password reuse for GordonB. The error alone does not distinguish an incorrect password from restrictions on remote access.

### Figure 6 — Confirmed Credential Reuse Through Pablo's WinRM Session

**Source:** `image(20261019-163220).png`  
**Caption:** The application credentials for `pablo` establish a remote PowerShell session on PLABDC01, displaying the prompt `C:\Users\pablo\Documents>`.

Together with the prior SQLmap output and domain enumeration, the successful login confirms password reuse between Pablo's application and domain accounts in this lab. The lab identifies this as a user-level session.

| Account | Observed result | Finding |
| --- | --- | --- |
| `gordonb` | Authorization error | Credential reuse unconfirmed |
| `pablo` | Remote PowerShell session established | Credential reuse confirmed |

## Security Significance

Reusing a password across application and domain accounts can allow an application-level exposure to lead to domain access. The lab describes this as horizontal privilege escalation. The evidence specifically demonstrates domain-authenticated remote access; it does not demonstrate administrator privileges.

## Skills Demonstrated

- Correlating application credentials with domain identities.
- Interpreting WinRM login outcomes.
- Distinguishing user-level access from administrative access.
- Documenting confirmed credential reuse.

## Next Stage

[Exercise 2, Task 1 — Enumerate Active Directory](exercise-02-task-01.md) uses the domain account to collect data for BloodHound analysis.

Screenshot captions are provided here; the original images are not embedded because their command lines display passwords.

[Project overview](../README.md)
