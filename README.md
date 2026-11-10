# ServiceNow SIR Runbooks

Step by step runbooks for configuring ServiceNow Security Incident Response (SIR). Written for analysts and engineers who need exact clicks, not concepts.

## Contents

| File | What it covers |
|---|---|
| [docs/add-subcategories.md](docs/add-subcategories.md) | Create an update set, then add subcategories under existing SIR categories, verify them, and wrap up for promotion |

## Example data

The subcategory names in this repository are generic examples: 15 under **Forensics** and 4 under **Threat Intelligence**. Replace them with your own before use.

## Notes

- Menu labels vary by ServiceNow release. If a screen does not match, look for the same feature under a nearby menu.
- Always work inside the **Security Incident Response** application scope and a named update set, so your changes can be promoted from development to test to production.
