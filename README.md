# Geo-Targeted Ad Experiment

An A/B testing and product analytics project evaluating how geographic ad constraints affect user engagement, advertising inventory, and revenue on a local search platform.

Using R, this project analyzes 175,000 search observations from Yelp's Box Search Experiment. The analysis compares a treatment group that receives advertisements restricted to the visible map area with a control group that receives all otherwise relevant advertisements.

The results demonstrate an important product trade-off: stricter geographic targeting improves click-through rate among displayed ads, but substantially reduces ad availability and overall revenue.

---

## Project Overview

Advertising platforms must balance two competing goals:

- Show users highly relevant advertisements
- Maintain sufficient advertising inventory and revenue

In map-based search, an advertisement may be relevant to the user's search query but located outside the geographic area currently visible on the map.

This experiment evaluates whether restricting advertisements to businesses inside the map-defined area improves relevance and engagement enough to offset the resulting reduction in ad inventory.

The analysis examines the complete advertising funnel:

```text
Search
→ Eligible for Advertising
→ Advertisement Shown
→ Advertisement Clicked
→ Revenue Generated
```

---

## Business Question

The primary business question is:

> Should Yelp enforce strict geographic constraints so that map-search users only see advertisements located inside the visible map area?

The analysis evaluates whether the treatment:

- Improves click-through rate
- Changes advertising eligibility
- Reduces the probability that an advertisement is shown
- Affects revenue per click
- Affects revenue per eligible search
- Produces different effects for local and non-local service searches

---

## Experimental Design

### Control Group

Users in the control group can receive all relevant advertisements, including advertisements located outside the visible map-defined area.

### Treatment Group

Users in the treatment group only receive advertisements located inside the visible map-defined area.

### Hypothesis

```text
Enforcing geographic constraints will increase ad relevance
and improve user engagement.
```

### Expected Trade-Off

Stricter geographic targeting may improve the quality of displayed advertisements but reduce the number of advertisements available to show.

This creates a trade-off between:

```text
Ad relevance and engagement
versus
Ad inventory and revenue
```

---

## Dataset

The analysis uses:

```text
yelp_data.csv
```

The dataset contains:

```text
175,000 observations
8 variables
```

Each observation represents one Yelp search.

### Variables

| Variable | Description |
|---|---|
| `Treatment` | Indicates whether the search belongs to the treatment or control group |
| `Desktop` | Indicates whether the user accessed Yelp through desktop or mobile |
| `LocalService` | Indicates whether the search was for a local service or a non-local business |
| `Eligible` | Indicates whether the search was eligible to receive an advertisement |
| `AdShown` | Indicates whether an advertisement was shown |
| `AdClick` | Indicates whether the displayed advertisement was clicked |
| `Revenue` | Revenue generated from the search in USD |
| `Date` | Date on which the Yelp search occurred |

The original `Yelp.xlsx` workbook was used as reference material for the experiment description, data dictionary, and replication guidance. It is not included in this repository.

---

## Tools and Technologies

- R
- Jupyter Notebook
- tidyverse
- dplyr
- ggplot2
- readr
- tidyr
- A/B Testing
- Hypothesis Testing
- Funnel Analysis
- Two-Sample t-Tests
- Two-Proportion Tests
- Two-Way ANOVA
- Heterogeneous Treatment Effect Analysis
- Revenue Analytics

---

## Project Workflow

1. Import and validate the experimental dataset.
2. Conduct exploratory data analysis.
3. Compare treatment and control group assignment.
4. Analyze advertising eligibility rates.
5. Evaluate advertisement shown rates.
6. Compare click-through rates.
7. Analyze revenue outcomes.
8. Examine the full advertising conversion funnel.
9. Conduct local versus non-local subgroup analysis.
10. Perform statistical significance testing.
11. Evaluate treatment interactions using two-way ANOVA.
12. Develop product and experimentation recommendations.

---

## Exploratory Data Analysis

The dataset contains the following overall patterns:

| Characteristic | Share |
|---|---:|
| Local-service searches | Approximately 60% |
| Mobile searches | Approximately 70% |
| Searches eligible for ads | Approximately 95% |
| Eligible ads shown | Approximately 80% |
| Shown ads clicked | Approximately 64% |

### Revenue Distribution

The revenue distribution is approximately bimodal:

- A large concentration near `$0`, representing searches that did not generate a paid click
- A concentration near `$6`, primarily associated with higher-value local-service advertisements
- A smaller concentration near `$1.50`, associated mainly with non-local advertisements

