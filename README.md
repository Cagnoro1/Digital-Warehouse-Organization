# Digital-Warehouse-Organization

## Table of contents
- [Project Overview](#project-overview) 
- [Data Sources](#data-sources)
- [Tools](#tools)
- [Relational Diagram](#relational-diagram)
- [Database](#database)
- [Exploratory Data Analysis](#exploratory-data-analysis)
- [Data Analysis](#data-analysis)
- [Limitation](#limitation)
- [References](#references)

### Project Overview 

The project aims to modernize and optimize the operations of Mr. Smith Johnson's medium-sized distributorship, which specializes in selling shoes, footwear, and accessories. Over the past five years, the business has experienced significant growth, resulting in an expanded inventory and customer base. However, the current manual record-keeping system is no longer sufficient to manage the increased workload efficiently. The project will focus on implementing digital solutions to address key business challenges and improve overall efficiency.


### Data Sources
Dataset was created using MySQL.

### Tools
- Microsoft Excel - Data cleaning, Data Analysis
- MySQL  - Data Analysis

### Relational Diagram

![Relational Diagram ](https://github.com/Cagnoro1/Digital-Warehouse-Organization/assets/135088212/7c7e76eb-2e55-40f9-9fc9-2d578b9d194f)

### Database

```SQL

CREATE TABLE Customers
( 
  cus_ID INT AUTO_INCREMENT NOT NULL,
  cus_name VARCHAR(50) NOT NULL,
  cus_Addr VARCHAR(50) NOT NULL,
  cus_city VARCHAR(50) NOT NULL,
  cus_st VARCHAR(50) NOT NULL,
  cus_zip VARCHAR(50) NOT NULL,
  cus_Odate DATE NOT NULL,
  cus_Balance decimal(15,2) NOT NULL,
  PRIMARY KEY (cus_ID)
);

CREATE TABLE Warehouse
(
  WH_ID INT NOT NULL,
  WH_name VARCHAR(50) NOT NULL,
  WH_Addr VARCHAR(50) NOT NULL,
  WH_city VARCHAR(50) NOT NULL,
  WH_st VARCHAR(50) NOT NULL,
  WH_zip VARCHAR(50) NOT NULL,
  PRIMARY KEY (WH_ID)
);

CREATE TABLE Accounts
(
  acc_ID INT AUTO_INCREMENT NOT NULL,
  acc_dueD DATE NOT NULL,
  acc_payD DATE NOT NULL,
  cus_ID INT NOT NULL,
  sup_ID INT NOT NULL,
  prod_type VARCHAR NOT NULL,
  PRIMARY KEY (acc_ID),
  FOREIGN KEY (cus_ID) REFERENCES Customers(cus_ID),
  FOREIGN KEY (sup_ID) REFERENCES Suppliers(sup_ID),
  FOREIGN KEY (prod_type) REFERENCES Products(prod_type)
);


CREATE TABLE Products
(
  prod_ID INT AUTO_INCREMENT NOT NULL,
  prod_name VARCHAR(50) NOT NULL,
  prod_type VARCHAR(50) NOT NULL,
  prod_price decimal(15,2) NOT NULL,
  prod_instock INT NOT NULL,
  prod_sold INT NOT NULL,
  prod_QOH VARCHAR(50) NOT NULL,
  prod_date DATE NOT NULL,
  WH_ID INT,
  PRIMARY KEY (prod_ID),
  FOREIGN KEY (WH_ID) REFERENCES Warehouse(WH_ID)
);


CREATE TABLE Suppliers
 (sup_ID INT NOT NULL, 
  sup_dueD DATE NOT NULL,
  sup_payD DATE NOT NULL, 
  WH_ID INT NOT NULL, 
  PRIMARY KEY (sup_ID),
  FOREIGN KEY (WH_ID) REFERENCES Warehouse(WH_ID);


CREATE TABLE Pro_Sys 
(proS_ID INT NOT NULL,
 prod_ID INT NOT NULL,
 prod_name VARCHAR(50) NOT NULL,
 cus_ID INT NOT NULL,
 WH_ID INT NOT NULL,
 sup_ID INT NOT NULL,
 acc_ID INT NOT NULL,
 PRIMARY KEY (proS_ID),
 FOREIGN KEY (prod_ID) REFERENCES Products(prod_ID),
 FOREIGN KEY (cus_ID) REFERENCES Customers(cus_ID),
 FOREIGN KEY (WH_ID) REFERENCES Warehouse(WH_ID),
 FOREIGN KEY (acc_ID) REFERENCES Accounts(acc_ID),
 FOREIGN KEY (sup_ID) REFERENCES Suppliers(sup_ID)
);

![image](https://github.com/Cagnoro1/Digital-Warehouse-Organization/assets/135088212/d4a317a1-0fcf-4a41-9958-eac75546679d)


```


