---
name: sql-analyst
description: Database connection and SQL querying skill. Use this to connect to SQLite, MySQL, or PostgreSQL databases to extract and analyze data.
---

# SQL Data Analyst Skill

This skill teaches how to connect to databases, execute SQL queries, and load the results into Pandas DataFrames for analysis.

## Dependencies
```bash
pip install sqlalchemy pandas
# For specific databases, you may also need:
# pip install pymysql (MySQL)
# pip install psycopg2-binary (PostgreSQL)
```

## Guidelines

1. **Read-Only by Default**: Unless explicitly asked to modify data, ALWAYS use `SELECT` statements. Never run `DROP`, `DELETE`, or `UPDATE` unless specifically instructed.
2. **Limit Results**: When exploring an unknown database, always use `LIMIT 10` or `LIMIT 100` to avoid loading massive datasets into memory.
3. **Use Pandas**: Always load SQL results into a Pandas DataFrame for easier manipulation and display.

## Example: SQLite Connection (Local)

```python
import pandas as pd
import sqlite3

# Connect to local SQLite DB
conn = sqlite3.connect('database.db')

# Query data
query = """
    SELECT category, SUM(sales) as total_sales
    FROM transactions
    WHERE date >= '2023-01-01'
    GROUP BY category
    ORDER BY total_sales DESC
    LIMIT 10;
"""

# Load into DataFrame
df = pd.read_sql_query(query, conn)
print(df.head())

# Always close connection
conn.close()
```

## Example: SQLAlchemy (MySQL/PostgreSQL)

```python
import pandas as pd
from sqlalchemy import create_engine

# Connection string format: dialect+driver://username:password@host:port/database
# Example for MySQL:
# engine = create_engine('mysql+pymysql://user:pass@localhost/dbname')

# Example for PostgreSQL:
# engine = create_engine('postgresql://user:pass@localhost/dbname')

# query = "SELECT * FROM users LIMIT 5"
# df = pd.read_sql(query, engine)
# print(df)
```
