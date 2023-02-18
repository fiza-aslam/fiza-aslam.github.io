# Bellabeat Case Study
#### Author: Fiza Aslam
#### Date: 18/02/2023
#
This case study follows from the capstone project from the Google Data Analytics Course. I will be using the 6 step data analysis process for this case study: Ask, Prepare, Process, Analyze, Share and Act. 

## Background
Bellabeat is a high tech manufacturer focused on health products for women. As of now, Bellabeat is a small company which would like to to grow in the smart device market. The CEO believes that analyzing smart device data will allow the company to exploit opportunities to grow in a market where technology is always evolving. Therefore our team has been asked to analyze smart device data to see how consumers are using their smart devices aswell as providing high level reconmendations for Bellabeats marketing strategy. From this analysis, Bellabeat will have greater insights on how to improve their services aswell as their marketing strategy.

## 1. Ask 
Business Task: Analyze smart device useage data provided by Bellabeat to see how consumers use non-Bellabeat smart devices. Finalize insights into a report and presentation on how Bellabeat should proceed with their products and marketing strategies. 

Key stakeholders: women who use health products, Urska (CEO of Bellabeat), Sando (cofounder), executive team, bellabeat marketing team, team of data analysts. 

## 2. Prepare
Data source: https://www.kaggle.com/datasets/arashnic/fitbit (CC0: Public Domain, dataset made available through Mobius

This dataset was generated by respondents to a distributed survey via Amazon Mechanical Turk between 03/12/2016-05/12/2016. Thirty eligible Fitbit users consented to the submission of personal tracker data. Data includes 18 sets of data including types of daily activity. However, only 6 datasets which are the following: daily activity, weight log, sleep, hourly steps, hourly intensities and hourly calories. Rest of the datasets are irrelevant for this analysis. 

Are there any issues with bias or credivitility of data source - Does it ROCCC? 
- Reliabile: Dataset is unreliable. Although central limit theorem applies as it sample size is 30, and therefore can use t test for statistical analysis, a bigger sample size would be more representative of the population. Furthermore, it does not include demographics such as gender, location, age, occupation etc.
- Original: not original data. data set through third party from Kaggle and from amazon mechanical turk.
- Comprehensive: Useful datasets are provided such as physical activity, heart rate per second and hourly activity. These factors are valuable for Fitbit analysis, however data is only recorded from Tuesday Wednesday and Thursday which makes it less comprehensive.  
- Current: Dataset is not current as it is from 7 years ago (2016). However, may still be useful for analysis. 
- Cited: Dataset states it is updated annually however last updated 2 years ago. Data set from Kaggle, user: MÖBIUS. 

Dataset is under CC0: public Domain lisecnce which means creator has copyright law. 

## 3. Process
Tools that will be used: Excel for data cleaning and Rstudio for analysis and creating visualizations. 
To ensure for data integrity, limitations of datasets will be accounted for by using excel to clean the data. The cleaned dataset overcomes he limitations and hence contributes to the overall accuracy, completeness and consistency of the data. 

Data cleaning process for each dataset: 
- Weight log: As stated before, data has 33 individuals studied. However, for Weight data, only 8 of them are included. This small sample size can bias our results. Used the text to column function to split date and time into separate columns. 
- Sleep: 3 duplicate values were found. These were removed now 410 unique values remain. Only 25 IDs included therefore only 25 individuals for sleep studied. Used the text to column function to split date and time into separate columns. Also, SleepDate date was incorrectly formatted, so changed the format into date column. 
- Hourly steps: Used the text to column function to split date and time into separate columns.
- Hourly intensity: Used the text to column function to split date and time into separate columns.
- Hourly calories: Used the text to column function to split date and time into separate columns.
 
Datamapping: In analysis stage, we need to ensure datasets are compatible so they datasets can be merged for analysis. By using text to column, we ensured headings (consistent naming conventions) and cell format were identical to all other datasets. Also by formatting all date columns in each dataset to ‘date’ ensures compatibility.  

## 4. Analyze
Cleaned dataset from excel has been imported and now ready for analysis. Daily activity and sleep datasets will be merged for further analysis. 

```
#create dataframes
daily_activity <- read.csv("dailyActivity_merged.csv")
sleep_day <- read.csv("sleepDay_merged.csv")
hourly_calories <- read.csv("hourlyCalories_merged.csv")
hourly_intensities2 <- read.csv("hourlyIntensities_merged.csv")
hourly_steps <- read.csv("hourlySteps_merged.csv")
weight_log <- read.csv("weightLogInfo_merged.csv")
```

```
#create summary statistics
daily_activity %>%  
  select(TotalSteps,
         TotalDistance,
         SedentaryMinutes) %>%
  summary()

sleep_day %>%  
  select(TotalSleepRecords,
         TotalMinutesAsleep,
         TotalTimeInBed) %>%
  summary()

hourly_calories %>%  
  select(ActivityHour, Calories) %>%
  summary()

hourly_intensities2 %>%  
  select(ActivityHour, TotalIntensity, AverageIntensity) %>%
  summary()

hourly_steps %>%  
  select(ActivityHour, StepTotal) %>%
  summary()

weight_log %>%  
  select(WeightKg, WeightPounds, Fat, BMI, IsManualReport) %>%
  summary()
```
![summary statistics2](https://user-images.githubusercontent.com/125687123/219881798-4e94d735-2fe6-4056-8f7d-09ece3ad3184.png)

```
#plotting relationship between steps taken and sedentary minutes 
ggplot(data=daily_activity, aes(x=TotalSteps, y=SedentaryMinutes)) + geom_point(colour="purple", size=0.5)+geom_smooth(method="lm")

```
![sedenmin](https://user-images.githubusercontent.com/125687123/219888135-85100c20-3380-4d7a-98ff-49e55906d732.jpeg)
![sedenmin]https://user-images.githubusercontent.com/125687123/219890444-e37bdb61-a0ee-4187-9d21-03cc1761d7b3.jpeg
