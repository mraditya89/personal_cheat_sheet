###### tags : `tutorial` `sql` `mysql`
# MYSQL Cheat Sheet

## 1. Show, create, use, drop database
```
SHOW DATABASES;
CREATE DATABASE <dbname>;
USE <dbname>;
DROP DATABASE <dbname>;
```
## 2.Tipe Data
### 2.1 number : 
- integer (signed, unsigned) : tinyint, smallint, mediumint, int, bigint
- float (signed, unsigned) : float, double
- decimal : decimal(5,2) => 5 digit, 2 angka di belakang koma,

attribut: 
- type(n) : show n digit
- zerofill : INT(3) zerofill : add zero with total 3 digits: 007
### 2.2 string
- char (static size) : char(10) => char with max 10 characters
- varchar (dynamic size) : varchar(10) => varchar with max 10 characters
- text : tinytext, text, mediumtext, longtext
- enum : string with limited option, ex ("male", "female") 
### 2.3 date time
- date : yyyy-mm-dd
- datetime : yyyy-mm-dd hh-mm-ss
- timestamp : yyyy-mm-dd hh-mm-ss
- time : hh-mm-ss
- year : yyyy
### 2.4 boolean : TRUE or FALSE
### 2.5 lain2
- blob
- spatial
- json
 
## 3. Tables

### 3.1 show tables
```
SHOW TABLES;
```
### 3.2 create table
```
CREATE TABLE barang (
  kode INT NOT NULL,
   nama VARCHAR (100),
   harga INT ,
   jumlah INT, 
   PRIMARY KEY (kode)
) ENGINE = InnoDB;

CREATE TABLE admin (
  id INT NOT NULL AUTO_INCREMENT, 
  username VARCHAR(100), 
  pasword VARCHAR(100), 
  PRIMARY KEY (id)
) ENGINE = InnoDB;
```
### 3.3 See table schema
```
DESCRIBE barang;
```
### 3.4 Alter / modify table
```
ALTER TABLE barang
ADD COLUMN nama_kolom TEXT,
DROP COLUMN nama, 
RENAME COLUMN nama TO nama_baru;

ALTER TABLE barang
MODIFY 
  jumlah INT NOT NULL DEFAULT 0, 
ADD COLUMN 
  waktu_dibuat TIMESTAMP NOT NULL DEFAULT CURRENT_TIMESTAMP;

ALTER TABLE barang
  ADD PRIMARY KEY (kode);

ALTER TABLE barang
# change "nama" type data and put it after jumlah
  MODIFY COLUMN nama VARCHAR(100) AFTER jumlah;

ALTER TABLE products
    ADD COLUMN category ENUM('Electronic', 'House', 'Others')
    AFTER name;
```
### 3.5 Recreate Table
Delete all rows and create a table with same schema
```
TRUNCATE TABLE barang;
```
### f. Delete Table
```
DROP TABLE barang;
```
## 4. Insert Data
```
INSERT INTO products 
  (id, name, price, quantity) 
VALUES 
  (1, 'Mi 10', 5000000, 100);
    
INSERT INTO products 
  (id, name, price, quantity) 
VALUES 
  (2, 'HP Pavilion Gaming', 13000000, 50), 
  (3, 'Samsung Smartwatch', 3500000, 75), 
  (4, 'Keyboard Logitech', 350000, 150);
```
## 5. Select Data
### 5.1 General Query
```
SELECT * 
FROM products;

SELECT 
  id, 
  name, 
  price, 
  quantity 
FROM products;

SELECT id, 
  name as nama, 
  price as harga 
FROM products;
```
### 5.2 Where Clause
Used for filter a query

```
SELECT * 
FROM products 
WHERE quantity=100;

SELECT * 
FROM products 
WHERE price <= 10000000;

SELECT * 
FROM products 
WHERE name = 'Mi 10';
```
> Note : in mysql, default is case insensitive, so when name = 'Mi 10' is equal to name = 'mi 10'  


## 6. Update Data

```
//Update a column
UPDATE products
SET category = 'Makanan'
WHERE id = 1;

//Update multiple column
UPDATE products
SET category = 'Minuman', 
description ='Mie ayam original + ceker '
WHERE id = 2;

// Update with existing value
UPDATE products
SET price = price + 5000
WHERE id = 1;
```
## 7. Delete Data
```
DELETE FROM products
WHERE id = 2;
```
## 8. Alias
```
SELECT 
  id AS 'Kode',
  name AS 'Nama' ,
  category AS 'Kategory'
FROM products;

SELECT 
  p.id AS 'Kode', 
  p.name AS 'Nama', 
  p.category AS 'Category'
FROM products AS p;  
```

## 9.  Where Operator
### 9.1 Comparison Operator


| Column 1 | Column 2 | 
| -------- | -------- | 
| `=`     | Equal to     | 
| `<>` or `!=`     | Not equal to     | 
| <     | Less than     | 
| <=     | Less than or equal to     | 
| >     | Greater than    | 
| >=     | Greater than or equal to     | 

```
SELECT * 
FROM products
WHERE quantity > 100;

SELECT * 
FROM products 
WHERE category != 'Makanan';
```
### 9.2 Logical Operator
```
SELECT * 
FROM products 
WHERE 
category != 'Makanan' AND price <= 20000;

SELECT * 
FROM products
WHERE (category = 'Makanan' OR quantity > 500)
AND price > 100000;
```
### 9.3 Like Operator

| Column 1 | Column 2 |
| -------- | -------- |
| LIKE 'mie%'     | A string begin with 'mie'     |
| LIKE '%mie'     | A string end with 'mie'     |
| LIKE '%mie%'     | A string include 'mie'     |
| NOT LIKE '%mie%'     | A string not include 'mie'     |

```
SELECT *
FROM products
WHERE name LIKE 'mie%'; 
```

### 9.4 NULL Operator
```
SELECT * 
FROM products 
WHERE price IS NULL;
```
### 9.5 BETWEEN Operator
```
SELECT * 
FROM products 
WHERE 
  price BETWEEN 10000 AND 20000;
```
### 9.6 IN Operator
```
SELECT * 
FROM products 
WHERE category IN ('Makanan', 'Minuman');
```

### 9.7 LIMIT Operator
```
# Get 2 data
SELECT * 
FROM products 
LIMIT 2;

# skip 10 data, get 2 data
SELECT * 
FROM products 
LIMIT 10, 2;
```
### 9.8 DISTINT Operator
```
SELECT 
  distinct category 
FROM products;
```

## Numeric Function
- Arithmetic Operator
`%` : MOD
`*` : Multiplication
`+` : Addition Operator
`-` : Minus Operator, Change Sign
`/` : Division Operator
`DIV` : integer divison

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


# USER
- Create User
`CREATE USER [IF NOT EXISTS] '<account_name>' IDENTIFIED BY '<password>';`
- Show User
`SELECT USER FROM mysql.user;`
- Add Privileges
`GRANT ALL PRIVILEGES ON <dbname.*> TO '<account_name>';`
- Delete User
`DROP USER '<account_name>';`

mysql -u root -p <database> < <file_dump.sql>
