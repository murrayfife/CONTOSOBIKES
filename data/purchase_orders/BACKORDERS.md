# Planned Purchase Orders

## Entity: PurchaseOrderHeadersV2 / PurchaseOrderLinesV2

All orders have:
- **dataAreaId**: cbks
- **CurrencyCode**: USD
- **ReceivingSiteId**: AMER
- **ReceivingWarehouseId**: AMER-WH1

These purchase orders replenish components to fulfill the backordered sales orders (SO CBKS-000009 through CBKS-000016). Orders are grouped by **Requested Delivery Date** based on vendor lead times and component criticality.

> **CORRECTED 2026-05-21**: POs restructured to align with approved vendor list and trade agreement pricing. Grouped by delivery date to sequence production scheduling.

---

# Delivery Group 1 — May 26, 2026 (Commodity & Small Components)

Short-lead commodity items needed first for sub-assembly prep.

---

## PO CBKS-000014 — Miscellaneous Hardware (VEND-0016)
- **Order Date**: 2026-05-21
- **Requested Delivery**: 2026-05-26

| Line | Item | Qty | Unit Price | Line Total |
|------|------|-----|-----------|-----------|
| 1 | MISC-HW (Miscellaneous Hardware) | 200 | $5.00 | $1,000.00 |

**PO Total**: $1,000.00

---

## PO CBKS-000013 — Pedals & Saddles (VEND-0015)
- **Order Date**: 2026-05-21
- **Requested Delivery**: 2026-05-26

| Line | Item | Qty | Unit Price | Line Total |
|------|------|-----|-----------|-----------|
| 1 | PED-STD (Standard Pedals) | 100 | $12.00 | $1,200.00 |
| 2 | PED-CLIP (Clipless Pedals) | 40 | $28.00 | $1,120.00 |
| 3 | SADL-COMF (Comfort Saddle) | 50 | $18.00 | $900.00 |
| 4 | SADL-PERF (Performance Saddle) | 30 | $32.00 | $960.00 |

**PO Total**: $4,180.00

---

## PO CBKS-000006 — Tires (VEND-0008)
- **Order Date**: 2026-05-21
- **Requested Delivery**: 2026-05-26

| Line | Item | Qty | Unit Price | Line Total |
|------|------|-----|-----------|-----------|
| 1 | TIRE-ROAD (Road Tire) | 80 | $18.00 | $1,440.00 |
| 2 | TIRE-BMX (BMX Tire) | 60 | $15.00 | $900.00 |
| 3 | TIRE-MTB (MTB Tire) | 50 | $22.00 | $1,100.00 |
| 4 | TIRE-CRUISE (Cruiser Tire) | 40 | $16.00 | $640.00 |

**PO Total**: $4,080.00

**Group 1 Total**: $9,260.00 (3 POs)

---

# Delivery Group 2 — May 28, 2026 (Mechanical Assemblies)

Assembled mechanical components — brakes, cockpits, drivetrains.

---

## PO CBKS-000010 — Cockpit Kits (VEND-0012)
- **Order Date**: 2026-05-21
- **Requested Delivery**: 2026-05-28

| Line | Item | Qty | Unit Price | Line Total |
|------|------|-----|-----------|-----------|
| 1 | CKIT-DROP (Drop Bar Cockpit Kit) | 30 | $35.00 | $1,050.00 |
| 2 | CKIT-FLAT (Flat Bar Cockpit Kit) | 40 | $22.00 | $880.00 |
| 3 | CKIT-RISE (Rise Bar Cockpit Kit) | 35 | $25.00 | $875.00 |

**PO Total**: $2,805.00

---

## PO CBKS-000009 — Brake Systems (VEND-0011)
- **Order Date**: 2026-05-21
- **Requested Delivery**: 2026-05-28

| Line | Item | Qty | Unit Price | Line Total |
|------|------|-----|-----------|-----------|
| 1 | BRK-HDISC (Hydraulic Disc Brake) | 40 | $85.00 | $3,400.00 |
| 2 | BRK-MDISC (Mechanical Disc Brake) | 50 | $45.00 | $2,250.00 |
| 3 | BRK-RIM (Rim Brake) | 60 | $20.00 | $1,200.00 |

