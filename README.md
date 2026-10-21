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



### Destination Popularity and Data Sparsity

The dataset contains 39,901 distinct destination city identifiers across 217,686 unique trips.

The most frequently booked destination, City ID 23921, appears in 8,205 trips, representing 3.769% of all transactions.

The city frequency distribution is highly sparse:

- 12,349 cities (30.9%) appear in only one trip.
- 30,605 cities (76.7%) appear in fewer than ten trips.
- The most popular destination appears in approximately 3.77% of transactions.

These findings indicate a pronounced long-tail distribution in destination popularity, presenting challenges for frequent itemset discovery.

### Frequent Itemset Mining

An initial minimum support threshold of 0.1% (218 trips) was selected to explore frequent individual cities and city pairs.

The analysis uses PySpark DataFrame transformations compatible with Databricks Free Edition.

Cities that fail to meet the minimum support threshold are excluded from candidate pair generation. Pair support is calculated relative to all 217,686 original transactions.

The resulting itemsets and threshold sensitivity will be evaluated before association rules are generated.


### Frequent City Combinations

Using a minimum support threshold of 0.1%, the analysis identified **969 frequent city pairs** across 217,686 unique trip transactions.

The most frequent combination was City 55128 and City 64876, which appeared together in 4,022 trips (1.848% support).

### Preliminary Association Insight

For the rule **City 55128 → City 64876**:

- Support: 1.85%
- Confidence: 55.76%
- Lift: 17.97

The high lift indicates that these destinations co-occur much more frequently than would be expected from their individual booking frequencies under an independence assumption.

These patterns could help identify candidates for personalized recommendations or destination bundles. However, the findings do not establish causal relationships or prove that these recommendations would increase bookings.

### Association Rule Evaluation

The analysis generated directional association rules from frequent city pairs identified using a minimum support threshold of 0.1%.

Rules were evaluated using three metrics:

- **Support:** Proportion of trips containing both destinations.
- **Confidence:** Conditional probability that the consequent city is included when the antecedent city is present.
- **Lift:** Strength of the association relative to the consequent city's overall frequency.

Initial rule-selection thresholds were set at 20% minimum confidence and 1.2 minimum lift.

Rules were ranked separately by co-booking frequency and lift to assess both their observed frequency and association strength.

The next stage evaluates three selected rules and discusses potential applications in travel recommendations, destination bundles, and personalized marketing.

## 8. Business Insights and Recommendations

### Insight 1 — Destination Recommendation

**Rule: City 64876 → City 55128**

- Co-occurring trips: 4,022
- Confidence: 59.5%
- Lift: 17.97

Approximately 59.5% of trips containing City 64876 also contain City 55128.

**Business recommendation:** A travel platform could test recommending City 55128 to customers planning trips that include City 64876.

### Insight 2 — Travel Package Bundling

**Rule: City 18417 → City 66648**

- Co-occurring trips: 3,174
- Confidence: 80.6%
- Lift: 30.29

The high confidence indicates that these destinations frequently occur together within trips containing City 18417.

**Business recommendation:** Explore combined travel packages featuring both destinations and test their commercial appeal.

### Insight 3 — Targeted Personalization

**Rule: City 36020 → City 45025**

- Co-occurring trips: 236
- Confidence: 95.9%
- Lift: 513.11

This rule exhibits an exceptionally high lift and confidence. However, its relatively low support of approximately 0.11% limits its potential reach and warrants additional validation.

**Business recommendation:** Investigate this highly specific travel pattern as a candidate for targeted recommendations rather than mass-market campaigns.

### Analytical Limitations

Association rules identify co-occurrence, not causality or travel sequence.

The analysis uses anonymized city identifiers, preventing direct geographical interpretation without a city reference table.

The historical dataset covers 2015–2017, and discovered patterns may not reflect current travel behavior.

Recommendations should be evaluated using more recent data and controlled experiments before deployment.
