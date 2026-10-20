# Multi-City Travel Booking Affinity Analysis
Travel booking affinity analysis using Databricks and PySpark


**Status:** In Progress  
**Project Type:** Academic Data Analytics & Portfolio Project  
**Platform:** Databricks Free Edition

## 1. Project Overview

This project investigates patterns in multi-city travel bookings using affinity analysis and association rule mining.

The objective is to identify destination cities that frequently appear together within individual trips and explore how these patterns could support travel recommendations, marketing, and personalization.

## 2. Business Question

Which destination cities are frequently booked together, and how can these relationships inform business decisions?

## 3. Project Objectives

- Prepare and validate travel-booking records.
- Group unique destination cities by trip ID.
- Explore trip sizes and city popularity.
- Identify frequent city combinations.
- Calculate support, confidence, and lift.
- Interpret association rules in a business context.
- Evaluate limitations and potential applications.

## 4. Tools and Technologies

- Databricks Free Edition
- Python and PySpark
- Spark SQL
- Matplotlib (visualization)
- Git and GitHub

## 5. Analytical Methodology

Each `utrip_id` represents one transaction, and its distinct `city_id` values represent the items in that transaction.

Frequent itemsets and association rules will be calculated using Spark-based data transformations compatible with Databricks serverless compute.

## Exploratory Data Analysis

### Trip-Size Distribution

The first exploratory analysis examines the distribution of unique destination cities per trip.

The analysis distinguishes between single-city and multi-city trips to evaluate the suitability of the dataset for association rule mining.

**Methodology:**
- Group booking records using `utrip_id`.
- Count distinct `city_id` values per transaction.
- Calculate descriptive trip-size statistics.
- Visualize the distribution of cities per trip.

**Findings:** Pending validation of the analytical results.

Additional exploratory analysis will examine destination popularity and potential data sparsity.

### Initial Data Quality and Exploratory Findings

The analysis examined 1,166,835 booking records, representing 217,686 unique trips and 39,901 distinct destination city identifiers.

**Data quality:** No missing values were identified in the nine dataset columns. Initial validation also found no missing or blank trip identifiers, missing city identifiers, or checkout dates preceding check-in dates.

**Trip characteristics:**
- Average unique cities per trip: 4.75
- Minimum unique cities: 1
- Maximum unique cities: 39
- Multi-city trips: 212,661 (97.7%)
- Single-city trips: 5,025 (2.3%)

**Preliminary interpretation:**

The distribution of trip sizes peaks at four distinct cities. Most trips contain multiple destinations, providing a substantial transaction base for identifying co-occurring cities.

However, the large number of distinct destination identifiers may lead to sparse city combinations. Further analysis of city popularity and itemset frequency is required before selecting appropriate support thresholds.

These findings describe historical booking patterns and do not establish causation or destination-visit order.

## 6. Project Progress

- [X] Data ingestion and validation
- [X] Transaction preparation
- [ ] Exploratory data analysis
- [ ] Frequent itemset discovery
- [ ] Association rule analysis
- [ ] Business interpretation
- [ ] Final documentation

## 7. Dataset

The dataset contains travel-booking records, including trip identifiers, destination city identifiers, booking dates, traveler countries, and booking channels.

**Dataset source:** To be verified.

The original CSV is not included in this repository. Reproduction instructions and data requirements will be documented.

## 8. Results and Business Recommendations

This section will be completed after the analysis.

## 9. Limitations

Potential limitations include popularity bias, data sparsity, low-frequency destination combinations, and the fact that association does not establish causation.
