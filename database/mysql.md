###### tags : `tutorial` `sql` `mysql`

# MYSQL Cheat Sheet

## A. Introduction

### 1. MYSQL Data Type

#### Number
Number data type
- integer (signed, unsigned) : tinyint, smallint, mediumint, int, bigint
- float (signed, unsigned) : float, double
- decimal : decimal(5,2) => 5 digit, 2 angka di belakang koma,

Attribute: 
- type(n) : show n digit
- zerofill : INT(3) zerofill : add zero with total 3 digits: 007

#### String
- char (static size) : char(10) => char with max 10 characters
- varchar (dynamic size) : varchar(10) => varchar with max 10 characters
- text : tinytext, text, mediumtext, longtext
- enum : string with limited option, ex ("male", "female") 

#### Datetime
- date : yyyy-mm-dd
- datetime : yyyy-mm-dd hh-mm-ss
- timestamp : yyyy-mm-dd hh-mm-ss
- time : hh-mm-ss
- year : yyyy

#### Boolean : TRUE or FALSE
#### Misc : blob, spatial, json

### 2. Using Mysql CLI
- connect to mysql database : 
```
mysql -u <username> -p
```
- Create a sql from a database
```
mysql -u root -p <db_name> > <file_dump.sql>
```
- Execute a sql script into a certain database
```
mysql -u root -p <db_name> < <file_dump.sql>
```
> Note : make sure <db_name> is exists to inject sql script. 

## B. Data Definition Language (DDL) 
DDL deals with database schemas and descriptions, of how the data should reside in the database

- CREATE - to create a database and its objects like (table, index, views, store procedure, function, and triggers)
- ALTER - alters the structure of the existing database
- DROP - delete objects from the database
- TRUNCATE - remove all records from a table, including all spaces allocated for the records are removed
- COMMENT - add comments to the data dictionary
- RENAME - rename an object

### 1. Create

#### Create a Database
```
CREATE DATABASE <db_name>
```

Common used SQL command related to a database
- `USE <db_name>` : Use a database
- `SHOW DATABASES` : Show database list

#### Create a Table

```
CREATE TABLE <tb_name> (
  <field_1> <data_type> <attribute>, 
  <field_2> <data_type> <attribute>, 
  ... 
  <keyword> <field>
) ENGINE = InnoDB;
```

Example
```
CREATE TABLE categories(
    id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(100) NOT NULL
) ENGINE=InnoDB;

CREATE TABLE products (
  id INT NOT NULL AUTO INCREMENT,
  name VARCHAR(100),
  price UNSIGNED INT NOT NULL,
  quantity UNSIGNED SMALL INT DEFAULT 0,
  categoryId INT, 
  PRIMARY KEY (id), 
  FOREIGN KEY (categoryId) 
        REFERENCES categories(id)
) ENGINE = InnoDB;
```

Common used SQL command related to a table
- `SHOW TABLES` : Show table list
- `DESCRIBE <tb_name>` : Get table description

### 2. Alter
#### Alter a Table

Supported method : 
- `ADD <field> <data_type> <attribute>`
- `DROP <field>` 
- `RENAME <field> to <new_field>`
- `MODIFY <field> <data_type> <attribute>`

Basic Syntax : 

```
ALTER TABLE <tb_name>
<alter_method>;
```

Example
```
ALTER TABLE products
  ADD COLUMN createdAt TIMESTAMP NOT NULL DEFAULT CURRENT_TIMESTAMP,
  DROP COLUMN categories, 
  RENAME COLUMN name TO productName;

ALTER TABLE products
  ADD PRIMARY KEY (id);

-- change name type data and put it after jumlah
ALTER TABLE barang
  MODIFY COLUMN name VARCHAR(100) 
    AFTER jumlah;

ALTER TABLE products
  ADD COLUMN 
    category ENUM('Electronic', 'House', 'Others')
    AFTER name;
```
### 3. Drop
> Note : drop a large database or a table will takes time

