# Bike-Share-Analysis

## Table of Contents

- [Project Overview](#project-overview)
- [Data Source](#data-source)
- [Tools Used](#tools-used)
- [Data Cleaning/Preparation](#data-cleaning/preparation)
- [Data Analysis](#data-analysis)
- [Results/Findings](#results/findings)
- [Recommendations](Recommendations)

### Project Overview

The main goal of this project is to maximize the number of annual memberships by understanding the differences in usage patterns between casual riders and annual members. This report will provide data-driven insights to help design a marketing strategy to convert casual riders into annual members.

### Data Source

The data used for this analysis includes historical trip data from Cyclistic. The datasets are public data provided by Motivate International Inc. under a specific license. The data includes trip start and end times, trip duration, bike IDs, and user types (casual or member).

### Tools Used
- Google Spreadsheet- Data Cleaning and Visualization
- SQL- Data Cleaning and Analysis

### Data Cleaning/Preparation

In the data preparation phase we have done the following
- Remove Duplicate Records
- Handle Missing Values
- Standardize Data Formats
- Correct Data Types
- Remove Outliers
- Verify Data Consistency

### Defining the Problem

Three questions will guide the future marketing program

- How do annual members and casual riders use Cyclistic bikes differently
- Why would casual riders buy Cyclistic annual memberships
- How can Cyclistic use digital media to inuence casual riders to become members

### Main question to be answered in this analysis

How do annual members and casual riders use Cyclistic bikes differently

### Data Analysis

Some codes used

#### Count of Rides by Member Type

```sql
SELECT member_casual, COUNT(ride_id) AS ride_count
FROM `able-brace-422016-m0.trips_data.trips20`
GROUP BY member_casual;
```

#### Average Duration of Rides by Member Type

```sql
SELECT member_casual,
      AVG((ended_at) - (started_at)) AS avg_duration_days
FROM `able-brace-422016-m0.trips_data.trips20`
GROUP BY member_casual;
```

#### Most Popular Bike Type by Member TypeFindings

```sql
SELECT member_casual, rideable_type, COUNT(ride_id) AS ride_count
FROM `able-brace-422016-m0.trips_data.trips20`
GROUP BY member_casual, rideable_type
ORDER BY member_casual, ride_count DESC;
```

#### Ride Frequency by Day of the Week

```sql

SELECT member_casual,
      EXTRACT(DAYOFWEEK FROM started_at) AS day_of_week,  -- 1=Sunday, 2=Monday, ..., 7=Saturday
      COUNT(ride_id) AS ride_count
FROM `able-brace-422016-m0.trips_data.trips20`
GROUP BY member_casual, day_of_week
ORDER BY member_casual, day_of_week;
```

#### Ride Duration by Time of Day

```sql
SELECT member_casual,
      EXTRACT(HOUR FROM started_at) AS hour_of_day,
      AVG(TIMESTAMP_DIFF(ended_at, started_at, SECOND) / 3600) AS avg_duration_hours
FROM `able-brace-422016-m0.trips_data.trips20`
GROUP BY member_casual, hour_of_day
ORDER BY member_casual, hour_of_day;
```

### Results/Findings

Generally the analysis result shows as indicated below:
- Annual members use the bikes more frequently and for longer durations, indicating a likely reliance on bikes for commuting or daily use.
- Casual riders use the bikes less frequently but tend to ride more on weekends.
- Annual members show a consistent preference for certain bike types, while casual riders exhibit more variability.
- Annual members’ ride patterns align with traditional commuting hours, whereas casual riders use bikes more sporadically throughout the day.
- Certain stations are more popular among casual riders, indicating potential hotspots for targeted marketing campaigns.

### Recommendations

Based on the analysis, we highly recommend the following 

#### Targeted Marketing Campaigns:

- For Casual Riders: Promote bike usage during weekdays through targeted advertisements and incentives to encourage more frequent use.
- For Annual Members: Offer additional perks or rewards for maintaining high usage rates to enhance loyalty.

#### Service Enhancements:
- Bike Availability: Ensure that popular bike types are available in high-demand areas and during peak usage times.
- Station Placement: Optimize the placement of bike stations to cater to the higher usage on weekends and holidays for casual riders.

#### Operational Adjustments:
- Maintenance Schedule: Align bike maintenance schedules with peak usage times to minimize downtime and improve user experience.

#### User Engagement:
- Feedback Collection: Regularly collect feedback from both annual members and casual riders to refine bike services and address any issues.






