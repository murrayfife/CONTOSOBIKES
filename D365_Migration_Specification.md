# Contoso Bikes — Dynamics 365 Finance & Operations Migration Specification

## 1. Executive Summary

This document defines the configuration and data migration specification for moving Contoso Bikes from its current SAP Datasphere/HANA platform to Microsoft Dynamics 365 Finance & Supply Chain Management. The company is a B2B bicycle wholesaler operating across three global regions with 42 products, 40 business partners, and ~$20M annual revenue.

---

## 2. Legal Entity Structure

### Primary Legal Entity

| Field | Value |
|-------|-------|
| Legal Entity ID | `CBKS` |
| Company Name | Contoso Bikes Inc. |
| Country/Region | US |
| Primary Address | United States |
| Primary Currency | USD |
| Fiscal Calendar | Standard Calendar Year (Jan–Dec) |
| Chart of Accounts | Shared — `CBKS-COA` |
| Language | en-us |

### Consideration: Multi-Company

All operations are US-based. Future expansion may evaluate:
- `CBKS-WEST` — Contoso Bikes West Coast
- `CBKS-EAST` — Contoso Bikes East Coast

For initial migration, a single legal entity with USD is recommended.

---

## 3. Fiscal Calendar

| Attribute | Value |
|-----------|-------|
| Calendar Name | `CBKS-FY` |
| Fiscal Year Convention | Calendar Year |
| Period Structure | 12 monthly periods + Opening + Closing |
| Start Date | January 1 |
| Opening Balance Period | Period 0 (January 1) |
| Go-Live Fiscal Year | FY2026 |
| Historical Data Import | FY2018–FY2019 (for reference/analytics) |

---

## 4. Chart of Accounts

### Account Structure: `CBKS-MAIN`

| Main Account | Description | Account Type | Category |
|--------------|-------------|--------------|----------|
| 1100 | Cash and Bank | Asset | Cash |
| 1200 | Accounts Receivable | Asset | AR |
| 1300 | Inventory | Asset | Inventory |
| 1310 | Inventory - eBikes | Asset | Inventory |
| 1320 | Inventory - Racing | Asset | Inventory |
| 1400 | Prepaid Expenses | Asset | Prepaid |
| 1500 | Fixed Assets | Asset | Fixed Asset |
| 2100 | Accounts Payable | Liability | AP |
| 2200 | Accrued Liabilities | Liability | Accrual |
| 2300 | Sales Tax Payable | Liability | Tax |
| 3100 | Retained Earnings | Equity | Equity |
| 3200 | Common Stock | Equity | Equity |
| 4100 | Product Revenue - Bikes | Revenue | Revenue |
| 4200 | Product Revenue - eBikes | Revenue | Revenue |
| 4300 | Product Revenue - Accessories | Revenue | Revenue |
| 5100 | Cost of Goods Sold | Expense | COGS |
| 5200 | COGS - eBikes | Expense | COGS |
| 6100 | Salaries & Wages | Expense | Operating |
| 6200 | Rent & Facilities | Expense | Operating |
| 6300 | Marketing & Advertising | Expense | Operating |
| 6400 | Shipping & Freight | Expense | Operating |
| 6500 | Depreciation | Expense | Operating |
| 9999 | Error/Suspense Account | Expense | System |

### Financial Dimensions

| Dimension | Purpose | Values |
|-----------|---------|--------|
| Region | US sales region | AMER, WEST, EAST, SOUTH |
| ProductLine | Category-level P&L | ROAD, BMX, CYCLO, MTB, RACE, DOWN, EBIKE, CRUISE, HYBRID |
| Department | Cost center | SALES, OPS, ADMIN, WAREHOUSE |

---

## 5. Sales Tax Configuration

| Field | Value |
|-------|-------|
| Tax Group | `STANDARD` |
| Item Tax Group | `TAXABLE` |
| Tax Rate | 12.5% (based on source data uniform rate) |
| Tax Code | `ST-125` |
| Tax Direction | Sales tax payable |
| Tax Calculation | Line-level |

