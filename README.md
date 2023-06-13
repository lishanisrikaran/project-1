# Road Fatalities: An Exploratory Analysis of Road Accidents and Fatalities in the USA in the year 2020.

---------------------
Team Members:
- Eimaan (Ash) Ejaz
- Savina Boateng
- Zeeshan Karim
- Lishani Srikaran
---------------------

Road accidents and fatalities are unfortunately a common occurrence in almost all parts of the world. For this project, we hoped to find insights with regards to different factors and variables affecting road accidents and fatalities.

We focused on answering the following 4 main questions:
1) Is there a relationship between the age of the driver and the number of accidents? - Eimaan (Ash) Ejaz
2) How do weather conditions and route impact the likelihood of fatalities? - Savina Boateng
3) Are road fatalities more likely to occur at a certain time of day? - Zeeshan Karim
4) What impact does speed limit have on the total number of fatalities? - Lishani Srikaran

# Data Source

We chose to source our data from The National Highway Traffic Safety Administration (NHTSA). This is an agency of the U.S. federal government, so we trusted that our data would be reliable and accurate. The NHTSA road fatality records are available to source both though an API and also through CSV files for each year.

API: https://crashviewer.nhtsa.dot.gov/CrashAPI

CSV Archives: https://www.nhtsa.gov/file-downloadsp=nhtsa/downloads/FARS/2021/National/

We were unable to make API requests without providing additional filters which would have reduced the size of the dataset - this is explored later in the analysis. For this reason we decided to utilise the CSV file instead.

