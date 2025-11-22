# Sales Analytics
Dataset: Private license

<br>

## Analysis
Examines sales data from a database, calculating totals, identifying product trends, and analyzing customer behaviors across specific periods and locations, focusing on metrics like order counts, revenue generation, and product popularity.

<br>

### How many orders were placed in January?
```sql
SELECT 
    COUNT(orderid) AS total_january_sales
FROM BIT_DB.JanSales
WHERE length(orderid) = 6
    AND orderid <> 'Order ID';
```
<details>
  <summary><i>Show result</i></summary>
    
| total_january_sales |
|----------------|
| 9681           |
</details>

<br>

### How many of those orders were for an iPhone?
```sql
SELECT 
    COUNT(orderid) AS total_january_iphone_sales
FROM BIT_DB.JanSales
WHERE Product='iPhone'
    AND length(orderid) = 6
    AND orderid <> 'Order ID';
```
<details>
  <summary><i>Show result</i></summary>

| total_january_iphone_sales |
|----------------|
| 379            |
</details>

<br>

### Select the customer account numbers for all the orders that were placed in February. 
```sql
SELECT DISTINCT 
    acctnum
FROM BIT_DB.customers cust
INNER JOIN BIT_DB.FebSales Feb
    ON cust.order_id=FEB.orderid
WHERE length(orderid) = 6
    AND orderid <> 'Order ID';
```
<details>
  <summary><i>Show result</i></summary>
    
| acctnum   |
|:---------:|
| 40161414  |
| 54428584  |
| 59221952  |
| 88742323  |
| 78191203  |
| 74990905  |
| 52970206  |
| 30785465  |
| 53139396  |
| 28100900  |
|   ...     |
</details>

<br>

### Which product was the cheapest one sold in January, and what was the price?
```sql
SELECT DISTINCT 
    product, 
    price
FROM BIT_DB.JanSales
ORDER BY price ASC 
LIMIT 1;
```
<details>
  <summary><i>Show result</i></summary>
    
| product                | price |
|------------------------|-------|
| AAA Batteries (4-pack) | 2.99  |
</details>

<br>

### What is the total revenue for each product sold in January?
```sql
SELECT 
    product,
    SUM(quantity) * price as revenue
FROM BIT_DB.JanSales
GROUP BY product;
```
<details>
  <summary><i>Show result</i></summary>
    
| product                   | revenue            |
|---------------------------|--------------------|
|                           | 0                  |
| 20in Monitor              | 23647.85           |
| 27in 4K Gaming Monitor    | 121676.88          |
| 27in FHD Monitor          | 62845.81           |
| 34in Ultrawide Monitor    | 119316.86          |
| AA Batteries (4-pack)     | 5472               |
| AAA Batteries (4-pack)    | 4772.04            |
| Apple Airpods Headphones  | 122100             |
| Bose SoundSport Headphones| 65893.41           |
| Flatscreen TV             | 72900              |
| Google Phone              | 190800             |
| LG Dryer                  | 23400              |
| LG Washing Machine        | 25200              |
| Lightning Charging Cable  | 17207.45           |
| Macbook Pro Laptop        | 399500             |
| Product                   | 0                  |
| ThinkPad Laptop           | 216997.83          |
| USB-C Charging Cable      | 15343.8            |
| Vareebadd Phone           | 50000              |
| Wired Headphones          | 12961.19           |
| iPhone                    | 265300             |
</details>

<br>

### Which products were sold in February at 548 Lincoln St, Seattle, WA 98101, how many of each were sold, and what was the total revenue?
```sql
SELECT
    product,
    SUM(quantity) total_quantity,
    SUM(quantity)*price as revenue
FROM BIT_DB.FebSales
WHERE location = '548 Lincoln St, Seattle, WA 98101'
GROUP BY product;
```
<details>
  <summary><i>Show result</i></summary>
    
| product                | total_quantity | revenue |
|------------------------|----------------|---------|
| AA Batteries (4-pack)  | 2              | 7.68    |
</details>

<br>

### How many customers ordered more than 2 products at a time, and what was the average amount spent for those customers? 
```sql
SELECT
    COUNT(DISTINCT cust.acctnum) AS acctnum,
    avg(quantity*price) AS avg_amount_spent
FROM BIT_DB.FebSales Feb
LEFT JOIN BIT_DB.customers cust
    ON FEB.orderid=cust.order_id
WHERE Feb.Quantity>2
    AND length(orderid) = 6
    AND orderid <> 'Order ID';
```
<details>
  <summary><i>Show result</i></summary>
    
