# Exercise 2 — Exfiltrate a Sensitive File

## Task 1 — Enumerate Active Directory

**Stage:** Data collection completed in the supplied output; BloodHound graph analysis pending.  
**Environment:** Authorized Practice Labs training environment  
**Workstation:** PLABKALI  
**Domain:** `practicelabs.com`  
**Domain controller / nameserver:** `192.168.0.1`  
**Account:** `pablo`  
**Tools:** BloodHound-Python and BloodHound

## Objective

Collect Active Directory objects and relationships using the domain account identified in Exercise 1. Prepare the data for BloodHound analysis to investigate potential privilege escalation paths associated with Pablo's account.

BloodHound is a graph-based analysis and visualization tool. BloodHound-Python collects the directory data that BloodHound uses to examine account rights and relationships.

## Methodology

### 1. Open a Separate Kali Terminal Tab

A new terminal tab provides a local Kali shell for data collection while keeping the existing Evil-WinRM session available in the original tab.

**Figure 7 — Preparing a Local Terminal for Active Directory Collection**  
**Source:** `image(20261019-163546).png`  
**Caption:** Opening a new Kali terminal tab alongside the existing remote PowerShell session for Pablo.

### 2. Collect Domain Data with BloodHound-Python

The collector uses Pablo's domain credentials to query the lab domain. The password is replaced with a placeholder in this public documentation.

```bash
bloodhound-python -u pablo -p '<LAB_PASSWORD>' -ns 192.168.0.1 -d practicelabs.com -c All
```

| Parameter | Purpose |
| --- | --- |
| `-u pablo` | Specifies the domain username |
| `-p '<LAB_PASSWORD>'` | Supplies the account's lab password |
| `-ns 192.168.0.1` | Specifies the DNS server used for domain resolution |
| `-d practicelabs.com` | Identifies the domain to query |
| `-c All` | Selects the collector's `All` collection option |

The lab describes the collection output as JSON files for analysis in BloodHound. The `All` option requests the data covered by that collection mode; access permissions and collector support still determine what can be retrieved.

## Observed Results

The supplied terminal output shows a connection to `plabdc01.practicelabs.com`, directory enumeration, and computer queries. It ends with `Done in 00M 13S`.

| Object type | Reported count |
| --- | ---: |
| Domains | 1 |
| Computers | 4 |
| Users | 11 |
| Groups | 54 |
| Group Policy Objects (GPOs) | 3 |
| Organizational Units (OUs) | 2 |
| Containers | 22 |
| Trusts | 0 |

The collector queries `PLABDM02`, `PLABDM01`, `PLABWIN10`, and `PLABDC01` in the lab domain.

**Figure 8 — BloodHound-Python Active Directory Collection Results**  
**Source:** `image(20261019-163629).png`  
**Caption:** BloodHound-Python reports domain object counts, queries four computers, and completes collection in approximately 13 seconds.

## Findings and Interpretation

The output demonstrates that Pablo's domain account can retrieve directory information for subsequent relationship analysis. The collected objects provide the basis for examining group membership, permissions, and possible paths to higher privileges.

At this stage, the evidence shows successful collection rather than a verified privilege escalation path. The next step is to inspect the generated JSON files and analyze their relationships in BloodHound. No sensitive-file exfiltration is shown in this part of Exercise 2.

## Skills Demonstrated

- Separating local collection commands from a remote PowerShell session.
- Configuring authenticated Active Directory data collection.
- Interpreting domain object counts and collection output.
- Preparing evidence for graph-based permission analysis.

## Evidence Notes

This entry is based on the supplied lab instructions and screenshots. The screenshots are labeled above but are not embedded because their command lines expose the lab password. The JSON files themselves have not been supplied for inspection.

[Previous: Exercise 1, Task 2](exercise-01-task-02.md) | [Project overview](../README.md)