---

## 6. Product Configuration

### Item Model Groups

| Group ID | Name | Inventory Model | Stocked |
|----------|------|-----------------|---------|
| FIFO | First In First Out | FIFO | Yes |

### Item Groups

| Group ID | Description | Revenue Account | COGS Account |
|----------|-------------|-----------------|--------------|
| ROAD | Road Bikes | 4100 | 5100 |
| BMX | BMX Bikes | 4100 | 5100 |
| CYCLO | Cyclo-cross Bikes | 4100 | 5100 |
| MTB | Mountain Bikes | 4100 | 5100 |
| RACE | Racing Bikes | 4100 | 5100 |
| DOWN | Downhill Bikes | 4100 | 5100 |
| EBIKE | Electric Bikes | 4200 | 5200 |
| CRUISE | Cruiser Bikes | 4100 | 5100 |
| HYBRID | Hybrid Bikes | 4100 | 5100 |

### Storage Dimension Group

| Dimension | Active | Primary Stocking |
|-----------|--------|-----------------|
| Site | Yes | Yes |
| Warehouse | Yes | Yes |
| Location | No | — |
| Pallet | No | — |

### Tracking Dimension Group

| Dimension | Active |
|-----------|--------|
| Batch Number | No |
| Serial Number | No |

### Released Products (42 SKUs)

| Item Number | Name | Category | Unit | Weight (kg) | Price (USD) |
|-------------|------|----------|------|-------------|-------------|
| RO-1001 | Roady 1001 | ROAD | EA | 7.7 | 525.00 |
| RO-1002 | Roady 1002 | ROAD | EA | 8.0 | 689.00 |
| RO-1003 | Roady 1003 | ROAD | EA | 9.1 | 721.00 |
| BX-1011 | BMX Vintage 1011 | BMX | EA | 11.1 | 249.00 |
| BX-1012 | BMX Jump 1012 | BMX | EA | 12.0 | 399.00 |
| BX-1013 | BMX Jump Lux I | BMX | EA | 13.1 | 449.00 |
| BX-1014 | BMX Jump Lux II | BMX | EA | 11.8 | 799.00 |
| BX-1015 | BMX Optima | BMX | EA | 12.5 | 299.00 |
| BX-1016 | BMX Optima II | BMX | EA | 12.8 | 319.00 |
| CC-1021 | Cyclone Basic | CYCLO | EA | 8.1 | 1,144.00 |
| CC-1022 | Cyclone Speed | CYCLO | EA | 8.0 | 1,200.00 |
| CC-1023 | Cyclone III | CYCLO | EA | 8.6 | 1,361.00 |
| MB-1031 | Mt Discovery Basic | MTB | EA | 12.7 | 649.00 |
| MB-1032 | Mt Discovery Drive | MTB | EA | 12.0 | 1,299.00 |
| MB-1033 | Mt Discovery Rush | MTB | EA | 13.1 | 3,999.00 |
| MB-1034 | Mt Discovery Ultimate | MTB | EA | 12.5 | 2,499.00 |
| RC-1051 | Tornado I | RACE | EA | 7.1 | 2,499.00 |
| RC-1052 | Tornado II | RACE | EA | 7.5 | 3,999.00 |
| RC-1053 | Stream I | RACE | EA | 6.9 | 4,599.00 |
| RC-1054 | Stream II | RACE | EA | 7.0 | 5,499.00 |
| RC-1055 | Veloflash | RACE | EA | 7.2 | 1,999.00 |
| RC-1056 | Veloflash SE | RACE | EA | 7.8 | 2,499.00 |
| RC-1057 | Veloflash Ultimate | RACE | EA | 7.3 | 4,999.00 |
| DB-1081 | Rooty Basic | DOWN | EA | 13.6 | 1,499.00 |
| DB-1082 | Capricorn | DOWN | EA | 14.3 | 1,250.00 |
| DB-1083 | Capricorn II | DOWN | EA | 15.4 | 1,199.00 |
| EB-1131 | Flash Drive | EBIKE | EA | 18.1 | 1,500.00 |
| EB-1132 | Flash Drive II | EBIKE | EA | 18.8 | 1,900.00 |
| EB-1133 | Lazy Cat | EBIKE | EA | 21.0 | 2,250.00 |
| EB-1134 | Lazy Cat II | EBIKE | EA | 20.1 | 4,800.00 |
| EB-1135 | Speedeon | EBIKE | EA | 19.3 | 3,000.00 |
| EB-1136 | Speedeon Light | EBIKE | EA | 20.5 | 5,000.00 |
| EB-1137 | Speedeon Cross | EBIKE | EA | 22.0 | 7,900.00 |
| CB-1161 | La Plage | CRUISE | EA | 15.0 | 399.00 |
| CB-1162 | La Plage Limited | CRUISE | EA | 18.0 | 400.00 |
| CB-1163 | La Plage Gold | CRUISE | EA | 16.0 | 288.00 |
| HB-1171 | Star Cruise | HYBRID | EA | 11.0 | 699.00 |
| HB-1172 | Star Cruise II | HYBRID | EA | 12.1 | 799.00 |
| HB-1173 | Universal One | HYBRID | EA | 13.5 | 649.00 |
| HB-1174 | Universal Two | HYBRID | EA | 11.8 | 379.00 |
| HB-1175 | Specifica | HYBRID | EA | 12.5 | 899.00 |
| HB-1176 | Specifica Gold | HYBRID | EA | 12.9 | 1,199.00 |

