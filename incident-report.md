@"
# Incident Report: Repeated Failed Authentication Attempts (Azure Entra ID)

## 1. Executive Summary
Multiple failed authentication attempts were observed for a test Azure Entra ID user with a privileged role assignment. This activity was investigated using Azure Entra **Sign-in Logs** and correlated with **Audit Logs** to validate role assignment context and identify IAM risk. The pattern is consistent with password guessing or credential stuffing against an identity that retains elevated permissions.

---

## 2. Environment
- Identity Provider: Azure Entra ID
- Log Sources:
  - Sign-in logs
  - Audit logs
- Account Under Review: `jdoe_test`

---

## 3. Timeline (UTC or Local Time)
- T0 — User created: `jdoe_test`
- T1 — Baseline sign-in completed (success)
- T2 — Role assigned (RBAC): <role name here>
- T3 — Multiple failed sign-in attempts observed
- T4 — Investigation completed and recommendations documented

---

## 4. Detection & Evidence
### 4.1 Detection Source
- Azure Entra ID **Sign-in Logs**

### 4.2 Indicators Observed
- Repeated failed sign-ins for `jdoe_test`
- Same/different IP addresses (document what you saw)
- Browser-based attempts

### 4.3 Supporting Evidence
- Screenshot(s) of failed sign-in events (Status = Failure)
- Screenshot of audit log event showing role assignment

(See `./evidence/`)

---

## 5. Analysis
- The account `jdoe_test` held a role assignment at the time of repeated failed sign-in attempts.
- Repeated authentication failures increase likelihood of:
  - Password guessing
  - Credential stuffing
  - Attempted unauthorized access
- Privileged role context increases potential impact if authentication succeeds.

---

## 6. Impact / Risk
- If authentication succeeds, attacker may gain access consistent with assigned role.
- Incomplete access governance (roles not reviewed) increases blast radius.

---

## 7. Remediation
- Remove unnecessary role assignments from accounts no longer requiring access.
- Reset password and verify MFA / Conditional Access enforcement.
- Review recent sign-in events for other privileged identities.
- Validate offboarding and access review procedures.

---

## 8. Prevention
- Enforce Joiner/Mover/Leaver (JML) automation
- Require MFA and Conditional Access for privileged roles
- Periodic access reviews for admin roles
- Alerting thresholds for failed sign-in bursts (e.g., N failures in M minutes)

---

## 9. Lessons Learned
- Identity telemetry requires correlating authentication events with access changes.
- Privileged roles elevate severity of otherwise common authentication failures.
"@ | Out-File -Encoding utf8 incident-report.md
