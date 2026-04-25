# Atria Database

Central hub for Atria/Comtel database knowledge and documentation.

---
## ðŸ“‹ Overview

The Atria database is the core system for [add your description].

**Key Systems**:
- PPM Validation Suite
- DRR (Daily Response Report)
- KMBE (Kantar Media Back End)
- FMDP (Focal Meter Data Processing)
- CDP (Client Data Platform)
- OCR (Optical Character Recognition)
- Fusion
- Calibration

---
## ðŸ“Š Tables

Document important tables using `/data-table` template:
### Core Tables
- Add your frequently used tables here
### Audit Tables
- AT0022, AT0023, AT0027, etc.

```query
{:title "All Data Tables"
 :query [:find (pull ?b [*])
         :where
         [?b :block/content ?c]
         [(clojure.string/includes? ?c "**Table**::")]]
 :collapsed? false}
```

---
## ðŸ” Common Queries
### Example: Find Active Homes
```sql
-- Add your frequently used queries here
SELECT * FROM homes WHERE status = 'ACTIVE';
```
### Example: Check Data Quality
```sql
-- Add data quality checks
```

---
## ðŸ—ï¸ Architecture
- Data flow diagrams
- System dependencies
- Integration points

---
## ðŸ› Troubleshooting

Common issues and solutions:
### Issue: [Problem Name]
- **Symptoms**:
- **Cause**:
- **Solution**: 

---
## ðŸ“š Resources
- [[ðŸ”§ Data Engineering]] - General concepts
- [[ðŸ› ï¸ Tools & Tech]] - SQL patterns
- Internal documentation links