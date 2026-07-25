# Porter Delivery Operations Analysis using Python

## Project Overview

This project analyzes Porter delivery operations using Python to identify delivery delay patterns, SLA breaches, operational bottlenecks, and practical business recommendations.

The main goal is to use Python for business problem solving, KPI analysis, segmentation, visual exploration, and scenario-based recommendations.

## Business Problem

Porter works with restaurants and delivery partners to complete customer orders. Late deliveries can reduce customer satisfaction, increase customer complaints, create pressure on delivery partners, and affect operational efficiency.

The business problem is:

> How can Porter identify the major drivers of delayed deliveries and improve delivery reliability using order, restaurant, time, and delivery partner data?

## Business Questions

This project answers the following questions:

1. What is the typical delivery time?
2. What percentage of orders breach 45-minute and 60-minute delivery thresholds?
3. Which days and hours create the highest delivery pressure?
4. Which markets, order protocols, and food categories have higher delay risk?
5. Are partner availability and outstanding orders connected with longer delivery time?
6. Which segments contribute the highest number of delayed orders?
7. What operational actions can reduce delayed deliveries?

## Dataset

The analysis uses the provided dataset:

- `Porter_Dataset.csv`

Dataset size before cleaning:

- Rows: `197,428`
- Columns: `14`

Dataset size after delivery duration cleaning:

- Rows used for main analysis: `196,304`

Rows removed during delivery duration cleaning:

- Orders below 10 minutes: `27`
- Orders above 120 minutes: `1,090`

These extreme delivery durations were removed from the main analysis because they may represent timestamp issues or rare operational exceptions that can distort normal delivery performance.

## Tools Used

- Python
- pandas
- numpy
- matplotlib
- seaborn
- Jupyter Notebook

## Project Files

| File | Description |
|---|---|
| `Porter_Dataset.csv` | Original dataset used for analysis |
| `python_business_analysis.ipynb` | Main improved Python business analysis notebook |
| `README.md` | Project documentation |

## KPI Framework

The project does not depend only on average delivery time. The following KPIs are used to measure delivery performance more practically:

| KPI | Meaning |
|---|---|
| Average Delivery Time | Overall delivery speed |
| Median Delivery Time | Typical customer delivery experience |
| P90 Delivery Time | Delivery time for the slowest 10% of orders |
| P95 Delivery Time | Delivery time for the slowest 5% of orders |
| 45-Minute SLA Breach Rate | Percentage of orders taking more than 45 minutes |
| 60-Minute SLA Breach Rate | Percentage of orders taking more than 60 minutes |
| Partner Utilization | Busy partners divided by on-shift partners |
| Available Partner Ratio | Spare partner capacity available during order time |
| Outstanding Orders per Partner | Operational workload pressure |

## Overall Delivery Performance

| Metric | Value |
|---|---:|
| Total cleaned orders analyzed | `196,304` |
| Average delivery time | `47.10 minutes` |
| Median delivery time | `44.22 minutes` |
| P90 delivery time | `69.83 minutes` |
| P95 delivery time | `79.65 minutes` |
| 45-minute SLA breach rate | `47.99%` |
| 60-minute SLA breach rate | `19.43%` |

### Interpretation

Almost half of the orders take more than 45 minutes. This shows that delivery reliability is a major operational issue. The P90 delivery time is close to 70 minutes, which means the slowest 10% of customers experience a much worse delivery time than the average suggests.

## Methodology

The notebook follows this analysis flow:

1. Business context and problem framing
2. Dataset loading and basic inspection
3. Missing value and data quality checks
4. Timestamp conversion and delivery duration creation
5. Feature engineering for time, partner availability, utilization, and workload
6. Delivery duration cleaning
7. KPI framework creation
8. Demand pattern analysis
9. SLA breach analysis
10. Market, protocol, and category segmentation
11. Partner availability and operational load analysis
12. Order complexity analysis
13. Delay contribution analysis
14. Delay impact matrix
15. Root-cause style summary
16. Scenario simulation
17. Final business recommendations

## Key Insights

### 1. Weekend Demand Is Highest

The highest order volume happens on weekends:

| Day | Orders |
|---|---:|
| Saturday | `34,370` |
| Sunday | `33,457` |
| Friday | `27,806` |

Saturday and Sunday are the busiest days, which means partner planning and restaurant readiness should be stronger around weekends.

### 2. Saturday and Monday Have the Worst Delivery Performance

| Day | Average Delivery Time | P90 Delivery Time | 45-Min SLA Breach Rate |
|---|---:|---:|---:|
| Saturday | `49.59 min` | `72.75 min` | `54.92%` |
| Monday | `50.19 min` | `77.49 min` | `53.47%` |
| Sunday | `47.99 min` | `70.64 min` | `50.56%` |

Monday has the highest average and P90 delivery time, while Saturday has the highest order volume and the highest SLA breach rate among major days.

### 3. Late Night Orders Create the Largest Delay Burden

| Time Period | Orders | Average Delivery Time | 45-Min SLA Breach Rate | Delay Contribution |
|---|---:|---:|---:|---:|
| Late Night | `119,343` | `49.86 min` | `55.32%` | `70.09%` |
| Evening | `39,579` | `44.22 min` | `40.52%` | `17.02%` |
| Night | `28,323` | `41.58 min` | `32.94%` | `9.90%` |
| Morning | `8,498` | `39.97 min` | `29.36%` | `2.65%` |
| Afternoon | `561` | `51.13 min` | `55.61%` | `0.33%` |

Late Night contributes around 70% of delayed orders above 45 minutes. This is the most important operational window for improvement.

### 4. Market 1 Has the Weakest Delivery Performance

