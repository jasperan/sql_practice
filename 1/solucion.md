```sql
WITH country_invoice_data AS (
  SELECT 
    c.country_name, 
    COUNT(i.id) AS invoice_count, 
    AVG(i.total_price) AS avg_invoice_amount
  FROM 
    country c
    JOIN city ON c.id = city.country_id
    JOIN customer ON city.id = customer.city_id
    JOIN invoice i ON customer.id = i.customer_id
  GROUP BY 
    c.country_name
), 
global_avg_data AS (
  SELECT AVG(avg_invoice_amount) AS global_avg_invoice_amount
  FROM country_invoice_data
)
SELECT 
  country_name, 
  invoice_count, 
  AVG(avg_invoice_amount) AS avg_invoice_amount
FROM 
  country_invoice_data
  JOIN global_avg_data ON 1=1
WHERE 
  avg_invoice_amount > global_avg_invoice_amount
GROUP BY 
  country_name, 
  invoice_count

```

The query first creates a common table expression (CTE) called country_invoice_data that calculates the country name, invoice count, and average invoice amount. Then, it calculates the global average invoice amount and stores it in another CTE global_avg_data. Finally, the query selects the country name, invoice count, and average invoice amount, and returns only those countries whose average invoice amount is greater than the global average invoice amount.


1. First, we calculate the average of all invoices:

```sql
WITH avg_invoice_amount AS (
    SELECT AVG(total_price) AS avg_invoice_amount
    FROM invoice
)

```

2. Next, we join the `invoice` table with the `customer` table to get the `customer_id` and the `total_price` for each invoice.

```sql
, invoice_customer AS (
    SELECT i.customer_id, i.total_price
    FROM invoice i
    JOIN customer c ON i.customer_id = c.id
)

```

3. We join the previous `invoice_customer` table with the `city` table to get the `country_id` for each invoice.

```sql
, invoice_city AS (
    SELECT ic.customer_id, ic.total_price, ci.country_id
    FROM invoice_customer ic
    JOIN city ci ON ic.customer_id = ci.id
)
```

4. We join the previous `invoice_city` table with the `country` table to get the `country_name` for each invoice.

```sql
SELECT c.country_name, COUNT(*) AS total_invoices, AVG(ic.total_price) AS avg_invoice_amount
FROM country c
JOIN invoice_city ic ON c.id = ic.country_id
GROUP BY c.country_name

```

5. Finally, we filter the result set to show only those countries where their average invoice amount is greater than the average invoice amount over all invoices.

```sql
SELECT *
FROM (
    SELECT c.country_name, COUNT(*) AS total_invoices, AVG(ic.total_price) AS avg_invoice_amount
    FROM country c
    JOIN invoice_city ic ON c.id = ic.country_id
    GROUP BY c.country_name
) subquery
WHERE avg_invoice_amount > (SELECT avg_invoice_amount FROM avg_invoice_amount)

```

The full query is the following:

```sql
WITH avg_invoice_amount AS (
    SELECT AVG(total_price) AS avg_invoice_amount
    FROM invoice
), invoice_customer AS (
    SELECT i.customer_id, i.total_price
    FROM invoice i
    JOIN customer c ON i.customer_id = c.id
), invoice_city AS (
    SELECT ic.customer_id, ic.total_price, ci.country_id
    FROM invoice_customer ic
    JOIN city ci ON ic.customer_id = ci.id
)
SELECT *
FROM (
    SELECT c.country_name, COUNT(*) AS total_invoices, AVG(ic.total_price) AS avg_invoice_amount
    FROM country c
    JOIN invoice_city ic ON c.id = ic.country_id
    GROUP BY c.country_name
) subquery
WHERE avg_invoice_amount > (SELECT avg_invoice_amount FROM avg_invoice_amount)

```