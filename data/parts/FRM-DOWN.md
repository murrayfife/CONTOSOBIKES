# Part: FRM-DOWN

## Entity: `ReleasedProductCreationsV2`

| Field | Value |
| --- | --- |
| ItemNumber | FRM-DOWN |
| ProductName | Downhill Frame - Aluminum Alloy |
| SearchName | Downhill Frame - Aluminum Alloy |
| ProductGroupId | COMP |
| ItemModelGroupId | FIFO |
| StorageDimensionGroupName | SITE-WH |
| TrackingDimensionGroupName | NONE |
| InventoryUnitSymbol | EA |
| SalesUnitSymbol | EA |
| PurchaseUnitSymbol | EA |
| BOMUnitSymbol | EA |
| NetWeight | 3.2 |
| WeightUnit | KG |
| PurchasePrice | 130.00 |
| PurchaseCurrencyCode | USD |
| DefaultOrderType | Purchase |
| dataAreaId | cbks |

## Default Order Settings

| Field | Value |
| --- | --- |
| ItemNumber | FRM-DOWN |
| InventSiteId | AMER |
| InventWarehouseId | AMER-WH1 |
| dataAreaId | cbks |

## Vendor Assignment

| Field | Value |
| --- | --- |
| DefaultVendorAccountNumber | [VEND-0002](../vendors/VEND-0002.md) |
| VendorName | Contoso BMX Frames |
| TradeAgreementPrice | 130.00 |
| TradeAgreementCurrency | USD |
| TradeAgreementFromDate | 2026-01-01 |
| TradeAgreementToDate | 2027-12-31 |

## Coverage Planning

| Field | Value |
|-------|-------|
| CoverageGroup | PURCH (Purchased Components) |
| CoveragePeriodDays | 1 (daily) |
| PlannedOrderType | Purchase |

> Master planning groups requirements by day — one planned PO per item per day.

## Used In BOMs
- [DB-1081](../boms/DB-1081.md)
- [DB-1082](../boms/DB-1082.md)
- [DB-1083](../boms/DB-1083.md)
