# Tools & Tech

Quick reference for tools, commands, and code snippets.

---
## ðŸ’¾ SQL Snippets
### Common Queries
```sql
-- Find duplicates
SELECT column_name, COUNT(*)
FROM table_name
GROUP BY column_name
HAVING COUNT(*) > 1;
```

```sql
-- Date range query
SELECT *
FROM table_name
WHERE date_column BETWEEN TO_DATE('2024-01-01', 'YYYY-MM-DD')
                      AND TO_DATE('2024-12-31', 'YYYY-MM-DD');
```
### Oracle Specific
```sql
-- Check table structure
DESC table_name;

-- View constraints
SELECT * FROM user_constraints WHERE table_name = 'TABLE_NAME';
```

---
## ðŸ Python Patterns
### Data Processing
```python
import pandas as pd

# Read CSV
df = pd.read_csv('file.csv')

# Basic cleaning
df = df.dropna()
df = df.drop_duplicates()
```
### Database Connection
```python
import cx_Oracle

# Oracle connection
conn = cx_Oracle.connect('user/password@host:port/service')
cursor = conn.cursor()
```

---
## ðŸ–¥ï¸ Command Line
### File Operations
```bash
# Find large files
find . -type f -size +100M

# Search in files
grep -r "pattern" /path/to/search
```
### Git
```bash
# Common workflow
git status
git add .
git commit -m "message"
git push
```

---
## âš™ï¸ Configuration
### Environment Setup
- Virtual environments
- Package management
- Configuration files

---
## ðŸ”— Related
- [[ðŸ“Š Atria Database]] - Database-specific queries
- [[ðŸ”§ Data Engineering]] - Concepts behind the tools
- [[ðŸ’¼ Professional]] - Applied in work