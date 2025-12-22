# Vehicle Rental Management System - Database Design

A robust relational database system designed to manage users, vehicle inventory, and rental bookings. This project demonstrates database normalization, relationship management, and advanced SQL querying.

## 📌 Project Overview

This system handles three core entities:

- **Users**: Manages accounts for both Admins and Customers.
- **Vehicles**: Tracks inventory across different types (Cars, Bikes, Trucks) and their maintenance/availability status.
- **Bookings**: Records the transactional link between users and vehicles, including duration and cost.

## 🏗️ Database Schema

The database is built on a relational model with the following logic:

- **Users (1:N) Bookings**: A single user can have multiple rental records.
- **Vehicles (1:N) Bookings**: A single vehicle can be booked many times over its lifecycle.
- **Unique Constraints**: Enforced on User emails and Vehicle registration numbers to ensure data integrity.

---

## 🔍 SQL Query Explanations

The `queries.sql` file contains solutions for common business intelligence scenarios. Below is a breakdown of the logic used:

### 1. Booking Details (INNER JOIN)

**Purpose:** Combines data from three tables to provide a human-readable booking report.

- **Logic:** It links the `Bookings` table with `Users` and `Vehicles` using their respective Foreign Keys. This allows the system to display the Customer Name and Vehicle Name instead of just ID numbers.

### 2. Inventory Gaps (NOT EXISTS)

**Purpose:** Identifies "dead stock" or vehicles that have never been rented.

- **Logic:** This subquery checks every vehicle against the entire `Bookings` table. If a vehicle's ID does not appear in any booking record, it is returned in the results. This is more efficient than a `LEFT JOIN` for large datasets.

### 3. Availability Search (WHERE)

**Purpose:** Filters inventory based on specific customer needs.

- **Logic:** This query uses multiple conditions in the `WHERE` clause to narrow down results to a specific category (`car`) and a specific state (`available`).

### 4. High-Demand Vehicles (GROUP BY & HAVING)

**Purpose:** Identifies popular vehicles that have been booked more than twice.

- **Logic:** It groups the rental records by vehicle name and uses the `COUNT()` aggregate function. The `HAVING` clause is applied after the grouping to filter out vehicles that don't meet the "more than 2" threshold.

---

## 🚀 How to Use

1.  **Schema Setup:** Run your DDL statements (CREATE TABLE) to establish the structure.
2.  **Data Entry:** Import the sample data for Users, Vehicles, and Bookings.
3.  **Analysis:** Execute `queries.sql` in your SQL editor (MySQL, PostgreSQL, or SQL Server, beekeeper) to generate reports.
