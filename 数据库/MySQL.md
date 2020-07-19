---
typora-root-url: ./
typora-copy-images-to: figure
---

# 华为云RDS for MySQL

DAS  数据管理服务

### 1.表和索引

- 库
- 表

![image-20200717104407325](figure/image-20200717104407325.png)

![image-20200717104647856](/figure/image-20200717104647856.png)

![image-20200717104724556](/figure/image-20200717104724556.png)

![image-20200717104805903](/figure/image-20200717104805903.png)

![image-20200717104900387](/figure/image-20200717104900387.png)

![image-20200717104937030](/figure/image-20200717104937030.png)

![image-20200717105103880](/figure/image-20200717105103880.png)

- 索引

  ![image-20200717105128021](/figure/image-20200717105128021.png)

![image-20200717105215820](/figure/image-20200717105215820.png)

![image-20200717105304519](/figure/image-20200717105304519.png)

![image-20200717105341723](/figure/image-20200717105341723.png)

![image-20200717105404035](/figure/image-20200717105404035.png)

![image-20200717105422293](/figure/image-20200717105422293.png)

![image-20200717105519229](/figure/image-20200717105519229.png)

如果需要其它字段，则需要回表查询

![image-20200717105555547](/figure/image-20200717105555547.png)

![image-20200717105639195](/figure/image-20200717105639195.png)

![image-20200717105802665](/figure/image-20200717105802665.png)

![image-20200717105828418](/figure/image-20200717105828418.png)

![image-20200717105919412](/figure/image-20200717105919412.png)

![image-20200717110023852](/figure/image-20200717110023852.png)

```
SHOW DATABASES;

CREATE DATABASE library;

SHOW DATABASES;

USE library;

SHOW TABLES;

CREATE TABLE authors (

  first_name VARCHAR(20) CHARACTER SET utf8mb4,

  last_name VARCHAR(20) CHARACTER SET utf8mb4,

  gender ENUM('Male', 'Female'),

  age TINYINT UNSIGNED DEFAULT 0,

  address VARCHAR(512),

  phone_number VARCHAR(20),

  PRIMARY KEY(first_name, last_name),

  UNIQUE KEY(phone_number),

  KEY(address))

ENGINE=INNODB ROW_FORMAT=DYNAMIC

CHARACTER SET=utf8mb4;

SHOW TABLES;

SHOW CREATE TABLE authors;
```

### 2.DDL和DML

![image-20200717113706302](/figure/image-20200717113706302.png)

![image-20200717113731739](/figure/image-20200717113731739.png)

表是位于数据库下的元素

![image-20200717113758499](/figure/image-20200717113758499.png)

![image-20200717113816531](/figure/image-20200717113816531.png)

![image-20200717113844070](/figure/image-20200717113844070.png)

![image-20200717113932136](/figure/image-20200717113932136.png)

![image-20200717113959313](/figure/image-20200717113959313.png)

![image-20200717114024469](/figure/image-20200717114024469.png)

![image-20200717114057039](/figure/image-20200717114057039.png)

![image-20200717114129794](/figure/image-20200717114129794.png)

![image-20200717114141940](/figure/image-20200717114141940.png)

![image-20200717114219771](/figure/image-20200717114219771.png)

![image-20200717114235960](/figure/image-20200717114235960.png)

![image-20200717114310190](/figure/image-20200717114310190.png)

![image-20200717114322164](/figure/image-20200717114322164.png)

![image-20200717114332159](/figure/image-20200717114332159.png)

- DML

  ![image-20200717114406865](/figure/image-20200717114406865.png)

![image-20200717114420415](/figure/image-20200717114420415.png)

![image-20200717114442860](/figure/image-20200717114442860.png)

![image-20200717114507925](/figure/image-20200717114507925.png)

![image-20200717114540082](/figure/image-20200717114540082.png)

![image-20200717114604992](/figure/image-20200717114604992.png)

![image-20200717114643865](/figure/image-20200717114643865.png)

![image-20200717114710736](/figure/image-20200717114710736.png)

