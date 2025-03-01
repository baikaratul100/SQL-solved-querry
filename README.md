# SQL-solved-querry

CREATE DATABASE practis;

USE practiS;

SELECT * FROM car_dataset;

-- Retrieve all columns for cars manufactured in the year 2020.
select * 
from car_dataset
where year = 2020;

-- Find the average price of all cars in the dataset.
select round(avg(price),0) as avg_price
from car_dataset;

-- List all unique car brands in the dataset.
select  distinct brand
from car_dataset;

-- Find the total number of cars that use Diesel as their fuel type.
SELECT brand, count(brand) 
FROM car_dataset
where fuel_type = "diesel"
group by brand;


 -- Retrieve the details of the car with the highest mileage.
SELECT *
FROM car_dataset
order by mileage desc
limit 1;

-- Find the average price of cars for each brand
select brand, round(avg(price),0) as avg_price
from car_dataset
group by brand;

-- List the top 5 most expensive cars in the dataset.
select brand
from car_dataset
order by price desc
limit 5;

-- Find the number of cars for each transmission type
select transmission, count(transmission) as total_cars
from car_dataset
group by transmission ;

-- Retrieve the details of cars that have more than 3 owners
select * 
from car_dataset
where owner_count >3;


-- Find the average mileage of cars for each fuel type.
select fuel_type, avg(mileage)
from car_dataset
group by fuel_type;


-- Find the brand and model of the car with the lowest price.
select brand, model
from car_dataset
order by price asc
limit 1;

-- List the cars that have a price above the average price of all cars.
select avg(price)
from car_dataset;

select *
from car_dataset
where price > (select avg(price)
from car_dataset);

-- Find the total number of cars for each year, sorted by year in descending order.
select year, count(brand) as no_of_cars
from car_dataset
group by year
order by year desc;

-- Retrieve the details of cars that have an engine size greater than 3.0 and are automatic.
select *
from car_dataset
where engine_size > 3.0 and transmission = "automatic";


-- Find the average price of cars for each year, but only for cars that have less than 50,000 mileage.
select year, round(avg(price),0)
from car_dataset
where mileage < 50000
group by year;

-- Find the brand and model of the car with the highest price for each year.

select year, brand, model, price
from car_dataset
where (year, price) in 
		(select year, max(price) 
		from car_dataset
		group by year ) ;


-- List the top 3 brands with the highest average price.
select brand, avg(price) as AVG_PRICE
from car_dataset
group by brand
order by AVG_PRICE desc
limit 3;


--  Find the brand and model of the car with the highest mileage for each fuel type.

select fuel_type, max(mileage)
from car_dataset
group by fuel_type;

select fuel_type, brand, model, mileage 
from car_dataset
where (fuel_type, mileage) in 
		(select fuel_type, max(mileage)
		from car_dataset
		group by fuel_type);
        

SET SESSION wait_timeout = 600;
SET SESSION interactive_timeout = 600;

-- Retrieve the details of cars that have a price within the top 10% of all car prices.
-- Confusion but trying to understand the logic

-- Find the average price of cars for each brand, but only include brands that have more than 10 cars in the dataset.		
select brand, avg(price) as AVGPRICE
from car_dataset
group by brand  
having count(*)>10;
