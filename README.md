## MoBike -- Bay Area Bike Share Lifecycle Prediction

### Abstract

Bike share programs provide an environmentally friendly and healthy alternative to commuting within and exploring a city. However, Ford GoBike currently expends extra energy in order to consistently check on the condition of their bikes. To determine whether a bike is in need of repair, they depend on customer feedback or must send employees on frequent rounds to check up on bikes at each station. In this paper, we applied machine learning models to help For GoBike predict the total length of the lifetime for bikes within the San Francisco Bay Area. We defined the lifecycle of a bike to be the total duration for each of its trips before the bike was repaired or recycled. We determined this definition of lifecycle by using K-Means and Probability Distribution methods. We found the best intervals of inactivity between lifecycles (7 days and 4 days when parking station is changed) to group trips into distinct lifecycles. Data analysis was then conducted to study the relationship between lifecycle and potential features, including trip count, subscriber ratio, temperature, education level, etc. After that, we applied and compared Linear Regression with Lasso Regularization, Decision Tree, and Random Forest Models to predict the lifecycle of bikes based on features of trips, weather, income, education, and crime data. Through error analysis using the error percentage (defined in section 7) of the Linear Regression Model, we found and excluded outliers within the data. With the new trimmed dataset, we trained Decision Tree and Random Forest Models, and reached a better error percentage of 20%.

### Keywords

Bike Share, Lifecycle, Machine Learning, Linear Regression, Decision Tree, Random Forest


### Problem Statement
**1. Background**

Bike sharing systems are getting more and more popular in urban life, especially in big cities. Their automated features and convenient access have made them an important supplement to public transportation. However, the damaged bicycles which are still parked in stations may hinder the efficiency of the whole bike sharing system. Currently, it is technically hard for the bike sharing companies to determine when they should rotate their bicycles out of the system for maintenance. The only practical way to find out is to check regularly. Thus a forecast of bike lifetime would be of great help to this issue and would enable the bike sharing companies to plan their inventory budget accordingly. On top of that, it would also help ensure the hardware quality and thus reduce hardware risks to bike users.

**2. Related work**

There have been a number of studies conducted using the San Francisco bike share data to predict bike deficits at stations, trip duration, and other information about individual bike trips. The most popular kernel for the dataset on Kaggle is a model that predicts how many bike trips will occur on any given day using only known data from the morning of that particular day, such as weather, number of available bikes, and whether or not it is a business day. Wang et. al. conducted a different study using Minnesota bike share data to understand how nearby businesses and access to jobs correlate with bike share usage. Trip duration is another popular target variable using this dataset. One popular kernel on Kaggle uses correlations between available features, such as day of the week, year, season, and city (San Francisco vs. Palo Alto), to determine the duration of a bike trip. This is accomplished using a linear regression model. Another group predicted the bike station destinations and arrival times of bike trips. In order to predict these target variables, they used features about the users (subscriber status, gender), features about the department time (time, day), and features about the stations (location). To determine potential destinations, they used regression trees as their model. For trip duration, they used a lasso regression model. The goal of studies that explore individual trips like the ones above is often to help the bike share company predict surpluses and deficits at bike stations so that they may better optimize the stocking of their bikes. 


**3. Motivations**

In order to ensure each bike is being used to its maximum potential, the bike share company needs to quickly detect when a bike is in need of repair so that it is not just sitting unused at a station. Currently, Ford GoBike does not have an efficient system for checking up on its bikes. After speaking with a GoBike employee, we learned that there is a button on each bike for customers to notify the company that a bike is broken. In addition to this button, the employees will frequently go on rounds to each station to check on the statuses of the bikes. This takes a lot of time and unnecessary energy. We aim to predict the actual times that a bike becomes in need of repair so that the employees can check stations at targeted times.

### Objectives
**1. Research questions**

- How do external factors, namely, weather, crime, education, and income, affect the lifetime of a bike?

- Can we use trip, weather, crime, education, and income data to predict the length of a bike’s active duration (i.e. lifecycle)? 

**2. Expected outcomes**

We expected to see some visible patterns in the relationship between bike lifetimes and weather and crime data since bikes might fare worse in poor weather or suffer from vandalism in areas with high crime. Similarly, we thought that education and income might affect bike usage and therefore bike lifecycles. Our ultimate goal was to use all of our features to predict the time when a bike would need to be checked on for maintenance.

### Dataset
The main dataset we used is provided by Kaggle, which is in fact a transformed version of published data by Bay Area Bike Share. The data contains four parts, including station, status, trip, and weather data. The station data is for bike stations at which users can pickup or return their bikes. The status section is the number of bikes and docks available for a given station and minute. The trip section represents an individual bike trip. And weather represents the weather for a specific day and zip code. 

We also incorporated external weather, income, education and crime data. The weather data is provided by Weather Underground. Compared with the weather data by Kaggle, it provides more detailed hourly weather data with which we can use to correlate with each trip to get more precise relationship. Besides that, we also added income, education, crime data for each bike stations to explore how those data can influence the trip activity. 

The crime data is  provided by the San Francisco Police Department, Santa Clara County Police Department, Redwood City Police Department, and Palo Alto Police Department. We used this data to count how many crimes occurred in the same zip code locations as the bike stations. The education and income data is provided by United States Census Bureau, which has a detailed education and income reports.
