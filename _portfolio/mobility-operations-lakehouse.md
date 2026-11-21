---
title: "Mobility Operations Lakehouse"
order: 0
excerpt: "Built a seven-task Databricks batch pipeline with PySpark and Delta Lake. Validated 29,936 synthetic trip requests across citywide and pickup-zone reporting."
---

![Databricks Jobs](https://img.shields.io/badge/Databricks%20Jobs-B92718?style=for-the-badge&logo=databricks&logoColor=white)
![PySpark](https://img.shields.io/badge/PySpark-A34013?style=for-the-badge&logo=apachespark&logoColor=white)
![Delta Lake](https://img.shields.io/badge/%CE%94%20Delta%20Lake-006B77?style=for-the-badge)

I built a batch lakehouse in Databricks to answer two questions about a synthetic ride-hailing system. When was demand high relative to citywide driver availability? Which pickup zones saw the most requests and longest waits?

## From raw files to dashboard

| Layer | What I built |
| --- | --- |
| Bronze | Loaded five CSVs into Delta tables using explicit schemas. Recorded the source file, ingestion time, and batch ID. |
| Silver | Used PySpark to deduplicate trips, quarantine invalid records, and prepare reference tables. Used Delta MERGE to update location and driver-availability records by business key. |
| Gold | Built two hourly reporting tables and validated the stored outputs before dashboard use. |

I orchestrated ingestion, transformations, and validation as seven dependent notebook tasks in Databricks Jobs.

## Why I built two Gold tables

The driver-availability feed provided one record per citywide hour. Trip demand could be grouped by pickup zone and hour. Joining citywide supply directly to each zone would repeat the same driver counts across zones, so I kept two outputs at different levels of detail.

- **Citywide hour** for trip demand, driver availability, and utilization.
- **Pickup zone and hour** for requests, cancellations, and rider wait times.

This design supports comparisons across pickup zones and analysis of citywide capacity. Estimating driver shortages by zone would require location-level supply data.

## What I verified

- The seven-task Databricks job completed in **5 minutes 28 seconds** in the recorded run.
- Both Gold tables reconciled to **29,936 synthetic trip requests** from Silver. The citywide join preserved the source total for summed hourly active-driver counts.
- Publish checks passed for unique, non-null keys, nonnegative measures, and valid utilization rates.
- Rerunning the Silver upserts with the same data preserved the location and driver-availability row counts.
