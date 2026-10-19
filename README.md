# multicity-travel-affinity-analysis
Travel booking affinity analysis using Databricks and PySpark
# Multi-City Travel Booking Affinity Analysis

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

## 6. Project Progress

- [ ] Data ingestion and validation
- [ ] Transaction preparation
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
