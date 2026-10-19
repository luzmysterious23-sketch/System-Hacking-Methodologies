# Exercise 2 — Exfiltrate a Sensitive File

## Task 1 — Enumerate Active Directory

**Stage:** Collection and BloodHound graph review documented; privilege-change validation follows in Task 2.  
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

## BloodHound Import and Graph Analysis

### 3. Start the Neo4j Database

The lab's BloodHound version uses Neo4j as its graph database. The supplied terminal screenshot shows:

```bash
sudo neo4j console
```

The output ends with `Started.`, confirming database startup for this lab configuration.

**Figure 9 — Neo4j Database Startup Confirmed**  
**Source:** `image(20261019-164547).png`  
**Caption:** Neo4j starts successfully and reports its local database interfaces.

### 4. Import the Collected JSON Files

BloodHound is opened from the Kali application search. Using **Upload Data**, the seven JSON files in the home folder are selected together: computers, containers, domains, GPOs, groups, OUs, and users. The upload panel shows completed imports.

**Figure 10 — Selecting Seven Active Directory JSON Files**  
**Source:** `image(20261019-164714).png`  
**Caption:** The seven collection files are selected for import into BloodHound.

**Figure 11 — BloodHound Import Progress**  
**Source:** `image(20261019-164734).png`  
**Caption:** The upload panel displays completed entries as the directory data is imported.

### 5. Examine Paths to Domain Admins

With Pablo's account displayed, the lab opens **More Info → Analysis → Find Shortest Paths to Domain Admins** and selects `DOMAIN ADMINS@PRACTICELABS.COM` as the target group. The graph exposes relationships involving Marketing Managers and Domain Admins.

**Figure 12 — Selecting the Domain Admins Path Analysis**  
**Source:** `image(20261019-164844).png`  
**Caption:** BloodHound's built-in shortest-path analysis is selected to investigate routes to Domain Admins.

**Figure 13 — Reviewing the Marketing Managers Relationship to Domain Admins**  
**Source:** `image(20261019-164947).png`  
**Caption:** The graph displays Marketing Managers connected to Domain Admins, alongside other directory relationships.

## Findings and Interpretation

The lab instructions identify Pablo as a member of Marketing Managers and describe that group as having `GenericAll` over Domain Admins. This describes an excessive delegation that could permit modification of the privileged group.

**Evidence distinction:** The supplied graph visibly labels the Marketing Managers-to-Domain Admins connection `MemberOf`, rather than `GenericAll`. Group nesting and delegated control are different relationships. The graph therefore supports a connection between the groups but does not independently verify the specific permission described by the instructions. The relevant edge details or directory permissions would be needed to resolve this mismatch.

The portfolio records the lab's intended escalation path separately from the visible graph evidence. Task 2 documents the prescribed membership-change validation; successful elevation is not claimed from this graph alone.

## Skills Demonstrated

- Collecting and importing Active Directory relationship data.
- Starting the lab's Neo4j database.
- Using BloodHound's built-in path analysis.
- Distinguishing group membership from delegated permissions.
- Checking conclusions against visible evidence.

## Evidence Notes

Screenshots are labeled by their supplied filenames; images are not embedded. Earlier collection screenshots contain passwords. The JSON contents have not been supplied for independent inspection.

[Next: Task 2 — Escalate User Privileges](exercise-02-task-02.md) | [Project overview](../README.md)