This pattern suggests that Yelp's advertising marketplace contains substantially different revenue tiers by search category.

---

## Primary Metrics

### Click-Through Rate

```text
CTR = Number of clicked ads / Number of shown ads
```

### Ad Shown Rate

```text
Ad Shown Rate = Number of ads shown / Number of eligible searches
```

### Revenue per Click

```text
Revenue per Click = Total revenue / Number of clicked ads
```

### Revenue per Eligible Search

```text
Revenue per Eligible Search
= Total revenue / Number of eligible searches
```

### Overall Revenue per Search

```text
Revenue per Search = Total revenue / Total searches
```

---

## Conversion Funnel Results

The advertising funnel consists of three major stages:

```text
Eligibility Rate
× Ad Shown Rate
× Click-Through Rate
= Overall Search-to-Click Conversion Rate
```

### Funnel Comparison

| Funnel Metric | Control | Treatment |
|---|---:|---:|
| Eligibility Rate | 94.99% | 95.17% |
| Ad Shown Rate | 94.25% | 73.96% |
| CTR among Shown Ads | 75.92% | 85.74% |
| Overall Conversion Rate | 67.98% | 60.34% |

### Interpretation

The treatment produces:

- A small and statistically insignificant increase in advertising eligibility
- A large and statistically significant decrease in the ad shown rate
- A large and statistically significant increase in CTR among shown ads
- A lower overall search-to-click conversion rate

The improvement in CTR is not large enough to offset the reduction in available advertisements.

The main bottleneck is therefore:

```text
Ad Shown Rate
```

---

## Aggregate Experiment Results

| Metric | Control | Treatment | Treatment Change |
|---|---:|---:|---:|
| Click-Through Rate | 75.9% | 85.7% | +9.8 percentage points |
| Ad Shown Rate | 94.3% | 74.0% | -20.3 percentage points |
| Revenue per Click | $4.41 | $4.18 | -5.2% |
| Revenue per Eligible Search | $3.16 | $2.65 | -16.1% |
| Revenue per Search | $3.00 | $2.52 | -16.0% |

All four primary treatment comparisons were statistically significant at conventional levels, except where otherwise stated in the detailed analysis.

---

## Statistical Testing

### Eligibility Rate

| Group | Eligibility Rate |
|---|---:|
| Control | 94.99% |
| Treatment | 95.17% |

The difference in eligibility rate was not statistically significant:

```text
p ≈ 0.09
```

This indicates that random assignment did not materially change whether searches were eligible for advertising.

### Ad Shown Rate

Among eligible searches:

| Group | Ad Shown Rate |
|---|---:|
| Control | 94.25% |
| Treatment | 73.96% |

The reduction was highly statistically significant:

```text
p < 0.0001
```

### Click-Through Rate

Among searches where an advertisement was shown:

| Group | CTR |
|---|---:|
| Control | 75.92% |
| Treatment | 85.74% |

The treatment increased CTR by approximately:

```text
9.8 percentage points
```

The difference was highly statistically significant:

```text
p < 0.0001
```

---

## Revenue Impact Analysis

### Revenue per Search

| Group | Revenue per Search |
|---|---:|
| Control | $3.00 |
| Treatment | $2.52 |

The treatment reduced average revenue per search by approximately:

```text
16%
```

### Revenue per Eligible Search

| Group | Revenue per Eligible Search |
|---|---:|
| Control | $3.16 |
| Treatment | $2.65 |

The treatment generated approximately 16.1% less revenue per eligible search.

The reduction was statistically significant:

```text
p < 0.0001
```

### Revenue per Shown Ad

| Group | Revenue per Shown Ad |
|---|---:|
| Control | $3.35 |
| Treatment | $3.58 |

When an advertisement was actually displayed, treatment searches generated approximately 7% more revenue per shown ad.

This suggests that the displayed treatment ads were more likely to attract clicks, but there were substantially fewer opportunities to display them.

### Revenue per Click

| Group | Revenue per Click |
|---|---:|
| Control | $4.41 |
| Treatment | $4.18 |

Although the treatment improved CTR, it produced slightly lower revenue per click.

The treatment therefore increased engagement but did not improve the monetary value of each click.

---

## Local versus Non-Local Search Analysis

Search type was evaluated as a potential moderator of treatment performance.

### Engagement Metrics