#### Drop a Database
```
DROP DATABASE <db_name>;
```

#### Drop a Table
```
DROP TABLE <tb_name>;
```

### 4. Truncate
```
TRUNCATE TABLE <tb_name>;
```

## C. Data Manipulation Language (DML) 
DML deals with data manipulation and includes most common SQL statements such SELECT, INSERT, UPDATE, DELETE, etc., and it is used to store, modify, retrieve, delete and update data in a database.

- SELECT - retrieve data from a database
- INSERT - insert data into a table
- UPDATE - updates existing data within a table
- DELETE - Delete all records from a database table
- MERGE - UPSERT operation (insert or update)
- CALL - call a PL/SQL or Java subprogram
- EXPLAIN PLAN - interpretation of the data access path
- LOCK TABLE - concurrency Control

### 1. Select
#### 1.1 Basic Query

```
SELECT 
  DISTINCT 
  <TOP_specification> 
  <select_list>
FROM <left_tb>
  <join_type> JOIN <right_tb>
  ON <join_condition>
WHERE 
  <where_condition>
GROUP BY 
  <group_by_list>
HAVING 
  <having_condition>
ORDER BY 
  <order_by_list>
LIMIT 
  <limit_parameter>;
```

Example
```
-- select all field in products
SELECT * 
FROM products
ORDER BY createdAt DESC
LIMIT 10;
```

#### 1.2 Select Clause
- Select multiple field with alias
```
SELECT 
  <keyword> <field_1> AS <alias>, 
  <field_2> AS <alias>, 
  ...
FROM <tb_name> AS <alias>;
```

- A wild card
use `*` to select all field on the table
```
SELECT * FROM <tb_name>;
```
- Use Distinct Keyword to get distinct field
```
SELECT 
DISTINCT category 
FROM products;
```

- Example
```
SELECT 
  p.id AS 'Kode', 
  p.name AS 'Nama', 
  p.category AS 'Kategori'
FROM products AS p;  
```


#### 1.3 Where Clause
Use `where` clause to filter query with specific criteria.

- Comparison Operator

| Operator | Description | 
| -------- | -------- | 
| `=`     | Equal to     | 
| `<>` or `!=`     | Not equal to     | 
| `<`     | Less than     | 
| `<=`     | Less than or equal to     | 
| `>`     | Greater than    | 
| `>=`     | Greater than or equal to     | 


> Mysql is case insensitive, so filtering name = 'product' and name = 'Product' are equivalent 

```
-- filter a query that created after 2021-01-18
...
WHERE 
  createdAt > '2021-01-18'
...

-- Find product which category is not 'food'
...
WHERE 
  category != 'food'
...
```
- Logical Operator
  - Available Operator : `AND` and `OR` 
  - Similar with mathematic's operation, `AND` will execute first before `OR`
  - Example
  ```
  ...
  WHERE 
    category = handphone AND
    price < 5000000
  ...
  ```
- In and Between Operator
  - In : filter a query if the value is on the list
  - Between : filter a query between two numbers
  - Example
  ```
  ...
  WHERE 
    <field> IN (<value_1>, <value_2>)
  
  ...
  WHERE 
    <field> BETWEEN <value_1> AND <value_2> 
  
  ```
- Like Operator
  - Basic operator

    | Example | Description |
    | -------- | -------- |
    | LIKE '`<keyword>%`'     | A string begin with `<keyword>`     |
    | LIKE '`%<keyword>`'     | A string end with `<keyword>`     |
    | LIKE '`%<keyword>%`'     | A string include `<keyword>`     |
    | NOT LIKE '`%<keyword>%`'     | A string not include `<keyword>` |
  
  - Example
    ```
    SELECT *
    FROM products
    WHERE 
      name LIKE 'smartphone%'; 
    ```
    
- Null Operator
```
SELECT * 
FROM products 
WHERE price IS NULL;
```
    
