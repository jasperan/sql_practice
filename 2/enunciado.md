# Problema 2

For each pair of city and product, return the names of the city and product, as well the total amount spent on the product to 2 decimal places. Order the result by the amount spent from hight to low then city name and product name in ascending order.

There are 5 tables: customer, city, invoice, invoice_item, product.

## City
| NAME | TYPE | DESCRIPTION |
|------|------|-------------|
| id | int | This is a primary key |
| city_name | varchar(128) | Name of the city |
| postal_code | varchar(16) | Postal code of the city |
| country_id | int | Unique id representing different countries |

## Customer
| NAME | TYPE | DESCRIPTION |
|------|------|-------------|
| id | int | This is a primary key |
| customer_name | varchar(255) | Customer name |
| city_id | int | Foreign key referencing city_id |
| customer_address | varchar(255) | Address |
| contact_person | varchar(255) | Can be NULL |
| email | varchar(128) | Email |
| phone | varchar(128) | Phone number |
| is_active | int | Boolean |

## Invoice
| NAME | TYPE | DESCRIPTION |
|------|------|-------------|
| id | int | This is a primary key |
| invoice_number | Varchar (255) | Invoice number |
| customer_id | int | Foreign key referencing customer_id |
| user_account_id | int | User account id |
| total_price | Decimal (8,2) | Total price |

## Invoice Item
| NAME | TYPE | DESCRIPTION |
|------|------|-------------|
| id | int | This is a primary key |
| invoice_id | int | Foreign key referencing invoice_id |
| product_id | int | Foreign key referencing product_id |
| quantity | decimal (8,2) | Quantity |
| price | decimal (8,2) | Price |
| line_total_price | decimal (8,2) | Line total price |

## Product
| NAME | TYPE | DESCRIPTION |
|------|------|-------------|
| id | int | This is a primary key |
| sku | varchar(32) | SKU |
| product_name | varchar(128) | Name |
| product_description | varchar(255) | Description of the product |
| current_price | decimal (8,2) | Current price |
| quantity_in_stock | decimal (8,2) | Quantity |
| is_active | int | Boolean |


# **Sample Data Tables**


## city
| id | city_name | postal_code | country_id |
|----|-----------|-------------|-----------|
| 1  | Wien      | 1010        | 1         |
| 2  | Berlin    | 10115       | 2         |
| 3  | Hamburg   | 20095       | 2         |
| 4  | London    | EC4V 4AD    | 3         |

## customer
| id | customer_name  | city_id | customer_address  | contact_person | email                       |
|----|----------------|---------|------------------|---------------|----------------------------|
| 1  | Drogerie Wien  | 1       | Deckergasse 15A  | Emil Steinbach| ----@---.com                |
| 2  | Cosmetics Store| 4       | Watling Street 147| Jeremy Cobyn  | ----@---.com                |
| 3  | Kosmetikstudio | 3       | Rothenbaum 53     | Willy Brandit | ----@---.com                |
| 4  | Neue Kosmetik | 1       | KarlsPlatz 27    | NULL         | ----@---.com                |
| 5  | Bio Kosmetik   | 2       | Motzstrasse 42   | Clara Zetkin | ----@---.com                |
| 6  | K-Wien         | 1       | Kartnerstrasse 165| Maria Rauch  | ----@---.com                |
| 7  | Natural Cosmetics| 4       | Clerkenwell 89   | Glenda Jackson | ----@---.com            |
| 8  | Kosmetik PLus  | 2       | Unter den Linden 1| Angela Merkel | ----@---.com                |
| 9  | New Line Cosmetics| 4       | Devonshire 45  | Oliver Crowel | ----@---.com                |

## invoice
| id | invoice_number                | customer_id | user_account_id | total_price |
|----|--------------------------------|-------------|----------------|------------|
| 1  | in_25181b07ba800c8d2fc967fe991807d9 | 7         | 4             | 1436      |
| 2  | 8fba0000fd456b27502b9f81e9d52481   | 9         | 2             | 1000      |
| 3  | 9lkij0000fd64ñkji22b9f81e9d58765   | 3         | 2             | 360       |
| 4  | 5jgnh890887la01254987lñj98khu481   | 5         | 2             | 1675      |
| 5  | 84hfjg768fhj2785fjdncb7v8d524uj   | 6         | 2             | 9500      |
| 6  | 12fdbc6584hgnb2968hjkvntu98d52481 | 4         | 2             | 150       |



## invoice_item
| id	| invoice_id	| product_id	| quantity	| price	| line_total_price| 
|----|--------------------------------|-------------|----------------|------------|----------------|
| 1	| 1	| 1	| 20	| 65	| 1300 | 
| 2	| 1	| 7	| 2	| 68	| 136 | 
| 3	| 1	| 5	| 10	| 100| 	1000 | 
| 4	| 3	| 10	| 2	| 180	| 360 | 
| 5	| 4	| 1	| 5	| 65| 	325 | 
| 6	| 4	| 2	| 10	| 95	| 950 | 
| 7	| 4	| 5	| 4	| 100	| 400 | 
| 8	| 5	| 10	| 100	| 95	| 9500 | 
| 9	| 6	| 4	| 6	| 25	| 150 | 

## product
Id	| Sku	| product_name	 | product_description | 
|----|--------------------------------|----------------|------------|
|  1	|  330120	|  Name 1	|  Description 1 | 
|  2	|  330121	|  Name 2	|  Description 2 | 
|  3	|  330122	|  Name 3	|  Description 3 | 
|  4	|  330123	|  Name 4	|  Description 4 | 
|  5	|  330124	|  Name 5	|  Description 5 | 
|  6	|  330125	|  Name 6	|  Description 6 | 
|  7	|  330126	|  Name 7	|  Description 7 | 
|  8	|  330127	|  Name 8	|  Description 8 | 
|  9	|  330128	|  Name 9	|  Description 9  | 
|  10	|  330129	|  Name 10	|  Description 10 | 


Invoices from ida 1 through 6 correspond to city ids 4, 4, 3, 2, 1 and a respectly. Hence the invoice items correspond to cities 4, 4, 4, 3, 2, 2, 2, 1 and 1 respectly. The city_product pairs of interent are (4,1), (4,7), (4,5), (3,10), (2,1), (2, 2), (2, 5), (1, 10) and (1,4).