| Metric | Local Control | Local Treatment | Non-Local Control | Non-Local Treatment |
|---|---:|---:|---:|---:|
| CTR | 81.1% | 90.0% | 68.0% | 80.2% |
| Ad Shown Rate | 95.2% | 69.9% | 92.9% | 80.1% |

### Key Observations

Local searches have a higher baseline CTR than non-local searches.

The treatment improves CTR for both categories:

```text
Local:
81.1% → 90.0%

Non-local:
68.0% → 80.2%
```

However, the treatment also reduces ad shown rates:

```text
Local:
95.2% → 69.9%
Change: -25.3 percentage points

Non-local:
92.9% → 80.1%
Change: -12.8 percentage points
```

The treatment causes a much larger loss of ad exposure among local-service searches.

Because local-service advertisements are also the highest-value ads, this decline is especially damaging to revenue.

---

## Revenue by Search Type

| Metric | Local Control | Local Treatment | Non-Local Control | Non-Local Treatment |
|---|---:|---:|---:|---:|
| Revenue per Click | $6.00 | $6.00 | $1.50 | $1.50 |
| Revenue per Eligible Search | $4.63 | $3.77 | $0.95 | $0.96 |

### Local Searches

Revenue per click remained effectively unchanged:

```text
Control:   $6.00
Treatment: $6.00
```

However, revenue per eligible local search decreased by approximately 18.6%:

```text
Control:   $4.63
Treatment: $3.77
```

This indicates that the local revenue decline was caused primarily by fewer ads being shown, not by lower-value clicks.

### Non-Local Searches

Revenue per eligible search increased slightly:

```text
Control:   $0.95
Treatment: $0.96
```

The improvement was statistically significant but economically small.

---

## Moderator Analysis

Two-way ANOVA was used to evaluate the effects of:

- Treatment assignment
- Local-service status
- Treatment × Local-service interaction

### ANOVA Summary

| Metric | Treatment Effect | Local-Service Effect | Interaction Effect |
|---|---|---|---|
| CTR | Significant | Significant | Significant |
| Ad Shown Rate | Significant | Significant | Significant |
| Revenue per Click | Not significant | Significant | Not significant |
| Revenue per Eligible Search | Significant | Significant | Significant |

### Interpretation

The interaction effects confirm that treatment performance differs between local and non-local searches for:

- CTR
- Ad shown rate
- Revenue per eligible search

Revenue per click, however, is determined primarily by whether the search is local or non-local rather than by treatment assignment.

---

## Key Findings

1. Strict geographic constraints improved CTR from **75.9% to 85.7%**.

2. The treatment reduced the ad shown rate from **94.3% to 74.0%**.

3. The decrease in ad availability was larger than the improvement in engagement.

4. Revenue per eligible search declined from **$3.16 to $2.65**.

5. Average revenue per search declined from **$3.00 to $2.52**.

6. Local-service searches generated substantially higher revenue per click than non-local searches.

7. The treatment caused the largest inventory loss within the high-value local-service segment.

8. The strict treatment should not be launched universally in its current form.

---

## Business Recommendations

### 1. Introduce a Hybrid Geographic Constraint

Apply strict geographic constraints only when enough relevant advertising inventory is available inside the map area.

When inventory is insufficient, gradually expand the permitted geographic radius.

Example decision logic:

```text
If sufficient in-map inventory exists:
    Apply strict geographic targeting

If in-map inventory is limited:
    Expand the radius incrementally

If no suitable in-map inventory exists:
    Use the most relevant available advertisement
```

This approach would preserve much of the CTR improvement while reducing lost advertising opportunities.

### 2. Use a Softer Strategy for Local Services

Apply less restrictive geographic rules to local-service searches.

Local advertisements generate approximately `$6.00` per click compared with approximately `$1.50` for non-local advertisements.

Protecting local ad inventory should therefore be a product priority.

### 3. Implement Dynamic Auction and Inventory Management

Adjust:

- Geographic radius
- Reserve prices
- Ranking rules
- Ad inventory thresholds

using real-time information about:

- Available advertisers
- Expected click probability
- Expected revenue per click
- Search category
- Map density
- Local-service status

### 4. Optimize for Revenue per Eligible Search

CTR should not be treated as the only success metric.

A treatment may increase CTR while still reducing total business value.

The primary decision metric for the next experiment should be:

```text
Revenue per Eligible Search
```

Guardrail metrics should include:

