# Costing Configuration — CBKS (Contoso Bikes)

## Overview

This document covers the manufacturing costing infrastructure configured for the CBKS legal entity in D365 Finance & Supply Chain Management.

---

## 0. Calculation Group

A BOM calculation group controls how cost calculations behave (warnings, explosion stops, cost price methods). All released products in CBKS are assigned to the STD group.

| Field | Value |
|-------|-------|
| Group ID | STD |
| Group Name | Standard Calculation |
| Company | cbks |
| Zero Consumption Warning | Yes |
| No Active BOM Warning | Yes |
| No Active Route Warning | Yes |
| Zero Cost Price Warning | Yes |
| Stop Explosion at Item | No |
| Unit Cost Calculation Method | *(default)* |
| Sales Price Calculation Method | *(default)* |

### Assignment

All released products in CBKS have `CostCalculationGroupId = STD` set on the product record (Engineer fast tab). This was applied via OData bulk update to `ReleasedProductsV2`.

### OData Entity

- **Entity**: `CostCalculationGroups`
- **Key**: `dataAreaId` + `GroupId`
- **Product field**: `ReleasedProductsV2.CostCalculationGroupId`

---

## 1. Costing Version

| Field | Value |
|-------|-------|
| Version ID | STD |
| Name | Standard Cost |
| Costing Type | Standard |
| Explosion Mode | Single Level |
| Default From Date | *(none)* |
| Purchase Price Model | Purchase Price (from trade agreements) |
| Cost Price Model | Item Cost Price |
| Fallback Principle | Current Active |
| Unit Price Incl. Charges | Yes |
| Recording Restriction | Yes (Site: AMER) |
| Restrict Calculation | Yes |
| Block Version | No |
| Block Activation | No |
| Allow Purchase Prices | Yes |
| Allow Cost Prices | Yes |
| Allow Sales Prices | No |
| Round Off Calculation | No |
| Profit Setting | Standard |

### Purpose
The STD costing version holds standard costs for all manufactured and purchased items at site AMER. It supports single-level BOM explosion and uses purchase trade agreement prices as the basis for raw material costs.

---

## 2. Cost Groups

Cost groups segment the total manufactured cost into reporting categories.

| Group ID | Name | Type | Behavior |
|----------|------|------|----------|
| MAT-FRM | Frame Materials | Direct Materials | Variable |
| MAT-CMP | Component Materials | Direct Materials | Variable |
| MAT-MSC | Misc Materials | Direct Materials | Variable |
| LAB-ASM | Assembly Labor | Direct Manufacturing | Variable |
| LAB-FIN | Finishing Labor | Direct Manufacturing | Variable |
| LAB-QC | QC Labor | Direct Manufacturing | Fixed |
| OVH-MAT | Material Overhead | Indirect | Variable |
| OVH-MFG | Manufacturing Overhead | Indirect | Fixed |

### Cost Group Assignment Guide

| Cost Group | Assigned To |
|------------|-------------|
| MAT-FRM | Frame components (FRM-*) |
| MAT-CMP | All other components (FORK-*, WHL-*, TIRE-*, DRV-*, BRK-*, CKIT-*, SADL-*, PED-*) |
| MAT-MSC | Miscellaneous hardware (MISC-HW) |
| LAB-ASM | Assembly operations (FRAME, WHEEL, DRIVE, FINAL) |
| LAB-FIN | Finishing operations (PAINT — if applicable) |
| LAB-QC | Quality check and packaging operations (QC, PACK) |
| OVH-MAT | Material overhead surcharge (calculated as % of materials) |
| OVH-MFG | Manufacturing overhead surcharge (calculated as % of labor or per-hour rate) |

---

## 3. Costing Sheet Structure

The costing sheet defines the cost breakdown hierarchy and indirect cost calculations.

### Configured Nodes (via automation)

```
Root
└── Materials — Direct Materials [Price header, Type: Costs of purchase]
    ├── MAT-FRM — Frame Materials [Cost group → MAT-FRM]
    ├── MAT-CMP — Component Materials [Cost group → MAT-CMP]
    ├── MAT-MSC — Misc Materials [Cost group → MAT-MSC]
    └── MatTotal — Total Materials [Total/Subtotal]
```

### Remaining Nodes (manual setup required)

The following nodes must be added manually via **Cost management > Indirect cost accounting policies setup > Costing sheets**:

```
Root
├── Materials — Direct Materials [COMPLETED]
│   ├── MAT-FRM [COMPLETED]
│   ├── MAT-CMP [COMPLETED]
│   ├── MAT-MSC [COMPLETED]
│   └── MatTotal [COMPLETED]
├── MatOvh — Material Overhead [Surcharge node]
│   └── Calculation: 5% of MatTotal (surcharge basis = Materials subtotal)
│   └── Cost group: OVH-MAT
├── Labor — Direct Manufacturing [Price header, Type: Cost of goods manufactured]
│   ├── LAB-ASM — Assembly Labor [Cost group → LAB-ASM]
│   ├── LAB-FIN — Finishing Labor [Cost group → LAB-FIN]
│   ├── LAB-QC — QC Labor [Cost group → LAB-QC]
│   └── LabTotal — Total Labor [Total/Subtotal]
├── MfgOvh — Manufacturing Overhead [Surcharge node]
│   └── Calculation: 150% of LabTotal (surcharge basis = Labor subtotal)
│   └── Cost group: OVH-MFG
└── GrandTotal — Total Manufactured Cost [Total with Total checkbox checked]
```

### Manual Steps to Complete Costing Sheet

1. Navigate to: **Cost management > Indirect cost accounting policies setup > Costing sheets**
2. Select the CBKS costing sheet (Root node)
3. Click **New** and add:
   - **Labor** header node (Price type: Cost of goods manufactured, check Header)
   - Under Labor: add cost group nodes LAB-ASM, LAB-FIN, LAB-QC
   - Under Labor: add Total node "LabTotal"
4. Select Root again, click **New** and add:
   - **MatOvh** surcharge node (Indirect cost type: Surcharge, Basis: MatTotal, Rate: 5%)
   - **MfgOvh** surcharge node (Indirect cost type: Surcharge, Basis: LabTotal, Rate: 150%)
5. Select Root, add **GrandTotal** (Total node with Total checkbox checked)
6. Click **Validate** to verify the costing sheet

---

## 4. Costing Sheet Calculation Factors

Once surcharge nodes are created in the tree, configure the rates in **Costing sheet node calculation factors** (or via OData entity `CostSheetNodeCalculationFactors`):

| Node Name | Site | Costing Version | Surcharge % | Rate Amount | Unit Amount |
|-----------|------|-----------------|-------------|-------------|-------------|
| MatOvh | AMER | STD | 5% | 0 | 0 |
| MfgOvh | AMER | STD | 150% | 0 | 0 |

---

## 5. Remaining Prerequisites for BOM Cost Calculation

| Item | Status | Action Required |
|------|--------|-----------------|
| Calculation Group (STD) | ✅ Created & Assigned | All items assigned to STD group |
| Costing Version (STD) | ✅ Created | — |
| Cost Groups (8) | ✅ Created | Assign to items and cost categories |
| Costing Sheet - Materials | ✅ Configured | — |
| Costing Sheet - Labor & Overhead | ⚠️ Pending | Manual UI setup (see Section 3) |
| Cost Categories | ❌ Not created | Create for route operations (linked to cost groups) |
| Route Operation Times | ❌ Not set | Set run/setup times on RouteOperationsV2 |
| Pending Cost Records | ✅ Entered & Activated | All 41 purchased items at purchase price, site AMER |
| BOM Calculation | ⚠️ Ready to re-run | Material costs will calculate; labor costs require cost categories + routes |

### Cost Category Setup (Needed)

Cost categories link route operations to cost groups and hourly rates:

| Cost Category | Description | Cost Group | Hourly Rate (USD) |
|---------------|-------------|------------|-------------------|
| ASM-HR | Assembly per hour | LAB-ASM | $45.00 |
| FIN-HR | Finishing per hour | LAB-FIN | $50.00 |
| QC-HR | QC per hour | LAB-QC | $35.00 |
| PACK-HR | Packaging per hour | LAB-QC | $30.00 |

### Route Operation Time Estimates (Needed)

| Operation | Run Time (hrs/unit) | Setup Time (hrs) |
|-----------|--------------------:|------------------:|
| FRAME | 0.50 | 0.25 |
| WHEEL | 0.33 | 0.15 |
| DRIVE | 0.25 | 0.10 |
| FINAL | 0.75 | 0.20 |
| QC | 0.17 | 0.00 |
| PACK | 0.17 | 0.00 |
| PAINT | 0.33 | 0.50 |

---

## 6. Expected Cost Rollup Example (BX-1011)

Once fully configured, the BOM calculation for BX-1011 would yield:

| Cost Element | Calculation | Amount |
|---|---|---|
| Direct Materials | Sum of BOM component purchase prices | $259.00 |
| Material Overhead (5%) | 5% × $259.00 | $12.95 |
| Direct Labor | Sum of (operation hours × hourly rate) | ~$72.50* |
| Manufacturing Overhead (150%) | 150% × $72.50 | ~$108.75* |
| **Total Manufactured Cost** | | **~$453.20*** |

*Estimated based on proposed run times and rates above.

| Metric | Value |
|--------|-------|
| Sales Price | $249.00 |
| Manufactured Cost (est.) | $453.20 |
| Margin | -$204.20 (-82%) |

> **Note:** The negative margin indicates BX-1011 (BMX Vintage) may be a loss leader or the pricing needs revision. Consider adjusting sales prices or reviewing component sourcing for lower-cost alternatives.