- Regex Pattern
LIKE '`%<keyword>%`' and REGEXP '`<keyword>`' are equivalent
  - ^ : beginning with
  - $ : ending with
  - | : logical or
  - [abc]  : match single char
  - [a-z] : range a - z

Example pattern:
  - ^phone : begin with phone
  - phone$ : end with phone
  - phone|food : begin or end with phone or food
  - [gie] m  : begin or end with gm, im or em
  - a[abc] : begin or end with aa, ab, or ac
  - a[a-f] : begin or end with aa, ab, ac,... af

Regex On SQL query
```
-- Syntax
WHERE
  <field> REGEXP <pattern>
```
Example
```
SELECT 
    name
FROM
    products
WHERE
    product REGEXP '^smart';
```

#### 1.4 Order By Clause
- Available keyword are `DESC` and `ASC` with default value `ASC`  
- Basic Syntax
```
...
ORDER BY
    <field> <keyword>;
```
- Example
```
...
ORDER BY
    createdAt DESC;
```
        

#### 1.5 Limit Clause
Use `LIMIT` clause to set offset and limit of query
```
-- limit cluase with offset and limit
...
LIMIT <offset>, <limit>;


-- limit clause with a limit
...
LIMIT <limit>;
```
        
#### 1.6 Join Table
```
-- join 2 tables
SELECT 
  order_id, 
  first_name, 
  last_name, 
  o.customer_id
FROM orders o
JOIN customers c
  ON o.customer_id = c.costumer_id

-- self join
SELECT 
  e.employee_id, 
  e.first_name, 
  m.first_name AS manager
FROM employees e
JOIN employees m
  ON e.employee_id = m.employee_id

-- join multiple tables
SELECT *
  o.order_id, 
  o.order_date, 
  c.first_name, 
  c.last_name, 
  os.name AS status
FROM orders o
JOIN customers c
  ON o.customer_id = c.customer_id
JOIN order_statuses os
  ON o.status = os.order_status_id
```
        
#### 1.7 Group By
- Aggregate Function
available aggregate function : count, avg, min, max, sum, etc
```
SELECT 
AVG(price) AS 'average' 
FROM products; 
```
        
- Group By
```
SELECT 
  category,
  COUNT(id) AS 'Total Product' 
FROM products
GROUP BY category;
```

#### 1.8 Having Clause
Filter a data which meet group by condition
```
SELECT 
    ordernumber,
    SUM(quantityOrdered) AS itemsCount,
    SUM(priceeach*quantityOrdered) AS total
FROM
    orderdetails
GROUP BY 
   ordernumber
HAVING 
   total > 1000;       
```

### 2. Insert

Basic Syntax
```
INSERT INTO <tb_name>
  (field_1, field_2, ...)
VALUES
  (value_1, value_2, ...), 
  (value_1, value_2, ...);
```

Example
```
-- insert a record
INSERT INTO products 
  (id, name, price, quantity) 
VALUES 
  (1, 'Mi 10', 5000000, 100);

-- insert multiple record
INSERT INTO products 
  (id, name, price, quantity) 
VALUES 
  (2, 'HP Pavilion Gaming', 13000000, 50), 
  (3, 'Samsung Smartwatch', 3500000, 75), 
  (4, 'Keyboard Logitech', 350000, 150);
```

### 3. Update

Basic Syntax
```
UPDATE <tb_name>
SET 
  <field> = <new_value>, 
  <field> = <new_value>, 
  ...
WHERE
  <where_condition>
```

Example
```
-- update a column
UPDATE products
SET category = 'Makanan'
WHERE id = 1;

-- update multiple column
UPDATE products
SET category = 'Minuman', 
description ='Mie ayam original + ceker '
WHERE id = 2;

-- update with existing value
UPDATE products
SET price = price + 5000
WHERE id = 1;
```

### 4. Delete

```
DELETE FROM <tb_name>
WHERE
  <where_condition>;
```
> Note : Make sure filter a data that you want to delete. There is no warning on mysql CLI when you delete multiple records.

## D. Data Control Language (Data Control Language) 

