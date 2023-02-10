# INVOICES PER COUNTRY

A business is analyzing data by country. For each country, display the country name, total number of invoices and their average amount. Format the average as a floating point number with 6 decimal places. Return only those countries where trheir average invoice amount is greater than average invoice amount over all invoices.

There are **4 tables**: country, city, customer, invoice.

## SAMPLE DATA TABLES

### country
| id | country_name |
|----|--------------|
| 1  | Austria      |
| 2  | Germany      |
| 3  | United_Kingdom |

### city
| id | city_name   | postal_code | country_id |
|----|-------------|------------|-----------|
| 1  | Wien        | 1010       | 1         |
| 2  | Berlin      | 10115      | 2         |
| 3  | Hamburg     | 20095      | 2         |
| 4  | London      | EC4V 4AD   | 3         |

### customer
| id | customer_name | city_id | customer_address   | contact_person | email            |
|----|---------------|---------|-------------------|----------------|------------------|
| 1  | Drogerie Wien | 1       | Deckergasse 15A   | Emil Steinbach | ----@---.com    |
| 2  | Cosmetics Store | 4    | Watling Street 147 | Jeremy Cobyn   | ----@---.com    |
| 3  | Kosmetikstudio | 3     | Rothenbaum 53      | Willy Brandit  | ----@---.com    |
| 4  | Neue Kosmetik | 1      | KarlsPlatz 27      | NULL           | ----@---.com    |
| 5  | Bio Kosmetik  | 2      | Motzstrasse 42     | Clara Zetkin   | ----@---.com    |
| 6  | K-Wien        | 1      | Kartnerstrasse 165 | Maria Rauch    | ----@---.com    |
| 7  | Natural Cosmetics | 4 | Clerkenwell 89    | Glenda Jackson | ----@---.com    |
| 8  | Kosmetik PLus | 2      | Unter den Linden 1 | Angela Merkel  | ----@---.com    |
| 9  | New Line Cosmetics | 4 | Devonshire 45   | Oliver Crowel  | ----@---.com    |

### invoice
| id | invoice_number                           | customer_id | user_account_id | total_price |
|----|--------------------------------------------------|-------------|----------------|------------|
| 1  | in_25181b07ba800c8d2fc967fe991807d9 | 7           | 4            | 1436         |
| 2  | 8fba0000fd456b27502b9f81e9d52481  | 9           | 2            | 1000         |
| 3  | 9lkij0000fd64ñkji22b9f81e9d58765  | 3           | 2            | 360          |
| 4  | 5jgnh890887la01254987lñj98khu481  | 5           | 2            | 1675         |
| 5  | 84hfjg768fhj2785fjdncb7v8d524uj   | 6           | 2            | 9500         |
| 6  | 12fdbc6584hgnb2968hjkvntu98d52481 | 4           | 2            | 150          |

The average invoice is `2353,5`.

The average invoice amount of country with ids 1, 2 and 3 are `4825`, `1017,5` and `1218` respectly. Hence, the only country to report is `Austria`. 
