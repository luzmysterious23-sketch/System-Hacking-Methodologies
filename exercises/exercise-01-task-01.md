# Exercise 1 — Exploit Active Directory (AD)

## Task 1 — Review Previous Enumeration

**Project:** System Hacking Methodologies  
**Environment:** Authorized Practice Labs training environment  
**Documentation scope:** Review of the supplied lab instructions and reference screenshots. The credential validation results are documented in [Task 2](exercise-01-task-02.md).

## Objective

Review existing Nmap and SQLmap findings to identify the role of PLABDC01 and determine whether usernames recovered from the lab web application also exist in Active Directory. This establishes candidate accounts for the next stage of the credential-reuse investigation.

## Lab Environment

| Device | Operating system / role | Use in this task |
| --- | --- | --- |
| PLABKALI | Kali Linux workstation | Review saved reports, prepare the username list, and perform Kerberos enumeration |
| PLABDC01 | Windows Server 2019 domain controller | Active Directory target at `192.168.0.1` |
| PLABDM01 | Source of previously collected SQLmap results | Provide application account names for comparison |

**Domain:** `practicelabs.com`  
**Tools:** Nmap, the `krb5-enum-users` NSE script, saved SQLmap output, and nano.

## Methodology and Evidence

### 1. Review the existing Nmap report

The saved `PLABDC01_nmap_scan.html` report identifies the target as `192.168.0.1`. The lab notes describe LDAP, LDAPS, and Kerberos services, a combination consistent with a server supporting Active Directory. The later enumeration output directly shows TCP port 88 open for Kerberos.

**Figure 1 — Review of the Existing PLABDC01 Nmap Report**  
*Reference screenshot: `image(20261019-154053).png`.*  
Caption: Saved Nmap report for `192.168.0.1`, reviewed to understand the target before focused enumeration. The visible image shows the scan summary; the LDAP and LDAPS interpretation comes from the accompanying lab notes.

### 2. Extract candidate usernames from SQLmap results

The supplied `PLABDM01_SQLmap_Results.jpg` shows five usernames in the application's `dvwa.users` table: `admin`, `gordonb`, `1337`, `pablo`, and `smithy`. These names provide a focused list for checking whether application accounts overlap with domain accounts.

**Figure 2 — Application Usernames Identified in Prior SQLmap Results**  
*Reference screenshot: `image(20261019-154148).png`.*  
Caption: Previously collected SQLmap output containing five application usernames used as candidates for Active Directory enumeration.

### 3. Prepare the username list

The candidate names are entered into `users.txt`, with one username per line:

```text
admin
gordonb
1337
pablo
smithy
```

The saved-file screenshot displays nano's `Wrote 5 lines` confirmation. This file supplies the user database for the Nmap enumeration script.

**Figure 3 — Saved Username List for Domain Enumeration**  
*Reference screenshot: `image(20261019-160641).png`.*  
Caption: The five candidate usernames saved in `users.txt`, ready for comparison against the lab domain.

### 4. Compare candidate usernames against the domain

The lab uses the following command to query Kerberos on the domain controller:

```bash
nmap -Pn -p 88 --script=krb5-enum-users --script-args 'krb5-enum-users.realm=practicelabs.com,userdb=users.txt' 192.168.0.1
```

The command targets TCP port 88 and uses `users.txt` as the candidate list for the `practicelabs.com` realm. Straight quotes are used here so the command is suitable for a shell.

**Figure 4 — Kerberos Enumeration Identifies Matching Domain Accounts**  
*Reference screenshot: `image(20261019-161035).png`.*  
Caption: Nmap reports TCP port 88 open and returns the principals `pablo@practicelabs.com` and `gordonb@practicelabs.com`.

## Findings

| Finding | Supporting evidence | Interpretation |
| --- | --- | --- |
| Kerberos is available on the target | `88/tcp open kerberos-sec` | The target exposes the authentication service used for this enumeration |
| Two candidate usernames are returned as domain principals | `pablo@practicelabs.com` and `gordonb@practicelabs.com` | These application usernames also appear in the lab domain |
| Password reuse remains unconfirmed | The displayed command enumerates usernames; it does not validate passwords | Matching usernames alone do not establish that the same passwords work across systems |

The other three candidate usernames are not returned in the displayed output. This task records the two positive matches without treating omitted names as definitive proof that those accounts do not exist.

## Security Significance

Account information exposed by one application can help identify accounts elsewhere in an environment. Here, previously collected application usernames narrowed the domain enumeration to a small candidate list. The result demonstrates why protecting application account data matters beyond the application itself.

## Skills Demonstrated by This Analysis

- Interpreting existing network enumeration findings.
- Correlating application usernames with domain identities.
- Preparing structured input for an enumeration tool.
- Reading Kerberos enumeration output.
- Distinguishing verified findings from conclusions that require additional testing.

## Next Step

[Task 2 — Identify Credential Reuse](exercise-01-task-02.md) continues this investigation and documents the login results. Task 1 establishes username matches; Task 2 confirms password reuse for Pablo.

## Screenshot Selection

The four figures above capture the meaningful evidence for a portfolio. The remaining screenshots show folder navigation, opening nano, or an earlier view of the same username list; they are supporting workflow images rather than separate findings. Figure labels currently refer to the supplied source filenames; images are not embedded in this document.
