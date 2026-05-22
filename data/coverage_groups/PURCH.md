# Coverage Group: PURCH

## Entity: MasterPlanningProductCoverageGroups

| Field | Value |
|-------|-------|
| dataAreaId | cbks |
| GroupId | PURCH |
| GroupName | Purchased Components |
| CoverageMethod | Period (0) |
| CoveragePeriodDays | 1 |
| CoverageFenceDays | 60 |
| PositiveDays | 60 |
| NegativeDays | 3 |
| ReceiptSafetyMarginDays | 2 |
| IssueSafetyMarginDays | 1 |
| ReorderSafetyMarginDays | 2 |

## Purpose
Used for standard purchased components (frames, wheels, tires, etc.). Period-based coverage with a 1-day window groups all same-day requirements into a single planned purchase order per item per day. Wider positive/negative days accommodate supplier lead time variability.
