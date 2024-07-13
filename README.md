

## ETL Pipeline using Python and SQLAlchemy

This repository demonstrates an ETL pipeline using Python, pandas, SQLAlchemy, and pyodbc to interact with a Microsoft SQL Server database. The script reads Excel files, processes the data, and inserts it into an SQL table.

### Prerequisites

- Python 3.x
- pandas
- SQLAlchemy
- pyodbc
- Microsoft SQL Server

### Setup

1. Install the required Python libraries:

```bash
pip install pandas sqlalchemy pyodbc
```

2. Ensure that the ODBC driver for SQL Server is installed on your system.

### Usage

1. Clone the repository and navigate to the project directory:

```bash
git clone https://github.com/yourusername/etl-pipeline
cd etl-pipeline
```

2. Place your Excel files in the specified directory:

```plaintext
C:/Users/Rhugved/Desktop/Data Engineering/ETL Pipeline using Python/Equity
```

3. Update the database connection string in the script if necessary:

```python
conn = sal.create_engine('mssql+pyodbc://sqlserver')
```

### Script Description

1. **Import necessary libraries**:

```python
import pandas as pd
import sqlalchemy as sal
import pyodbc as odbc
import os
from sqlalchemy import text
```

2. **Create a connection to the SQL Server database**:

```python
conn = sal.create_engine('mssql+pyodbc://sqlserver')
```

3. **Change the directory to where the Excel files are located**:

```python
os.chdir("C:/Users/Rhugved/Desktop/Data Engineering/ETL Pipeline using Python/Equity")
```

4. **Verify the current working directory and list files**:

```python
os.getcwd()
os.listdir()
```

5. **Get the hostname and available ODBC drivers**:

```python
import socket
socket.gethostname()
odbc.drivers()
```

6. **Read and process each Excel file, then insert data into the SQL table**:

```python
for i in os.listdir():
    df = pd.read_excel(i)
    df = df.iloc[:100]
    df.to_sql('Equity', con=conn, if_exists='append', index=False)
```

7. **Read data from the SQL table**:

```python
pd.read_sql(sql='select * from Equity', con=connection)
```

8. **Connect to the database and execute a delete statement**:

```python
connection = conn.connect()
connection.execute(text('delete from Equity').execution_options(auto_commit=True))
```

### Additional Information

- Ensure your SQL Server instance is running and accessible.
- Modify the connection string based on your server configuration.
