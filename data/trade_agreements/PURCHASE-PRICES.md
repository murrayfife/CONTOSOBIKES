# Purchase Trade Agreements

## Entity: `PurchasePriceTradeAgreementJournalLines`

### Journal Header

| Field | Value |
| --- | --- |
| JournalNumber | PURCH-002 |
| Description | Component Purchase Prices 2026–2027 (Renewed) |
| dataAreaId | cbks |

> **Renewed 2026-05-21**: Previous journal PURCH-001 expired 2025-12-31. All prices carried forward at same rates pending vendor renegotiation.

### Lines

| ItemNumber | VendorAccount | Price (USD) | Unit | FromDate | ToDate |
| --- | --- | --- | --- | --- | --- |
| BRK-HDISC | VEND-0011 | 85 | EA | 2026-01-01 | 2027-12-31 |
| BRK-MDISC | VEND-0011 | 45 | EA | 2026-01-01 | 2027-12-31 |
| BRK-RIM | VEND-0011 | 20 | EA | 2026-01-01 | 2027-12-31 |
| CKIT-DROP | VEND-0012 | 35 | EA | 2026-01-01 | 2027-12-31 |
| CKIT-FLAT | VEND-0012 | 22 | EA | 2026-01-01 | 2027-12-31 |
| CKIT-RISE | VEND-0012 | 25 | EA | 2026-01-01 | 2027-12-31 |
| DRV-ENTRY | VEND-0009 | 35 | EA | 2026-01-01 | 2027-12-31 |
| DRV-HIGH | VEND-0010 | 150 | EA | 2026-01-01 | 2027-12-31 |
| DRV-MID | VEND-0009 | 75 | EA | 2026-01-01 | 2027-12-31 |
| EBATT-500 | VEND-0014 | 220 | EA | 2026-01-01 | 2027-12-31 |
| EBATT-750 | VEND-0014 | 350 | EA | 2026-01-01 | 2027-12-31 |
| ECTRL-STD | VEND-0014 | 90 | EA | 2026-01-01 | 2027-12-31 |
| EMOTOR-250 | VEND-0013 | 180 | EA | 2026-01-01 | 2027-12-31 |
| EMOTOR-500 | VEND-0013 | 280 | EA | 2026-01-01 | 2027-12-31 |
| FORK-BMX | VEND-0005 | 25 | EA | 2026-01-01 | 2027-12-31 |
| FORK-RIGID | VEND-0005 | 28 | EA | 2026-01-01 | 2027-12-31 |
| FORK-SUSP-L | VEND-0005 | 140 | EA | 2026-01-01 | 2027-12-31 |
| FORK-SUSP-M | VEND-0005 | 95 | EA | 2026-01-01 | 2027-12-31 |
| FORK-SUSP-S | VEND-0005 | 65 | EA | 2026-01-01 | 2027-12-31 |
| FRM-BMX | VEND-0002 | 60 | EA | 2026-01-01 | 2027-12-31 |
| FRM-CRUISE | VEND-0003 | 55 | EA | 2026-01-01 | 2027-12-31 |
| FRM-CYCLO | VEND-0001 | 110 | EA | 2026-01-01 | 2027-12-31 |
| FRM-DOWN | VEND-0002 | 130 | EA | 2026-01-01 | 2027-12-31 |
| FRM-EBIKE | VEND-0004 | 120 | EA | 2026-01-01 | 2027-12-31 |
| FRM-HYBRID | VEND-0003 | 75 | EA | 2026-01-01 | 2027-12-31 |
| FRM-MTB | VEND-0002 | 95 | EA | 2026-01-01 | 2027-12-31 |
| FRM-RACE | VEND-0001 | 145 | EA | 2026-01-01 | 2027-12-31 |
| FRM-ROAD | VEND-0001 | 85 | EA | 2026-01-01 | 2027-12-31 |
| MISC-HW | VEND-0016 | 5 | EA | 2026-01-01 | 2027-12-31 |
| PED-CLIP | VEND-0015 | 28 | EA | 2026-01-01 | 2027-12-31 |
| PED-STD | VEND-0015 | 12 | EA | 2026-01-01 | 2027-12-31 |
| SADL-COMF | VEND-0015 | 18 | EA | 2026-01-01 | 2027-12-31 |
| SADL-PERF | VEND-0015 | 32 | EA | 2026-01-01 | 2027-12-31 |
| TIRE-BMX | VEND-0008 | 15 | EA | 2026-01-01 | 2027-12-31 |
| TIRE-CRUISE | VEND-0008 | 16 | EA | 2026-01-01 | 2027-12-31 |
| TIRE-MTB | VEND-0008 | 22 | EA | 2026-01-01 | 2027-12-31 |
| TIRE-ROAD | VEND-0008 | 18 | EA | 2026-01-01 | 2027-12-31 |
| WHL-BMX | VEND-0007 | 30 | EA | 2026-01-01 | 2027-12-31 |
| WHL-MTB-27 | VEND-0006 | 42 | EA | 2026-01-01 | 2027-12-31 |
| WHL-MTB-29 | VEND-0007 | 48 | EA | 2026-01-01 | 2027-12-31 |
| WHL-ROAD | VEND-0006 | 45 | EA | 2026-01-01 | 2027-12-31 |

---

## Procurement Parameters — Trade Agreement Enforcement

| Parameter | Value | Purpose |
|-----------|-------|---------|
| Price tolerance validation | Enabled | Warn when PO line price deviates from trade agreement |
| Mandatory trade agreement match | Yes | Block PO confirmation if no active agreement exists |
| Override requires approval | Yes | Price overrides require procurement manager sign-off |
