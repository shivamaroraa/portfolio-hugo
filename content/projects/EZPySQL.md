---
title: "EZPySQL"
summary: EZPySQL is a Python module that simplifies interactions with SQLite and MySQL databases.
tags: ["Python", "SQL"]
---


#### Github Link: https://github.com/shivamaroraa/EZPySQL

## Overview
EZPySQL is a Python module that simplifies interactions with SQLite and MySQL databases.


## Project Structure
````
EZPySQL
├── README.md
├── __init__.py
├── config.py
├── connection.py
├── setup.py
├── utils.py
└── requirements.txt

````

## Installation
First, clone the repository to your local machine:
````
git clone https://github.com/shivamaroraa/EZPySQL.git
````
Navigate to the project directory and install the required dependencies:
````
cd EZPySQL
pip install -r requirements.txt
````
## Usage
You can use this library to perform various database operations such as querying, inserting, updating and deleting data.
First, import the required functions:
`````python
from EZPySQL.utils import get_valid_columns, get_table_data, insert_into_db, update_in_db, delete_from_db
`````

**get_valid_columns**:
This function returns a list of valid columns for a given table.
Example:
`````python
table_name = 'Users'
valid_columns = get_valid_columns(table_name)
`````
---

**get_table_data**:
This function retrieves data from a table with optional arguments for filtering and ordering the results.
Example:
`````python
table_name = 'Users'
columns = ['first_name', 'last_name']
order_by = 'last_name'
limit = 10
results, error = get_table_data(table_name, columns, order_by, limit)
`````

--- 

**insert_into_db**:
This function inserts new records into a table.
Example:
```python
table_name = 'Users'
records = [{'username': 'johndoe', 'email': 'john.doe@example.com'}, {'username': 'janedoe', 'email': 'jane.doe@example.com'}]
result, error = insert_into_db(table_name, records=records)
`````
**update_in_db**:
This function updates records in a table based on certain conditions.
Example:
`````python
table_name = 'Balances'
updates = {'ETH': 3.24}
conditions = {'user_id': 7838313}
result, error = update_in_db(table_name, updates=updates, conditions=conditions)
`````

---

**delete_from_db**:
This function deletes records from a table based on certain conditions.
Example:
`````python
table_name = 'Orders'
conditions = {'order_id': 'hAb2cb8'}
result, error = delete_from_db(table_name, conditions=conditions)
`````