---

## 7. Inventory & Warehouse Configuration

### Sites

| Site ID | Name | Region | Address |
|---------|------|--------|---------|
| AMER | Americas HQ and Manufacturing | AMER | Bethesda, MD |
| WEST | West Coast Distribution | WEST | Irvine, CA |
| EAST | East Coast Distribution | EAST | Charlotte, NC |

### Warehouses

| Warehouse ID | Name | Site | Type |
|--------------|------|------|------|
| AMER-WH1 | HQ Manufacturing Warehouse | AMER | Storage |
| WEST-WH1 | West Coast Warehouse | WEST | Storage |
| EAST-WH1 | East Coast Warehouse | EAST | Storage |

### Default Order Settings (All Products)

| Setting | Value |
|---------|-------|
| Default Sales Site | AMER |
| Default Sales Warehouse | AMER-WH1 |
| Default Purchase Site | AMER |
| Default Purchase Warehouse | AMER-WH1 |
| Default Inventory Site | AMER |
| Default Inventory Warehouse | AMER-WH1 |

---

## 8. Customer Configuration

### Customer Groups

| Group ID | Description | Payment Terms |
|----------|-------------|---------------|
| WHOLESALE | Wholesale Customers | Net 30 |
| DISTRIBUTOR | Authorized Distributors | Net 45 |

### Customers (20)

| Customer Account | Name | Group | Currency | Country | Region |
|-----------------|------|-------|----------|---------|--------|
| CUST-0001 | Pacific Coast Cycling | WHOLESALE | USD | US | WEST |
| CUST-0002 | Summit Trail Bikes | WHOLESALE | USD | US | WEST |
| CUST-0003 | Lakeshore Sports Co | WHOLESALE | USD | US | EAST |
| CUST-0004 | Peachtree Bicycle Works | WHOLESALE | USD | US | EAST |
| CUST-0005 | Liberty Cycle Hub | WHOLESALE | USD | US | EAST |
| CUST-0006 | Lone Star Bikes | WHOLESALE | USD | US | SOUTH |
| CUST-0007 | Redwood Cycling Co | WHOLESALE | USD | US | WEST |
| CUST-0008 | Cascade Bike Supply | WHOLESALE | USD | US | WEST |
| CUST-0009 | Desert Spoke Cycles | WHOLESALE | USD | US | WEST |
| CUST-0010 | Bay State Bicycles | RETAIL | USD | US | EAST |
| CUST-0011 | Palmetto Pedal Sports | RETAIL | USD | US | EAST |
| CUST-0012 | Great Plains Cycling | RETAIL | USD | US | AMER |
| CUST-0013 | Blue Ridge Bike Co | RETAIL | USD | US | EAST |
| CUST-0014 | Motor City Cycles | RETAIL | USD | US | EAST |
| CUST-0015 | Wichita Wheel Works | RETAIL | USD | US | AMER |
| CUST-0016 | Emerald City Bikes | RETAIL | USD | US | WEST |
| CUST-0017 | Gateway Bike Shop | RETAIL | USD | US | AMER |
| CUST-0018 | Coastal Pedal Sports | RETAIL | USD | US | SOUTH |
| CUST-0019 | Silver State Cycling | RETAIL | USD | US | WEST |
| CUST-0020 | Harbor Cycle Company | RETAIL | USD | US | EAST |

