# Account Structure: CBKS-ACCT

## Entity: `DimensionHierarchies`

| Field | Value |
| --- | --- |
| Name | CBKS-ACCT |
| Description | Contoso Bikes Account Structure |
| IsDraft | No |
| ChartOfAccountsId | CBKS-COA |

## Segments

| Order | Dimension | Mandatory | Description |
| --- | --- | --- | --- |
| 1 | MainAccount | Yes | GL Account (1000-9999) |
| 2 | Department | No | SALES, OPS, ADMIN, WAREHOUSE |
| 3 | Region | No | AMER, WEST, EAST, SOUTH |