DCL includes commands such as GRANT and mostly concerned with rights, permissions and other controls of the database system.

- GRANT - allow users access privileges to the database
- REVOKE - withdraw users access privileges given by using the GRANT command

### 1. Type of Permission

- `ALL PRIVILEGES` - this would allow a MySQL user full access to a designated database (or if no database is selected, global access across the system)
- `CREATE` - allows them to create new tables or databases
- `DROP` - allows them to them to delete tables or databases
- `DELETE` - allows them to delete rows from tables
- `INSERT` - allows them to insert rows into tables
- `SELECT` - allows them to use the SELECT command to read through databases
- `UPDATE` - allow them to update table rows
- `GRANT OPTION` - allows them to grant or remove other users’ privileges
      
      
### 2. Grant
- Basic Syntax
```
-- show grant
SHOW GRANTS FOR '<user>'@'localhost';

-- add grant to user 
GRANT <permission> ON <db_name>.<tb_name> TO '<user>'@'localhost';
```

Example
```
GRANT ALL PRIVILEGES ON schooldb.* TO 'aditya'@'localhost';
```
      
### 3. Revoke
```
REVOKE <permission> ON <db_name>.<tb_name> FROM '<user>'@'localhost';
```
      
## E. Transaction Control Language (TCL) 

TCL deals with a transaction within a database.

- COMMIT - commits a Transaction
- ROLLBACK - rollback a transaction in case of any error occurs
- SAVEPOINT- to rollback the transaction making points within groups
- SET TRANSACTION - specify characteristics of the transactio


## Numeric Function
- Arithmetic Operator
`%` : MOD
`*` : Multiplication
`+` : Addition Operator
`-` : Minus Operator, Change Sign
`/` : Division Operator
`DIV` : integer divison

      > aware of divide a number in mysql, 
```
SELECT 
  id, 
  price DIV 1000 as price_in_k 
FROM 
  products;

SELECT 
  id, name, price
FROM 
  products
WHERE 
  price DIV 1000 > 1000;

```

- Mathematic Operator
`PI()` : Get pi
`POWER(a,n)` : Power a of n
`LOG()` : Log function

```
SELECT 
  id,
  LOG(price) 
FROM 
  PRODUCTS;
```

## String Function
`LOWER()` : Transform a String to Lowercase
`LENGTH()` : Get length of String

```
SELECT 
  id, 
  LOWER(name) as 'Name Lower',
  UPPER(name) as 'Name Upper', 
  LENGTH(name) as 'Name Length'
FROM products;
```

## Datetime Function
`EXTRACT()` : GET Specific Time
```
SELECT 
  id,
  EXTRACT(YEAR FROM created_at) as Year, 
  EXTRACT(MONTH FROM created_at) as Month
FROM products;

```

## Flow Control Function
- Similar with IF ELSE in programming language
- `CASE` : Case Operator
- `IF` : If / else Construct
- `IFNULL()` : Null if / else construct
- `NULLIF()` : Return Null if expre1=expre2


```
SELECT id, 
  category
  CASE category
    WHEN 'Makanan' THEN 'Enak'
    WHEN 'Minuman' THEN 'Segar'
    ELSE 'Apa itu?'
    END AS 'comment'
FROM products;
```


```
SELECT 
  id, 
  price
  IF (price <= 15000, 'Murah', 'Mahal') 
    as comment
FROM products;


SELECT 
  id, 
  price
  IF (price <= 15000, 'Murah', 
    IF (price <= 20000, 'Mahal', 'Mahal Banget')) 
    as comment
FROM products;
```

#### Misc
```SELECT LAST_INSERT_ID();```


#### USER
- Create User
`CREATE USER [IF NOT EXISTS] '<account_name>' IDENTIFIED BY '<password>';`
- Show User
`SELECT USER FROM mysql.user;`
- Add Privileges
`GRANT ALL PRIVILEGES ON <dbname.*> TO '<account_name>';`
- Delete User
`DROP USER '<account_name>';`