### Customer Posting Profile

| Profile | AR Account | Revenue Account |
|---------|-----------|-----------------|
| DEFAULT | 1200 | 4100 |

---

## 9. Vendor Configuration

### Vendor Groups

| Group ID | Description | Payment Terms |
|----------|-------------|---------------|
| PARTS | Parts Suppliers | Net 30 |
| OEM | OEM Frame/Component Suppliers | Net 45 |

### Vendors (20)

| Vendor Account | Name | Group | Currency | Country | Region |
|---------------|------|-------|----------|---------|--------|
| VEND-0001 | American Frame Works | OEM | USD | US | EAST |
| VEND-0002 | Appalachian Alloy Fabrication | OEM | USD | US | EAST |
| VEND-0003 | Heartland Metals Inc | OEM | USD | US | AMER |
| VEND-0004 | Pacific Tube & Steel | OEM | USD | US | WEST |
| VEND-0005 | Freedom Fork Manufacturing | OEM | USD | US | EAST |
| VEND-0006 | Great Lakes Wheel Co | OEM | USD | US | EAST |
| VEND-0007 | Pioneer Rim & Spoke | OEM | USD | US | WEST |
| VEND-0008 | Continental Rubber Products | RAW | USD | US | EAST |
| VEND-0009 | Precision Gear Systems | OEM | USD | US | EAST |
| VEND-0010 | Cascade Drivetrain Corp | OEM | USD | US | WEST |
| VEND-0011 | Iron Horse Brake Systems | OEM | USD | US | EAST |
| VEND-0012 | Summit Components LLC | OEM | USD | US | WEST |
| VEND-0013 | Liberty Electric Motors | OEM | USD | US | EAST |
| VEND-0014 | Patriot Power Systems | OEM | USD | US | EAST |
| VEND-0015 | Carolina Saddle & Seat Co | OEM | USD | US | EAST |
| VEND-0016 | Keystone Hardware Supply | RAW | USD | US | EAST |
| VEND-0017 | Columbia Packaging Solutions | SERVICE | USD | US | WEST |
| VEND-0018 | Buckeye Industrial Coatings | RAW | USD | US | EAST |
| VEND-0019 | Magnolia Chain & Cable | OEM | USD | US | SOUTH |
| VEND-0020 | Granite State Machining | OEM | USD | US | EAST |

### Vendor Posting Profile

| Profile | AP Account | Purchase Expenditure |
|---------|-----------|---------------------|
| DEFAULT | 2100 | 5100 |

---

## 10. Sales Order Configuration

### Order Types

| Type | Description | Usage |
|------|-------------|-------|
| SO | Standard Sales Order | Default for all wholesale orders |

### Sales Order Number Sequence

| Attribute | Value |
|-----------|-------|
| Prefix | `SO-` |
| Format | `SO-#######` |
| Starting Number | SO-0500000 |
| Scope | Company |

### Sales Pricing

| Approach | Detail |
|----------|--------|
| Base Price | Per-product fixed price (see product table) |
| Price List | Single USD base price list |
| Currency Conversion | Exchange rate at order date |
| Discounts | None defined (future: volume/trade agreements) |

