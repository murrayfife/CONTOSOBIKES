# Part: TIRE-CRUISE

## Entity: `ReleasedProductCreationsV2`

| Field | Value |
| --- | --- |
| ItemNumber | TIRE-CRUISE |
| ProductName | Cruiser Tire Set (2x 26 inch) |
| SearchName | Cruiser Tire Set (2x 26 inch) |
| ProductGroupId | COMP |
| ItemModelGroupId | FIFO |
| StorageDimensionGroupName | SITE-WH |
| TrackingDimensionGroupName | NONE |
| InventoryUnitSymbol | EA |
| SalesUnitSymbol | EA |
| PurchaseUnitSymbol | EA |
| BOMUnitSymbol | EA |
| NetWeight | 1.0 |
| WeightUnit | KG |
| PurchasePrice | 16.00 |
| PurchaseCurrencyCode | USD |
| DefaultOrderType | Purchase |
| dataAreaId | cbks |

## Default Order Settings

| Field | Value |
| --- | --- |
| ItemNumber | TIRE-CRUISE |
| InventSiteId | AMER |
| InventWarehouseId | AMER-WH1 |
| dataAreaId | cbks |

## Vendor Assignment

| Field | Value |
| --- | --- |
| DefaultVendorAccountNumber | [VEND-0008](../vendors/VEND-0008.md) |
| VendorName | Contoso Tire Co |
| TradeAgreementPrice | 16.00 |
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
