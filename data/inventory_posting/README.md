# Inventory Posting Setup

## Configuration Method: Manual (D365 UI)

> **Note:** Inventory posting profiles cannot be created via OData. They must be configured
> manually in D365 via **Inventory management > Setup > Posting > Posting**.

## Required Posting Types

### Sales Order Tab

| Posting Type | Item Group | Main Account | Description |
|-------------|-----------|-------------|-------------|
| Revenue | ALL | 4100 | Sales Revenue |
| Cost of goods sold, invoiced | ALL | 5200 | COGS |
| Sales order issue | ALL | 1400 | Inventory (issue) |

### Purchase Order Tab

| Posting Type | Item Group | Main Account | Description |
|-------------|-----------|-------------|-------------|
| Purchase expenditure for product | ALL | 5100 | Purchase Expense |
| Cost of purchased materials invoiced | ALL | 1300 | Purchased Materials |
| Purchase order receipt | ALL | 1400 | Inventory (receipt) |

### Inventory Tab

| Posting Type | Item Group | Main Account | Description |
|-------------|-----------|-------------|-------------|
| Inventory issue | ALL | 1400 | Inventory Asset |
| Inventory receipt | ALL | 1400 | Inventory Asset |
| Physical issue | ALL | 1400 | Inventory Asset |
| Physical receipt | ALL | 1400 | Inventory Asset |

## Known Limitations

- ListBox controls for posting type switching are non-interactive via MCP
- Tab navigation works: `form_open_or_close_tab(tabName="ctrlTabSales")` etc.
- Must manually switch posting types in D365 UI