---

## 11. Purchase Order Configuration

### PO Number Sequence

| Attribute | Value |
|-----------|-------|
| Prefix | `PO-` |
| Format | `PO-#######` |
| Starting Number | PO-0000001 |

---

## 12. Currency & Exchange Rates

### Currencies Required

| Currency | ISO Code | Description | Rounding |
|----------|----------|-------------|----------|
| US Dollar | USD | Primary company currency | 0.01 |
| Euro | EUR | Reporting currency | 0.01 |
| British Pound | GBP | Reference rate | 0.01 |
| Australian Dollar | AUD | Reference rate | 0.01 |
| Indian Rupee | INR | Reference rate | 0.01 |
| UAE Dirham | AED | Reference rate | 0.01 |
| Canadian Dollar | CAD | Reference rate | 0.01 |

### Exchange Rate Type

| Type | Description |
|------|-------------|
| DEFAULT | Daily spot rate for transactions |
| BUDGET | Monthly average for budgeting |

---

## 13. Number Sequences

| Reference | Format | Scope |
|-----------|--------|-------|
| Sales Order | SO-####### | Company |
| Purchase Order | PO-####### | Company |
| Customer Account | CUST-#### | Company |
| Vendor Account | VEND-#### | Company |
| Invoice | INV-####### | Company |
| Product Receipt | PR-####### | Company |
| Journal Batch | JRN-###### | Company |
| Voucher | V-######## | Fiscal Year |

---

## 14. Employees / Workers

| Worker ID | Name | Department | Region |
|-----------|------|------------|--------|
| EMP-001 | Derrick L. Magill | Sales | AMER |
| EMP-002 | Brandon T. Foster | Sales | EAST |
| EMP-003 | Ellis K. Robertson | Sales | EAST |
| EMP-004 | William M. Mussen | Sales | EAST |
| EMP-005 | Jason R. Patel | Sales | SOUTH |
| EMP-006 | Heather A. Yates | Sales | WEST |
| EMP-007 | Roberta M. Holloway | Sales | AMER |
| EMP-008 | Patricia G. Duval | Sales | SOUTH |
| EMP-009 | Kirk J. Lee | Sales | AMER |
| EMP-010 | Janet R. Gray | Sales | AMER |
| EMP-011 | Nelson J. Wilkens | Sales | WEST |
| EMP-012 | Willard R. Chatman | Sales | WEST |
| EMP-013 | Carroll S. Pewitt | Sales | AMER |
| EMP-014 | Kenneth H. Weiss | Sales | EAST |

---

## 15. Payment Terms

| Terms ID | Description | Days | Discount |
|----------|-------------|------|----------|
| NET30 | Net 30 Days | 30 | 0% |
| NET45 | Net 45 Days | 45 | 0% |
| NET60 | Net 60 Days | 60 | 0% |
| 2-10-30 | 2% 10 Net 30 | 30 | 2% / 10 days |

---

## 16. Posting Profiles

### Inventory Posting

| Tab | Posting Type | Item Group | Main Account |
|-----|-------------|------------|--------------|
| Sales order | Revenue | ALL | 4100 |
| Sales order | Revenue | EBIKE | 4200 |
| Sales order | COGS - Invoiced | ALL | 5100 |
| Sales order | COGS - Invoiced | EBIKE | 5200 |
| Inventory | Physical Issue | ALL | 1300 |
| Inventory | Physical Receipt | ALL | 1300 |
| Purchase order | Purchase Expenditure | ALL | 5100 |
| Purchase order | Purchase Expenditure | EBIKE | 5200 |

### Accounts Receivable Posting

| Profile | Debit (AR) | Credit (Revenue) |
|---------|-----------|-----------------|
| DEFAULT | 1200 | Per item group |

### Accounts Payable Posting

| Profile | Debit (Expense) | Credit (AP) |
|---------|----------------|-------------|
| DEFAULT | Per item group | 2100 |

---

## 17. Data Migration Plan

### Phase 1 — Foundation (Week 1–2)

