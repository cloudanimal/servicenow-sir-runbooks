# Adding Subcategories Under Forensics and Threat Intelligence

This runbook adds 15 subcategories under the **Forensics** category and 4 under the **Threat Intelligence** category in ServiceNow Security Incident Response (SIR). The same steps work for any subcategory under any category.

## Part 0: Create the update set

1. Click the **globe icon** at the top right and set **Application scope** to **Security Incident Response** first. Update sets belong to one scope, so set the scope before you create it.
2. In the filter navigator, type **Local Update Sets**. It is under **System Update Sets**.
3. Click **New**.
4. Fill in:
   - **Name:** follow your team's convention. If there is none, use something like `CHG0012345 SIR Forensics and TI subcategories` with your real ticket number.
   - **Application:** confirm it shows **Security Incident Response**. If it shows **Global**, stop, go back to Step 1, and fix the scope.
   - **State:** leave it at **In progress**.
   - **Description:** for example, *Adds 15 subcategories under Forensics and 4 under Threat Intelligence for SIR.*
   - **Release date:** optional. Leave it blank unless your team uses it.
5. Click **Submit and Make Current**. This creates the update set and makes it active in one step. Plain **Submit** creates it but does not make it active.

## Part 1: Confirm your setup

6. Click the **globe icon** again and confirm both:
   - **Application scope:** Security Incident Response
   - **Update set:** the one you just created

   If either one is wrong, fix it before you touch any subcategory.

## Part 2: Get the parent category value (once per category)

7. Open the **Security Incident Response Workspace**.
8. Go to **Administration > Category Management > Category**.
9. Open the parent category (**Forensics** or **Threat Intelligence**).
10. Write down its **Value** exactly, including capitalization. Close it without changing anything.

## Part 3: Add each subcategory (repeat for every one)

11. Go to **Category Management > Subcategory**.
12. Click **New**.
13. Fill in:
    - **Label:** the name analysts see
    - **Value:** lowercase with underscores
    - **Category / Dependent value:** the parent value from Step 10
    - **Sequence:** controls the display order
    - **Inactive:** leave unchecked
    - **Hint:** optional one line description
14. Click **Save**.
15. Return to Step 12 for the next subcategory.

## Part 4: Verify (once per category)

16. Open a test security incident in development.
17. Set **Category** to the parent category.
18. Open the **Subcategory** dropdown and confirm every new entry appears, in the correct order.
19. Switch to a different category and confirm the new entries disappear. This proves the dependency is wired correctly.
20. Back out without saving.

## Part 5: Wrap up

21. Open your update set and confirm it lists one record per subcategory added: 15 for Forensics and 4 for Threat Intelligence, 19 in total.
22. Set the update set to **Complete** when your team's process says to, so it can be promoted.

> **Tip:** If you step away, or switch to work in another scope, check the globe icon again when you return. ServiceNow can switch the active update set when the scope changes. If a record lands in the wrong update set, it can be moved, but it is easier to avoid.

## Subcategories: Forensics (15)

| Label | Value | Sequence |
|---|---|---|
| BusinessContinuity | `business_continuity` | 10 |
| Compliance | `compliance` | 20 |
| CyberResilience | `cyber_resilience` | 30 |
| DLP | `dlp` | 40 |
| EnhancedMonitoring | `enhanced_monitoring` | 50 |
| FinancialCrimes | `financial_crimes` | 60 |
| Fraud | `fraud` | 70 |
| Geolocation | `geolocation` | 80 |
| HR | `hr` | 90 |
| InsiderRisk | `insider_risk` | 100 |
| InsiderRisk-Escalate | `insider_risk_escalate` | 110 |
| Legal | `legal` | 120 |
| Monitoring-Escalate | `monitoring_escalate` | 130 |
| Regulatory | `regulatory` | 140 |
| SecurityPolicy | `security_policy` | 150 |

## Subcategories: Threat Intelligence (4)

| Label | Value | Sequence |
|---|---|---|
| Threat Hunt | `threat_hunt` | 10 |
| RFI | `rfi` | 20 |
| Task | `ti_task` | 30 |
| File Analysis | `file_analysis` | 40 |

> **Note:** Before adding the Threat Intelligence subcategories, repeat Part 2 for the **Threat Intelligence** category so they attach to the correct parent.

## Conventions used

- **Labels** match exactly what analysts should see, including capitalization and hyphens.
- **Values** are lowercase with underscores. Hyphens usually work, but underscores never cause trouble in scripts, filters, or integrations.
- **Sequences** use gaps of 10, so new entries can be inserted later (for example 15 or 25) without renumbering.
- **`ti_task` instead of `task`:** a generic value like `task` could collide with a subcategory under another category later and muddy reports. The label still reads **Task**.

## Legacy releases

If your release has no Category Management screen, subcategories are stored as choice records. Add `sys_choice` records on table `sn_si_incident`, element `subcategory`, with `dependent_value` set to the parent category value. The labels, values, and sequences are the same.
