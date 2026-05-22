# Contoso Bikes — D365 F&O Implementation Repository

This repository contains the configuration data, business rules, and implementation artifacts for the **Contoso Bikes Inc.** Microsoft Dynamics 365 Finance & Supply Chain Management deployment.

---

## Company Overview

**Contoso Bikes Inc.** is a US-based bicycle manufacturer and wholesale distributor (B2B), selling to retail partners and distributors across four US regions. The company is migrating from its legacy ERP/analytics platform to D365 F&O under legal entity **`CBKS`**.

| Attribute | Detail |
|-----------|--------|
| Industry | Bicycle Manufacturing & Distribution |
| Legal Entity | `CBKS` — Contoso Bikes Inc. |
| Currency | USD |
| Go-Live Target | FY2026 |
| Source System | Legacy ERP / Analytics Platform |

---

## Repository Structure

```
CONTOSOBIKES/
├── data/                        # Master data files organized by domain
│   ├── account_structures/      # Chart of accounts structures
│   ├── approved_vendors/        # Approved vendor catalog (parts & components)
│   ├── boms/                    # Bills of Materials for all bike SKUs
│   ├── chart_of_accounts/       # Main account definitions
│   ├── customers/               # Customer master records
│   ├── parts/                   # Raw parts and components
│   ├── products/                # Finished goods product catalog
│   ├── purchase_orders/         # Sample purchase orders
│   ├── routes/                  # Production routing data
│   ├── sales_orders/            # Sample sales orders
│   ├── sites/                   # Warehouse sites and locations
│   ├── vendors/                 # Vendor master records
│   ├── work_centers/            # Manufacturing work centers
│   └── ...                      # Additional configuration domains
├── content/                     # Reference documentation and sample data
│   ├── COMPANY_PROFILE.md       # Full company profile and specifications
│   ├── Sample_Bikes_Sales_content/  # Bike sales model and CSV data
│   └── ...
├── scripts/                     # PowerShell automation scripts
│   ├── cost-rollup.ps1          # Cost rollup automation
│   └── update-product-sourcing.ps1
├── D365_Migration_Specification.md  # Detailed migration specification
└── Implementation_Plan.md       # Phased D365 implementation plan
```

---

## Product Catalog

9 product lines across 42 SKUs, with prices ranging from $249 to $7,900:

| Code | Category | Price Range |
|------|----------|-------------|
| RO | Road Bike | $525 – $721 |
| BX | BMX | $249 – $799 |
| CC | Cyclo-cross Bike | $1,144 – $1,361 |
| MB | Mountain Bike | $649 – $3,999 |
| RC | Racing Bike | $1,999 – $5,499 |
| DB | Downhill Bike | $1,199 – $1,499 |
| EB | eBike | $1,500 – $7,900 |
| CB | Cruiser | $288 – $399 |
| HB | Hybrid Bike | $379 – $899 |

---

## Implementation Phases

| Phase | Scope | Timeline |
|-------|-------|----------|
| Phase 1 | Foundation — legal entity, currencies, fiscal calendar, ledger | Week 1–2 |
| Phase 2 | Inventory & products — items, BOMs, routes, work centers | Week 3–4 |
| Phase 3 | Procurement — vendors, purchase orders, accounts payable | Week 5–6 |
| Phase 4 | Sales — customers, sales orders, accounts receivable | Week 7–8 |
| Phase 5 | Costing & manufacturing — cost categories, production orders | Week 9–10 |

See [Implementation_Plan.md](Implementation_Plan.md) for the full phased task list and [D365_Migration_Specification.md](D365_Migration_Specification.md) for migration details.

---

## Sales Regions

| Region | Code | Coverage |
|--------|------|----------|
| Americas HQ | AMER | Mid-Atlantic, Midwest |
| West Coast | WEST | CA, OR, WA, NV, AZ, UT, CO |
| East Coast | EAST | NY, PA, MA, CT, MI, NC, SC, MD |
| Southern US | SOUTH | TX, FL, LA, GA |

---

## Related Documentation

- [Company Profile](content/COMPANY_PROFILE.md)
- [Sample Bike Sales Data](content/Sample_Bikes_Sales_content/README.md)