| Task | Entity | Records |
|------|--------|---------|
| Legal Entity setup | LegalEntities | 1 |
| Fiscal Calendar | FiscalCalendars | 1 (12 periods) |
| Chart of Accounts | MainAccounts | ~22 |
| Account Structure | DimensionHierarchies | 1 |
| Financial Dimensions | FinancialDimensionValues | ~16 |
| Currencies | Currencies | 7 |
| Number Sequences | NumberSequenceReferences | ~8 |
| Payment Terms | PaymentTerms | 4 |
| Tax Configuration | TaxCodes | 1 |

### Phase 2 — Master Data (Week 3–4)

| Task | Entity | Records |
|------|--------|---------|
| Item Model Groups | InventModelGroups | 1 |
| Item Groups | InventItemGroups | 9 |
| Storage Dimension Groups | StorageDimensionGroups | 1 |
| Tracking Dimension Groups | TrackingDimensionGroups | 1 |
| Sites | InventSites | 3 |
| Warehouses | InventWarehouses | 3 |
| Released Products | ReleasedProductCreationsV2 | 42 |
| Customer Groups | CustomerGroups | 2 |
| Customers | CustomersV3 | 20 |
| Vendor Groups | VendorGroups | 2 |
| Vendors | VendorsV2 | 20 |
| Workers | Workers | 14 |

### Phase 3 — Transactional Setup (Week 5–6)

| Task | Entity | Records |
|------|--------|---------|
| Posting Profiles (AR) | CustPostingProfiles | 1 |
| Posting Profiles (AP) | VendPostingProfiles | 1 |
| Inventory Posting | Manual via UI | ~8 rows |
| Sales Pricing | TradeAgreementJournals | 42 |
| Opening Balances | GeneralJournals | As needed |

### Phase 4 — Validation & Cutover (Week 7–8)

| Task | Description |
|------|-------------|
| End-to-end SO test | Create SO → Confirm → Pick → Pack → Invoice |
| End-to-end PO test | Create PO → Confirm → Receive → Invoice |
| Inventory adjustment | Load opening stock via movement journals |
| AR/AP opening balances | Journal entries for outstanding invoices |
| GL trial balance | Reconcile to source system |
| User acceptance testing | Sales team validates workflows |

---

## 18. Integration Considerations

| Integration | Direction | Method |
|-------------|-----------|--------|
| Bank reconciliation | Inbound | Electronic bank statement import |
| Exchange rates | Inbound | Exchange rate provider (ECB/Federal Reserve) |
| Shipping/Logistics | Outbound | Future: carrier integration |
| Reporting | Outbound | Power BI via Dataverse/Data Lake |
| E-commerce | Bidirectional | Future: Dynamics 365 Commerce |

---

## 19. Security Roles (Initial)

| Role | Users | Access |
|------|-------|--------|
| System Administrator | IT Admin | Full access |
| Sales Manager | Regional leads | SO, Customers, Pricing |
| Sales Clerk | Sales reps (14) | Create/edit SO, view customers |
| Purchasing Manager | Ops lead | PO, Vendors |
| Accounts Receivable Clerk | Finance | AR, Collections, Payments |
| Accounts Payable Clerk | Finance | AP, Vendor payments |
| Inventory Manager | Warehouse lead | Inventory journals, stock |

---

## 20. Manufacturing & Costing Configuration

### 20.1 Cost Categories

Cost categories represent the hourly rates assigned to manufacturing operations for BOM/route costing.

| Cost Category ID | Name | Type | Hourly Rate | Cost Group |
|------------------|------|------|-------------|------------|
| LABOR-STD | Standard Assembly Labor | DirectLabor | $40.00 | MFG-LAB |
| LABOR-SKILL | Skilled Technical Labor | DirectLabor | $55.00 | MFG-LAB |
| MACHINE | Machine and Tooling Time | Machine | $20.00 | MFG-MCH |

### 20.2 Route Groups