| acctnum | avg_amount_spent       |
|---------|------------------------|
| 278     | 13.82794964028773      |
</details>

<br>

### List all the products sold in Los Angeles in February, and include how many of each were sold.
```sql
SELECT 
    Product, 
    SUM(quantity) total_february_sales
FROM BIT_DB.FebSales
WHERE location like '%Los Angeles%'
GROUP BY Product;
```
<details>
  <summary><i>Show result</i></summary>
    
| Product                    | total_february_sales |
|----------------------------|----------------------|
| 20in Monitor               | 44                   |
| 27in 4K Gaming Monitor     | 70                   |
| 27in FHD Monitor           | 81                   |
| 34in Ultrawide Monitor     | 63                   |
| AA Batteries (4-pack)      | 293                  |
| AAA Batteries (4-pack)     | 351                  |
| Apple Airpods Headphones   | 140                  |
| Bose SoundSport Headphones | 131                  |
| Flatscreen TV              | 36                   |
| Google Phone               | 52                   |
| LG Dryer                   | 5                    |
| LG Washing Machine         | 6                    |
| Lightning Charging Cable   | 243                  |
| Macbook Pro Laptop         | 46                   |
| ThinkPad Laptop            | 42                   |
| USB-C Charging Cable       | 271                  |
| Vareebadd Phone            | 25                   |
| Wired Headphones           | 191                  |
| iPhone                     | 71                   |
</details>

<br>

### Which locations in New York received at least 3 orders in January, and how many orders did they each receive?
```sql
SELECT 
    DISTINCT location,
    COUNT(orderID) AS total_january_orders
FROM BIT_DB.JanSales
WHERE location like '%NY%'
    AND orderID <> ''
    AND LENGTH(orderID) = 6
GROUP BY location
HAVING COUNT(orderID) > 2;
```
<details>
  <summary><i>Show result</i></summary>
    
| location                               | total_january_orders |
|----------------------------------------|----------------------|
| 148 Elm St, New York City, NY 10001    | 3                    |
| 515 Lincoln St, New York City, NY 10001| 3                    |
| 916 Pine St, New York City, NY 10001   | 3                    |
| 961 Jefferson St, New York City, NY 10001 | 4                  |
</details>

<br>

### How many of each type of headphone was sold in February?
```sql
SELECT
    Product,
    SUM(Quantity) quantity
FROM BIT_DB.FebSales
WHERE Product like '%Headphones%'
GROUP BY Product;
```
<details>
  <summary><i>Show result</i></summary>
    
| Product                    | quantity |
|----------------------------|----------|
| Apple Airpods Headphones   | 1013     |
| Bose SoundSport Headphones | 844      |
| Wired Headphones           | 1282     |
</details>

<br>

### What was the average amount spent per account in February?
```sql
SELECT 
    AVG(Quantity * price) AS avg_spent_per_account
FROM BIT_DB.FebSales Feb
LEFT JOIN BIT_DB.customers cust
ON FEB.orderid = cust.order_id
WHERE LENGTH(orderid) = 6 
    AND orderid <> 'Order ID';
```
<details>
  <summary><i>Show result</i></summary>
    
| avg_spent_per_account |
|-----------------------|
| 190.00034676304287    |
</details>

<br>

### What was the average quantity of products purchased per account in February?
```sql
SELECT 
    SUM(Quantity) / COUNT(cust.acctnum) AS avg_quantity_items_purchased
FROM BIT_DB.FebSales Feb
LEFT JOIN BIT_DB.customers cust
ON FEB.orderid = cust.order_id
WHERE LENGTH(orderid) = 6 
    AND orderid <> 'Order ID';
```
<details>
  <summary><i>Show result</i></summary>
    
| avg_quantity_items_purchased |
|----------------------------|
| 1                          |
</details>

<br>

### Which product brought in the most revenue in January and how much revenue did it bring in total?
```sql
SELECT
    Product,
    SUM(Quantity * price) revenue
FROM BIT_DB.JanSales
WHERE LENGTH(orderid) = 6 
    AND orderid <> 'Order ID'
GROUP BY Product
ORDER BY revenue DESC
LIMIT 1
```
<details>
  <summary><i>Show result</i></summary>
    
| Product            | revenue |
|--------------------|---------|
| Macbook Pro Laptop | 399500  |
</details>

<br>
