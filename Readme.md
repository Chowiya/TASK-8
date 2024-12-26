# SQL TASK

## CREATE A DATABASE AND TABLE TO MANAGE A SIMPLE E-COMMERCE SYSTEM.


### REQUIREMENTS:


# 1.) Create a database named ecommerce.
 
SQL CODE:

```sql
create database ecommerce;
use ecommerce;
```


# 2.)Create three tables: Customers, orders and product.

## --> Creating customers table:

SQL CODE:

```sql
create table customers (
id int auto_increment primary key,
name varchar(100),
email varchar(100),
address text
);
```

PREVIEW OF CUSTOMERS TABLE
-------------------------------------
| **Column**    | **Type**        | **Description**                      |
|---------------|-----------------|--------------------------------------|
| id            | INT(Primary Key)| customer's id
| name          | VARCHAR(255)    | Customer's name                      |
| email         | VARCHAR(255)    | Customer's email address             |
| address       | TEXT            | Customer's address                   |

-----------------------------------------------------------------
## --> Creating order table:

SQL CODE:

```sql
CREATE TABLE orders (
    id INT AUTO_INCREMENT PRIMARY KEY,
    customer_id INT,
    order_date DATE,
    total_amount DECIMAL(10, 2),
    FOREIGN KEY (customer_id) REFERENCES customers(id)
);
```

PREVIEW OF ORDERS TABLE
--------------------------------------------------------------

 **orders Table**
| **Column**    | **Type**        | **Description**                      |
|---------------|-----------------|--------------------------------------|
| id            | INT(Primary Key)| order id                             |
| customer_id   | INT(Foreign Key)| Customer who placed the order        |
| order_date    | DATE            | Date the order was placed            |
| total_amount  | DECIMAL(10, 2)  | Total amount of the order            |

------------------------------------------------------

## --> Creating products table:

SQL CODE:

```sql
create table products(
    id int auto_increment primary key,
    name varchar(100) not null,
    price decimal(10,2) not null,
    description text
);
```

PREVIEW OF PRODUCTS TABLE
--------------------------------------------
| **Column**    | **Type**        | **Description**                      |
|---------------|-----------------|--------------------------------------|
| id            | INT(Primary Key)|products id                           |
| name          | VARCHAR(255)    | Product's name                       |
| price         | DECIMAL(10, 2)  | Product's price                      |
| description   | TEXT            | Product's description                |
----------------------------------------------

# 3.) insert some sample data into the table.

-- Sample data into customers table:

SQL CODE:

```sql
insert into customers (name,email,address)
values('Surya','surya@gmail.com','no:3 anna nagar'),
     ('Vijay','vijay@gmail.com','no:8 jothi nagar'),
     ('Arjun','aa@gmail.com','no:1 ganesh nagar');
```

```sql
select * from customers;
```

This is the output of the above sql code.

![image alt](https://github.com/Chowiya/TASK-8/blob/2f82d18e7e44b1b659264d8a9f6dd570c3752b0f/Screenshot%202024-12-24%20114233.png)


-- Sample data into orders table:

SQL CODE:

```sql
insert into orders(customer_id,order_date,total_amount)
values (1,curdate(),50.00),
       (2,curdate() - interval 10 day ,75.00),
       (3,curdate() - interval 40 day ,30.00);
```


```sql
select * from orders;
```

This is the output of the above sql code.

![image alt](https://github.com/Chowiya/TASK-8/blob/2f82d18e7e44b1b659264d8a9f6dd570c3752b0f/Screenshot%202024-12-24%20114504.png)


-- Sample data into products table:

SQL CODE:

```sql
insert into products (name,price,description)
values('Product A',30.00,'discription of product A'),
      ('Product B',40.00,'discription of product B'),
      ('Product C',25.00,'discription of product C');
```

```sql
select * from products;
```

This is the output of the above sql code:

![image alt](https://github.com/Chowiya/TASK-8/blob/2f82d18e7e44b1b659264d8a9f6dd570c3752b0f/Screenshot%202024-12-24%20134255.png)

# QUERIES:

### (1) Retrieve all customers who have placed an order in the last 30 days.

SQL CODE:

```SQL
select distinct c.*
from customers c
join orders o on c.id = o.customer_id
where o.order_date >= curdate() - interval 30 day;
```

### (2) Get the total amount of all orders placed by each customer.

SQL CODE:

```sql
select c.name, SUM(o.total_amount) as total_spent
from customers c
join orders o on c.id = o.customer_id
group by c.id;
```

### (3) Update the price of Product C to 45.00.

SQL CODE:
```sql
update products 
set price = 45.00
where name = products
```

### (4) Add a new column discount to the products table.
 
 SQL CODE:

 ```sql
 alter table products
 add column discount decimal(5,2) default 0.00;
 ```

### (5) Retrieve the top 3 products with the highest price.

SQL CODE:

```sql
select * products 
order by price desc
limit 3;
```

### (6) Get the names of customers who have ordered Product A.

SQL CODE:

```sql
select distinct c.name
from customers c
join orders o on c.id = o.customer_id
join order_items oi on o.id = oi.order_id
join products p on oi.product_id = p.id
where p.name = 'Product A';
```
### (7) Join the orders and customers tables to retrieve the customer's name and order date for each order.

SQL CODE:

```sql
select c.name, o.order_date
from orders o
join customers c on o.customer_id = c.id;
```
### (8) Retrieve the orders with a total amount greater than 150.00

SQL CODE:
```sql
select * from orders
where total_amount > 150.00;
```

### (9) Normalize the database by creating a separate table for order items and updating the orders table to reference the order_items table.

SQL CODE:

```SQL
create table order_items (
    id int auto_increment primary key,
    order_id int,
    product_id int,
    quantity int default 1,
    Foreign key  (order_id) references orders(id),
    Foreign key (product_id) references products(id));
```
### (10)Retrieve the average total of all orders.

SQL CODE:

```SQL
select AVG(total_amount) as average_order_total
FROM orders;
```




