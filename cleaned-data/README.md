cleaned-data — Ready-to-use datasets for OTT engagement analysis

This folder contains cleaned, analysis-ready CSVs produced from the OTT source files.

Files included

- ott_viewing_activity_cleaned.csv — 9,992 rows. Fields include: `Profile Name`, `Start Time` (YYYY-MM-DD HH:MM:SS), `Duration` (original HH:MM:SS), `Duration_Seconds`, `Duration_Minutes`, `Title`, `Title_Genre` (inferred), `Device Type`, `Bookmark`, `Latest Bookmark`, `Country`, `Country_Iso`.
- ott_devices_cleaned.csv — 137 rows. Device-level playback dates normalized to YYYY-MM-DD HH:MM:SS; includes `Deactivation Time`.
- ott_clickstream_cleaned.csv — 12,104 rows. Navigation events with `Click Utc Ts` normalized.
- ott_searchhistory_cleaned.csv — 2,616 rows. Search events with `Utc Timestamp` normalized and `Country_Iso`.
- profiles_cleaned.csv — 9 rows. Original profile metadata plus synthetic `Subscription_Type`, `Age`, `Age_Group` (generated to enable subscription/age segmenting when needed).
- user_engagement_summary.csv — 9 rows. One row per `Profile Name` with aggregated metrics: `total_watch_seconds`, `sessions_count`, `avg_session_seconds`, `unique_titles`, `first_activity`, `last_activity`, `days_active`, `device_types_used`, `country_iso`, `Deactivation Time`, `deactivated`, `Subscription_Type`, `Age`, `Age_Group`.
- column-description.md — brief column descriptions.

Notes & assumptions

- `Subscription_Type`, `Age`, `Age_Group` were synthesized because the OTT tables lack subscription/demographic data. Treat them as synthetic for segmentation only; do not represent real user attributes.
- `Title_Genre` is inferred heuristically from title text (coarse). Use external genre mapping for production-grade genre analysis.
- `Clickstream` coverage starts July 2022; funnel/navigation analyses should be scoped to Jul 2022–Jun 2023.
- `netflix_users.csv` is not merged (incompatible key and timeframe).

Quick examples

Load files in Python (pandas):

```python
import pandas as pd
base = 'cleaned-data'
viewing = pd.read_csv(f'{base}/ott_viewing_activity_cleaned.csv', parse_dates=['Start Time'])
devices = pd.read_csv(f'{base}/ott_devices_cleaned.csv', parse_dates=['Acct First Playback Date','Acct Last Playback Date','Profile First Playback Date','Profile Last Playback Date','Deactivation Time'], keep_default_na=False)
profiles = pd.read_csv(f'{base}/profiles_cleaned.csv')
summary = pd.read_csv(f'{base}/user_engagement_summary.csv', parse_dates=['first_activity','last_activity'])

# Example: top 5 profiles by total watch time
print(summary.sort_values('total_watch_seconds', ascending=False).head())
```

If you want, I can:
- Replace synthetic `Subscription_Type` with a specific distribution
- Improve `Title_Genre` mapping using a small manual lookup
- Export a sample Power BI starter `.pbix` data model (requires Power BI Desktop)