**PO Total**: $6,850.00

---

## PO CBKS-000007 — Entry/Mid Drivetrains (VEND-0009)
- **Order Date**: 2026-05-21
- **Requested Delivery**: 2026-05-28

| Line | Item | Qty | Unit Price | Line Total |
|------|------|-----|-----------|-----------|
| 1 | DRV-ENTRY (Entry Drivetrain) | 35 | $35.00 | $1,225.00 |
| 2 | DRV-MID (Mid-Range Drivetrain) | 30 | $75.00 | $2,250.00 |

**PO Total**: $3,475.00

---

## PO CBKS-000008 — High-End Drivetrains (VEND-0010)
- **Order Date**: 2026-05-21
- **Requested Delivery**: 2026-05-28

| Line | Item | Qty | Unit Price | Line Total |
|------|------|-----|-----------|-----------|
| 1 | DRV-HIGH (High-End Drivetrain) | 15 | $150.00 | $2,250.00 |

**PO Total**: $2,250.00

**Group 2 Total**: $15,380.00 (4 POs)

---

# Delivery Group 3 — Jun 2, 2026 (Structural Components)

Wheels, forks, and frames — longer lead due to fabrication.

---

## PO CBKS-000004 — Road/MTB-27 Wheels (VEND-0006)
- **Order Date**: 2026-05-21
- **Requested Delivery**: 2026-06-02

