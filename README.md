# Vehicle Rental Management System

## Project Overview
The Vehicle Rental Management System is a relational database–driven project designed to manage vehicle rentals efficiently.  
It manages users, vehicles, and bookings while ensuring proper relationships through the use of primary and foreign keys.
---

## Technologies Used
- PostgreSQL (Relational Database)
- SQL
- drawsql

---

## Database Tables
The system consists of the following tables:

### 1. Users
Stores customer and admin information.

### 2. Vehicles
Stores vehicle details available for rent.

### 3. Bookings
Stores rental booking information and links users with vehicles.

---

## Entity Relationships
- `bookings.user_id` → references `users.user_id`
- `bookings.vehicle_id` → references `vehicles.vehicle_id`
---

## Key Features
- Relational database design
- Proper use of primary & foreign keys
- Clean and readable SQL structure

---

## Learning Outcomes
- Understand relational database design
- Learn SQL JOIN operations

---

## 👨‍💻 Author
**Md. Ikram Hossain**  
Full-Stack Web Developer | CS Student at UCLan Cyprus
