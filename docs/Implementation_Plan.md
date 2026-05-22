# Contoso Bikes — D365 F&O Implementation Plan

## Overview

| Item | Detail |
|------|--------|
| Project | Contoso Bikes D365 Finance & Supply Chain Management |
| Legal Entity | `CBKS` — Contoso Bikes Inc. |
| Go-Live Target | FY2026 |
| Approach | Phased configuration via OData/Data entities + manual UI steps |
| Source System | Legacy ERP / Analytics Platform |

---

## Phase 1 — Foundation Setup (Week 1–2)

Foundation configuration that all other modules depend on. Must be completed in order.

### Step 1.1 — Legal Entity

| # | Task | Method | Entity/Form | Dependency |
|---|------|--------|-------------|------------|
| 1.1.1 | Create legal entity CBKS | OData | `LegalEntities` | None |
| 1.1.2 | Set primary address (US) | OData | `LegalEntities` | 1.1.1 |
| 1.1.3 | Set accounting currency (USD) | Part of ledger setup | — | 1.1.1 |

### Step 1.2 — Currencies

| # | Task | Method | Entity/Form | Dependency |
|---|------|--------|-------------|------------|
| 1.2.1 | Create/verify USD | OData | `Currencies` | 1.1.1 |
| 1.2.2 | Create EUR (reporting) | OData | `Currencies` | 1.1.1 |
| 1.2.3 | Create GBP (reference) | OData | `Currencies` | 1.1.1 |
| 1.2.4 | Create AUD (reference) | OData | `Currencies` | 1.1.1 |
| 1.2.5 | Create INR (reference) | OData | `Currencies` | 1.1.1 |
| 1.2.6 | Create AED (reference) | OData | `Currencies` | 1.1.1 |
| 1.2.7 | Create CAD (reference) | OData | `Currencies` | 1.1.1 |
| 1.2.8 | Configure exchange rate types | OData | `ExchangeRateTypes` | 1.2.1 |

### Step 1.3 — Fiscal Calendar

| # | Task | Method | Entity/Form | Dependency |
|---|------|--------|-------------|------------|
| 1.3.1 | Create fiscal calendar CBKS-FY | OData | `FiscalCalendars` | 1.1.1 |
| 1.3.2 | Create FY2026 fiscal year | OData | `FiscalCalendarYears` | 1.3.1 |
| 1.3.3 | Create Opening period | OData | `FiscalCalendarPeriods` | 1.3.2 |
| 1.3.4 | Create 12 monthly periods (sequential) | OData | `FiscalCalendarPeriods` | 1.3.3 |
| 1.3.5 | Create Closing period | OData | `FiscalCalendarPeriods` | 1.3.4 |

### Step 1.4 — Chart of Accounts & Ledger

| # | Task | Method | Entity/Form | Dependency |
|---|------|--------|-------------|------------|
| 1.4.1 | Create Chart of Accounts (CBKS-COA) | OData | `ChartOfAccounts` | 1.1.1 |
| 1.4.2 | Create 22 Main Accounts | OData | `MainAccounts` | 1.4.1 |
| 1.4.3 | Create Account Structure (CBKS-MAIN) | Form | `DimensionConfigureAccountStructure` | 1.4.2 |
| 1.4.4 | Activate Account Structure | Form (batch) | `DimensionConfigureAccountStructure` | 1.4.3 |
| 1.4.5 | Create Ledger for CBKS | OData | `Ledgers` | 1.4.4, 1.3.1 |
| 1.4.6 | Assign Account Structure to Ledger | Form | Ledger form → Account structures | 1.4.5 |

### Step 1.5 — Financial Dimensions

