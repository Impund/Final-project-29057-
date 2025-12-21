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

---

# 🌱 INNOVATION & ADVANCED PL/SQL IMPLEMENTATION

### **Smart Compliance & Environmental Impact Engine using PL/SQL**

---

### **2.1 Innovation Overview**

The main innovation of this project is the transformation of the Oracle database into an **intelligent decision-making engine**.

Instead of simply storing data, the database:

* Evaluates user behavior
* Enforces environmental rules
* Calculates environmental impact
* Generates compliance scores automatically

All intelligence is implemented **inside Oracle using PL/SQL**, without relying on external applications.

---

### **2.2 Problem Addressed by the Innovation**

Traditional e-waste systems face the following problems:

* No automatic enforcement of rules
* Manual monitoring of collectors
* No measurement of environmental impact
* Limited support for decision-making

This innovation directly solves these challenges.

---

### **2.3 Innovation Components**

#### **A. Eco-Compliance Scoring Engine**

Each collector is assigned an **Eco Score (0–100)** based on behavior.

**Scoring Factors:**

* Allowed collection days
* Number of violations
* Type of items collected
* Frequency of compliant actions

**PL/SQL Implementation:**

* Functions calculate scores
* Triggers update scores automatically
* Audit logs record all activities

📌 This promotes accountability and responsible behavior.

---

#### **B. Environmental Impact Estimation**

Each e-waste item is assigned an **environmental risk weight**.

Example:

* Battery → High risk
* Laptop → Medium risk
* Phone → Lower risk

PL/SQL functions calculate:

* Total environmental damage prevented
* Impact per collector
* Monthly sustainability metrics

📌 This introduces **environmental awareness at database level**.

---

#### **C. Automatic Compliance Enforcement**

Triggers prevent:

* Collections on restricted days
* Repeated policy violations

All attempts are:

* Blocked automatically
* Logged in the audit table
* Reported in BI dashboards

📌 This removes dependency on human supervision.

---

### **2.4 Why This Innovation Is Exceptional**

* Uses advanced PL/SQL features
* Solves a real-world environmental problem
* Fully automated
* Scalable and auditable
* Supports analytics and BI

This innovation demonstrates **deep understanding of database intelligence**, not just CRUD operations.

---

## **3. Business Requirements Document (BRD)**

---

### **3.1 Functional Requirements**

| ID  | Requirement                                        |
| --- | -------------------------------------------------- |
| FR1 | The system shall register users with defined roles |
| FR2 | The system shall record e-waste items              |
| FR3 | The system shall track collection events           |
| FR4 | The system shall block restricted collections      |
| FR5 | The system shall calculate eco-compliance scores   |
| FR6 | The system shall log all actions automatically     |
| FR7 | The system shall generate analytical reports       |

---

### **3.2 Non-Functional Requirements**

| ID   | Requirement                                |
| ---- | ------------------------------------------ |
| NFR1 | The system shall ensure data integrity     |
| NFR2 | The system shall enforce security rules    |
| NFR3 | The system shall handle large data volumes |
| NFR4 | The system shall be scalable               |
| NFR5 | The system shall support BI analytics      |
| NFR6 | The system shall maintain audit trails     |

---

## **4. Business Intelligence (BI) Implementation**

---

### **4.1 BI Objectives**

* Support management decision-making
* Monitor environmental performance
* Identify trends and risks
* Improve operational efficiency

---

### **4.2 KPIs Implemented**

* Average Eco Score per collector
* Total e-waste collected
* Environmental impact reduced
* Violation frequency
* Top-performing collectors

---

### **4.3 BI Dashboards**

#### **Executive Dashboard**

* KPI cards
* Monthly trends
* Performance summaries

#### **Compliance Dashboard**

* Violations per user
* Restricted-day attempts
* Audit summaries

#### **Environmental Dashboard**

* Impact by category
* Pollution prevented
* High-risk item tracking

---

### **4.4 BI Architecture Diagram (Suggested)**

```
[Oracle Database]
     |
[PL/SQL Logic]
     |
[Analytics Queries]
     |
[Dashboards & Reports]
```

---

## **5. Conclusion**

This innovation elevates the E-Waste Collection & Recycling Tracking System into a **smart, environmentally responsible, and analytics-driven platform**.

By embedding intelligence directly into the Oracle database using PL/SQL, the system:

* Enforces rules automatically
* Encourages ethical behavior
* Supports sustainability
* Enables informed decision-making

This work demonstrates advanced database mastery and real-world problem-solving.

> *“The database does not just store data — it protects the environment.”* 🌍

---



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
