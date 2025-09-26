# la-county-uninsured-analysis
Analysis of Los Angeles County health insurance coverage using U.S. Census ACS 5-Year data. This project calculates the percentage of uninsured residents and prepares data for visualization in R.

# 📊 Capstone Project: Analyzing Health Insurance Coverage in Los Angeles County
🔎 Summary / Business Task

Our client is a healthcare policy consulting firm seeking insights into health insurance coverage in Los Angeles County.
The goal of this analysis is to:

Measure the total population and the number of uninsured residents.

Calculate the percent of uninsured residents.

Begin exploring demographic and socioeconomic factors for future policy recommendations.

**Key Question**:

How many residents in Los Angeles County lack health insurance, and what percentage of the population do they represent?

### 📝 Dataset Description
(Source	Description)

U.S. Census Bureau – American Community Survey (ACS) 5-year Estimates	We used tidycensus to pull the 2019-2023 ACS 5-year estimates. Specifically variables: B27010_001 (total population) and B27010_017 (uninsured population).
FIPS codes	Used to correctly identify state and county names.

Geography: County (Los Angeles, CA)
Time Frame: 2019–2023 ACS 5-year estimates

## 🛠 Tools Used

* R + RStudio

* tidycensus (Census API access)

* dplyr / tidyr (data cleaning and reshaping)

* Base R plotting (initial visualization)

### 🧹 Data Preparation & Cleaning

Registered and loaded the Census API key securely.

Pulled raw ACS data with get_acs() for Los Angeles County.

Verified variables using FIPS codes.

Transformed data from long to wide format with pivot_wider().

Created new calculated field percent_uninsured for analysis.
```{r}

insurance_la_summary <- insurance_la_raw %>%
  select(GEOID, NAME, variable, estimate) %>%
  pivot_wider(names_from = variable, values_from = estimate) %>%
  rename(total_population = total,
         uninsured_count = uninsured) %>%
  mutate(percent_uninsured = (uninsured_count / total_population) * 100)
  ```
## 📈 Analysis & Early Findings

Total Population (Los Angeles County): 9,778,622

Uninsured Residents: 76,991

Percent Uninsured: ~0.79%

This provides a first look at the uninsured population in Los Angeles County. Future iterations will add demographic and geographic breakdowns at the census tract level for deeper insight.

## 📊 Visualizations

Example scatterplot of Median Household Income vs. Median Age across CA counties:



**Next Steps:** 

* Build maps to visualize uninsured rates by census tract.

* Create dashboards or charts in R or Tableau for stakeholder presentation.

**🤔 Further Questions**

* How does health insurance coverage vary across census tracts in LA County?

* Which demographic or socioeconomic factors correlate with higher uninsured rates?

* How can policymakers use these findings to allocate resources effectively?

**📬 High-Level Insights**

* Using public ACS data via tidycensus, you can quickly measure health insurance coverage rates.

* Transforming data with dplyr + tidyr makes it easier to compute policy-relevant metrics.

* Even early exploratory plots can reveal relationships between socioeconomic indicators and health coverage.
