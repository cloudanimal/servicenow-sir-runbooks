# Copilot Prompt: Recreate the Subcategory Runbook

Paste everything inside the box into Microsoft Copilot. Copilot tends to paraphrase and "improve" content, so the prompt carries the full document and tells it not to change anything.

**Tips**

- For a Word document or OneNote page, add a first line such as *"Output this as a Word document."* Copilot in Word or Loop handles tables better than Copilot chat.
- Spot check the tables afterward. Copilot is most likely to change `ti_task` back to `task` or renumber the sequences. The "Copilot Notes" section gives it somewhere to put opinions instead of editing your content.

```text
You are helping me document a ServiceNow configuration task. Reproduce the document below EXACTLY as written. Do not summarize, shorten, reword, reorder, add steps, remove steps, or add commentary. Keep every heading, step number, field name, value, and table row. Format it as a clean document with headings, numbered steps, and tables. If something seems wrong to you, still reproduce it as written, then list any concerns separately at the very end under a heading called "Copilot Notes".

=== DOCUMENT START ===

ServiceNow SIR: Adding Subcategories Under Forensics and Threat Intelligence

PART 0: CREATE THE UPDATE SET

1. Click the globe icon at the top right and set Application scope to Security Incident Response first. Update sets belong to one scope, so set the scope before creating it.
2. In the filter navigator, type Local Update Sets. It is under System Update Sets.
3. Click New.
4. Fill in:
   - Name: follow the team convention. If there is none, use something like "CHG0012345 SIR Forensics and TI subcategories" with the real ticket number.
   - Application: confirm it shows Security Incident Response. If it shows Global, stop, go back to Step 1, and fix the scope.
   - State: leave it at In progress.
   - Description: for example, "Adds 15 subcategories under Forensics and 4 under Threat Intelligence for SIR."
   - Release date: optional, leave blank unless the team uses it.
5. Click Submit and Make Current. This creates the update set and makes it active in one step. Plain Submit creates it but does not make it active.

PART 1: CONFIRM SETUP

6. Click the globe icon again and confirm both:
   - Application scope: Security Incident Response
   - Update set: the one just created
   If either is wrong, fix it before touching any subcategory.

PART 2: GET THE PARENT CATEGORY VALUE (once per category)

7. Open the Security Incident Response Workspace.
8. Go to Administration > Category Management > Category.
9. Open the parent category (Forensics or Threat Intelligence).
10. Write down its Value exactly. Close it without changing anything.

PART 3: ADD EACH SUBCATEGORY (repeat for every one)

11. Go to Category Management > Subcategory.
12. Click New.
13. Fill in:
   - Label: the name analysts see
   - Value: lowercase with underscores
   - Category / Dependent value: the parent value from Step 10
   - Sequence: controls display order
   - Inactive: leave unchecked
   - Hint: optional one-line description
14. Click Save.
15. Return to Step 12 for the next subcategory.

PART 4: VERIFY (once per category)

16. Open a test security incident in dev.
17. Set Category to the parent category.
18. Open the Subcategory dropdown and confirm every new entry appears in the correct order.
19. Switch to a different category and confirm the new entries disappear.
20. Back out without saving.

PART 5: WRAP UP

21. Open the update set and confirm it lists one record per subcategory added: 15 for Forensics and 4 for Threat Intelligence, 19 total.
22. Set the update set to Complete when the team process says to, so it can be promoted.

TIP: If you step away or switch to work in another scope, check the globe icon again when you return. ServiceNow can switch the active update set when the scope changes.

SUBCATEGORIES: FORENSICS (15)

| Label | Value | Sequence |
| BusinessContinuity | business_continuity | 10 |
| Compliance | compliance | 20 |
| CyberResilience | cyber_resilience | 30 |
| DLP | dlp | 40 |
| EnhancedMonitoring | enhanced_monitoring | 50 |
| FinancialCrimes | financial_crimes | 60 |
| Fraud | fraud | 70 |
| Geolocation | geolocation | 80 |
| HR | hr | 90 |
| InsiderRisk | insider_risk | 100 |
| InsiderRisk-Escalate | insider_risk_escalate | 110 |
| Legal | legal | 120 |
| Monitoring-Escalate | monitoring_escalate | 130 |
| Regulatory | regulatory | 140 |
| SecurityPolicy | security_policy | 150 |

SUBCATEGORIES: THREAT INTELLIGENCE (4)

| Label | Value | Sequence |
| Threat Hunt | threat_hunt | 10 |
| RFI | rfi | 20 |
| Task | ti_task | 30 |
| File Analysis | file_analysis | 40 |

Note: Before adding the Threat Intelligence subcategories, repeat Part 2 for the Threat Intelligence category so they are attached to the correct parent.

=== DOCUMENT END ===
```
