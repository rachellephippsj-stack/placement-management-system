# University Placement Management System

A relational database project built in **Oracle APEX 26.1** that models how a university manages student work placements — from departments and companies through to job openings, applications, interviews, and final offers.

> Author: **Rachelle Phipps** · Information Systems and Databases — Portfolio Element 2

---

## Overview

This project takes a real-world problem — matching students to placement opportunities and tracking them through the full hiring pipeline — and turns it into a fully normalised, data-driven system. It demonstrates relational design, SQL, constraint enforcement, reporting queries, and a database view.

- **8 interconnected tables** with enforced primary and foreign keys
- **336 records** of realistic sample data, with every foreign key validated for integrity
- **8 reporting queries** answering practical business questions
- **1 database view** (`Eligible_Students_View`) for fast short-listing of eligible students
- Full **ER diagram** and entity specifications (see the portfolio document)

---

## Database Schema

| Table | Description | Rows |
|-------|-------------|------|
| `Department` | Academic departments | 8 |
| `Company` | Employers posting placements | 30 |
| `Placement_Officer` | Staff managing placements | 6 |
| `Student` | Students seeking placements | 100 |
| `Job_Opening` | Vacancies posted by companies | 50 |
| `Application` | Student applications to openings | 60 |
| `Interview` | Interview stages per application | 55 |
| `Offer` | Offers made to applicants | 27 |

### Key relationships
- Each **student** belongs to one **department**; a department has many students and placement officers.
- Each **company** posts many **job openings**; each opening belongs to one company.
- A **student** submits many **applications**; each application targets one job opening.
- An **application** can have multiple **interview** stages, each managed by one placement officer.
- An **application** may result in one **offer**, tracked by status (Accepted, Pending, Declined).

---

## Reporting Queries

1. Placement success rate by department
2. Student application tracker
3. Interview outcomes summary
4. Open opportunities ranked by value
5. Pending offers nearing expiry (follow-up list)
6. Placement officer workload
7. Applications by company and industry
8. Highest-value open roles

---

## How to Run

1. Open your **Oracle APEX 26.1** workspace and go to **SQL Workshop → SQL Scripts** (or **SQL Commands**).
2. Upload / paste **[`placement_system_full.sql`](placement_system_full.sql)** and run it.
3. The script drops any existing objects first, then creates all tables, constraints, sample data, queries, and the view — so it is safe to re-run.
4. Explore the data using the reporting queries, or query the view directly:

```sql
SELECT * FROM Eligible_Students_View;
```

---

## Files in this repository

| File | Description |
|------|-------------|
| `placement_system_full.sql` | Complete database: tables, constraints, 336 records, and the view |
| `README.md` | This file |

---

## Notes on Design

- **Normalisation:** student names are not duplicated in the `Application` table — applications link to students via `student_id`. Placement officers reference departments by `department_id` rather than storing department names as text.
- **Constraints:** `UNIQUE` constraints on student and officer email addresses prevent duplicate accounts. `CHECK` constraints enforce valid status domains (e.g. application status, offer acceptance status).
- **Data types:** salaries and stipends are stored with currency formatting; dates and timestamps use Oracle `TO_DATE` / `TO_TIMESTAMP` conversions.

---

*Built as part of a university Information Systems and Databases module.*
