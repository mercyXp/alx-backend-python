# Python Decorators for Database Operations

This project demonstrates practical uses of Python decorators to enhance database operations with logging, connection handling, transactions, retries, and caching.

## 📁 Project Structure
```
python-decorators-0x01/
├── 0-log_queries.py       # Task 0: Query logging decorator
├── 1-with_db_connection.py # Task 1: Connection management decorator
├── 2-transactional.py     # Task 2: Transaction handling decorator
├── 3-retry_on_failure.py  # Task 3: Retry mechanism decorator
├── 4-cache_query.py       # Task 4: Query caching decorator
└── README.md              # This documentation
```

## 🛠️ Tasks & Implementation

### 0. Logging Database Queries
**File**: `0-log_queries.py`  
**Objective**: Create a decorator that logs SQL queries before execution.

**Implementation**:
```python
def log_queries(func):
    @functools.wraps(func)
    def wrapper(query):
        print(f"Executing query: {query}")
        return func(query)
    return wrapper
```

**Usage**:
```python
@log_queries
def fetch_all_users(query):
    # Database operations...
    pass
```

### 1. Database Connection Decorator
**File**: `1-with_db_connection.py`  
**Objective**: Automate connection handling.

**Implementation**:
```python
def with_db_connection(func):
    @functools.wraps(func)
    def wrapper(*args, **kwargs):
        conn = sqlite3.connect('users.db')
        try:
            result = func(conn, *args, **kwargs)
            return result
        finally:
            conn.close()
    return wrapper
```

**Usage**:
```python
@with_db_connection
def get_user_by_id(conn, user_id):
    # Query execution...
    pass
```

### 2. Transaction Management
**File**: `2-transactional.py`  
**Objective**: Automatic commit/rollback handling.

**Implementation**:
```python
def transactional(func):
    @functools.wraps(func)
    def wrapper(conn, *args, **kwargs):
        try:
            result = func(conn, *args, **kwargs)
            conn.commit()
            return result
        except Exception as e:
            conn.rollback()
            raise e
    return wrapper
```

**Usage**:
```python
@with_db_connection
@transactional
def update_user_email(conn, user_id, new_email):
    # Update operation...
    pass
```

### 3. Retry Mechanism
**File**: `3-retry_on_failure.py`  
**Objective**: Retry failed operations.

**Implementation**:
```python
def retry_on_failure(retries=3, delay=2):
    def decorator(func):
        @functools.wraps(func)
        def wrapper(*args, **kwargs):
            for attempt in range(retries):
                try:
                    return func(*args, **kwargs)
                except Exception as e:
                    if attempt == retries - 1:
                        raise e
                    time.sleep(delay)
        return wrapper
    return decorator
```

**Usage**:
```python
@with_db_connection
@retry_on_failure(retries=3, delay=1)
def fetch_users_with_retry(conn):
    # Query execution...
    pass
```

### 4. Query Caching
**File**: `4-cache_query.py`  
**Objective**: Cache query results.

**Implementation**:
```python
def cache_query(func):
    @functools.wraps(func)
    def wrapper(conn, query):
        if query in query_cache:
            return query_cache[query]
        result = func(conn, query)
        query_cache[query] = result
        return result
    return wrapper
```

**Usage**:
```python
@with_db_connection
@cache_query
def fetch_users_with_cache(conn, query):
    # Query execution...
    pass
```

## 🔄 Decorator Stacking
Decorators can be combined for powerful functionality:
```python
@with_db_connection
@transactional
@retry_on_failure
@log_queries
def secure_db_operation(conn, query):
    # Fully protected operation
    pass
```

## 🚀 How to Use
1. Ensure SQLite database (`users.db`) exists
2. Run individual task files to test functionality
3. Import decorators into your projects as needed

This project demonstrates how decorators can elegantly solve common database operation challenges while keeping code DRY and maintainable.