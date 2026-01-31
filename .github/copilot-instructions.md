# Copilot Instructions for OTT User Engagement & Retention Analysis

## Project Overview

This is a **pure analytics project** analyzing user engagement and retention on an OTT streaming platform. It combines **Excel, SQL, Python, and Power BI** to transform raw user activity data into actionable business insights. **No machine learning or predictive modeling** is used—focus is on descriptive and diagnostic analytics.

## Core Architecture & Data Model

### Multi-Source Data Integration
The project integrates 5 interconnected CSV data sources centered on user profiles:

- **`All_Profiles.csv`**: Master profile/user table with metadata (creation date, language, maturity level, streaming quality, profile locks, auto-playback settings)
- **`All_ViewingActivity.csv`**: Core engagement data (9,994 records) with start time, duration, content title, device type, device bookmarks, and country
- **`All_Devices.csv`**: Device-level playback tracking (account-level and profile-level playback dates, deactivation status)
- **`All_Clickstream.csv`**: Navigation behavior (12,106 records) showing user clicks across navigation levels (browseTitles, movieDetails, signupPrompt) with timestamps
- **`All_SearchHistory.csv`**: Search behavior (2,618 records) including device type, search queries, displayed content, and actions (play, select)

**Key Pattern**: Analyses join on `Profile Name` as the common identifier. Data spans April 2021 to November 2022.

### Critical Dimensions for Analysis
- **Temporal**: All analyses use timestamp columns (Start Time, Click Utc Ts, Utc Timestamp) for cohort analysis and retention trends
- **Content**: Use `Title` field from ViewingActivity for genre/content performance analysis
- **Device**: `Device Type` appears consistently across ViewingActivity, Clickstream, and Devices tables—key for engagement segmentation
- **Geography**: `Country` field enables regional retention analysis
- **Behavioral State**: Profile creation dates enable cohort analysis; deactivation times in Devices table identify churned users

## Key Questions the Analytics Should Answer

The project's core questions drive all SQL queries and EDA:
1. How frequently do users return to the platform? (Session frequency)
2. Average watch time per user? (Engagement depth)
3. Which genres/content drive higher engagement? (Content performance)
4. How does engagement differ between retained and churned users?
5. When and why do users stop watching? (Churn timing)

## Workflow & Tools

### 1. Data Cleaning & Inspection (Excel, Python)
- Validate timestamps, handle missing values, remove duplicates
- Verify Profile Name consistency across all 5 tables (primary key)
- Check data type conversions (dates, durations in HH:MM:SS format)
- No script files exist yet; future Python scripts should use **pandas for data cleaning** and **csv reading**

### 2. SQL Analysis Phase
- **Expected location**: SQL scripts not yet created—future scripts should query this CSV-based structure
- **Pattern**: SQL queries should aggregate at user level for retention metrics, use window functions for cohort analysis
- Example metrics to compute:
  - `MAU/DAU` = Count distinct profiles per month/day from ViewingActivity
  - `Retention Rate` = Returned users in Month N / Users in Month N-1
  - `Churn Detection` = Profiles with no activity for 30+ days

### 3. Power BI Dashboard Phase
- Visualizations not yet built; design should include:
  - User engagement KPIs (DAU/MAU, watch time trends)
  - Retention cohort tables
  - Content performance (title-level watch counts, completion rates)
  - Device/geography breakdowns
  - Churn risk segmentation

### 4. Business Insights & Recommendations
- Document findings in analysis reports
- Focus on actionable insights: which content to promote, high-risk churn segments, device preference patterns

## Project-Specific Patterns & Conventions

### Data Timestamp Handling
- ViewingActivity uses `Start Time` (format: YYYY-MM-DD HH:MM:SS)
- Clickstream and SearchHistory use UTC timestamps (format: YYYY-MM-DD HH:MM:SS, sometimes with Ts suffix)
- Device table uses ISO format timestamps (YYYY-MM-DDTHH:MM:SS.sssZ)
- **Convention**: Normalize all to YYYY-MM-DD HH:MM:SS for consistency

### Duration/Time Values
- ViewingActivity stores `Duration` in HH:MM:SS format (e.g., "00:09:39" = 9 minutes 39 seconds)
- Bookmark columns in ViewingActivity show playback position (also HH:MM:SS format)
- **Pattern**: Convert to total seconds for numeric analysis; always document the original format

### Profile Name Identifier
- All tables use `Profile Name` as the unique user identifier (User 0, User 1, etc.)
- **Critical**: This is the primary join key across all 5 tables
- Profile creation dates in All_Profiles enable cohort analysis

### Data Volume Awareness
- ViewingActivity: 9,994 rows (largest engagement dataset)
- Clickstream: 12,106 rows (navigation data, often sparser per user)
- SearchHistory: 2,618 rows (search-specific interactions)
- Profiles: ~11 rows (small master table)
- Devices: ~139 rows (device registry, many-to-many with profiles)

### Engagement Metrics Hierarchy
1. **Activity Level**: Any content play = engaged user
2. **Depth**: Total watch time and session count per user
3. **Retention**: User returns in subsequent months (cohort-based)
4. **Content Affinity**: Specific titles watched per user
5. **Navigation Behavior**: Clicks before play (measured in Clickstream)

## Critical Developer Notes

### Before Starting Analysis
1. Inspect all 5 CSV files for missing values in key columns (Profile Name, timestamps, Title)
2. Verify all profiles in ViewingActivity exist in Profiles table (data integrity check)
3. Understand date range coverage: April 2021 to November 2022 (7 months of data)
4. Check for duplicate entries (especially in ViewingActivity with same Profile/Title/StartTime)

### When Writing Queries (SQL/Python)
- **Always** aggregate at the Profile level first (distinct profiles, sum watch time, count sessions)
- Use window functions for retention cohorts: `ROW_NUMBER() OVER (PARTITION BY Profile Name ORDER BY Date)`
- Filter by Deactivation Time in Devices table to identify active vs. churned users
- Join on Profile Name carefully; some profiles may not appear in all tables

### Common Pitfalls
- Clickstream and SearchHistory are much sparser than ViewingActivity; not all profiles will have these behaviors
- Device table can have multiple device rows per profile (account-level vs. profile-level playback dates)
- Duration field requires time-to-seconds conversion for numeric calculations
- Be careful with timezone handling; ensure all timestamp columns are normalized to single timezone

## File Organization & Key References

```
├── README.md                          # Project overview & goals
├── Idea.md                            # Detailed problem statement & project rationale
├── data/
│   ├── All_ViewingActivity.csv        # Primary engagement data (~10K rows)
│   ├── All_Profiles.csv               # User master table (~11 rows)
│   ├── All_Devices.csv                # Device tracking (~139 rows)
│   ├── All_Clickstream.csv            # Navigation behavior (~12K rows)
│   └── All_SearchHistory.csv          # Search interaction (~2.6K rows)
└── .github/copilot-instructions.md    # This file
```

## Next Steps for AI Agents

1. **Exploration**: Read `All_Profiles.csv` and sample 50 rows from ViewingActivity to understand user base
2. **Validation**: Verify referential integrity (all profiles in ViewingActivity exist in Profiles)
3. **Cleaning**: Identify missing values, duplicates, and data type issues
4. **Analysis Foundation**: Create user-level engagement summary (total watch time, session count, date range per profile)
5. **Retention Framework**: Build cohort tables showing user retention month-over-month
