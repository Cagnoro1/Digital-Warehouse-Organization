# Warehouse Digital Organization

## Table of contents
- [Project Overview](#project-overview) 
- [Data Sources](#data-sources)
- [Tools](#tools)
- [Relational Diagram](#relational-diagram)
- [Database](#database)
- [Populated Tables](#populated-tables)
- [Data Analysis](#data-analysis)
- [Limitation](#limitation)
- [Recommendations](#recommendations)
- [References](#references)

### Project Overview 

The project aims to modernize and optimize the operations of Mr. Smith Johnson's medium-sized distributorship, which specializes in selling shoes, footwear, and accessories. Over the past five years, the business has experienced significant growth, resulting in an expanded inventory and customer base. However, the current manual record-keeping system is no longer sufficient to manage the increased workload efficiently. The project will focus on implementing digital solutions to address key business challenges and improve overall efficiency.


### Data Sources
The dataset was created using MySQL.

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



```

### Data Analysis

1) Retrieve all the products that sell quickly!

```SQL

SELECT prod_ID, prod_name, prod_instock, prod_date, prod_sold, prod_QOH, prod_price
FROM Products
WHERE prod_instock = 200 AND prod_QOH <= 5 AND prod_date >= '2022-10-01' AND prod_date <= '2023-01-31';

```

2) Retrieve all the products that sell slowly!

```SQL

SELECT prod_ID, prod_name, prod_instock, prod_date, prod_sold, prod_QOH, prod_price
FROM Products
WHERE prod_instock = 200 AND prod_QOH > 150 AND prod_date >= '2022-10-01' AND prod_date <= '2023-01-31';

```

3) Retrieve all the current customers (from 2020 to 2023) from the Customer table.

```SQL 

SELECT cus_ID, cus_name, cus_Odate
FROM Customers
WHERE YEAR(cus_Odate) BETWEEN 2020 AND 2023;

```

4) Retrieve all the customers whose accounts are overdue together with the respective products they purchased.

 ```SQL

SELECT Customers.cus_ID, Customers.cus_name, Products.prod_name, Accounts.acc_dueD
FROM Accounts
JOIN Customers ON Accounts.cus_ID = Customers.cus_ID
JOIN Products ON Accounts.prod_type = Products.prod_type
WHERE Accounts.acc_dueD < acc_payD;
![image](https://github.com/Cagnoro1/Digital-Warehouse-Organization/assets/135088212/8fe4f712-91f9-43c7-bee0-385346e52256)

```
### Recommendations
1) Inventory Management Optimization: This company needs to prioritize products that sell fast to maximize their revenues. These products are: Converse, Roxy, Nike, Clarks, New Balance, Maidden Girl, Adidas Samba, Nike Air Max, Wide Width Loafers, Wedges Ankle Strap, Adidas Ultraboost, Drawstring Backpack, Silk Scarf, Shoe Polish (black), Leather Cleaner, Shoe Deodorizer, Shoe Laces (flat), Shoe Horn, Loafers Tassel, Nike Air Force 1.
   
2) Implement Promotion: They should implement promotions and discounts for products that sell slowly to clear out their inventories and make room for more profitable items.

3) Customer Retention Strategies: Implementing customer loyalty programs especially for repeating customers. It will encourage them to keep shopping and help them foster long-term relationships with the business.

4)  Account Receivable Management: Develop a system to manage overdue accounts to minimize losses and maintain a good cash flow. Implementing reminders for overdue payments and implementing other flexible methods of payment could be beneficial to customers facing financial difficulties.

5)  Supplier Relationship Enhancement: To negotiate better terms such as volume discounts or extended deadlines, the company has to strengthen its relationship with the Suppliers. That will Improve profitability and reduce costs.

6)  Improve Customer Service: Companies should invest in staff training. This will upskill them in customer service, and help them provide personalized assistance to the customers.
      
7)  Increase Online presence: Online presence is very important for businesses nowadays. 
the business should optimize its social media engagement, online advertisement, and website to enhance that. This will reach a wider audience and attract new customers.

9) Regular Performance Monitoring: Monitor key performance indicators (KPIs) such as customer satisfaction scores, sales revenue, inventory turnover, and accounts receivable aging. This will help in identifying areas for improvement and taking proactive measures to address any issues.

10) Adaptation to Changing Market Conditions: Stay adaptable to changing market conditions by regularly reviewing and adjusting business strategies.