![screenshot_2023-06-12_at_21 14 51_720](https://github.com/lishanisrikaran/project-1/assets/130323046/1da95830-d7b2-45af-a87e-9315e83a0a38)


# Data Clean-up

The data clean-up process involved the following steps:

- The .csv file was imported and read into a DataFrame.
- Redundant columns were removed as well as any rows containing null values.
- The data types of the "age" and "speed limit" were converted from float to integer values.
- The columns were renamed to be more self-explanatory.

# Files

- The clean-up can be found in the file titled "road_fatalities - clean up process.ipynb"
- The full analysis can be found in the file titled "road_fatalities - final.ipynb"
- The .csv file utilised is located in the "source_data" folder.
- All graphs and charts created during the analysis can be found in the "output_data" folder.
- The presentation used is titled "Road Fatalities.pptx".

# Initial Exploration: Mapping Accidents

Using hvplot.pandas, we plotted all accidents on a map visualisation to see the spread of accidents on a national level.

![image](https://github.com/lishanisrikaran/project-1/assets/130323046/8dff1daa-1a11-417b-944d-87050e0f4d97)


The map visualisation shows a higher concentration of datapoints in the Eastern half of the US as well as along the West Coast. After further research we determined that this aligned with the population density and National Highway Network of the US. It made sense that where population is higher and there are more extensive road networks, a larger number of accidents occur.

# Q1: Is there a relationship between the age of the driver and the number of accidents?

This analysis was performed by: Eimaan (Ash) Ejaz.

There is a common assertion that younger drivers tend to cause more road accidents. We were hoping to prove this empirically by comparing the number of road accidents by the age of the driver and identifying any trends.

For an initial exploration, a histogram was produced to determine the distribution of ages of drivers in our accident database.

![image](https://github.com/lishanisrikaran/project-1/assets/130323046/2c56e14f-865b-4be1-9f05-ab40aa1999ed)


The results show that the data is right-skewed, meaning there is a higher frequency of datapoints at the lower end of the age scale i.e. more accidents where the driver was younger.

Since our data is right-skewed, the mode and median would be more representative of the average driver than the mean as they are less susceptible to outlier values. The calculated averages were as follows:

- The Mean Age of drivers in accidents is 43
- The Mode Age of drivers in accidents is 28
- The Median Age of drivers in accidents is 40

Here, the summary statistics support the assertion that road accidents are more often caused by younger drivers.

We then performed a linear regression to explore the relationship between driver age and number of accidents and calculated the Pearson correlation coefficient for this relationship.

![image](https://github.com/lishanisrikaran/project-1/assets/130323046/f05f0dff-16fe-4185-ad23-3f5a8d67f9aa)

The regression showed a strong negative correlation between driver age and the number of accidents, supported by the Pearson correlation coefficient value of r = -0.94. This does support the assertion that younger drivers cause the highest number of accidents.

However, it is important to note that the number of accidents per age group is influenced by the number of drivers for each age group. For example, though a relatively small number of accidents are caused by drivers over the age of 80, this may be due to the fact that there are likely very few drivers on the road that are over the age of 80. We can also see this for the 16 and 17 year old age groups. As 16 and 17 year olds are younger than 18+ year olds, we would expect them to involved in a greater number of accidents than 18+ year olds, however the opposite is the case in this analysis. We determined that this is due to there being a smaller number of drivers aged 16 and 17 than drivers over the age of 18 as the minimum driving age varies by state and not all states allow under 18s to drive.

For the final part of the analysis for this question, the ages were grouped and summary percentages were calculated for each age group, as seen by  the pie chart below:

![image](https://github.com/lishanisrikaran/project-1/assets/130323046/9df99d0d-2b32-47b4-ab4e-3ac0af03b97c)

We were able to show that younger drivers cause the greatest number of accidents, with drivers aged 16-35 contributing to almost half of all road accidents. The most common age among drivers involved in road accidents was 28 and the 26-35 year old age group contributed to the greatest percentage of accidents.

We can conclude that further research is necessary to determine whether the number of accidents per age group is representative of the population of drivers for each age group, and which factors may influence the rate of road accidents for different age groups.

The following recommendations could also be made from the results of our analysis:

Increased education including targeted interventions may be necessary for younger drivers or newer drivers.
Stricter driving examinations could be enforced for individuals seeking to get their driving license.
A consistent, nation-wide minimum driving age limit may be beneficial to reduce the number of younger drivers on the road

# Q2: How do weather conditions and route impact the likelihood of fatalities? 

This analysis was performed by: Savina Boateng.

This analysis was performed to examine the impact of weather conditions and specific routes on the number of fatalities.

Initially, a bar chart displaying the Distribution of Fatal Accidents by Weather Conditions was plotted.
![image](https://github.com/lishanisrikaran/project-1/assets/130323046/ee17f863-e04e-46cd-bb8a-a20758380696)

Most accidents occurred with clear weather conditions (almost 25000), compared to the other weather conditions outlined.

The pie chart below shows the Distribution of Fatalities vs Visibility.
![image](https://github.com/lishanisrikaran/project-1/assets/130323046/d67a7d04-1b91-4aab-9a2c-1b3d1d0acf72)

It is clearly shown that most fatalities (46.3%) occurred during the daylight. . This makes sense as during daylight hours is when the majority of the population are using motor transport to commute for their daily obligations. During these daily obligations, it is likely that people are not 100% focused on their driving, causing more fatalities to be recorded.

Subsequently, a bar chart showing the Total Number of Fatal Accidents by Route Name was plotted.
![image](https://github.com/lishanisrikaran/project-1/assets/130323046/2eb7a699-7c8d-417c-af09-d0642917f386)

It is seen that most fatalities (over 10000) occurred on the State Highway. State highways often experience a significant amount of traffic due to their role in connecting various cities, towns, and rural areas within a state. The increased volume of vehicles on these highways can contribute to a higher probability of accidents occurring. 

Finally, two stacked bar charts (the first showing Fatal Accidents by Route Name and Weather Condition and the second showing Fata Accidents by Weather Conditions and Visibility) were plotted. 
![image](https://github.com/lishanisrikaran/project-1/assets/130323046/3b83b5a2-2fe6-44eb-b965-111dd57785e6)
![image](https://github.com/lishanisrikaran/project-1/assets/130323046/70b0e8c3-583b-4e19-8ad3-01f0cfb8afff)


Both stacked bar charts show that most fatalities occurred in clear weather conditions, during the daylight, as shown per our previous pie chart. This is probably due to the fact that most drivers would drive during daylight due to their jobs and various responsibilities, instead of times with dark visibility.

In conclusion:
- The analysis above indicates that clear weather conditions pose a higher risk for fatal accidents regardless of the specific route
- Due to people using transport to commute to their daily obligations, it is also seen that most accidents occur during daylight rather than darker times.

# Q3: Are road fatalities more likely to occur at a certain hour of the day?

This analysis was performed by: Zeeshan Karim

Initially, a line chart and bar chart showing the Hourly Distribution of Fatality Counts were plotted.
![image](https://github.com/lishanisrikaran/project-1/assets/130323046/e54baf59-77bb-4740-9f97-a9c68ea1b5ce)
![image](https://github.com/lishanisrikaran/project-1/assets/130323046/15c57663-39dd-4253-bba0-9b78a8381867)

A steady increase in the number of fatalities is observed between hours 10 and 18, with most fatalities occurring between the hours 18 to 22. 

Subsequently, a bar chart showing the Number of Fatalities per State (filtered to the Top 5) was plotted.
![image](https://github.com/lishanisrikaran/project-1/assets/130323046/080a3486-cfb6-442a-9657-d84ae2062051)

The bar chart shows that California has the highest number of fatalities, followed by Texas. These findings are congruent with the Map of Accidents shown in #Q1.

In conclusion:
- Between 10 to 18 hours, the steady increase observed is likely due to more activity of road users.
- Most fatalities occurred between the hours 18 to 22. This could be as a result of reduced visibility as it gets darker later in the day.
- California’s number of fatalities is likely a result of a higher population density compared to other states.

# Q4: What impact does speed limit have on the total number of road fatalities? 

This analysis was performed by: Lishani Srikaran

The null hypothesis for this question is the increasing speed limit of a road does not affect the likelihood of an individual experiencing a fatal road accident. 

Initially, the speed limit data’s distribution was observed using a histogram.
![image](https://github.com/lishanisrikaran/project-1/assets/130323046/f012bd79-e297-47a7-ace6-2a48d6811552)

A bell shaped curve structure is followed, showing normal distribution. This is also supported by the following findings:
- Roughly 68% of the recorded road incidents occurred between 33.19MPH and 67.27MPH.
- Roughly 95% of the recorded road incidents occurred between 16.15MPH and 84.31MPH.
- Roughly 99.7% of the recorded road incidents occurred between 0.89MPH and 101.35MPH.

A box plot was also plotted, virtually showing the same mean and median.
![image](https://github.com/lishanisrikaran/project-1/assets/130323046/bd94b261-00c7-4373-af16-a3407fd2086d)
![image](https://github.com/lishanisrikaran/project-1/assets/130323046/a18d7066-ad04-4706-b9c2-d9f2e2a66180)

It can be seen that on average a road accident is most likely to occur at 50MPH,  due to the data being normally distributed. 

Next, a scatter chart was plotted showing speed limit versus fatality counts.
![image](https://github.com/lishanisrikaran/project-1/assets/130323046/42816192-3a8b-4ab8-b645-9562b4fb09cf)

The correlation coefficient calculated was 0.1, indicating a very weak linear correlation. An increase of one MPH in the speed limit corresponds to a increase of 14 additional fatalities which is very insignificant when observing on a nationwide scale. 

Although the scatter plot did not indicate a linear relationship, when the speed limits are grouped, as shown below, it is seen that most incidents occurred between the two middle groups, therefore, there is still some correlation, even though not linear.
![image](https://github.com/lishanisrikaran/project-1/assets/130323046/d28570f9-7646-4ebf-ab27-cc5b82c00a9c)


The probable reason a linear regression is not followed could be due to less roads present with higher speed limits, so the cumulative fatality counts recorded are lower. A Bragg’s function regression would help regress values better. 

Finally, an Anova t-test was performed, confirming that the median of speed limits does increase up until a certain point. 
![image](https://github.com/lishanisrikaran/project-1/assets/130323046/bc036fdc-3834-497f-befb-9ea18c8263a0)

However, the computed p value is below the significance level of 0.05 and therefore, the null hypothesis could be rejected.

In conclusion:
- A road fatality is most likely to occur on a road of 50MPH.
- Speed limit does have a impact on the likelihood of a fatality, the relationship is not linear however. 

# What are the impacts of our findings?

- Improve road safety measures (e.g. filtering systems during busy times).
- Public awareness and education/targeted interventions for those at more risk such as younger/first time drivers including refreshing knowledge.
- Stricter driving examination for those applying for licenses.
- Implementation of a nation-wide minimum driving age (18).
- Improve policy development.

# Additional findings

![image](https://github.com/lishanisrikaran/project-1/assets/130323046/159a1966-c9d2-44fd-a1b8-276f0accb1b5)
![image](https://github.com/lishanisrikaran/project-1/assets/130323046/c91fcc4d-ccc6-4a70-b3d3-1a5df2751424)
![image](https://github.com/lishanisrikaran/project-1/assets/130323046/a86d3575-67f1-4f23-9953-57870ddbcd9a)


# PLEASE NOTE

We had issues pushing our individual analysis into the  "road_fatalities - final.ipynb" file (Our Instructor Joanna, and TA Sharoz have been made aware of this). Therefore, this was done manually.
The individual analysis can still be found in the individual branches.