| # | Task | Method | Entity/Form | Dependency |
|---|------|--------|-------------|------------|
| 1.5.1 | Create Region dimension | OData | `FinancialDimensions` | 1.4.5 |
| 1.5.2 | Create Region values (AMER, WEST, EAST, SOUTH) | OData | `FinancialDimensionValues` | 1.5.1 |
| 1.5.3 | Create ProductLine dimension | OData | `FinancialDimensions` | 1.4.5 |
| 1.5.4 | Create ProductLine values (9 values) | OData | `FinancialDimensionValues` | 1.5.3 |
| 1.5.5 | Create Department dimension | OData | `FinancialDimensions` | 1.4.5 |
| 1.5.6 | Create Department values (4 values) | OData | `FinancialDimensionValues` | 1.5.5 |

### Step 1.6 — Payment Terms

| # | Task | Method | Entity/Form | Dependency |
|---|------|--------|-------------|------------|
| 1.6.1 | Create NET30 | OData | `PaymentTerms` | 1.1.1 |
| 1.6.2 | Create NET45 | OData | `PaymentTerms` | 1.1.1 |
| 1.6.3 | Create NET60 | OData | `PaymentTerms` | 1.1.1 |
| 1.6.4 | Create 2-10-30 | OData | `PaymentTerms` | 1.1.1 |

### Step 1.7 — Sales Tax

| # | Task | Method | Entity/Form | Dependency |
|---|------|--------|-------------|------------|
| 1.7.1 | Create tax code ST-125 (12.5%) | OData | `TaxCodes` | 1.4.5 |
| 1.7.2 | Create tax group STANDARD | OData | `TaxGroups` | 1.7.1 |
| 1.7.3 | Create item tax group TAXABLE | OData | `ItemTaxGroups` | 1.7.1 |
| 1.7.4 | Set tax settlement account (2300) | OData | `TaxLedgerAccountGroups` | 1.7.1 |

### Step 1.8 — Number Sequences

