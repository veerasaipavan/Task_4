# Task_4
Task-4-SQL-Analysis




## 🗂 Database: `task_3`
The database consists of **three main tables**: `films`, `customers`, and `rentals`.
### 1️⃣ Films Table

Stores information about movies available for rent.

| Column        | Type          | Description                  |
|---------------|---------------|------------------------------|
| `films_id`    | INT           | Primary key                  |
| `title`       | VARCHAR(200)  | Movie title (NOT NULL)       |
| `release_year`| INT           | Year of release              |
| `rental_rate` | DECIMAL(4,2)  | Rental price of the film     |

**Sample Data:**
```sql
INSERT INTO films (films_id, title, release_year, rental_rate) VALUES
(101, 'The Matrix', 1999, 4.99),
(102, 'Inception', 2010, 5.99),
(103, 'PulpFiction', 1994, 3.99),
(104, 'Parasite', 2019, 4.99),
(105, 'Amelie', 2001, 2.99);

---

###  Customers Table**
```markdown
### 2️⃣ Customers Table

Stores information about the customers.

| Column        | Type           | Description                  |
|---------------|----------------|------------------------------|
| `customer_id` | INT            | Primary key                  |
| `first_name`  | VARCHAR(100)   | Customer first name          |
| `last_name`   | VARCHAR(100)   | Customer last name           |
| `email`       | VARCHAR(255)   | Customer email               |
| `is_active`   | BOOLEAN        | Active status of customer    |

**Sample Data:**
```sql
INSERT INTO customers (customer_id, first_name, last_name, email, is_active) VALUES
(1, 'Alice', 'Smith', 'alice@example.com', TRUE),
(2, 'Bob', 'Johnson', 'bob@example.com', TRUE),
(3, 'Charlie', 'Brown', 'charlie@example.com', FALSE),
(4, 'Diana', 'Prince', 'diana@example.com', TRUE);

---

### Rentals Table**
```markdown
### 3️⃣ Rentals Table

Stores rental transactions between customers and films.

| Column        | Type        | Description                                |
|---------------|------------|--------------------------------------------|
| `rental_id`   | INT        | Primary key, AUTO_INCREMENT               |
| `customer_id` | INT        | Foreign key referencing `customers`       |
| `films_id`    | INT        | Foreign key referencing `films`           |
| `rental_date` | DATE       | Date when the film was rented             |
| `return_date` | DATE       | Date when the film was returned           |

**Sample Data:**
```sql
INSERT INTO rentals (customer_id, films_id, rental_date, return_date) VALUES
(1, 101, '2025-09-01', '2025-09-03'),
(2, 102, '2025-09-01', '2025-09-04'),
(1, 103, '2025-09-05', '2025-09-06'),
(4, 101, '2025-09-06', '2025-09-08'),
(2, 104, '2025-09-07', NULL);

---

### **Part 5: Queries and Outputs**
```markdown
## 📝 Queries & Outputs

### 1️⃣ Films released after 2005
```sql
SELECT title, release_year, rental_rate
FROM films
WHERE release_year > 2005
ORDER BY release_year;
SELECT f.title AS film_title, SUM(f.rental_rate) AS total_revenue
FROM rentals r
INNER JOIN films f ON r.films_id = f.films_id
GROUP BY f.title
ORDER BY total_revenue DESC;
### 2️⃣ Total revenue per film

SELECT f.title AS film_title, SUM(f.rental_rate) AS total_revenue
FROM rentals r
INNER JOIN films f ON r.films_id = f.films_id
GROUP BY f.title
ORDER BY total_revenue DESC;

### 3️⃣ Customers with more than one rental

SELECT c.first_name, c.last_name, COUNT(r.rental_id) AS total_rentals
FROM customers c
INNER JOIN rentals r ON c.customer_id = r.customer_id
GROUP BY c.customer_id, c.first_name, c.last_name
HAVING total_rentals > 1;

### 4️⃣ Films with rental rate above average
SELECT title, rental_rate
FROM films
WHERE rental_rate > (SELECT AVG(rental_rate) FROM films);

### 5️⃣ Average Revenue Per User (ARPU)
SELECT SUM(f.rental_rate) / COUNT(DISTINCT r.customer_id) AS Avg_user
FROM rentals r
INNER JOIN films f ON r.films_id = f.films_id;

### 6️⃣ Rental Report View
CREATE VIEW rental_report_view AS
SELECT r.rental_id, c.first_name, c.last_name, f.title AS film_title, f.rental_rate, r.rental_date
FROM rentals r
INNER JOIN customers c ON r.customer_id = c.customer_id
INNER JOIN films f ON r.films_id = f.films_id
ORDER BY r.rental_date DESC;

SELECT * FROM rental_report_view WHERE rental_rate >= 4.99;



### 7️⃣ Indexing for performance

CREATE INDEX idx_customer_lastname ON customers (last_name);
---

```

## 🔑 Key Learnings
- Created tables with **primary keys, foreign keys, and auto-increment columns**.  
- Resolved **column naming and foreign key issues** (`film_id` vs `films_id`).  
- Practiced **joins**, **aggregations**, **grouping**, and **HAVING clause**.  
- Created **views** for reusable reporting.  
- Applied **indexing** for performance optimization.  
- Calculated **ARPU**, total revenue per film, and filtered data based on business logic.



---

## 👤 Author

**Veera Sai Pavan Chavvakula**  
- 📧 Email: [veerasaipavan6673@gmail.com](mailto:veerasaipavan6673@gmail.com)  
- 📞 Phone: +91 7416243771  
- 🔗 LinkedIn: [https://www.linkedin.com/in/veera-sai-pavan-chavvakula-6260a72bb](https://www.linkedin.com/in/veera-sai-pavan-chavvakula-6260a72bb)  

Aspiring **Data Analyst** skilled in **Python, SQL, Power BI, Automation, and Machine Learning**.  
This task is part of learning and demonstrating SQL database design, queries, and analytics skills.


