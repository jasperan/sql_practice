```sql
SELECT c.city_name, p.product_name, SUM(ii.line_total_price) as total_amount
FROM city c
JOIN customer cu ON c.id = cu.city_id
JOIN invoice i ON cu.id = i.customer_id
JOIN invoice_item ii ON i.id = ii.invoice_id
JOIN product p ON ii.product_id = p.id
GROUP BY c.city_name, p.product_name
ORDER BY total_amount DESC, c.city_name, p.product_name
```

- We start by joining the city table with the customer table on the `city_id` column in the `customer` table.
- Then, we join the result of the first join with the invoice table on the `customer_id` column in the `invoice` table.
- Next, we join the result of the second join with the invoice_item table on the `invoice_id` column in the `invoice_item` table.
- Finally, we join the result of the third join with the product table on the `product_id` column in the `invoice_item` table.
- We use the _GROUP BY_ clause to group the result by the `city_name` and `product_name` columns.
- We use the _SUM_ function to calculate the total amount spent on each `product` for each `city`.
- The result is ordered by the `total_amount` in *descending* order, and then by the `city_name` and `product_name` in **ascending** order.