| # | Task | Method | Entity/Form | Dependency |
|---|------|--------|-------------|------------|
| 1.8.1 | Configure SO number sequence (SO-#######) | OData | `NumberSequences` | 1.1.1 |
| 1.8.2 | Configure PO number sequence (PO-#######) | OData | `NumberSequences` | 1.1.1 |
| 1.8.3 | Configure Customer sequence (CUST-####) | OData | `NumberSequences` | 1.1.1 |
| 1.8.4 | Configure Vendor sequence (VEND-####) | OData | `NumberSequences` | 1.1.1 |
| 1.8.5 | Configure Invoice sequence (INV-#######) | OData | `NumberSequences` | 1.1.1 |
| 1.8.6 | Configure Voucher sequence (V-########) | OData | `NumberSequences` | 1.1.1 |

---

## Phase 2 — Master Data (Week 3–4)

Product, customer, and vendor master data. Requires Phase 1 complete.

### Step 2.1 — Inventory Infrastructure

| # | Task | Method | Entity/Form | Dependency |
|---|------|--------|-------------|------------|
| 2.1.1 | Create Unit of Measure (EA, KG) | OData | `Units` | 1.1.1 |
| 2.1.2 | Create Item Model Group (FIFO) | OData | `ItemModelGroups` | 1.1.1 |
| 2.1.3 | Create Storage Dimension Group | OData | `StorageDimensionGroups` | 1.1.1 |
| 2.1.4 | Create Tracking Dimension Group | OData | `TrackingDimensionGroups` | 1.1.1 |
| 2.1.5 | Create 9 Item Groups | OData | `ItemGroups` | 1.4.2 |

### Step 2.2 — Sites & Warehouses

| # | Task | Method | Entity/Form | Dependency |
|---|------|--------|-------------|------------|
| 2.2.1 | Create Site: AMER | OData | `Sites` | 1.1.1 |
| 2.2.2 | Create Site: WEST | OData | `Sites` | 1.1.1 |
| 2.2.3 | Create Site: EAST | OData | `Sites` | 1.1.1 |
| 2.2.4 | Create Warehouse: AMER-WH1 | OData | `Warehouses` | 2.2.1 |
| 2.2.5 | Create Warehouse: WEST-WH1 | OData | `Warehouses` | 2.2.2 |
| 2.2.6 | Create Warehouse: EAST-WH1 | OData | `Warehouses` | 2.2.3 |

### Step 2.3 — Released Products (42 items)

| # | Task | Method | Entity/Form | Dependency |
|---|------|--------|-------------|------------|
| 2.3.1 | Create all 42 released products | OData (batch) | `ReleasedProductCreationsV2` | 2.1.1–2.1.5, 2.2.4 |
| 2.3.2 | Set default order settings per product | OData | `ProductDefaultOrderSettings` | 2.3.1 |
| 2.3.3 | Set sales prices (trade agreements) | OData | `TradeAgreementJournals` | 2.3.1 |

### Step 2.4 — Customers

| # | Task | Method | Entity/Form | Dependency |
|---|------|--------|-------------|------------|
| 2.4.1 | Create Customer Group: WHOLESALE | OData | `CustomerGroups` | 1.6.1 |
| 2.4.2 | Create Customer Group: DISTRIBUTOR | OData | `CustomerGroups` | 1.6.2 |
| 2.4.3 | Create 20 Customer accounts | OData (batch) | `CustomersV3` | 2.4.1, 2.4.2 |

### Step 2.5 — Vendors

| # | Task | Method | Entity/Form | Dependency |
|---|------|--------|-------------|------------|
| 2.5.1 | Create Vendor Group: PARTS | OData | `VendorGroups` | 1.6.1 |
| 2.5.2 | Create Vendor Group: OEM | OData | `VendorGroups` | 1.6.2 |
| 2.5.3 | Create 20 Vendor accounts | OData (batch) | `VendorsV2` | 2.5.1, 2.5.2 |

---

## Phase 3 — Transactional Configuration (Week 5–6)

Posting profiles, GL integration, and process configuration.

### Step 3.1 — Posting Profiles

| # | Task | Method | Entity/Form | Dependency |
|---|------|--------|-------------|------------|
| 3.1.1 | Configure AR Posting Profile (DEFAULT) | OData | `CustPostingProfiles` | 2.4.3 |
| 3.1.2 | Configure AP Posting Profile (DEFAULT) | OData | `VendPostingProfiles` | 2.5.3 |
| 3.1.3 | Configure Inventory Posting — Sales tab | **Manual UI** | InventPosting form | 2.3.1 |
| 3.1.4 | Configure Inventory Posting — Inventory tab | **Manual UI** | InventPosting form | 2.3.1 |
| 3.1.5 | Configure Inventory Posting — Purchase tab | **Manual UI** | InventPosting form | 2.3.1 |
| 3.1.6 | Configure Error/Suspense account (9999) | OData | `LedgerAutomaticTransactionAccounts` | 1.4.2 |

### Step 3.2 — AR/AP Parameters

| # | Task | Method | Entity/Form | Dependency |
|---|------|--------|-------------|------------|
| 3.2.1 | Set AR parameters (posting profile, terms) | Form | AR Parameters | 3.1.1 |
| 3.2.2 | Set AP parameters (posting profile, terms) | Form | AP Parameters | 3.1.2 |
| 3.2.3 | Set Inventory parameters | Form | Inventory Parameters | 3.1.4 |

### Step 3.3 — Sales & Procurement Setup

| # | Task | Method | Entity/Form | Dependency |
|---|------|--------|-------------|------------|
| 3.3.1 | Set Sales order default parameters | Form | Sales Parameters | 3.2.1 |
| 3.3.2 | Set Procurement default parameters | Form | Procurement Parameters | 3.2.2 |

---

## Phase 3B — Manufacturing & Costing Configuration (Week 5–6)

Production costing setup including cost categories, route groups, costing version, and BOM calculations. Runs in parallel with Phase 3.

### Step 3B.1 — Cost Categories & Route Groups

| # | Task | Method | Entity/Form | Dependency |
|---|------|--------|-------------|------------|
| 3B.1.1 | Create cost category LABOR-STD ($40/hr) | OData | `CostCategories` | 1.1.1 |
| 3B.1.2 | Create cost category LABOR-SKILL ($55/hr) | OData | `CostCategories` | 1.1.1 |
| 3B.1.3 | Create cost category MACHINE ($20/hr) | OData | `CostCategories` | 1.1.1 |
| 3B.1.4 | Create route group DISC | OData/Form | `RouteGroup` form | 1.1.1 |
| 3B.1.5 | **Enable Setup time + Run time calc on DISC** | **Form** | `RouteGroup` form | 3B.1.4 |

> ⚠️ **Critical**: Step 3B.1.5 is essential. Without checking "Setup time" and "Run time" under the Calculation section, BOM calculation ignores all route costs entirely.

### Step 3B.2 — Work Centers (Operations Resources)

| # | Task | Method | Entity/Form | Dependency |
|---|------|--------|-------------|------------|
| 3B.2.1 | Create Resource Group per operation | OData | `ResourceGroups` | 2.2.1 |
| 3B.2.2 | Create 7 Operations Resources | OData | `OperationsResources` | 3B.2.1, 3B.1.1–3 |
| 3B.2.3 | Assign cost categories to resources | OData | `OperationsResources` | 3B.2.2 |

### Step 3B.3 — Routes & Operations

| # | Task | Method | Entity/Form | Dependency |
|---|------|--------|-------------|------------|
| 3B.3.1 | Create 42 Route Headers | OData | `RouteHeaders` | 1.1.1 |
| 3B.3.2 | Create Route Operations (6–7 per route) | OData | `RouteOperationsV2` | 3B.3.1 |
| 3B.3.3 | Create Route Versions (link to items) | OData | `RouteVersions` | 3B.3.2, 2.3.1 |
| 3B.3.4 | Create RouteOperationsProperties (times + resources) | OData | `RouteOperationsProperties` | 3B.3.2, 3B.2.2 |
| 3B.3.5 | Approve Route Versions | OData | `RouteVersions` | 3B.3.3 |

### Step 3B.4 — Costing Version & BOM Calculation

| # | Task | Method | Entity/Form | Dependency |
|---|------|--------|-------------|------------|
| 3B.4.1 | Create costing version STD (Standard cost) | OData | `CostingVersions` | 1.1.1 |
| 3B.4.2 | Create purchased item pending prices (41 items) | OData | `InventItemPendingPricesV2` | 2.3.1, 3B.4.1 |
| 3B.4.3 | Activate purchased item prices | Form | CostingVersion → Activate | 3B.4.2 |
| 3B.4.4 | Assign cost groups to purchased items | OData | `ReleasedProductsV2` | 3B.4.1, 2.3.1 |
| 3B.4.5 | Set DefaultOrderType=Production (42 mfg items) | OData | `ReleasedProductsV2` | 2.3.1 |
| 3B.4.6 | Create pending cost category prices in STD | OData | `RoutePendingRouteCostCategoryUnitCosts` | 3B.4.1, 3B.1.1–3 |
| 3B.4.7 | Run BOM Calculation (Production only) | Form | CostingVersion → Calculation | 3B.4.3–6, 3B.3.4 |
| 3B.4.8 | Activate all pending prices | Form | CostingVersion → Activate | 3B.4.7 |

### Step 3B.5 — Costing Sheet (Manual UI)

| # | Task | Method | Entity/Form | Dependency |
|---|------|--------|-------------|------------|
| 3B.5.1 | Configure costing sheet nodes | **Manual UI** | `CostSheetDesigner` | 3B.4.1 |
| 3B.5.2 | Set material surcharge (5%) | **Manual UI** | `CostSheetDesigner` | 3B.5.1 |
| 3B.5.3 | Set manufacturing surcharge (150%) | **Manual UI** | `CostSheetDesigner` | 3B.5.1 |
| 3B.5.4 | Assign absorption cost groups to surcharge nodes | **Manual UI** | `CostSheetDesigner` | 3B.5.1 |

---

## Phase 3C — Master Planning (Week 6)

Master planning configuration including coverage groups, working time calendars, resource scheduling requirements, and planning parameters. Runs after Phase 3B manufacturing setup is complete.

### Step 3C.1 — Working Time Calendars

| # | Task | Method | Entity/Form | Dependency |
|---|------|--------|-------------|------------|
| 3C.1.1 | Create working time template "8-5" (8AM–5PM) | Form | `WorkTimeTable` | 1.1.1 |
| 3C.1.2 | Create calendar "STD" (Standard 5-Day) | Form | `WorkCalendarTable` | 3C.1.1 |
| 3C.1.3 | Compose calendar (1/1/2025–5/21/2027) | Form | `WorkCalendarTable` → Compose | 3C.1.2 |
| 3C.1.4 | Assign STD calendar to all 7 resource groups | OData | `ResourceGroups` PATCH | 3C.1.3, 3B.2.1 |
| 3C.1.5 | Assign STD calendar to all 7 resources | OData | `OperationsResources` PATCH | 3C.1.3, 3B.2.2 |

### Step 3C.2 — Resource Group Membership

| # | Task | Method | Entity/Form | Dependency |
|---|------|--------|-------------|------------|
| 3C.2.1 | Add WC-FRAME-0 to WC-FRAME group | **Form** | `WrkCtrResourceGroup` | 3B.2.1, 3B.2.2 |
| 3C.2.2 | Add WC-WHEEL-0 to WC-WHEEL group | **Form** | `WrkCtrResourceGroup` | 3B.2.1, 3B.2.2 |
| 3C.2.3 | Add WC-DRIVE-0 to WC-DRIVE group | **Form** | `WrkCtrResourceGroup` | 3B.2.1, 3B.2.2 |
| 3C.2.4 | Add WC-EBIKE-0 to WC-EBIKE group | **Form** | `WrkCtrResourceGroup` | 3B.2.1, 3B.2.2 |
| 3C.2.5 | Add WC-FINAL-0 to WC-FINAL group | **Form** | `WrkCtrResourceGroup` | 3B.2.1, 3B.2.2 |
| 3C.2.6 | Add WC-QC-01 to WC-QC group | **Form** | `WrkCtrResourceGroup` | 3B.2.1, 3B.2.2 |
| 3C.2.7 | Add WC-PACK-01 to WC-PACK group | **Form** | `WrkCtrResourceGroup` | 3B.2.1, 3B.2.2 |

> ⚠️ **Critical**: No OData entity exists for resource group membership (WrkCtrResourceGroupResource table). Must use the `WrkCtrResourceGroup` form: filter → click NewResource → set WrkCtrResourceGroupResource_WrkCtrId → save.

### Step 3C.3 — Resource Requirements on Routes

| # | Task | Method | Entity/Form | Dependency |
|---|------|--------|-------------|------------|
| 3C.3.1 | Create resource requirements for all 259 route operations | OData | `RouteOperationPropertiesResourceRequirements` | 3B.3.2, 3B.2.1 |

> Each route operation must have a resource requirement linking it to its resource group with both `WillOperationSchedulingUseRequirement` and `WillJobSchedulingUseRequirement` set to `Yes`. Without these, the scheduler cannot find applicable resources.

**Resource requirement mapping (per route operation number):**

| Op # | Operation | Resource Group |
|------|-----------|---------------|
| 10 | FRAME | WC-FRAME |
| 20 | WHEEL | WC-WHEEL |
| 30 | DRIVE | WC-DRIVE |
| 35 | EBIKE (e-bike routes only) | WC-EBIKE |
| 40 | FINAL | WC-FINAL |
| 50 | QC | WC-QC |
| 60 | PACK | WC-PACK |

### Step 3C.4 — Coverage Groups

| # | Task | Method | Entity/Form | Dependency |
|---|------|--------|-------------|------------|
| 3C.4.1 | Create CRITICAL coverage group (MinMax, 1-day period) | OData | `MasterPlanningProductCoverageGroups` | 1.1.1 |
| 3C.4.2 | Create FINISH coverage group (MinMax, 30-day period) | OData | `MasterPlanningProductCoverageGroups` | 1.1.1 |
| 3C.4.3 | Create PURCH coverage group (Period, 14-day period) | OData | `MasterPlanningProductCoverageGroups` | 1.1.1 |

### Step 3C.5 — Item Coverage

| # | Task | Method | Entity/Form | Dependency |
|---|------|--------|-------------|------------|
| 3C.5.1 | Set item coverage for 8 critical items (MinMax with min/max qty) | OData | `ItemCoverageSettingsV2` | 3C.4.1, 2.3.1 |
| 3C.5.2 | Set item coverage for 33 purchased items (PURCH group) | OData | `ItemCoverageSettingsV2` | 3C.4.3, 2.3.1 |
| 3C.5.3 | Set item coverage for 42 manufactured items (FINISH group) | OData | `ItemCoverageSettingsV2` | 3C.4.2, 2.3.1 |

### Step 3C.6 — Master Plans & Parameters

| # | Task | Method | Entity/Form | Dependency |
|---|------|--------|-------------|------------|
| 3C.6.1 | Create plan CBKS-STATI (Static Plan) | OData | `MasterPlans` | 1.1.1 |
| 3C.6.2 | Create plan CBKS-DYN (Dynamic Plan) | OData | `MasterPlans` | 1.1.1 |
| 3C.6.3 | Set master planning parameters (current static/dynamic plans) | Form | `ReqParameters` | 3C.6.1, 3C.6.2 |
| 3C.6.4 | Uncheck "Disable all planning processes" | Form | `ReqParameters` | 3C.6.3 |

### Step 3C.7 — Validation

| # | Task | Method | Expected Result |
|---|------|--------|-----------------|
| 3C.7.1 | Run master planning (CBKS-STATI, all items) | Form | `ReqCalcScheduleItemTable` action | Planned production + purchase orders generated |
| 3C.7.2 | Verify planned production orders exist | Form | `ReqPOGridViewProduction` | Multiple orders for manufactured items |
| 3C.7.3 | Verify planned purchase orders exist | Form | `ReqPOGridViewPurchase` | Orders for purchased components |
| 3C.7.4 | Verify no scheduling errors in log | Form | Planning history | No "no applicable resources" errors |

---

## Phase 4 — Validation & Cutover (Week 7–8)

### Step 4.1 — End-to-End Testing

| # | Task | Method | Expected Result |
|---|------|--------|-----------------|
| 4.1.1 | Create test Sales Order | OData | SO created, lines added |
| 4.1.2 | Confirm & Invoice SO | Form/OData | Revenue posted to 4100/4200 |
| 4.1.3 | Create test Purchase Order | OData | PO created with vendor |
| 4.1.4 | Receive & Invoice PO | Form/OData | Inventory & AP posted |
| 4.1.5 | Run inventory movement journal | OData | Stock adjusted |
| 4.1.6 | Verify GL trial balance | Report | All accounts balance |

### Step 4.2 — Data Cutover

| # | Task | Method | Detail |
|---|------|--------|--------|
| 4.2.1 | Load opening inventory balances | OData | Movement journal per site/warehouse |
| 4.2.2 | Load AR opening balances | OData | General journal with customer accounts |
| 4.2.3 | Load AP opening balances | OData | General journal with vendor accounts |
| 4.2.4 | Post beginning GL balances | OData | General journal entry |
| 4.2.5 | Reconcile trial balance to legacy system | Manual | Sign-off |

### Step 4.3 — Go-Live Checklist

| # | Task | Owner | Status |
|---|------|-------|--------|
| 4.3.1 | All posting profiles validated | Finance | ☐ |
| 4.3.2 | All customers can place orders | Sales | ☐ |
| 4.3.3 | All vendors can receive POs | Procurement | ☐ |
| 4.3.4 | Inventory quantities reconciled | Warehouse | ☐ |
| 4.3.5 | Trial balance matches legacy system extract | Finance | ☐ |
| 4.3.6 | Security roles assigned to users | IT | ☐ |
| 4.3.7 | Number sequences verified | IT | ☐ |
| 4.3.8 | Exchange rates loaded | Finance | ☐ |
| 4.3.9 | UAT sign-off received | Business | ☐ |
| 4.3.10 | Production cutover executed | IT | ☐ |

---

## Risks & Manual Steps

| Risk | Mitigation |
|------|-----------|
| InventPosting ListBox controls non-interactive via automation | Steps 3.1.3–3.1.5 must be done in D365 UI manually |
| Account structure activation is async | Use batch job via form; verify before proceeding |
| Ledger account structure assignment | Must use Ledger form UI (OData PATCH fails) |
| Fiscal calendar periods must be sequential | Create one-at-a-time in correct order |
| PO confirmation form-only in non-default company | Test PO flows in CBKS directly |
| Route group calc flags unchecked → zero route costs | Verify DISC route group has Setup/Run time calc = Yes before BOM calc |
| BOM Calc "Purchase order" checkbox cannot be unchecked via MCP | Use "Records to include" filter with item number wildcard pattern |
| DefaultOrderType must be Production for mfg items | If set to "Purch", BOM calc returns $0 for manufactured items |
| CostSheetDesigner tree control is not automatable | All costing sheet surcharge node config must be done manually in D365 UI |
| Resource group membership has no OData entity | Must use WrkCtrResourceGroup form — cannot automate member assignment |
| Working time calendar must be composed after creation | Without composing, resources have zero capacity and scheduling fails |
| Resource requirements mandatory for scheduling | Every route operation must have a resource requirement with scheduling flags = Yes |
| "Disable all planning processes" checked by default | Must uncheck in ReqParameters before master planning can run |
| Cost category prices must exist before BOM calc | Create via `RoutePendingRouteCostCategoryUnitCosts` entity then activate |

---

## Lessons Learned (May 21, 2026 Costing Diagnostic)

### Problem Statement
Costing sheet showed no costs for manufactured item BX-1011 despite BOMs, routes, and costing sheet being configured.

### Root Causes Identified (in discovery order)

| # | Issue | Impact | Resolution |
|---|-------|--------|-----------|
| 1 | CostGroupId blank on all 41 purchased items | Costing sheet cannot group/display material costs | Assigned MAT-FRM/MAT-CMP/MAT-MSC via OData |
| 2 | CostSheetNodeCalculationFactors surcharge = 0% | Overhead surcharges compute to zero | Set to 5% material / 150% manufacturing via OData |
| 3 | DefaultOrderType = "Purch" on all 42 mfg items | BOM calculation does not run for purchase-type items | Changed to "Production" via OData batch |
| 4 | Route operations had NO resource requirements | No link between operations and work centers/cost categories | Created 259 RouteOperationsProperties records via OData |
| 5 | Cost category prices missing from STD version | Even with resources linked, no hourly rate to multiply by | Created LABOR-STD=$40, LABOR-SKILL=$55, MACHINE=$20 |
| 6 | **Route group DISC "Calculation" flags unchecked** | BOM calc **completely ignores** all route costs | Checked "Setup time" and "Run time" calc flags via form |

---

## Lessons Learned (May 21, 2026 Master Planning Scheduling Fix)

### Problem Statement
Master planning run failed with: "Planned production order could not be scheduled using route since no applicable resources were found for operation 60"

### Root Causes Identified (in discovery order)

| # | Issue | Impact | Resolution |
|---|-------|--------|-----------|
| 1 | No working time calendar in CBKS | Scheduler has no capacity data for resources — cannot schedule any operation | Created STD calendar (Mon-Fri, 8AM-5PM), composed through 5/21/2027, assigned to all 7 resource groups and 7 resources |
| 2 | No resource requirements on ANY route operations | Scheduler doesn't know which resource group to use for each operation | Created all 259 resource requirements via OData (`RouteOperationPropertiesResourceRequirements`) linking each operation to its resource group |
| 3 | Resources not assigned as members of resource groups | Even with requirements pointing to groups, the groups had zero members so "applicable resources" = 0 | Added all 7 resources to their groups via `WrkCtrResourceGroup` form (no OData entity exists) |

### Key Diagnostic Approach
- Used "Applicable resources" lookup on route operations to verify 0 resources returned
- Confirmed resources existed but were not group members
- All three root causes had to be fixed for scheduling to succeed

### Critical Configuration Notes
- **Resource group membership has NO OData entity** — must use form: filter to group → NewResource → set WrkCtrResourceGroupResource_WrkCtrId → save
- **Working time calendars must be composed** — creating the calendar alone is insufficient; the "Compose working times" step generates the actual day-by-day capacity records
- **Resource requirements need both scheduling flags** — both `WillOperationSchedulingUseRequirement` and `WillJobSchedulingUseRequirement` must be `Yes`

---

### Key Entity Reference for Manufacturing Costing

| Entity | Purpose | Key Fields |
|--------|---------|-----------|
| `RouteOperationsProperties` | Links resources, times, and cost categories to route operations | RouteId, OperationId, ProcessTime, SetupTime, ProcessCostCategoryId, CostingOperationResourceId, RouteGroupId |
| `RoutePendingRouteCostCategoryUnitCosts` | Hourly rates for cost categories in a costing version | RouteCostCategoryId, CostingVersionId, ProductionSiteId, EffectiveDate, UnitCost |
| `InventItemPendingPricesV2` | Pending item cost/sales prices in costing version | ItemNumber, CostingVersionId, PriceType, Price, PriceSiteId |
| `RouteVersions` | Links route to released product | RouteId, ItemNumber, IsActive, ProductionSiteId |
| `RouteOperationsV2` | Basic route operation structure (no times/costs) | RouteId, OperationNumber, OperationId |

### BOM Calculation Procedure (Validated)

1. Open **Costing version setup** → select STD → click **Calculation**
2. Set Site = AMER, Calculation date = current
3. **Uncheck "Purchase order"** (or filter to manufactured items only)
4. Records to include → Filter → Item number = `BX-*,CB-*,CC-*,DB-*,EB-*,HB-*,MB-*,RC-*,RO-*`
5. Click OK → wait for "Operation completed"
6. Verify pending prices via `InventItemPendingPricesV2` query
7. Activate via **Activate** button → check Cost price + Sales price + Rate and ratio

---

## Data Entity Reference Files

All entity payloads are stored in the `/data/` folder as individual markdown files with field mappings and sample records ready for OData creation.

| File | Entity | Records |
|------|--------|---------|
| `01_legal_entity.md` | LegalEntities | 1 |
| `02_currencies.md` | Currencies | 7 |
| `03_fiscal_calendar.md` | FiscalCalendars + Periods | 1 + 14 |
| `04_chart_of_accounts.md` | ChartOfAccounts + MainAccounts | 1 + 22 |
| `05_financial_dimensions.md` | FinancialDimensions + Values | 3 + 16 |
| `06_payment_terms.md` | PaymentTerms | 4 |
| `07_sales_tax.md` | TaxCodes + TaxGroups | 3 |
| `08_number_sequences.md` | NumberSequences | 6 |
| `09_units_of_measure.md` | Units | 2 |
| `10_item_model_groups.md` | ItemModelGroups | 1 |
| `11_item_groups.md` | ItemGroups | 9 |
| `12_dimension_groups.md` | Storage + Tracking Dimension Groups | 2 |
| `13_sites.md` | Sites | 3 |
| `14_warehouses.md` | Warehouses | 3 |
| `15_released_products.md` | ReleasedProductCreationsV2 | 42 |
| `16_customer_groups.md` | CustomerGroups | 2 |
| `17_customers.md` | CustomersV3 | 20 |
| `18_vendor_groups.md` | VendorGroups | 2 |
| `19_vendors.md` | VendorsV2 | 20 |
| `20_posting_profiles.md` | CustPostingProfiles + VendPostingProfiles | 2 |
| `21_inventory_posting.md` | Manual UI configuration | 8 rows |

---

*Document Version: 1.2 — Updated May 21, 2026*
*Updates: Added Phase 3C (Master Planning), scheduling fix lessons learned, expanded Risks table*
