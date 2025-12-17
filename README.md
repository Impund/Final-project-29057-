Names: IMPUNDU GATERA Brazia
ID: 29057
# E-Waste Collection and Recycling Tracking System 🌱♻️

[![PL/SQL](https://img.shields.io/badge/PL--SQL-Oracle-blue.svg)](https://www.oracle.com/database/technologies/appdev/plsql.html)
[![Database](https://img.shields.io/badge/Database-PostgreSQL-orange.svg)](https://www.postgresql.org/)

---

## Table of Contents

1. [Project Overview](#project-overview)
2. [Features](#features)
3. [Database Schema](#database-schema)
4. [System Architecture & Workflow](#system-architecture--workflow)
5. [PL/SQL Components](#plsql-components)
6. [Innovation & Uniqueness](#innovation--uniqueness)
7. [Expected Results](#expected-results)
8. [Future Enhancements](#future-enhancements)

---

## Project Overview

The **E-Waste Collection and Recycling Tracking System** is a **PL/SQL-based project** designed to manage electronic waste collection and recycling. The system allows users, collectors, and recycling companies to **register, log, track, and report** e-waste activities efficiently, promoting environmental responsibility.

---

## Features

* **User Management:** Track users, collectors, and officers.
* **Collection Tracking:** Log items collected at different points.
* **Transfer Management:** Automate and track e-waste transfers to recyclers.
* **Eco-Rewards System:** Award points to users for recycling.
* **Reporting & Analytics:** Generate monthly and yearly summaries.

---

## Database Schema

| Table                 | Description                                    | Key Fields                                                                 |
| --------------------- | ---------------------------------------------- | -------------------------------------------------------------------------- |
| **USERS**             | System users (collectors, officers, recyclers) | user_id (PK), full_name, role, contact, location                           |
| **COLLECTION_POINTS** | Locations where e-waste is collected           | point_id (PK), point_name, district, capacity                              |
| **EWASTE_ITEMS**      | Collected items                                | item_id (PK), category, weight, condition, date_collected, point_id (FK)   |
| **RECYCLERS**         | Licensed recycling companies                   | recycler_id (PK), name, license_no, contact, location                      |
| **TRANSFER_LOGS**     | Tracks e-waste transfers                       | transfer_id (PK), item_id (FK), point_id (FK), recycler_id (FK), date_sent |
| **REWARDS**           | Stores eco-points earned by users              | reward_id (PK), user_id (FK), points_earned, redeemed_status               |

---

## System Architecture & Workflow

### **Database Schema Diagram**

```
USERS (user_id PK)
    |
    |--< REWARDS (reward_id PK, user_id FK)
COLLECTION_POINTS (point_id PK)
    |
    |--< EWASTE_ITEMS (item_id PK, point_id FK)
            |
            |--< TRANSFER_LOGS (transfer_id PK, item_id FK, point_id FK, recycler_id FK)
RECYCLERS (recycler_id PK)
```

✅ **Explanation:**

* Users register and earn points.
* E-waste items are linked to collection points.
* Transfers link items from collection points to recyclers.
* Rewards track eco-points per user.

---

### **Workflow Diagram (Text-Based)**

```
[User] --> Register --> [USERS Table]
[Collector] --> Add E-Waste --> [EWASTE_ITEMS Table]
    --> Trigger: Check capacity --> Alert if full
[System] --> Transfer to Recycler --> [TRANSFER_LOGS Table]
[System] --> Update Rewards --> [REWARDS Table]
[Admin/Officer] --> Generate Reports --> Monthly/Yearly Summary
```

**Step-by-Step Flow:**

1. User or collector registers.
2. Collector logs e-waste collection.
3. Trigger monitors collection point capacity.
4. Procedure transfers e-waste to recycler.
5. Function calculates eco-points for users.
6. Cursor generates monthly or yearly reports.
7. Admin/officer reviews analytics for decision-making.

---

## PL/SQL Components

### Triggers

* **Check Capacity:** Alert when collection point reaches maximum capacity.

### Procedures

* **Transfer Item:** Records transfer from collection point to recycler.

### Functions

* **Total Points:** Calculates total eco-points earned by a user.

### Cursors

* **Monthly Summary:** Generates reports of e-waste collected by category.

### Exceptions

* Handle errors such as duplicate entries, missing data, or invalid references.

---

## Innovation & Uniqueness

* **Eco-Rewards System:** Encourages recycling via points redeemable for benefits.
* **Environmental Awareness:** Promotes responsible disposal of e-waste.
* **Data-Driven Operations:** Enables efficient collection and recycling management.

---

## Expected Results

* Real-time tracking of e-waste collection and recycling.
* Automated reporting for government or environmental agencies.
* Increased community engagement and recycling awareness.
* Efficient operation of collection points and recyclers.

---

## Future Enhancements

* **Web Dashboard:** React-based interface for users and officers.
* **Mobile App Integration:** QR code scanning at collection points.
* **Advanced Analytics:** Predict trends, optimize collection routes.
* **Gamification:** Leaderboards and badges to motivate users further.

---
