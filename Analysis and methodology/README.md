# Methodology and analysis used in the project

## Here we do a deeper dive in the full workflow of the project, decisions made and techniques used

## My workflow
1. Identify information needs of our client and understand the business question
2. Data gathering, preprocessing and data model
3. Data-analysis and visuals with PowerBI
4. Results

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
#### 2.1 Current state data
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

#### 2.2 Future state data
- From tilastokeskus I used the prediction of population dataset for the year 2035, as the analysis for future state of counties.
- The variables for this dataset:

  1: County
  2: Year
  3: Population
  4: Different age groups

#### 2.3 Preprocessing of data
- From the GUI of tilastokeskus I uploaded the relevant data to excel. In excel I checked for missing values and formatted the variables to correct type. Since the tilastokeskus data is high in quality, there wasn't a lot to preprocess.
- After that I imported the datasets to PowerBI. In PowerBI I connected the data tables on **county** variable. The resulted data model:

  <img width="701" height="407" alt="image" src="https://github.com/user-attachments/assets/20bfb107-8fc6-4601-adf7-28f07e4f1afd" />

- This data model allowed me to compare the **future state of counties** with different metrics that were calculated on the **current state of counties**.

### 3. Data-analyis with PowerBI

#### 3.1 Splitting counties to groups
- My end goal was to find possible counties where my client should invest in. Since my dataset had 309 counties I decided to do a pruning approach, which would allow me to mark off irrelevant counties and do deeper analysis on the most potential counties.
- For this I started my analysis by splitting counties to different groups with a DAX query:

**Group 1: Counties with high avg-age and high median income** 

**Group 2: Counties with low avg-age and high median income** 

**Group 3: Counties with high avg-age and low income** 

- The splitting factor for age was avg-age over or under 45. Splitting factor for median-income was over or under 25000. The DAX query I used also pruned out counties with under 7000 in population, since demand in those counties isn't enough for good business.

(**NOTE** I know this approach is a bit naive, since I used arbitrary values as a splitting factor, but for this simulated task lets allow it...)

- Full DAX query:

  <img width="1200" height="213" alt="image" src="https://github.com/user-attachments/assets/30bf39f2-cc9d-414c-9ecb-4a4f058983c4" />

#### 3.2 Producing a tooltip
- Analysing the counties based on relevant metrics from just the tables proved to be irritating. I decided to make a tooltip that I could use on the visuals to help my compare the counties.
- In this tooltip I included relevant metrics for comparison between counties:

  <img width="525" height="279" alt="image" src="https://github.com/user-attachments/assets/ee6c12e2-4a73-47d2-a56f-4625acd40cba" />

- This tooltip was then used during the whole analysis process in all different visuals I created.

#### 3.3 Visualizing the groups
- From my grouping measure **potentiaali** that I made in part 3.1, I created a visual that showcased each group in a scatterplot.
- The scatterplot compared avg-age of counties on their median income.

  <img width="1207" height="681" alt="image" src="https://github.com/user-attachments/assets/17c656e0-7995-4358-8c41-f1c728b29820" />

- Since the plot was very crowded, I coulnd't include any markers that would identify counties by name. This is why I used the tooltip created in 3.2, to look into the counties relevant metrics.

  <img width="1210" height="698" alt="image" src="https://github.com/user-attachments/assets/fff8d29f-d812-4473-aa16-a959993295b6" />

- With these tools I created, I looked into the counties on the scatterplot. I could then conclude that the counties in the group **High avg-age, low median income** weren't potential for investing in, and I pruned them out of the analysis.

#### 3.4 Geographical analysis
- After previous pruning I was left with the 2 relevant groups of counties: **1: High avg-age, high median income** and **2: Low avg-age, high median income**.
- I then build a visual that would allow me to inspect these groups on their geographical locations. This would allow me to see wether the counties were located near areas that would provide too much competition.
- I used the **azure maps** visual for this:

  <img width="1204" height="675" alt="image" src="https://github.com/user-attachments/assets/1a8505ab-89a5-4e2a-8579-106620c122a2" />

- From this visual I could zoom in the different parts of Finland and analyze the geographical locations effect on the potential of good investment. I found that all the counties in the group **2: Low avg-age, high median income** were located around the largest Finnish cities. The competition would be too big for these counties, thus not enabling a market gap. This led me to prune this group out of further analysis.
  
#### 3.5 Future outlook of counties with high avg-age and high median income
- I was left with the most potential group for having a county with market gap, **Group 1: High avg-age, high median income**. This group had 39 counties, for which I wanted to analyze their future outlook of population change from my future state dataset.
- I used this DAX query to find out the percentage change in population predicted for 2035 when compared to 2023:

  <img width="500" height="137" alt="image" src="https://github.com/user-attachments/assets/7f5a351a-564d-4160-ba3e-82e464dbeaba" />

- I visualized the population change in a bar plot using the measure from DAX query:

  <img width="1214" height="682" alt="image" src="https://github.com/user-attachments/assets/ca14365f-25f2-414b-9603-b0e4e86085ab" />

- This visual helped me to analyze the future potential of the counties in terms of possible demand. The counties having high population loss predicted aren't looking good in sense of investment. On the other hand counties having population growth predicted seem more promising.
- From the visual we can see that the predicted percentage changes aren't that big to completely make decisions based on them. But they do give an outlook on which way the counties future is going in sense of population change. This helped me to find 2 potential targets for investment.


### 4. Results
- Based on analysis in part 3 I identified 2 possible counties that could be invested in. In the end I used all the different visuals and metrics I made in part 3, for analyzing all the possibilities. For the 2 targets chosen I build a visual to showcase their properties.

#### 4.1 Naantali

<img width="1194" height="677" alt="image" src="https://github.com/user-attachments/assets/9edc2331-76e8-4cb8-a228-e9604091c968" />

- First target is the county of Naantali, where the place of business would be in the city of Naantali.
- As a county, Naantali has huge potential for investment. The current numbers in sense of median income and average age of population is very good. The median income was in the highest 10% of all Finnish counties in 2023.
- What lacks in Naantali in 2023 is the population amount, and the amount of companies in the county, the two metrics that indicate possible demand in the county. But when looking into the population change metric (3.5), we can see that the predicted population change for 2035 is +9.93%. This suggests higher potential demand in the future.
- The demographic distibution of Naantalis population is also good. About 80% of naantalis population either pensioner or in the workforce, which is the target group for our client.
- 4.22% of Naantalis population is working in healthacre or social services. I used this visual to indicate possible supply for workforce for our client, and possible competition in the area. From this metric alone it's hard to make informed summary about the competetive situtation in Naantali.
- Naantali is located near city of Turku, that has lots of private healthcare businesses which could produce competition for my client. But when we look at Naantalis position geographically we can see that most of the county is in the archipelago and further away from Turku. As a place of business the city of Naantali gives and edge in this area, since its in the crossing to the archipelago, and near 2 other counties that had high potential: Masku and Raisio. With right placement of business, Naantali would gain the benefit of easy access to the healthcare center when compared to Turku, thus bringing in customers from around Naantali county that would otherwise go to Turku for their healthcare.

<img width="466" height="662" alt="image" src="https://github.com/user-attachments/assets/9d36d82d-f943-43f2-884e-575c0ff6d276" />

#### 4.2 Riihimäki area
