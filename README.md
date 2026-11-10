# ServiceNow SIR Runbooks

Click by click runbooks for configuring ServiceNow Security Incident Response (SIR). Each runbook is written so someone new to the platform can follow it without guessing, and so the change can be promoted cleanly from development to test to production.

## Runbooks

| Runbook | What it covers |
|---|---|
| [Add subcategories](docs/add-subcategories.md) | Create a scoped update set, add subcategories under existing SIR categories, verify the category to subcategory dependency, and wrap up for promotion |

## Add subcategories at a glance

| Part | Step |
|---|---|
| 0 | Create an update set in the **Security Incident Response** scope and make it current |
| 1 | Confirm the scope and update set from the globe icon |
| 2 | Look up the parent category's stored **Value** |
| 3 | Add each subcategory with a label, value, parent, and sequence |
| 4 | Verify the subcategories appear only under their parent |
| 5 | Confirm the update set contents and mark it **Complete** |

## Before you start

- **Roles:** you need a role that can manage SIR categories (typically `sn_si.admin`) and one that can create update sets (typically `admin`). Your platform team may use different roles.
- **Environment:** do the work in a development instance, then promote the update set.
- **Release differences:** menu labels vary by ServiceNow release. If a screen does not match, look for the same feature under a nearby menu. Older releases without Category Management store subcategories as `sys_choice` records, which the runbook also covers.

## Conventions

- **Labels** are exactly what analysts see, including capitalization and hyphens.
- **Values** are lowercase with underscores, which keeps scripts, filters, and integrations simple.
- **Sequences** use gaps of 10, so new entries can be inserted later without renumbering.
- **Values stay specific:** a generic value such as `task` is prefixed (for example `ti_task`) so reports never mix it with a same named subcategory under another category.