| Line | Item | Qty | Unit Price | Line Total |
|------|------|-----|-----------|-----------|
| 1 | WHL-ROAD (Road Wheelset) | 40 | $45.00 | $1,800.00 |
| 2 | WHL-MTB-27 (MTB 27.5" Wheelset) | 30 | $42.00 | $1,260.00 |

**PO Total**: $3,060.00

---

## PO CBKS-000005 — BMX/MTB-29 Wheels (VEND-0007)
- **Order Date**: 2026-05-21
- **Requested Delivery**: 2026-06-02

| Line | Item | Qty | Unit Price | Line Total |
|------|------|-----|-----------|-----------|
| 1 | WHL-BMX (BMX Wheelset) | 50 | $30.00 | $1,500.00 |
| 2 | WHL-MTB-29 (MTB 29" Wheelset) | 25 | $48.00 | $1,200.00 |

**PO Total**: $2,700.00

---

## PO CBKS-000003 — Fork Assemblies (VEND-0005)
- **Order Date**: 2026-05-21
- **Requested Delivery**: 2026-06-02

| Line | Item | Qty | Unit Price | Line Total |
|------|------|-----|-----------|-----------|
| 1 | FORK-BMX (BMX Fork) | 30 | $25.00 | $750.00 |
| 2 | FORK-RIGID (Rigid Fork) | 40 | $28.00 | $1,120.00 |
| 3 | FORK-SUSP-S (Short Travel Suspension Fork) | 30 | $65.00 | $1,950.00 |
| 4 | FORK-SUSP-M (Medium Travel Suspension Fork) | 25 | $95.00 | $2,375.00 |
| 5 | FORK-SUSP-L (Long Travel Suspension Fork) | 15 | $140.00 | $2,100.00 |

**PO Total**: $8,295.00

---

## PO CBKS-000001 — Road/Race/Cyclo Frames (VEND-0001)
- **Order Date**: 2026-05-21
- **Requested Delivery**: 2026-06-02

| Line | Item | Qty | Unit Price | Line Total |
|------|------|-----|-----------|-----------|
| 1 | FRM-ROAD (Road Frame) | 20 | $85.00 | $1,700.00 |
| 2 | FRM-RACE (Carbon Race Frame) | 10 | $145.00 | $1,450.00 |

**PO Total**: $3,150.00

---

## PO CBKS-000002 — BMX/MTB Frames (VEND-0002)
- **Order Date**: 2026-05-21
- **Requested Delivery**: 2026-06-02

| Line | Item | Qty | Unit Price | Line Total |
|------|------|-----|-----------|-----------|
| 1 | FRM-BMX (BMX Frame) | 30 | $60.00 | $1,800.00 |
| 2 | FRM-MTB (Mountain Bike Frame) | 25 | $95.00 | $2,375.00 |

**PO Total**: $4,175.00

**Group 3 Total**: $21,380.00 (5 POs)

---

# Delivery Group 4 — Jun 9, 2026 (Specialty Electronics)

E-bike motors, batteries, and controllers — longest lead time (regulated/specialty).

---

## PO CBKS-000011 — E-Bike Motors (VEND-0013)
- **Order Date**: 2026-05-21
- **Requested Delivery**: 2026-06-09

| Line | Item | Qty | Unit Price | Line Total |
|------|------|-----|-----------|-----------|
| 1 | EMOTOR-250 (E-Bike Motor 250W) | 20 | $180.00 | $3,600.00 |
| 2 | EMOTOR-500 (E-Bike Motor 500W) | 10 | $280.00 | $2,800.00 |

**PO Total**: $6,400.00

---

## PO CBKS-000012 — E-Bike Batteries & Controllers (VEND-0014)
- **Order Date**: 2026-05-21
- **Requested Delivery**: 2026-06-09

| Line | Item | Qty | Unit Price | Line Total |
|------|------|-----|-----------|-----------|
| 1 | EBATT-500 (E-Bike Battery 500Wh) | 20 | $220.00 | $4,400.00 |
| 2 | EBATT-750 (E-Bike Battery 750Wh) | 15 | $350.00 | $5,250.00 |
| 3 | ECTRL-STD (E-Bike Controller) | 25 | $90.00 | $2,250.00 |

**PO Total**: $11,900.00

**Group 4 Total**: $18,300.00 (2 POs)

---

## Summary by Delivery Date

| Delivery Date | PO Count | Lines | Group Total | Cumulative |
|---------------|----------|-------|-------------|-----------|
| **May 26, 2026** | 3 | 9 | $9,260 | $9,260 |
| **May 28, 2026** | 4 | 9 | $15,380 | $24,640 |
| **Jun 2, 2026** | 5 | 11 | $21,380 | $46,020 |
| **Jun 9, 2026** | 2 | 5 | $18,300 | $64,320 |

## Summary by PO

| PO Number | Vendor | Category | Delivery | Total |
|-----------|--------|----------|----------|-------|
| CBKS-000001 | VEND-0001 | Road/Race/Cyclo Frames | Jun 2 | $3,150 |
| CBKS-000002 | VEND-0002 | BMX/MTB Frames | Jun 2 | $4,175 |
| CBKS-000003 | VEND-0005 | Fork Assemblies | Jun 2 | $8,295 |
| CBKS-000004 | VEND-0006 | Road/MTB-27 Wheels | Jun 2 | $3,060 |
| CBKS-000005 | VEND-0007 | BMX/MTB-29 Wheels | Jun 2 | $2,700 |
| CBKS-000006 | VEND-0008 | Tires | May 26 | $4,080 |
| CBKS-000007 | VEND-0009 | Entry/Mid Drivetrains | May 28 | $3,475 |
| CBKS-000008 | VEND-0010 | High-End Drivetrains | May 28 | $2,250 |
| CBKS-000009 | VEND-0011 | Brake Systems | May 28 | $6,850 |
| CBKS-000010 | VEND-0012 | Cockpit Kits | May 28 | $2,805 |
| CBKS-000011 | VEND-0013 | E-Bike Motors | Jun 9 | $6,400 |
| CBKS-000012 | VEND-0014 | E-Bike Batteries & Controllers | Jun 9 | $11,900 |
| CBKS-000013 | VEND-0015 | Pedals & Saddles | May 26 | $4,180 |
| CBKS-000014 | VEND-0016 | Miscellaneous Hardware | May 26 | $1,000 |

**Grand Total**: $64,320.00 across 34 order lines (14 POs)

## Production Scheduling Note

Assembly can begin on **May 28** for BMX, Road, and Cruiser bikes (commodity components arrive May 26, mechanical assemblies May 28). Mountain and Race bikes require structural components (Jun 2). E-bikes cannot begin final assembly until **Jun 9** when motors/batteries arrive. Estimated full backorder fulfillment: **Jun 13–16, 2026**.
