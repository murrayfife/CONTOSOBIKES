# Fiscal Calendar: CBKS-FY

## Entity: `FiscalCalendars` + `FiscalCalendarYears` + `FiscalCalendarPeriods`

### Calendar

| Field | Value |
| --- | --- |
| CalendarId | CBKS-FY |
| Description | Contoso Bikes Fiscal Calendar |


### Fiscal Year

| Field | Value |
| --- | --- |
| CalendarId | CBKS-FY |
| FiscalYearName | FY2026 |
| StartDate | 2026-01-01 |
| EndDate | 2026-12-31 |


### Periods (create sequentially — one at a time, in order)

| CalendarId | FiscalYearName | Name | StartDate | EndDate | Type |
| --- | --- | --- | --- | --- | --- |
| CBKS-FY | FY2026 | Opening | 2026-01-01 | 2026-01-01 | Opening |
| CBKS-FY | FY2026 | January | 2026-01-01 | 2026-01-31 | Operating |
| CBKS-FY | FY2026 | February | 2026-02-01 | 2026-02-28 | Operating |
| CBKS-FY | FY2026 | March | 2026-03-01 | 2026-03-31 | Operating |
| CBKS-FY | FY2026 | April | 2026-04-01 | 2026-04-30 | Operating |
| CBKS-FY | FY2026 | May | 2026-05-01 | 2026-05-31 | Operating |
| CBKS-FY | FY2026 | June | 2026-06-01 | 2026-06-30 | Operating |
| CBKS-FY | FY2026 | July | 2026-07-01 | 2026-07-31 | Operating |
| CBKS-FY | FY2026 | August | 2026-08-01 | 2026-08-31 | Operating |
| CBKS-FY | FY2026 | September | 2026-09-01 | 2026-09-30 | Operating |
| CBKS-FY | FY2026 | October | 2026-10-01 | 2026-10-31 | Operating |
| CBKS-FY | FY2026 | November | 2026-11-01 | 2026-11-30 | Operating |
| CBKS-FY | FY2026 | December | 2026-12-01 | 2026-12-31 | Operating |
| CBKS-FY | FY2026 | Closing | 2026-12-31 | 2026-12-31 | Closing |


## Notes

- Periods MUST be created one-at-a-time sequentially — batch creation fails
- Create Opening first, then monthly periods in order, then Closing