- Ad shown rate
- CTR
- Revenue per click
- User experience indicators

### 5. Run a Follow-Up Experiment

Test multiple treatment levels rather than only strict versus unrestricted targeting.

Suggested experiment arms:

| Group | Geographic Rule |
|---|---|
| Control | No additional geographic restriction |
| Treatment A | Strict map-bound restriction |
| Treatment B | Moderate radius expansion |
| Treatment C | Dynamic inventory-based radius |
| Treatment D | Separate rules for local and non-local searches |

---

## Recommended Experiment Decision

The current strict geo-constraint treatment should not be rolled out to all users.

Although it improves ad relevance and engagement, it causes a substantial loss in:

- Ad impressions
- Overall conversion
- Revenue per eligible search
- Revenue per search

The recommended decision is:

```text
Do not launch the strict treatment globally.

Develop and test a hybrid geo-targeting strategy
that adapts to available inventory and search type.
```

---

## Limitations

### Revenue Is Only Recorded after a Click

The dataset assumes Yelp receives revenue only when an advertisement is clicked.

The analysis does not measure longer-term effects such as:

- Advertiser retention
- User retention
- Repeat visits
- Downstream purchases
- Lifetime value

### Limited User Context

The dataset does not include:

- User location
- Search radius
- Exact map boundaries
- Distance between users and advertisers
- Business category detail
- Advertiser quality
- Ranking position

These variables could help explain why certain advertisements were not shown.

### No Long-Term Experiment Outcomes

The analysis focuses on immediate engagement and revenue metrics.

It does not evaluate whether increased relevance improves future user behavior.

### Observed Statistical versus Business Significance

With 175,000 observations, small differences may be statistically significant even when their practical effect is limited.

Both effect size and business impact should therefore be considered.

---

## Future Improvements

Potential extensions include:

- Estimating treatment effects by desktop versus mobile platform
- Conducting additional heterogeneous treatment effect analysis
- Modeling expected revenue at the individual-search level
- Evaluating geographic radius as a continuous treatment
- Applying causal forests or uplift modeling
- Building a dynamic advertisement-selection policy
- Measuring advertiser and user lifetime value
- Creating a real-time experimentation dashboard

---

## Repository Structure

```text
geo-targeted-ad-experiment/
├── README.md
├── Ad_Experiment_Analysis.ipynb
├── Experiment_Results_Presentation.pdf
└── yelp_data.csv
```

---

## Repository Contents

| File | Description |
|---|---|
| `Ad_Experiment_Analysis.ipynb` | Complete R analysis covering exploratory analysis, funnel metrics, hypothesis testing, revenue analysis, subgroup analysis, and visualizations |
| `Experiment_Results_Presentation.pdf` | Executive presentation summarizing the experiment, statistical results, and product recommendations |
| `yelp_data.csv` | Experimental search-level dataset used in the analysis |
| `README.md` | Project overview, methodology, findings, limitations, and recommendations |

The original `Yelp.xlsx` workbook is not included because it was used only as reference material for the case context, data dictionary, and replication guidance.

---

## How to Run the Analysis

### Requirements

- R
- Jupyter Notebook or JupyterLab
- An R kernel for Jupyter
- tidyverse

### Install Required R Packages

```r
install.packages("tidyverse")
install.packages("IRkernel")
IRkernel::installspec()
```

### Clone the Repository

```bash
git clone https://github.com/your-username/geo-targeted-ad-experiment.git
```

### Open the Project Directory

```bash
cd geo-targeted-ad-experiment
```

### Start Jupyter Notebook

```bash
jupyter notebook
```

Open:

```text
Ad_Experiment_Analysis.ipynb
```

Make sure the dataset remains in the same directory:

```text
yelp_data.csv
```

The Notebook reads the data using:

```r
yelp <- read_csv("yelp_data.csv")
```

Run all cells in order.

---

## Skills Demonstrated

- A/B Testing
- Product Analytics
- Experiment Design
- Advertising Analytics
- Funnel Analysis
- Hypothesis Testing
- Two-Sample t-Tests
- Proportion Testing
- Two-Way ANOVA
- Interaction Analysis
- Heterogeneous Treatment Effects
- Revenue Analytics
- Business Decision-Making
- R
- tidyverse
- dplyr
- ggplot2
- Data Visualization

---

## Team

- Sisly Lyu
- Yousef Jafarnia Dabanloo
- Ricky Liang
- Connor Lyons
- Ronghao Wu
