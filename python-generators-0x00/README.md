# Python Generators Project

This project demonstrates various use cases of Python generators for efficient data processing with SQL databases.

## Project Structure

```
python-generators-0x00/
├── seed.py                # Database setup and seeding script
├── 0-stream_users.py      # Single-row streaming generator
├── 1-batch_processing.py  # Batch processing implementation
├── 2-lazy_paginate.py     # Lazy pagination implementation
└── 4-stream_ages.py       # Memory-efficient aggregation
```

## Tasks

### 0. Getting started with Python generators
**Objective**: Set up a MySQL database and populate it with sample data.

**Files**:
- `seed.py`

**Functions**:
- `connect_db()`: Connects to the MySQL database server
- `create_database(connection)`: Creates the `ALX_prodev` database
- `connect_to_prodev()`: Connects to the `ALX_prodev` database
- `create_table(connection)`: Creates the `user_data` table
- `insert_data(connection, data)`: Inserts data from CSV into the database

**Table Structure**:
```sql
CREATE TABLE user_data (
    user_id VARCHAR(36) PRIMARY KEY,
    name VARCHAR(255) NOT NULL,
    email VARCHAR(255) NOT NULL,
    age DECIMAL NOT NULL
);
```

### 1. Generator that streams rows from an SQL database
**Objective**: Create a generator that streams rows one by one from the database.

**Files**:
- `0-stream_users.py`

**Function**:
- `stream_users()`: Generator that yields user rows one at a time

**Requirements**:
- Uses `yield` for generator implementation
- Contains no more than 1 loop

### 2. Batch processing large data
**Objective**: Process data in batches from the database.

**Files**:
- `1-batch_processing.py`

**Functions**:
- `stream_users_in_batches(batch_size)`: Fetches rows in batches
- `batch_processing(batch_size)`: Processes batches to filter users over age 25

**Requirements**:
- Uses `yield` for generator implementation
- Contains no more than 3 loops

### 3. Lazy loading paginated data
**Objective**: Implement lazy loading of paginated data.

**Files**:
- `2-lazy_paginate.py`

**Functions**:
- `lazy_paginate(page_size)`: Generator that lazily loads pages of data
- `paginate_users(page_size, offset)`: Helper function to fetch paginated data

**Requirements**:
- Uses `yield` for generator implementation
- Contains only one loop

### 4. Memory-efficient aggregation with generators
**Objective**: Compute average age efficiently using generators.

**Files**:
- `4-stream_ages.py`

**Functions**:
- `stream_user_ages()`: Generator that yields user ages one by one
- (Additional function to calculate average age)

**Requirements**:
- Does not load entire dataset into memory
- Uses no more than two loops
- Does not use SQL AVERAGE function

## Usage Examples

1. **Database Setup**:
```bash
./0-main.py
```

2. **Streaming Users**:
```bash
./1-main.py
```

3. **Batch Processing**:
```bash
./2-main.py | head -n 5
```

4. **Lazy Pagination**:
```bash
python 3-main.py | head -n 7
```

## Requirements
- Python 3.x
- MySQL database server
- MySQL connector for Python
- Dataset: `user_data.csv`