# Python Context Managers & Async Database Operations

This project demonstrates the use of context managers for database operations and asynchronous query execution in Python.

## 📁 Project Structure
```
python-context-async-operations-0x02/
├── 0-databaseconnection.py  # Task 0: Basic context manager
├── 1-execute.py            # Task 1: Reusable query manager
├── 3-concurrent.py         # Task 2: Async queries
└── README.md               # This documentation
```

## 🛠️ Tasks & Implementation

### 0. Custom Class-Based Context Manager
**File**: `0-databaseconnection.py`  
**Objective**: Create a context manager for database connections.

**Implementation**:
```python
import sqlite3

class DatabaseConnection:
    def __init__(self, db_name):
        self.db_name = db_name
        self.conn = None

    def __enter__(self):
        self.conn = sqlite3.connect(self.db_name)
        return self.conn.cursor()

    def __exit__(self, exc_type, exc_val, exc_tb):
        if self.conn:
            self.conn.close()

# Usage
with DatabaseConnection('users.db') as cursor:
    cursor.execute("SELECT * FROM users")
    print(cursor.fetchall())
```

### 1. Reusable Query Context Manager
**File**: `1-execute.py`  
**Objective**: Create a reusable query executor.

**Implementation**:
```python
import sqlite3

class ExecuteQuery:
    def __init__(self, query, params=None):
        self.query = query
        self.params = params or ()
        self.conn = None
        self.cursor = None

    def __enter__(self):
        self.conn = sqlite3.connect('users.db')
        self.cursor = self.conn.cursor()
        self.cursor.execute(self.query, self.params)
        return self.cursor.fetchall()

    def __exit__(self, exc_type, exc_val, exc_tb):
        if self.conn:
            self.conn.close()

# Usage
results = ExecuteQuery(
    "SELECT * FROM users WHERE age > ?", 
    (25,)
)
print(results)
```

### 2. Concurrent Asynchronous Database Queries
**File**: `3-concurrent.py`  
**Objective**: Execute queries concurrently using asyncio.

**Implementation**:
```python
import asyncio
import aiosqlite

async def async_fetch_users():
    async with aiosqlite.connect('users.db') as db:
        cursor = await db.execute("SELECT * FROM users")
        return await cursor.fetchall()

async def async_fetch_older_users():
    async with aiosqlite.connect('users.db') as db:
        cursor = await db.execute("SELECT * FROM users WHERE age > 40")
        return await cursor.fetchall()

async def fetch_concurrently():
    return await asyncio.gather(
        async_fetch_users(),
        async_fetch_older_users()
    )

# Usage
if __name__ == "__main__":
    all_users, older_users = asyncio.run(fetch_concurrently())
    print("All users:", len(all_users))
    print("Users > 40:", len(older_users))
```

## 🚀 Key Features

1. **Context Managers**:
   - Automatic resource management
   - Clean connection handling
   - Exception-safe operations

2. **Async Operations**:
   - Concurrent query execution
   - Non-blocking database access
   - Efficient I/O handling

## 📦 Dependencies
- Python 3.7+
- sqlite3 (standard library)
- aiosqlite (`pip install aiosqlite`)

## 🔧 Usage
1. Clone the repository
2. Ensure you have a SQLite database named `users.db`
3. Run individual task files to test functionality:
   ```bash
   python 0-databaseconnection.py
   python 1-execute.py
   python 3-concurrent.py
   ```

This project demonstrates modern Python patterns for efficient and safe database operations.