| Route Group | Name | Setup Time Calc | Run Time Calc | Quantity Calc |
|-------------|------|-----------------|---------------|---------------|
| DISC | Discrete Manufacturing | ✅ Yes | ✅ Yes | No |

> **Critical**: The route group's "Setup time" and "Run time" checkboxes under the **Calculation** section must be **checked**. If unchecked, BOM calculation will completely ignore route costs — even when RouteOperationsProperties records exist with valid times and cost categories.

### 20.3 Operations Resources (Work Centers)

| Resource ID | Name | Type | Runtime Cost Category | Setup Cost Category |
|-------------|------|------|----------------------|---------------------|
| WC-FRAME-0 | Frame Preparation Station 1 | Machine | MACHINE | MACHINE |
| WC-WHEEL-0 | Wheel Assembly Station 1 | Machine | MACHINE | MACHINE |
| WC-DRIVE-0 | Drivetrain Assembly Station 1 | Personnel | LABOR-SKILL | LABOR-SKILL |
| WC-FINAL-0 | Final Assembly Station 1 | Personnel | LABOR-STD | LABOR-STD |
| WC-QC-01 | Quality Control Station 1 | Personnel | LABOR-SKILL | LABOR-SKILL |
| WC-PACK-01 | Packaging Station 1 | Personnel | LABOR-STD | LABOR-STD |
| WC-EBIKE-0 | E-Bike Electrical Assembly Station 1 | Personnel | LABOR-SKILL | LABOR-SKILL |

### 20.4 Costing Version

| Attribute | Value |
|-----------|-------|
| Version ID | STD |
| Name | Standard Cost |
| Costing Type | Standard cost |
| Block | No |
| Block Activation | No |
| BOM Explosion Level | Single Level |

### 20.5 Costing Sheet Structure

| Node | Type | Cost Group | Surcharge % | Basis |
|------|------|------------|-------------|-------|
| Material | Subtotal | — | — | Sum of MAT-* cost groups |
| Material Surcharge | Surcharge | MAT-SURCHG | 5% | Material subtotal |
| Manufacturing | Subtotal | — | — | Sum of MFG-* cost groups |
| Manufacturing Surcharge | Surcharge | MFG-SURCHG | 150% | Manufacturing subtotal |
| Total Cost | Total | — | — | All nodes |

> **Outstanding Manual Step**: Costing sheet surcharge nodes require absorption cost group assignment in the CostSheetDesigner tree control. This cannot be configured via MCP/OData.

### 20.6 Cost Groups

| Cost Group ID | Type | Purpose |
|---------------|------|---------|
| MAT-FRM | Direct materials | Frames and structural components |
| MAT-CMP | Direct materials | Mechanical/electrical components |
| MAT-MSC | Direct materials | Miscellaneous hardware and accessories |
| MFG-LAB | Direct manufacturing | Labor costs (LABOR-STD, LABOR-SKILL) |
| MFG-MCH | Direct manufacturing | Machine time costs |
| MAT-SURCHG | Indirect | Material overhead surcharge |
| MFG-SURCHG | Indirect | Manufacturing overhead surcharge |

### 20.7 Route Operation Mapping

All 42 manufactured products have routes with 6 standard operations (plus EBIKE for e-bikes). Each operation links to a work center resource via `RouteOperationsProperties`.

| Operation | Resource | Cost Category | Description |
|-----------|----------|---------------|-------------|
| FRAME | WC-FRAME-0 | LABOR-STD | Frame preparation and cutting |
| WHEEL | WC-WHEEL-0 | LABOR-STD | Wheel assembly and truing |
| DRIVE | WC-DRIVE-0 | LABOR-SKILL | Drivetrain assembly |
| FINAL | WC-FINAL-0 | LABOR-STD | Final assembly and adjustment |
| QC | WC-QC-01 | LABOR-SKILL | Quality inspection |
| PACK | WC-PACK-01 | LABOR-STD | Packaging for shipment |
| EBIKE | WC-EBIKE-0 | LABOR-SKILL | E-bike electrical assembly (7 items only) |

