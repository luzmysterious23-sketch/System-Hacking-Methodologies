# Exercise 2 — Exfiltrate a Sensitive File

## Task 2 — Escalate User Privileges

**Environment:** Authorized Practice Labs training environment  
**Evidence status:** Procedure documented from the supplied lab instructions. The attached screenshot shows terminal selection, not the membership-change results.

## Objective

Validate the privilege escalation route described by the lab by checking Pablo's group memberships, attempting the prescribed Domain Admins membership change, and reviewing the resulting group listing.

## Methodology

### 1. Review the Current Session's Groups

The lab returns to Pablo's remote PowerShell session and checks its security groups:

```powershell
whoami /groups
```

The lab notes identify Marketing Managers among Pablo's memberships. This check describes the current session's token.

**Figure 14 — Returning to the Remote-Session Terminal Tab**  
**Source:** `image(20261019-165153).png`  
**Caption:** The highlighted terminal tab indicates where to return for the remote-session commands. The visible terminal content shows collection and Neo4j output, not a completed privilege change.

### 2. Attempt the Lab's Prescribed Membership Change

```powershell
net group "Domain Admins" pablo /add /domain
```

This command requests that Pablo be added to the Domain Admins group. The lab attributes this ability to excessive permissions granted to Marketing Managers. As noted in Task 1, the supplied graph's relationship label differs from the lab's GenericAll explanation.

### 3. Review Domain Admins Membership

The supplied instructions then use:

```powershell
net group "Domain Admins"
```

The stated lab outcome is that Pablo appears in the group listing. A successful change followed by that listing would establish the directory membership change. An existing logon token may not immediately reflect newly added groups; a new authenticated session is a separate validation of effective access.

## Result to Document

| Check | Outcome described by the lab | Evidence available here |
| --- | --- | --- |
| Initial group review | Pablo belongs to Marketing Managers | Written instructions |
| Membership change | Pablo is added to Domain Admins | Written instructions; result screenshot not supplied |
| Follow-up group listing | Pablo appears in Domain Admins | Written instructions; result screenshot not supplied |

The lab describes vertical privilege escalation from an ordinary domain account to privileged group membership. This entry documents that prescribed outcome without presenting it as independently verified execution.

## Portfolio Evidence Labels

- **Domain Group Membership Before Escalation** — capture the relevant `whoami /groups` output.
- **Domain Admins Membership Change Result** — capture the command's success or failure message.
- **Pablo Listed in Domain Admins** — capture the follow-up group listing.

## Security Lesson

Excessive control over privileged groups can turn access to an ordinary account into a route to administrative access. Group nesting and delegated permissions should be examined separately when explaining how that route works.

[Previous: Task 1](exercise-02-task-01.md) | [Next: Task 3](exercise-02-task-03.md)