| Market | Orders | Average Delivery Time | 45-Min SLA Breach Rate |
|---|---:|---:|---:|
| Market 1 | `37,628` | `50.28 min` | `53.74%` |
| Market 4 | `47,392` | `46.79 min` | `48.24%` |
| Market 3 | `23,152` | `47.03 min` | `47.32%` |
| Market 6 | `14,374` | `46.68 min` | `46.31%` |
| Market 2 | `54,862` | `45.69 min` | `45.28%` |

Market 1 has the highest SLA breach rate and highest average delivery time. It should be investigated for local operational issues such as partner availability, restaurant delays, geography, or demand concentration.

### 5. Order Protocol 6 Performs Poorly

| Order Protocol | Orders | Average Delivery Time | 45-Min SLA Breach Rate |
|---|---:|---:|---:|
| Protocol 6 | `782` | `58.92 min` | `73.15%` |
| Protocol 1 | `54,383` | `49.31 min` | `53.52%` |
| Protocol 4 | `19,161` | `47.41 min` | `47.67%` |
| Protocol 2 | `23,903` | `46.72 min` | `47.25%` |
| Protocol 3 | `52,982` | `46.41 min` | `46.53%` |

Protocol 6 has low volume but very poor performance. It should be checked for process issues, manual steps, restaurant-side dependency, or legacy ordering flow.

### 6. Some Categories Have High Delay Rates

Among categories with at least 500 orders, the highest SLA breach rates are:

| Store Category | Orders | Delayed Orders | Average Delivery Time | 45-Min SLA Breach Rate |
|---|---:|---:|---:|---:|
| Burmese | `817` | `495` | `51.23 min` | `60.59%` |
| Steak | `1,088` | `648` | `51.27 min` | `59.56%` |
| Sushi | `2,171` | `1,260` | `50.77 min` | `58.04%` |
| Japanese | `9,106` | `5,210` | `51.12 min` | `57.22%` |
| Italian | `7,145` | `4,023` | `49.83 min` | `56.31%` |
| Pizza | `17,212` | `9,661` | `50.24 min` | `56.13%` |

High delay rate categories may involve longer preparation time, packaging complexity, or peak demand concentration.

### 7. Delay Contribution Is More Important Than Delay Rate Alone

The categories contributing the highest number of delayed orders are:

| Store Category | Orders | Delayed Orders | 45-Min SLA Breach Rate |
|---|---:|---:|---:|
| Pizza | `17,212` | `9,661` | `56.13%` |
| American | `19,286` | `9,248` | `47.95%` |
| Mexican | `17,038` | `6,897` | `40.48%` |
| Japanese | `9,106` | `5,210` | `57.22%` |
| Burger | `10,902` | `5,089` | `46.68%` |

Pizza is a major priority because it has both high volume and high delay contribution.

## Scenario Simulation

The notebook includes simple business simulations to estimate possible impact from operational improvements.

Examples:

1. Reduce late-night SLA breach rate by 10% relative.
2. Improve the worst-performing order protocol to the overall average breach rate.
3. Reduce the breach rate of the highest delay-contributing category by 10% relative.

These are not machine learning forecasts. They are business simulations used to estimate the possible number of delayed orders avoided under improvement assumptions.

## Business Recommendations

### 1. Improve Late-Night Partner Planning

Late Night orders contribute around `70.09%` of all delayed orders. Porter should improve partner availability, dispatch planning, and restaurant coordination during this window.

Priority: High

### 2. Investigate Market 1

Market 1 has the highest average delivery time and highest SLA breach rate among major markets. This market should be reviewed for local operational bottlenecks.

Priority: High

### 3. Review Protocol 6

Protocol 6 has a `73.15%` 45-minute SLA breach rate. Even though the order volume is small, the performance gap is large and may indicate a process issue.

Priority: High

### 4. Focus on High-Impact Categories

Pizza, American, Mexican, Japanese, and Burger categories contribute many delayed orders. Operational improvements in these categories can create larger business impact than focusing only on low-volume categories with high delay rates.

Priority: High

### 5. Track P90 Delivery Time and SLA Breach Rate Weekly

Average delivery time alone hides poor customer experience. Porter should track P90 delivery time and SLA breach rate along with average delivery time.

Priority: Medium

### 6. Monitor Partner Utilization and Outstanding Orders

Partner utilization and outstanding order pressure should be monitored as operational warning signals. These metrics can help identify periods where delays may increase.

Priority: Medium

## Final Conclusion

The analysis shows that Porter has a delivery reliability issue, with `47.99%` of cleaned orders taking more than 45 minutes. The largest delay burden comes from Late Night orders, Saturday/Monday operations, Market 1, Protocol 6, and high-volume food categories such as Pizza and American.

The most practical business opportunity is to reduce SLA breaches in the segments that contribute the largest number of delayed orders, not only the segments with the highest average delivery time.

## How to Run This Project

1. Clone or download this repository.
2. Make sure `Porter_Dataset.csv` is in the same folder as the notebook.
3. Open `porter_python_business_analysis.ipynb` in Jupyter Notebook or VS Code.
4. Run the cells from top to bottom.
5. Review the KPI tables, charts, delay contribution analysis, and recommendations.

## Resume-Friendly Project Title

**Porter Delivery Operations Analysis using Python**

## Suggested Resume Bullets

- Analyzed `196K+` delivery orders using Python to identify SLA breach patterns across time, market, order protocol, food category, and partner availability.
- Built operational KPIs including average delivery time, P90 delivery time, SLA breach rate, partner utilization, and outstanding orders per partner.
- Performed delay contribution and impact matrix analysis to identify high-volume, high-delay segments for operational prioritization.
- Created scenario simulations to estimate potential delayed-order reduction from late-night staffing, protocol improvement, and category-level operational actions.
