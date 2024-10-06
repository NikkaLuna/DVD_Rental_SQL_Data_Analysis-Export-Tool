
# DVD-Rental-SQL-Data-Analysis-Export-Tool

Overview
--------

This project demonstrates an end-to-end SQL-based analysis workflow using a DVD Rental Database. The project includes creating tables, transforming data, and implementing a trigger for automatic updates. The goal is to track DVD rental patterns per customer and identify trends for business promotion analysis.

Features
--------

1.  **Detailed and Summary Reports:**

    -   The **detailed report** captures customer information alongside rental data.
    -   The **summary report** provides a monthly breakdown of rentals for quick insights.
2.  **Data Transformation:**

    -   A custom function converts raw rental dates into countable metrics, allowing stakeholders to measure promotion impact.
3.  **Automated Table Updates:**

    -   Implemented with a trigger to automatically update the summary table as new data is inserted.
4.  **Stored Procedure:**

    -   A stored procedure automates the ETL process, clearing old data and refreshing both detailed and summary tables.

Table Schema
------------

### `detailed_table`:

| Field | Type | Description |
| --- | --- | --- |
| `customer_id` | `bigint` | Unique ID for each customer |
| `first_name` | `varchar(40)` | Customer's first name |
| `last_name` | `varchar(40)` | Customer's last name |
| `email` | `varchar(90)` | Customer email |
| `rental_id` | `integer` | Unique rental ID |
| `rental_date` | `timestamp` | Date and time of the rental |
| `return_date` | `timestamp` | Date and time of the DVD return |

### `summary_table`:

| Field | Type | Description |
| --- | --- | --- |
| `customer_id` | `bigint` | Unique ID for each customer |
| `rental_date` | `timestamp` | Date and time of the rental |
| `number_of_rentals` | `varchar` | Number of rentals per customer for a given period |

SQL Implementation
------------------

1.  **Create Tables:**

    -   Created detailed and summary tables using `CREATE TABLE` statements.
2.  **Data Extraction:**

    -   Inserted data into the `detailed_table` using `INNER JOIN` to merge `customer` and `rental` tables.
3.  **Custom Function:**

    -   The `update_summary_table()` function aggregates rentals and updates the summary table.
4.  **Trigger Implementation:**

    -   `CREATE TRIGGER refresh_tables` ensures real-time updates of the summary report whenever the `detailed_table` changes.
5.  **Stored Procedure:**

    -   `CREATE PROCEDURE refresh_tables()` clears old data and refreshes both tables for consistent, updated reporting.

How to Run
----------

1.  **Create Tables:**

    sql

    Copy code

    `DROP TABLE IF EXISTS detailed_table;
    CREATE TABLE detailed_table (...);

    DROP TABLE IF EXISTS summary_table;
    CREATE TABLE summary_table (...);`

2.  **Insert Data into Detailed Table:**

    sql

    Copy code

    `INSERT INTO detailed_table (...)
    SELECT ... FROM rental
    INNER JOIN customer ON c.customer_id = r.customer_id;`

3.  **Create and Execute Trigger:**

    sql

    Copy code

    `CREATE TRIGGER refresh_tables
    AFTER INSERT ON detailed_table
    FOR EACH STATEMENT
    EXECUTE PROCEDURE update_summary_table();`

4.  **Run the Stored Procedure Monthly:**

    sql

    Copy code

    `CALL refresh_tables();`

Suggested Use Cases
-------------------

1.  **Track Customer Rental Behavior:** Measure customer rental patterns before and after the introduction of promotions to determine effectiveness.

2.  **Promotion Analysis:** Implement and monitor marketing campaigns such as "Rent Nine, Get One Free" to track monthly rental trends.

Future Improvements
-------------------

-   **Customer Segmentation Analysis:** Enhance the detailed report to segment customers based on rental frequency.
-   **Integration with Business Intelligence Tools:** Use tools like Power BI or Tableau for visualization and deeper insights.
-   **Automation with pgAgent:** Schedule the stored procedure using `pgAgent` for seamless monthly data refresh.

Requirements
------------

-   PostgreSQL or any compatible SQL environment
-   Basic understanding of SQL triggers and stored procedures
-   Database: DVD Rental Database with `customer` and `rental` tables

## Authors

- [@NikkaLuna](https://github.com/NikkaLuna)


## 🚀 About Me
I'm a Software Engineer with an emphasis on Java, Python, SQL, and AWS.  


## 🔗 Links
[![linkedin](https://img.shields.io/badge/linkedin-0A66C2?style=for-the-badge&logo=linkedin&logoColor=white)](https://www.linkedin.com/in/andrea-hayes-msml/)
[![twitter](https://img.shields.io/badge/twitter-1DA1F2?style=for-the-badge&logo=twitter&logoColor=white)](https://twitter.com/AHayes_Ninja_)
[![art portfolio](https://img.shields.io/badge/my_art-888?style=for-the-badge&logo=ko-fi&logoColor=white)](https://andreachristinehayes.wixsite.com/andreahayesart/)
