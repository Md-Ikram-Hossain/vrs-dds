# SQL Queries

This document describes the SQL Queries for the Vehicle Rental System, including the data and SQL query outputs.

## SQL query Data (Input)

### Users Table
| user_id | name | email | phone | role |
| :--- | :--- | :--- | :--- | :--- |
| 1 | John Doe | john@example.com | 01711111111 | Customer |
| 2 | Alice Smith | alice@example.com | 01722222222 | customer |
| 3 | Bob Johnson | bob@example.com| 01733333333 | Customer |
| 4 | Emma Brown | emma@example.com | 01744444444 | Customer |
| 5 | Michael Lee | michael@example.com | 01755555555 | customer |
| 6 | Sophia Wilson | sophia@example.com | 01766666666 | Customer |
| 7 | David Miller | david@example.com | 01777777777 | Customer |
| 8 | Olivia Taylor | olivia@example.com | 01788888888 | customer |
| 9 | Admin One | admin1@example.com | 01911111111 | admin |
| 10 | Admin Two | admin2@example.com | 01922222222 | admin |

### Vehicles Table
| vehicle_id | name            | type  | model | registration_number | price_per_day | availability_status  |
|------------|-----------------|-------|-------|---------------------|---------------|---------------|
| 1          | Toyota Corolla  | car   | 2021  | CAR-1001            | 50.00         | available     |
| 2          | Honda Civic     | car   | 2020  | CAR-1002            | 55.00         | rented        |
| 3          | Ford Ranger     | truck | 2019  | TRK-2001            | 80.00         | available     |
| 4          | Yamaha R15      | bike  | 2022  | BIK-3001            | 30.00         | available     |
| 5          | Suzuki Gixxer   | bike  | 2021  | BIK-3002            | 28.00         | maintenance   |
| 6          | Nissan Sunny    | car   | 2018  | CAR-1003            | 45.00         | available     |
| 7          | Isuzu D-Max     | truck | 2020  | TRK-2002            | 85.00         | rented        |
| 8          | BMW X5          | car   | 2022  | CAR-1004            | 120.00        | available     |
| 9          | Kawasaki Ninja  | bike  | 2023  | BIK-3003            | 40.00         | available     |
| 10         | Tesla Model 3   | car   | 2023  | CAR-1005            | 150.00        | available     |


### Bookings Table
| booking_id | user_id | vehicle_id | start_date  | end_date   | booking_status | total_cost |
|------------|---------|------------|------------|------------|----------------|------------|
| 1          | 1       | 1          | 2024-01-01 | 2024-01-05 | completed      | 200.00     |
| 2          | 2       | 2          | 2024-01-03 | 2024-01-06 | confirmed      | 165.00     |
| 3          | 3       | 3          | 2024-01-05 | 2024-01-08 | completed      | 240.00     |
| 4          | 4       | 4          | 2024-01-07 | 2024-01-09 | completed      | 60.00      |
| 5          | 5       | 6          | 2024-01-10 | 2024-01-15 | confirmed      | 225.00     |
| 6          | 6       | 1          | 2024-01-12 | 2024-01-14 | completed      | 100.00     |
| 7          | 7       | 8          | 2024-01-15 | 2024-01-18 | pending        | 360.00     |
| 8          | 8       | 9          | 2024-01-18 | 2024-01-20 | confirmed      | 80.00      |
| 9          | 1       | 10         | 2024-01-20 | 2024-01-22 | pending        | 300.00     |
| 10         | 2       | 1          | 2024-01-25 | 2024-01-28 | completed      | 150.00     |


---

## Query Results

### Query 1: JOIN
**Requirement**: Retrieve booking information along with Customer name and Vehicle name.

** Output**:
| booking_id | customer_name | vehicle_name   | start_date | end_date   |booking_status|
| :---       | :---          | :---           | :---       | :---       | :---      |
| 1          | John Doe      | Toyota Corolla | 2024-01-01 | 2024-01-05 | completed |
| 2          | Alice Smith   | Honda Civic    | 2024-01-03 | 2024-01-06 | confirmed |
| 3          | Bob Johnson   | Ford Ranger    | 2024-01-05 | 2024-01-08 | completed |
| 4          | Emma Brown    | Yamaha R15     | 2024-01-07 | 2024-01-09 | completed |
| 5          | Sophia Wilson | Nissan Sunny   | 2024-01-10 | 2024-01-15 | confirmed |
| 6          | David Miller  | Toyota Corolla | 2024-01-12 | 2024-01-14 | completed |
| 7          | Olivia Taylor | BMW X5         | 2024-01-15 | 2024-01-18 | pending   |
| 8          | Michael Lee   | Kawasaki Ninja | 2024-01-18 | 2024-01-20 | confirmed |
| 9          | John Doe      | Tesla Model 3  | 2024-01-20 | 2024-01-22 | pending   |
| 10         | Alice Smith   | Toyota Corolla | 2024-01-25 | 2024-01-28 | completed |

---

### Query 2: EXISTS
**Requirement**: Find all vehicles that have never been booked.

**Output**:
| vehicle_id | name | type | model | registration_number | price_per_day | availability_status |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 5 | Suzuki Gixxer | bike | 2021 | BIK-3002 | 28.00 | maintenance |
| 7 | Isuzu D-Max | truck | 2020 | TRK-2002 | 85.00 | rented |

---

### Query 3: WHERE
**Requirement**: Retrieve all available vehicles of a specific type (e.g. cars).

** Output**:
| vehicle_id | name | type | model | registration_number | price_per_day | availability_status |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | Toyota Corolla | car | 2021 | CAR-1001 | 50.00 | available |
| 6 | Nissan Sunny | car | 2018 | CAR-1003 | 45.00 | available |
| 8 | BMW X5 | car | 2022 | CAR-1004 | 120.00 | available |
| 10 | Tesla Model 3 | car | 2023 | CAR-1005 | 150.00 | available |

---

### Query 4: GROUP BY and HAVING
**Requirement**: Find the total number of bookings for each vehicle and display only those vehicles that have more than 2 bookings.

** Output**:
| vehicle_id  | vehicle_name | total_bookings |
| :--- | :--- | :--- |
| 1    | Toyota Corolla | 3 |
