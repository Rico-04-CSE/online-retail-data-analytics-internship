# Data Dictionary

| Column | Meaning | Type | Project Treatment |
|---|---|---|---|
| InvoiceNo | Transaction/invoice identifier | Categorical | String; leading C indicates cancellation |
| StockCode | Product identifier | Categorical | String |
| Description | Product description | Text/Categorical | Trim whitespace; missing required for product analysis |
| Quantity | Quantity purchased | Integer | Numeric conversion; negative values interpreted alongside cancellation logic |
| InvoiceDate | Transaction timestamp | Datetime | Parsed to datetime |
| UnitPrice | Unit price in sterling | Numeric | Numeric conversion; non-positive sales prices removed |
| CustomerID | Customer identifier | Categorical | Missing values retained as GUEST |
| Country | Customer country | Categorical | Whitespace standardized |
| Revenue | Derived metric | Numeric | Quantity × UnitPrice |
| IsCancellation | Derived cancellation flag | Boolean | InvoiceNo starts with C |
| Price_Outlier | Derived anomaly flag | Boolean | IQR-based flag |
