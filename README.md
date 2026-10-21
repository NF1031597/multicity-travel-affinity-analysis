Multi-City Travel Booking Affinity Analysis
Databricks Free Edition | PySpark | Python | Association Rules | Git & GitHub
A reproducible exploratory analysis of historical multi-city booking patterns, using trip-level transactions to identify frequently co-booked destinations and evaluate opportunities for travel recommendations.

[**View the Databricks notebook**](Multicity_Booking_Project.ipynb)
Business question
Which destination cities tend to appear together within the same trip, and how might those patterns inform recommendations, travel packages, or personalized marketing?

This project examines co-occurrence, not travel order or causation. The findings describe historical booking behavior; proposed applications have not been commercially tested.
Dataset and scope
Attribute	Observed value
Booking-level records	1,166,835
Unique trips (utrip_id)	217,686
Distinct destinations (city_id)	39,901
Average unique cities per trip	4.75
Multi-city trips	212,661 (97.7%)
Date coverage	December 31, 2015 – February 28, 2017


The dataset includes user_id, checkin, checkout, city_id, device_class, affiliate_id, booker_country, hotel_country, and utrip_id. Each distinct utrip_id is treated as one transaction, containing the set of distinct city_id values booked within that trip. Repeated appearances of a city within the same trip count only once.

The original CSV is not distributed in this repository. Its original source and redistribution license still need confirmation. City identifiers have not been mapped to geographic names.
Methods
1. Data ingestion and checks: Read booking records in Databricks; inspect schema, missing values, trip IDs, city IDs, and date order. No missing values were found in the nine columns, and the targeted ID/date-order checks returned zero violations.
2. Transaction preparation: Group by utrip_id, applying collect_set(city_id) and sorting each basket.
3. Exploratory analysis: Study trip-size distribution, city popularity, and the long tail of infrequent destinations.
4. Frequent itemset mining: Calculate 1- and 2-city frequencies using PySpark DataFrame operations. Generate candidate three-city combinations only when all their constituent pairs are frequent (Apriori-style pruning), then validate their trip counts.
5. Association rules: Calculate both directions of each frequent city pair; filter and rank rules by confidence, lift, and observed frequency.
6. Business interpretation: Evaluate three representative rules and propose testable use cases.
The implementation uses PySpark DataFrame transformations compatible with Databricks Free Edition serverless, without relying on its unsupported Spark ML FP-Growth model.
Measures and thresholds
For destination set A and destination B, with N total trips:
- Support: support(A → B) = trips containing A and B / N
- Confidence: confidence(A → B) = trips containing A and B / trips containing A
- Lift: lift(A → B) = confidence(A → B) / support(B)
Parameters in the reported experiment:
Parameter	Value
Minimum itemset support	0.1% (at least 218 trips)
Minimum rule confidence	20%
Minimum rule lift	1.2
Support denominator	All 217,686 trips


A low support threshold was chosen for exploratory analysis because destination frequencies are sparse. These are selection thresholds, not evidence that every retained rule has predictive or commercial value.
Key results
Result	Count
Frequent individual cities	815
Frequent city pairs	969
Candidate three-city itemsets	1,092
Frequent three-city itemsets	405
Directional pair-based rules before filtering	1,938
Rules meeting confidence and lift thresholds	1,299


Destination concentration: City 23921 appeared in 8,205 trips (3.769% support). Among all 39,901 destination IDs, 12,349 (30.9%) appeared in only one trip, and 30,605 (76.7%) appeared in fewer than ten trips. This long tail motivates careful support-threshold selection.

Most frequent city pair: 55128 + 64876 appeared together in 4,022 trips (1.848% support).

Most frequent city triple: 18417 + 30520 + 66648 appeared together in 2,571 trips (1.181% support).
Visualizations
Figure 1 — Unique destinations per trip

The distribution peaks at four distinct destination cities per trip. Only 5,025 trips (2.3%) contain a single city; nearly all trips can therefore contribute to city-to-city co-occurrence analysis.
Figure 2 — Most frequent destinations

Even the most popular individual city occurs in fewer than 4% of trips, consistent with a large and sparse set of destinations.
Figure 3 — Most frequent three-city combinations

The strongest three-city combination occurs in 2,571 trips, providing an additional perspective on destination clusters beyond city pairs.
Three business-oriented association insights
Directional rule	Co-occurring trips	Support	Confidence	Lift	Potential application
64876 → 55128	4,022	1.848%	59.5%	17.97	Test destination recommendations
18417 → 66648	3,174	1.458%	80.6%	30.29	Explore multi-destination bundles
36020 → 45025	236	0.108%	95.9%	513.11	Investigate narrowly targeted personalization


Interpretation: A higher lift means stronger co-occurrence relative to the consequent's background frequency, not necessarily greater business reach or incremental impact. For example, 36020 → 45025 has exceptionally high confidence and lift but only 236 observed co-occurrences. The highest-frequency rules may have broader reach; rare rules require additional stability checks. A/B tests and up-to-date data would be needed before deployment.
Reproducing the analysis
1. Obtain the original dataset through an authorized source. The CSV is not hosted in this repository.
2. Open Databricks Free Edition and upload the CSV to a Unity Catalog volume or accessible table.
3. Import or open [`Multicity_Booking_Project.ipynb`](Multicity_Booking_Project.ipynb).
4. In the first data-loading cell, replace the existing CSV/table location with your own Databricks path, for example /Volumes/<catalog>/<schema>/<volume>/multi_city_booking.csv.
5. Verify that checkin and checkout are parsed as dates and that the key columns match the names documented above.
6. Run the notebook from top to bottom. Compare the final audit counts with the table in this README.
The notebook uses the Spark DataFrame API, with small aggregated results collected to Python for plotting. Exact environment configuration and data access affect reproducibility; the underlying raw dataset is a required external input.
Limitations and possible extensions
- Anonymized destinations: Without a reliable city-ID lookup, geographic or tourism-route interpretations cannot be confirmed.
- Historical data: The observed patterns span 2015–2017 and may not reflect current behavior.
- Sparsity and selection: Most destinations occur rarely, and thresholds influence which rules are reported.
- Association is not causation: The rules do not establish visit sequence, underlying traveler motivation, or incremental recommendation effectiveness.
- Alternative aggregations: Grouping by hotel_country may yield more stable but less geographically specific rules; this has not been tested here.
- Segmentation: Comparing device_class or booker_country groups could reveal differences, but smaller samples may make some rules less stable; this is future work.
- Tourism vs. routing: The available fields cannot conclusively distinguish tourism preferences from transport connections or itinerary constraints.
Repository contents
multicity-travel-affinity-analysis/
├── Multicity_Booking_Project.ipynb
├── README.md
├── .gitignore
└── figures/
    ├── trip_size_distribution.png
    ├── top_15_destination_cities.png
    └── top_10_frequent_city_triples.png
Project type: Academic data analytics exercise extended into a GitHub portfolio case study. This repository contains analytical code and illustrations, not a deployed recommendation system.
