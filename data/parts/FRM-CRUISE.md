# Part: FRM-CRUISE

## Entity: `ReleasedProductCreationsV2`

| Field | Value |
| --- | --- |
| ItemNumber | FRM-CRUISE |
| ProductName | Cruiser Frame - Steel |
| SearchName | Cruiser Frame - Steel |
| ProductGroupId | COMP |
| ItemModelGroupId | FIFO |
| StorageDimensionGroupName | SITE-WH |
| TrackingDimensionGroupName | NONE |
| InventoryUnitSymbol | EA |
| SalesUnitSymbol | EA |
| PurchaseUnitSymbol | EA |
| BOMUnitSymbol | EA |
| NetWeight | 3.5 |
| WeightUnit | KG |
| PurchasePrice | 55.00 |
| PurchaseCurrencyCode | USD |
| DefaultOrderType | Purchase |
| dataAreaId | cbks |

## Default Order Settings

| Field | Value |
| --- | --- |
| ItemNumber | FRM-CRUISE |
| InventSiteId | AMER |
| InventWarehouseId | AMER-WH1 |
| dataAreaId | cbks |

## Vendor Assignment

| Field | Value |
| --- | --- |
| DefaultVendorAccountNumber | [VEND-0003](../vendors/VEND-0003.md) |
| VendorName | Contoso Leisure Frames |
| TradeAgreementPrice | 55.00 |
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
- [CB-1161](../boms/CB-1161.md)
- [CB-1162](../boms/CB-1162.md)
- [CB-1163](../boms/CB-1163.md)
