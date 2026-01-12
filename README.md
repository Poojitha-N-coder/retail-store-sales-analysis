# retail-store-sales-analysis
sql projest analyzing  retail store data 


create database retailstore_sales;

use retailstore_sales;

create table sales
(order_id int auto_increment not null primary key,
order_date int not null,
product_name varchar(78) unique,
category varchar(90) not null,
quantity int not null,
price int not null,
revenue int not null,
country varchar(99) not null)
auto_increment=100;


select * from sales;

alter table sales 
modify order_date date;




INSERT INTO sales (order_date, product_name, category, quantity, price, revenue, country) VALUES
('2024-01-05', 'Laptop', 'Electronics', 1, 800, 800, 'India'),
('2024-01-06', 'Mobile Phone', 'Electronics', 2, 500, 1000, 'India'),
('2024-01-07', 'Headphones', 'Accessories', 3, 50, 150, 'UK'),
('2024-01-08', 'Office Chair', 'Furniture', 1, 200, 200, 'UK'),
('2024-01-09', 'Notebook', 'Stationery', 10, 5, 50, 'India'),
('2024-01-10', 'Tablet', 'Electronics', 1, 600, 600, 'USA'),
('2024-01-11', 'Desk Lamp', 'Furniture', 2, 40, 80, 'USA'),
('2024-01-12', 'Mouse', 'Accessories', 4, 25, 100, 'India'),
('2024-01-13', 'Printer', 'Electronics', 1, 300, 300, 'UK'),
('2024-01-14', 'Backpack', 'Accessories', 2, 60, 120, 'USA');



-- total_revenue of the store
select sum(revenue) as total_revenue
from sales;

-- revenue by product
select product_name, sum(revenue) as total_revenue
from sales
group by product_name
order by product_name asc;


-- revenue by category
select category, sum(revenue)as total_revenue
from sales
group by category
order by category desc;

-- revenue per day
select order_date, sum(revenue)as revenue_perday
from sales 
group by order_date
order by order_date asc;

-- where clause 
select *
from sales
where product_name='laptop';

-- revenue by country
select country, sum(revenue) as total_revenue
from sales
group by country
order by country desc;

-- avarage revenue 
select avg(revenue)as avarage_revenue
from sales; 

-- revenue greater than 500
select order_id,product_name, revenue 
from sales
where revenue > 500;

-- electornic catogiry revenue
select category,sum(revenue) as eloctronics_revenue
from sales
where category='electronics'
group by category;

select category from sales
group by category;

-- furniture revenue
select category, sum(revenue) as furniture_revenue
from sales
where category='furniture'
group by category;

-- accessories revenue
select category, sum(revenue) as accessories_revenue
from sales 
where category='accessories'
group by category;

-- stationery revenue 
select category, sum(revenue)as stationery_revenue
from sales 
where category='stationery'
group by category;

-- orders in usa
select * from sales 
where country='usa';

-- orders in india 
select * from sales 
where country='india';

-- orders in uk
select* from sales 
where country='uk';


-- country wise orders
select country, count(quantity) as country_products
from sales 
group by country 
order by country desc;
