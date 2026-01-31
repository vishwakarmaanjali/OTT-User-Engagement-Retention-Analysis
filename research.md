# OTT User Engagement & Retention Analysis

## End-to-End Research Document

---

## 1. Project Overview

### Project Title

**OTT User Engagement & Retention Analysis**

### Project Type

Descriptive and Diagnostic Analytics 

### Tools Used

* **Excel** – Initial data inspection and basic cleaning
* **SQL** – Data extraction, joins, aggregations, and preparation
* **Python** – Exploratory Data Analysis (EDA only)
* **Power BI** – Dashboarding, visualization, and insight delivery

---

## 2. Business Context

OTT platforms operate on subscription-based models where long-term success depends heavily on user engagement and retention. High competition and low switching costs make it critical for platforms to understand user behavior patterns and reasons for churn.

### Key Challenges

* Users disengaging after initial usage
* High churn after free trials or early subscription periods
* Lack of clarity on what drives repeat viewership
* Limited visibility into engagement trends across content types

---

## 3. Problem Statement

The OTT platform lacks a centralized analytics solution to measure and analyze user engagement and retention. Without this visibility, it is difficult for business teams to make informed decisions related to content strategy, user experience, and subscription optimization.

---

## 4. Project Objectives

### Primary Objectives

* Measure user engagement levels
* Analyze user retention patterns over time
* Identify behavioral trends linked to disengagement

### Secondary Objectives

* Compare engagement across content types, genres, and subscription plans
* Understand time-based viewing behavior
* Provide actionable business recommendations

---

## 5. Scope of the Project

### In Scope

* User viewing behavior
* Watch time and session analysis
* Repeat usage and retention trends
* Subscription duration analysis
* Time-based engagement patterns

### Out of Scope

* Machine learning or predictive modeling
* Recommendation systems
* Complex DAX calculations
* Real-time streaming analytics

---

## 6. Data Collection Strategy (Conceptual)

### Data Sources

* User activity logs
* Content metadata systems
* Subscription and billing records

### Logical Data Entities

#### User Data

* User ID
* Region
* Age group
* Subscription plan

#### Content Data

* Content ID
* Genre
* Content type (Movie / Series)

#### Viewing Activity Data

* User ID
* Content ID
* Watch duration
* Session timestamp

#### Subscription Data

* User ID
* Plan start and end date
* Subscription status

### Data Granularity

* Session-level data for engagement analysis
* User-level aggregation for retention analysis

---

## 7. Data Cleaning Research Plan

### Excel

* Remove duplicate records
* Identify and handle missing values
* Standardize date and time formats
* Validate primary and foreign keys

### SQL

* Join user, content, viewing, and subscription tables
* Filter invalid or incomplete records
* Standardize categorical fields
* Create derived fields such as session duration and activity flags

### Python

* Validate data consistency
* Identify outliers in watch time
* Generate summary statistics for sanity checks

---

## 8. Exploratory Data Analysis (EDA) Plan

### Engagement Analysis

* Distribution of watch time per user
* Session frequency patterns
* Content completion behavior

### Retention Analysis

* Repeat users vs one-time users
* Retention trends over time
* Subscription duration patterns

### Content Impact Analysis

* Engagement by genre
* Movie vs series comparison
* Content longevity trends

### Time-Based Analysis

* Hourly viewing behavior
* Weekday vs weekend engagement
* Monthly and seasonal trends

---

## 9. Key Metrics Framework

### Engagement Metrics

* Average watch time per user
* Sessions per user
* Completion rate
* Daily and monthly active users

### Retention Metrics

* User retention rate
* Repeat viewership ratio
* Subscription renewal rate
* Churn percentage

---

## 10. SQL Usage (Research Scope)

SQL will serve as the primary data processing layer:

* Integrating multiple data sources
* Aggregating engagement and retention metrics
* Creating analysis-ready tables for Python and Power BI

---

## 11. Python Usage (EDA Only)

Python will be used strictly for exploratory analysis:

* Data profiling and distribution checks
* Trend visualization
* Anomaly detection

No predictive or machine learning models will be applied.

---

## 12. Power BI Dashboard Design (Research Level)

### Planned Dashboard Pages

#### Executive Overview

* Total users
* Active users
* Average watch time
* Retention rate

#### User Engagement Dashboard

* Watch time trends
* Sessions per user
* Engagement by content type

#### Retention Dashboard

* Repeat vs churned users
* Retention trends over time
* Subscription duration analysis

#### Content Impact Dashboard

* Genre-wise engagement
* Movie vs series performance

### Design Principles

* Business-focused KPIs
* Clean and minimal visuals
* Interactive filters and slicers
* Drill-down and drill-through functionality

---

## 13. Expected Dashboard Insights

The dashboard is expected to provide insights into:

* Engagement health of the platform
* Behavioral differences between retained and churned users
* Content types that drive long-term engagement
* Time periods with peak and low activity

---

## 14. Recommendation Framework

### Content Strategy

* Focus on genres with high retention
* Promote series content to encourage repeat viewing

### User Engagement Strategy

* Improve onboarding for low-engagement users
* Highlight popular content during peak viewing hours

### Subscription Strategy

* Optimize plans based on engagement behavior
* Introduce loyalty incentives for long-term users

---

## 15. Final Deliverables

* End-to-end research documentation
* Data collection and cleaning framework
* EDA and metrics design
* Power BI dashboard blueprint
* Business recommendation roadmap


