# 🏥 LA County Uninsured Analysis – Capstone Project
This project analyzes **uninsured rates across California counties**, focusing on **Los Angeles County** using the U.S. Census Bureau’s **American Community Survey (ACS)** data.  
The goal is to identify **relationships between income and insurance coverage**, revealing geographic and socioeconomic disparities.

## 🔎 Summary / Business Task

Our client is a healthcare policy consulting firm seeking insights into health insurance coverage in Los Angeles County.
The goal of this analysis were to:

* Measure the total population and the number of uninsured residents.
* Calculate the percent of uninsured residents.
* Begin exploring demographic and socioeconomic factors for future policy recommendations.

**Key Question**:

How many residents in Los Angeles County lack health insurance, and what percentage of the population do they represent?

### 📝 Dataset Description

Source: U.S. Census Bureau – American Community Survey (ACS) 5-year Estimates (2022)

* Variables:
  * B27010_001: Total population
  * B27010_017: Uninsured population
  * B19013_001: Median household income
* Geography: County (Los Angeles, CA)
* Time Frame: 2022 ACS 5-year estimates

**California State Averages (2022):** 
* Mean percent uninsured: 0.9586%
* Mean median income: $82,966.60

### Tools & Technologies
- **R**: tidycensus, tidyverse, ggplot2, ggrepel, sf, viridis  
- **Data cleaning & analysis**: dplyr, tidyr  
- **Visualization**: ggplot2, ggrepel, viridis  
- **Geospatial analysis**: sf, tigris
  
### 🧹 Data Preparation & Cleaning

* Registered and loaded the Census API key securely.
* Pulled raw ACS data with get_acs() for Los Angeles County.
* Verified variables using FIPS codes.
* Transformed data from long to wide format with pivot_wider().
* Created new calculated field percent_uninsured for analysis.
```{r}

insurance_la_summary <- insurance_la_raw %>%
  select(GEOID, NAME, variable, estimate) %>%
  pivot_wider(names_from = variable, values_from = estimate) %>%
  rename(total_population = total,
         uninsured_count = uninsured) %>%
  mutate(percent_uninsured = (uninsured_count / total_population) * 100)
  ```
## 📈 Analysis & Early Findings

  * **GEOID:** 06037
  * **County Name**: Los Angeles County
  * **Total Population**: 9,866,623
  * **Uninsured Residents**: 80,508
  * **Percent Uninsured**: 0.82%
  * **Median Household Income**: $83,411
**California State Averages:**
  * **Percent Uninsured**: 0.9586%
  * **Median Household Income**: $82,966.60

These results indicate that Los Angeles County has a slightly lower uninsured rate than the state average, despite having a median income near the state mean.

## 🗺️ Key Visuals
**1️⃣ Income vs. Uninsured Rate by County (2022)**  
Scatter plot showing the relationship between median household income and percent uninsured across California counties. Los Angeles County is highlighted in blue.

![Income vs Uninsured](<img width="1344" height="960" alt="Income_vs_uninsured_2022" src="https://github.com/user-attachments/assets/8dd85e93-0473-42ac-8966-e32e2a8c6612" />
)

**2️⃣ Map of Uninsured Rates in Los Angeles County**  
Choropleth map displaying uninsured rates by census tract within Los Angeles County. Darker areas indicate higher uninsured rates.

![LA County Map](<img width="1344" height="960" alt="LA_County_Uninsured_Map" src="https://github.com/user-attachments/assets/315d2fad-2a22-4db3-9986-40a6ba980f99" />
)

## 📌 Key Insights 
* **Uninsured Rate**: Los Angeles County’s uninsured rate is 0.82%, slightly below the California state average of 0.9586%.
* **Income Disparities**: Lower-income areas show higher uninsured rates, revealing a negative correlation between income and insurance coverage.
* **Geographic Clusters**: High uninsured populations are concentrated in South and East Los Angeles.

## 🔮 Next Steps & Recommendations

* **Target High-Uninsured Areas**: Focus outreach in South and East Los Angeles to increase insurance enrollment. (Responsible: County health departments; Timeline: 6–12 months)
* **Integrate Socioeconomic Data**: Include poverty, education, and race/ethnicity in future analyses for tailored policy recommendations. (Responsible: Analytics team; Timeline: 3–6 months)
* **Monitor Trends Continuously**: Track uninsured rates annually using ACS data to measure program effectiveness. (Responsible: Analytics/reporting teams; Timeline: Ongoing)
* **Interactive Dashboards**: Build dashboards in R Shiny or Tableau to help stakeholders visualize coverage gaps. (Responsible: Data/BI teams; Timeline: 2–4 months)
**Recommendation**: Prioritize targeted outreach supported by data-informed strategies and continuous monitoring to reduce health disparities and improve coverage effectively.

## 📂 View Full Analysis
The complete R Markdown notebook with all code, tables, and visualizations can be viewed here 
