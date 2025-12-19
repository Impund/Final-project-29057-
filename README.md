Names: IMPUNDU GATERA Brazia
ID: 29057

# E-Waste Collection and Recycling Tracking System 🌱♻️

[![PL/SQL](https://img.shields.io/badge/PL--SQL-Oracle-blue.svg)](https://www.oracle.com/database/technologies/appdev/plsql.html)
[![Database](https://img.shields.io/badge/Database-PostgreSQL-orange.svg)](https://www.postgresql.org/)

---

## Table of Contents

1. [Project Overview](#project-overview)
2. [Features](#features)
3. [System Architecture](#system-architecture)
4. [Database Schema & ERD](#database-schema--erd)
5. [Data Dictionary](#data-dictionary)
6. [PL/SQL Components](#plsql-components)
7. [Workflow](#workflow)
8. [Innovation & Uniqueness](#innovation--uniqueness)
9. [Expected Results](#expected-results)
10. [Future Enhancements](#future-enhancements)

---

## Project Overview

The **E-Waste Collection and Recycling Tracking System** is a **PL/SQL-based solution** for managing electronic waste collection, transfer, and recycling. It is designed to:

* Track e-waste collection and recycling activities.
* Enable users, collectors, and recyclers to interact efficiently.
* Provide automated reports and eco-reward points.
* Promote responsible e-waste disposal and environmental sustainability.

This project combines **technology, database management, and environmental innovation** to support communities and recycling companies.

---

## Features

* User Registration & Role Management
* E-Waste Collection Logging
* Automated Transfer to Recyclers
* Eco-Rewards Tracking
* Reporting & Analytics for decision-making
* Alerts for Collection Point Capacity

---

## System Architecture

The system is designed in a **three-layer architecture**:

```
+------------------+        +-------------------+        +------------------+
|    Presentation  |  <---> |   Business Logic  |  <---> |     Database     |
| (Web Interface)  |        |  (PL/SQL Scripts) |        |  (Tables/Views) |
+------------------+        +-------------------+        +------------------+
```

**Components:**

1. **Presentation Layer**

   * Optional Web/GUI interface (React, HTML/JS) for input and reporting.

2. **Business Logic Layer**

   * PL/SQL scripts including triggers, procedures, functions, cursors, and exception handling.
   * Handles data validation, reward calculation, and transfer logic.

3. **Database Layer**

   * Relational database (Oracle/PostgreSQL) storing all user, collection, recycler, transfer, and reward data.

---

## Database Schema & ERD

### Tables Overview

| Table             | Description                                                                 |
| ----------------- | --------------------------------------------------------------------------- |
| USERS             | Stores information about system users (collectors, officers, general users) |
| COLLECTION_POINTS | Locations where e-waste is collected                                        |
| EWASTE_ITEMS      | Records of collected electronic waste items                                 |
| RECYCLERS         | Licensed recycling companies                                                |
| TRANSFER_LOGS     | Tracks e-waste movement from collection points to recyclers                 |
| REWARDS           | Eco-points earned by users for recycling activities                         |

### Entity-Relationship Diagram (ERD)

```
+------------------+       +------------------+
|      USERS       |       | COLLECTION_POINTS|
|------------------|       |-----------------|
| user_id (PK)     |       | point_id (PK)    |
| full_name        |       | point_name       |
| role             |       | district         |
| contact          |       | capacity         |
| location         |       +-----------------+
+--------+---------+             |
         |                       |
         |                       |
         |                  +----v----+
         |                  | EWASTE_ITEMS |
         |                  |-------------|
         +----< REWARDS     | item_id PK  |
                            | category    |
                            | weight      |
                            | condition   |
                            | date_collected |
                            | point_id FK |
                            +-------------+
                                   |
                                   |
                                   v
                             +----------------+
                             | TRANSFER_LOGS  |
                             |----------------|
                             | transfer_id PK |
                             | item_id FK     |
                             | point_id FK    |
                             | recycler_id FK |
                             | date_sent      |
                             +----------------+
                                   ^
                                   |
                             +----------------+
                             |   RECYCLERS    |
                             |----------------|
                             | recycler_id PK |
                             | name           |
                             | license_no     |
                             | contact        |
                             | location       |
                             +----------------+
```

---

## Data Dictionary

| Table             | Column          | Data Type     | Description                             |
| ----------------- | --------------- | ------------- | --------------------------------------- |
| USERS             | user_id         | NUMBER        | Primary Key, unique ID for each user    |
|                   | full_name       | VARCHAR2(100) | Full name of user                       |
|                   | role            | VARCHAR2(20)  | Role: user, collector, officer          |
|                   | contact         | VARCHAR2(50)  | Phone or email                          |
|                   | location        | VARCHAR2(50)  | User’s city/district                    |
| COLLECTION_POINTS | point_id        | NUMBER        | Primary Key, unique collection point ID |
|                   | point_name      | VARCHAR2(100) | Name of collection point                |
|                   | district        | VARCHAR2(50)  | Location of point                       |
|                   | capacity        | NUMBER        | Max number of items allowed             |
| EWASTE_ITEMS      | item_id         | NUMBER        | Primary Key, unique e-waste ID          |
|                   | category        | VARCHAR2(50)  | Type: phone, battery, laptop, etc.      |
|                   | weight          | NUMBER        | Weight in kg                            |
|                   | condition       | VARCHAR2(50)  | Working, broken, etc.                   |
|                   | date_collected  | DATE          | Date item was collected                 |
|                   | point_id        | NUMBER        | FK linking to COLLECTION_POINTS         |
| RECYCLERS         | recycler_id     | NUMBER        | Primary Key, unique recycler ID         |
|                   | name            | VARCHAR2(100) | Name of recycler company                |
|                   | license_no      | VARCHAR2(50)  | Official license number                 |
|                   | contact         | VARCHAR2(50)  | Contact info                            |
|                   | location        | VARCHAR2(50)  | City or district                        |
| TRANSFER_LOGS     | transfer_id     | NUMBER        | Primary Key, unique transfer ID         |
|                   | item_id         | NUMBER        | FK to EWASTE_ITEMS                      |
|                   | point_id        | NUMBER        | FK to COLLECTION_POINTS                 |
|                   | recycler_id     | NUMBER        | FK to RECYCLERS                         |
|                   | date_sent       | DATE          | Transfer date                           |
| REWARDS           | reward_id       | NUMBER        | Primary Key, unique reward ID           |
|                   | user_id         | NUMBER        | FK to USERS                             |
|                   | points_earned   | NUMBER        | Eco-points earned                       |
|                   | redeemed_status | VARCHAR2(10)  | Yes/No if points redeemed               |

---

## PL/SQL Components

### Triggers

* **Check Capacity Trigger** – Alerts when collection point reaches full capacity.

### Procedures

* **Transfer Item Procedure** – Logs item transfers from collection points to recyclers.

### Functions

* **Total Points Function** – Calculates total eco-points for each user.

### Cursors

* **Monthly Summary Cursor** – Generates summary reports for government or company use.

### Exceptions

* Handles errors like **duplicate entries, missing data, invalid foreign keys**.

---

## Workflow

```
[User] --> Register --> USERS
[Collector] --> Log E-Waste --> EWASTE_ITEMS
          --> Trigger: Check Capacity
[System] --> Transfer Items --> TRANSFER_LOGS
[System] --> Update Rewards --> REWARDS
[Admin/Officer] --> Generate Reports --> Analytics
```

---

## Innovation & Uniqueness

* **Eco-Rewards System:** Incentivizes recycling with points redeemable for benefits.
* **Data-Driven Decision-Making:** Efficiently monitors collection and recycling.
* **Environmental Impact:** Promotes responsible disposal of e-waste.

---

## Expected Results

* Full visibility of e-waste collection and recycling.
* Automated reports for government, environmental agencies, and recycling companies.
* Increased user participation in recycling.
* Improved operational efficiency for collection points and recyclers.

---

## Future Enhancements

* React-based **Web Dashboard** for real-time monitoring.
* QR code-enabled **Mobile App** for easy logging.
* Predictive analytics for **optimal collection schedules**.
* **Gamification:** Leaderboards, badges, and community challenges.

---
