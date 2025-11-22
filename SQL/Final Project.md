# Final SQL Project

<br>

## Analysis
Analyzes a music store database to deliver insights on financial performance, music genre preferences, top-selling tracks, and customer spending behaviors.

<br>

### What is the total revenue from all invoices?
```SQL
SELECT
    ROUND(SUM(invoices.total)) AS "TotalRevenue"
FROM invoices;
```
<details>
  <summary><i>Show result</i></summary>
  
| TotalRevenue |
|--------------|
| 2329         |
</details>

<br>

### How many tracks are there in each genre?
```SQL
SELECT
    genres.Name AS "Genre",
    COUNT(tracks.TrackId) AS "TotalTracks"
FROM genres
JOIN tracks
ON genres.GenreId = tracks.GenreId
GROUP BY genres.Name
ORDER BY genres.Name;
```
<details>
  <summary><i>Show result</i></summary>
  
| Genre             | TotalTracks |
|:------------------|------------:|
| Alternative       | 40          |
| Alternative & Punk| 332         |
| Blues             | 81          |
| Bossa Nova        | 15          |
| Classical         | 74          |
| Comedy            | 17          |
| Drama             | 64          |
| Easy Listening    | 24          |
| Electronica/Dance | 30          |
| Heavy Metal       | 28          |
| Hip Hop/Rap       | 35          |
| Jazz              | 130         |
| Latin             | 579         |
| Metal             | 374         |
| Opera             | 1           |
| Pop               | 48          |
| R&B/Soul          | 61          |
| Reggae            | 58          |
| Rock              | 1297        |
| Rock And Roll     | 12          |
| Sci Fi & Fantasy  | 26          |
| Science Fiction   | 13          |
| Soundtrack        | 43          |
| TV Shows          | 93          |
| World             | 28          |
</details>

<br>

### What are the top 5 selling tracks? (use a Common Table Expression / CTE)
```SQL
WITH TrackSales AS (
    SELECT
        tracks.TrackId,
        tracks.Name,
        SUM(invoice_items.Quantity) AS TotalSold
    FROM tracks
    JOIN invoice_items 
    ON tracks.TrackId = invoice_items.TrackId
    JOIN invoices ON invoice_items.InvoiceId = invoices.InvoiceId
    GROUP BY tracks.TrackId
)
SELECT
    TrackId,
    Name,
    TotalSold
FROM TrackSales
ORDER BY TotalSold DESC
LIMIT 5;
```
<details>
  <summary><i>Show result</i></summary>
  
| TrackId | Name             | TotalSold |
|---------|------------------|-----------|
| 2       | Balls to the Wall| 2         |
| 8       | Inject The Venom | 2         |
| 9       | Snowballed       | 2         |
| 20      | Overdose         | 2         |
| 32      | Deuces Are Wild  | 2         |
</details>

<br>

### Identify our top 5 customers and issue them discount codes.
```SQL
SELECT
    customers.CustomerId,
    customers.FirstName,
    customers.LastName,
    customers.Email,
    SUM(invoices.total) AS "TotalSpent",
    SUBSTR(MD5(RANDOM()), 1, 5) || '-' || 
        SUBSTR(MD5(RANDOM()), 6, 5) || '-' ||
        SUBSTR(MD5(RANDOM()), 11, 5) || '-' ||
        SUBSTR(MD5(RANDOM()), 16, 5) 
        AS "DiscountCode"
FROM customers
JOIN invoices
ON customers.CustomerId = invoices.CustomerId
GROUP BY customers.CustomerId
ORDER BY TotalSpent DESC
Limit 5;
```
<details>
  <summary><i>Show result</i></summary>
  
| CustomerId | FirstName   | LastName    | Email                        | TotalSpent | DiscountCode             |
|------------|-------------|-------------|------------------------------|------------|--------------------------|
| 6          | Helena      | Holý        | hholy@gmail.com              | 49.62      | 3dc70-2eb90-ea0d0-7eb4b  |
| 26         | Richard     | Cunningham  | ricunningham@hotmail.com     | 47.62      | 31f25-167f4-2500b-9c778  |
| 57         | Luis        | Rojas       | luisrojas@yahoo.cl           | 46.62      | 3d65b-605ce-651ef-b416d  |
| 45         | Ladislav    | Kovács      | ladislav_kovacs@apple.hu     | 45.62      | 51f33-26e82-60e75-743f5  |
| 46         | Hugh        | O'Reilly    | hughoreilly@apple.ie         | 45.62      | 82f5f-3905b-f5312-2f57f  |
</details>

<br>
