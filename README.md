# MS Partner Funding Navigator — Master Edition

All-in-one funding playbook for Microsoft partners in Indonesia. A single-file web app that puts **28 funding tracks** — migration subsidies, PoC credits, backend rebates/PAL, ISV Success, and co-marketing funds — into one searchable, bilingual (ID/EN) navigator.

**Live:** https://funding.developedbytoo.me

---

## What it does

The app answers the three questions a partner SE/AE asks on every deal:

1. **Which funding can this client actually claim?** → *Funding Finder* (filter by scenario, client readiness, client scale)
2. **What do I have to deliver to get paid?** → *Alur Klaim & PoE* (claim flow + Proof-of-Execution checklist per program)
3. **How do I bring it up in the meeting?** → *Skrip Pitching & Email AE* (bilingual pitch scripts and AE email templates)

Plus a master catalog with full eligibility detail for all 28 programs, and an official-reference tab linking every claim to its Microsoft source.

## Modules

| # | Tab | Contents |
|---|-----|----------|
| 1 | **Katalog Master** | All 28 programs as cards — estimate value, what's funded, eligibility, target client, PoE deliverables, presales tips, official source |
| 2 | **Funding Finder** | Guided wizard: scenario focus → client readiness stage → client scale → ranked program recommendations |
| 3 | **Alur Klaim & PoE** | Step-by-step claim flow and the PoE document checklist per program |
| 4 | **Skrip Pitching & Email AE** | Pitch scripts and AE email templates for each funding motion |
| 5 | **Referensi & Verifikasi Resmi** | Official Microsoft source links for verification |

## The 28 programs

### A. Migration & Modernization (6)
| Program | Estimate |
|---|---|
| Azure Accelerate (AWS / GCP / VMware / On-Prem VM Migration) | $6,000 – $50,000+ (ACR tiered) |
| Database Migration to Azure (SQL, Oracle, PostgreSQL, MySQL) | $6,000 – $35,000 |
| SAP on Azure Migration & RISE Modernization | $15,000 – $50,000+ |
| Azure VMware Solution (AVS) Rapid Migration | $10,000 – $40,000+ |
| Google Workspace to M365 Switcher Incentive | $2,000 – $12,000+ / bonus seats |
| Security Competitor Switcher (SIEM / EDR → Sentinel & Defender) | $4,000 – $15,000 |

### B. Data, AI & Copilot (6)
| Program | Estimate |
|---|---|
| Microsoft Fabric Assessment & PoC | $3,500 – $12,000 |
| Azure AI Foundry & Custom AI Agents | $5,000 – $20,000 |
| M365 Copilot Envisioning & Readiness | $3,500 – $5,500 |
| M365 Copilot Deployment Accelerator | $5,000 – $15,000 |
| Microsoft Purview & Data Governance Workshop (UU PDP) | $4,000 – $7,500 |
| Legacy BI / Synapse to Fabric Modernization | $8,000 – $30,000+ |

### C. Security, Modern Work & BizApps (5)
| Program | Estimate |
|---|---|
| Threat Protection (Defender & Sentinel) Workshop | $4,000 – $8,500 |
| Zero Trust & Entra ID Security Assessment | $3,500 – $6,000 |
| M365 E3/E5 & Business Premium Deployment | $2,500 – $10,000 |
| Windows 365 & Azure Virtual Desktop (AVD) | $4,000 – $15,000 |
| Dynamics 365 & Power Platform Catalyst / Pre-sales | $3,500 – $8,000 |

### D. Tactical Funds & PoC Credits (3)
| Program | Estimate |
|---|---|
| ECIF — End Customer Investment Funds (custom PoC & strategic deals) | $5,000 – $50,000+ |
| Azure Sponsorship / PoC Credits (direct cloud credits) | $1,000 – $5,000+ |
| Enterprise Skills Initiative (ESI) & ECIF Customer Skilling | Free (ESI) / $3,000 – $15,000 (ECIF) |

### E. Rebates, PAL & CPOR (4)
| Program | Estimate |
|---|---|
| CSP Transactional Rebates (back-end cashback) | 3% – 10%+ of transaction value |
| Net-New & Upsell Accelerator Rebates (E5, Copilot, BP) | +5% – +15% bonus |
| PAL (Partner Admin Link) — Azure consumption incentives | ACR credits & MCI Azure incentives |
| CPOR (Claiming Partner of Record) — usage & adoption | Usage incentives & designation score |

### F. ISV, Marketing & Partner Benefits (4)
| Program | Estimate |
|---|---|
| ISV Success Program (for SaaS / app builders) | Benefits worth up to $128,000+ |
| Marketplace Rewards (co-sell & joint marketing) | Free marketing & co-sell support |
| Partner Co-op Marketing Funds (events, booths, webinars, ads) | Reimbursement up to 100% of co-op balance |
| MDF, IUR (free internal licenses) & FastTrack Ready Partner | Save tens of thousands of $/year |

## Tech

- **Single file** — `index.html`, no build step, no backend
- Tailwind CSS via CDN, Google Fonts (Inter)
- Vanilla JS (no framework), all program data inline in `FUNDING_PROGRAMS`
- Bilingual ID/EN string table, no external API calls
- Works offline except for the Tailwind/font CDNs

## Deploy

Static hosting — serve `index.html` from any web root.

nginx example (already in use):

```nginx
server {
    listen 443 ssl;
    server_name funding.developedbytoo.me;
    root /var/www/html/funding;
    index index.html;
    location / { try_files $uri $uri/ =404; }
}
```

## Updating

Program data lives in the `FUNDING_PROGRAMS` array (search for `const FUNDING_PROGRAMS`). Each entry has `id`, `category`, `recipient`, and bilingual `name` / `estimate` / `shortDesc` / `whatFunded` / `requirement` / `targetClient` / `poeList` / `presalesTips` fields, plus `sourceName` / `sourceUrl` and a `wizardMeta` block that drives the Funding Finder filters.

To republish after an edit on the server:

```bash
cp /var/www/html/funding/index.html /home/ubuntu/Funding-MS/index.html
cd /home/ubuntu/Funding-MS
git add index.html && git commit -m "update funding programs"
git push
```
