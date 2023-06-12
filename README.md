# Road Fatalities: An Exploratory Analysis of Road Accidents and Fatalities in the USA in the year 2020.

---------------------
Team Members:
- Eimaan (Ash) Ejaz
- Savina Boateng
- Zeeshan Karim
- Lishani Srikaran
---------------------

Road accidents and fatalities are unfortunately a common occurance in almost all parts of the world. For this project, we hoped to find insights with regards to different factors and variables affecting road accidents and fatalities.

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
![Screenshot 2023-06-12 at 21 14 51](https://github.com/lishanisrikaran/project-1/assets/127614970/6840adda-4a2a-40c6-aa9f-e94f0bec7a7b)

# Data Clean-up

The data clean-up process involved the following steps:

- The .csv file was imported and read into a DataFrame.
- Redundant columns were removed as well as any rows containing null values.
- The data types of the "age" and "speed limit" were converted from float to integer values.
- The columns were renamed to be more self-explanatory.

Please see the file "road_fatalities - clean up process" for the full code.

# Initial Exploration: Mapping Accidents

Using hvplot.pandas, we plotted all accidents on a map visualisation to see the spread of accidents on a national level.
<img width="822" alt="image" src="https://github.com/lishanisrikaran/project-1/assets/127614970/0bd821be-7280-4616-a7b3-04f6e0ad73bf">

The map visualisation shows a higher concentration of datapoints in the Eastern half of the US as well as along the West Coast. After further research we determined that this aligned with the population density and National Highway Network of the US. It made sense that where population is higher and there are more extensive road networks, a larger number of accidents occur.

# Q1: Is there a relationship between the age of the driver and the number of accidents?

This analysis was performed by: Eimaan (Ash) Ejaz.

There is a common assertion that younger drivers are more likely to cause road accidents, and we hoped to prove this empirically.


