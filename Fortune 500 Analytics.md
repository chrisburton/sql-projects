# Fortune 500 Analytics
Dataset: [db-fiddle](https://www.db-fiddle.com/f/saxdDCCyos6z6UdpjeEXSJ/0)

<br>

## Analysis
Explores the databse of Fortune companies, examining employee tenure, revenue categories, maternity leave standards, and the relationship between healthcare benefits, paid time off, and employee retention across different sectors.

<br>

### Which industry has the highest tenure on average?
```sql
SELECT 
    industry,
    ROUND(AVG(avg_employee_tenure), 2) AS avg_tenure
FROM fortune_companies
GROUP BY industry
ORDER BY avg_tenure DESC;
```
<details>
  <summary><i>Show result</i></summary>

| industry            | avg_tenure |
|---------------------|-----------:|
| Energy              | 6.87       |
| Manufacturing       | 6.68       |
| Finance             | 6.04       |
| Technology          | 5.97       |
| Healthcare          | 5.92       |
| Retail              | 5.49       |
| Telecommunications  | 5.2        |
</details>

<br>

### Which companies in particular industries are "High Revenue" or "Low Revenue" based on a revenue threshold?
```sql
SELECT 
    company_name,
    industry,
    revenue,
    CASE 
        WHEN revenue >= 250 THEN 'high revenue'
        ELSE 'low revenue' 
    END AS revenue_threshold
FROM fortune_companies
ORDER BY revenue DESC;
```
<details>
  <summary><i>Show result</i></summary>
  
| company_name                | industry            | revenue | revenue_threshold |
|-----------------------------|---------------------|--------:|------------------:|
| Walmart Inc.                | Retail              | 523.96  | high revenue      |
| Company F                   | Technology          | 420.1   | high revenue      |
| Company B                   | Healthcare          | 400.7   | high revenue      |
| Company R                   | Technology          | 400.7   | high revenue      |
| Company J                   | Manufacturing       | 390.6   | high revenue      |
| Amazon.com Inc.             | Technology          | 386.06  | high revenue      |
| Company CC                  | Manufacturing       | 380     | high revenue      |
| Company JJ                  | Manufacturing       | 370     | high revenue      |
| Apple Inc.                  | Technology          | 365.7   | high revenue      |
| Company Q                   | Manufacturing       | 360     | high revenue      |
| Company V                   | Manufacturing       | 350.6   | high revenue      |
| Company M                   | Technology          | 340.9   | high revenue      |
| Company Y                   | Technology          | 320.9   | high revenue      |
| Company FF                  | Technology          | 300.9   | high revenue      |
| Company C                   | Manufacturing       | 300.2   | high revenue      |
| Company T                   | Energy              | 290.5   | high revenue      |
| Company E                   | Finance             | 280.7   | high revenue      |
| Company H                   | Energy              | 280.5   | high revenue      |
| Company HH                  | Energy              | 280.2   | high revenue      |
| Exxon Mobil Corporation     | Energy              | 265.01  | high revenue      |
| Company O                   | Energy              | 260.2   | high revenue      |
| Company EE                  | Finance             | 250.4   | high revenue      |
| Company X                   | Finance             | 240.4   | low revenue       |
| Company AA                  | Energy              | 240.2   | low revenue       |
| Company A                   | Retail              | 235.4   | low revenue       |
| Company L                   | Finance             | 230.4   | low revenue       |
| Company S                   | Retail              | 210.8   | low revenue       |
| Company N                   | Retail              | 200.6   | low revenue       |
| Company G                   | Retail              | 190.8   | low revenue       |
| Company GG                  | Retail              | 190.6   | low revenue       |
| Company Z                   | Retail              | 180.6   | low revenue       |
| Company K                   | Healthcare          | 180.2   | low revenue       |
| Company DD                  | Healthcare          | 170.2   | low revenue       |
| Company W                   | Healthcare          | 160.2   | low revenue       |
| JPMorgan Chase & Co.        | Finance             | 160.1   | low revenue       |
| Company D                   | Healthcare          | 150.5   | low revenue       |
| Company KK                  | Healthcare          | 150.2   | low revenue       |
| Company U                   | Telecommunications  | 140.3   | low revenue       |
| Verizon Communications Inc. | Telecommunications  | 131.88  | low revenue       |
| Company P                   | Telecommunications  | 130.5   | low revenue       |
| Company BB                  | Telecommunications  | 120.5   | low revenue       |
| Company II                  | Telecommunications  | 110.5   | low revenue       |
| Company I                   | Telecommunications  | 110.3   | low revenue       |
</details>

<br>

### Which companies respect the European ILO minimum maternity leave of 14 weeks?
```sql
SELECT 
    company_name,
    maternity_leave_weeks,
    CASE
        WHEN maternity_leave_weeks > 14 THEN 'mom friendly'
        WHEN maternity_leave_weeks = 14 THEN 'acceptable'
        ELSE 'fail'
    END maternity_leave_rating
FROM fortune_companies
ORDER BY maternity_leave_weeks DESC;
```
<details>
  <summary><i>Show result</i></summary>

| company_name              | maternity_leave_weeks | maternity_leave_rating |
|---------------------------|:---------------------:|-----------------------:|
| Company FF                | 16                    | mom friendly           |
| Company M                 | 15                    | mom friendly           |
| Company Y                 | 15                    | mom friendly           |
| Amazon.com Inc.           | 14                    | acceptable             |
| Company F                 | 14                    | acceptable             |
| Company Q                 | 14                    | acceptable             |
| Company V                 | 14                    | acceptable             |
| Company B                 | 13                    | fail                   |
| Company J                 | 13                    | fail                   |
| Company R                 | 13                    | fail                   |
| Company CC                | 13                    | fail                   |
| Apple Inc.                | 12                    | fail                   |
| JPMorgan Chase & Co.      | 12                    | fail                   |
| Company D                 | 12                    | fail                   |
| Company P                 | 12                    | fail                   |
| Company U                 | 12                    | fail                   |
| Company II                | 12                    | fail                   |
| Company JJ                | 12                    | fail                   |
| Company I                 | 11                    | fail                   |
| Company BB                | 11                    | fail                   |
| Company A                 | 10                    | fail                   |
| Company C                 | 10                    | fail                   |
| Company W                 | 10                    | fail                   |
| Company G                 | 9                     | fail                   |
| Company K                 | 9                     | fail                   |
| Company S                 | 9                     | fail                   |
| Company AA                | 9                     | fail                   |
| Company DD                | 9                     | fail                   |
| Company HH                | 9                     | fail                   |
| Walmart Inc.              | 8                     | fail                   |
| Company E                 | 8                     | fail                   |
| Company H                 | 8                     | fail                   |
| Company N                 | 8                     | fail                   |
| Company T                 | 8                     | fail                   |
| Company Z                 | 8                     | fail                   |
| Company KK                | 8                     | fail                   |
| Company L                 | 7                     | fail                   |
| Company O                 | 7                     | fail                   |
| Company X                 | 7                     | fail                   |
| Company GG                | 7                     | fail                   |
| Exxon Mobil Corporation   | 6                     | fail                   |
| Verizon Communications Inc.| 6                   | fail                   |
| Company EE                | 6                     | fail                   |

  </details>

<br>

### Analyze each industry on whether a clear relationship exists between healthcare benefits, paid time off, and average employee tenure.
```sql
SELECT
    industry,
    paid_time_off_days,
    avg_employee_tenure
FROM fortune_companies
WHERE healthcare_benefits = 1
GROUP BY industry
ORDER BY avg_employee_tenure DESC;
```
<details>
  <summary><i>Show result</i></summary>
  
| industry            | paid_time_off_days | avg_employee_tenure |
|---------------------|-------------------:|--------------------:|
| Energy              | 15                 | 7.2                 |
| Finance             | 21                 | 6.9                 |
| Retail              | 15                 | 6.2                 |
| Manufacturing       | 18                 | 5.8                 |
| Healthcare          | 22                 | 5.7                 |
| Telecommunications  | 19                 | 4.9                 |
| Technology          | 20                 | 4.5                 |
</details>
  
<br>