### 20.8 Route Time Profiles

| Profile | Items | FRAME | WHEEL | DRIVE | FINAL | QC | PACK | EBIKE |
|---------|-------|-------|-------|-------|-------|-----|------|-------|
| A (Light) | BX-1011–1013, RO-1001–1003, HB-1174, MB-1031, CB-1161–1163 | 0.20 | 0.26 | 0.40 | 0.26 | 0.20 | 0.14 | — |
| B (Medium) | CC-1021–1023, DB-1081–1083, HB-1171–1173, HB-1175–1176, MB-1032 | 0.25 | 0.33 | 0.50 | 0.33 | 0.25 | 0.17 | — |
| C (Heavy) | BX-1014–1016, MB-1033–1034, RC-1051–1057 | 0.32 | 0.43 | 0.65 | 0.43 | 0.32 | 0.22 | — |
| E-A | EB-1131 | 0.20 | 0.26 | 0.40 | 0.26 | 0.20 | 0.14 | 0.40 |
| E-B | EB-1132, EB-1133, EB-1135 | 0.25 | 0.33 | 0.50 | 0.33 | 0.25 | 0.17 | 0.50 |
| E-C | EB-1134, EB-1136, EB-1137 | 0.32 | 0.43 | 0.65 | 0.43 | 0.32 | 0.22 | 0.65 |

Setup times: FRAME=0.08hr, WHEEL=0.05hr, DRIVE=0.10hr, FINAL=0.05hr, QC=0, PACK=0, EBIKE=0.15hr.

### 20.9 Standard Cost Results (Activated)

Sample calculated standard costs (materials + route labor + overhead surcharges):

| Item | Description | Standard Cost |
|------|-------------|---------------|
| BX-1011 | BMX Freestyle 20" Basic | $412.50 |
| BX-1014 | BMX Park 20" Pro | $694.38 |
| CC-1021 | Cyclocross CX-1 Entry | $693.13 |
| DB-1081 | Downhill DH-1 Comp | $917.13 |
| EB-1131 | E-Bike Commuter 250W | $1,415.50 |
| EB-1134 | E-Bike Mountain 500W | $2,024.75 |
| RC-1051 | Road Race Carbon Elite | $1,276.38 |
| HB-1171 | Hybrid City Sport | $636.13 |

---

## 21. Key Assumptions & Decisions

| # | Decision | Rationale |
|---|----------|-----------|
| 1 | Single legal entity initially | Simplifies go-live; multi-company can follow |
| 2 | USD as accounting currency | Majority of revenue in USD; foreign currencies via exchange rates |
| 3 | FIFO inventory valuation | Standard for distribution/wholesale |
| 4 | No serial/batch tracking | Bicycles sold as standard items, not individually tracked |
| 5 | Fixed sales pricing | No complex trade agreements initially |
| 6 | 12.5% flat tax rate | Matches source data; refine post go-live per jurisdiction |
| 7 | Manual inventory posting setup | MCP tools cannot configure InventPosting ListBox controls |
| 8 | SAP Partner IDs → D365 Account Numbers | Mapped via CUST-/VEND- prefix convention |
| 9 | SAP SALESORDERID preserved | Stored as external reference on migrated orders |
| 10 | Historical orders imported as GL balances only | No open SO migration — clean cutover |
| 11 | Standard cost for all manufactured items | Single costing version (STD) with BOM+Route calculation |
| 12 | DefaultOrderType = Production for manufactured items | Required for BOM calculation to produce pending prices |
| 13 | Route group calculation flags must be enabled | DISC route group Setup/Run time calc = Yes for route costing |
| 14 | Cost category prices in costing version | Hourly rates stored as pending → activated in STD version |
| 15 | Costing sheet surcharges require manual UI | CostSheetDesigner tree control not accessible via MCP |

---

*Document Version: 1.1 — Updated May 21, 2026*
*Source: SAP Datasphere Bikes Sales sample content*
*Updates: Added Manufacturing & Costing Configuration (Section 20), revised decisions table*
