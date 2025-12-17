# Workflow of the project, Data model, DAX querys, visuals

## Here we do a deeper dive in the full workflow of the project, decisions made and techniques used

## Structure of project
1. Identify information needs of our client and understand the business question
2. Data gathering, preprocessing and data model
3. Data-analysis with PowerBI
4. Building visuals for informed decision making with PowerBi

### 1. Information needs and business understanding
- Client wanted to find clear market gaps in Finnish counties to invest in. Market gap was defined as: Counties where competition is low and demand for private healthcare service is high. For a prosperous investement the future of the county is also to be looked in.
- Private healthcare can be expensive, which means we must target counties with higher income. It is also known that a need for healthcare increases with ageing.
- Big part of private healthcares business comes from occupational health contracts with other businesses.
- From these information needs I identified these spots to be derived from data:

   **1. Counties with high avg-age and high median income**
  
  **2. Factors that effect in demand: Population, demography of population, amount of businesses in the area**
  
  **3. Counties population movement in the future**
  
  **4. Competition in- or around the counties**

### 2. Data gathering, preprocessing and data model
#### Current state data
- I used open demographic data from 2021-2023 Finnish counties (https://stat.fi/tup/avoin-data/paikkatietoaineistot/paavo.html) from tilastokeskus, as my analysis for counties current state. Tilastokeskus didn't have data for 2024 or 2025 yet.
- This dataset had lots of variables on county level to do analysis based on the information needs. The relevant variables that I used:

  1: County
  2: Population
  3: Amount of companies
  4: Average age of population
  5: Median income
  6: Workforce
  7: Unemployment
  8: Workforce in healthcare and social services
  9: Year

#### Future state data
- From tilastokeskus I used the prediction of population dataset for the year 2035, as the analysis for future state of counties.
- The variables for this dataset:

  1: County
  2: Year
  3: Population
  4: Different age groups




