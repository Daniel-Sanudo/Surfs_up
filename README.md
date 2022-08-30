# Surfs_up

This project is aimed at analyzing the precipitation and weather data through the season to determine the viablity of a surf and ice cream shop at Hawaii using SQLalchemy, python and pandas.

## Overview

The analysis is done by extracting the data from the dataset that holds the precipitation and temperature measurements for different dates ranging from 2010 to 2017. Since these record hold historical data, it's possible to use them to determine how likely the surf and ice cream shop bussiness ideas are to succeed.

A python engine is first set up to connect with the datase which in this case is a sqlite file. After connecting to the engine, the data in each table from the sqlite file is reflected into the measurement (which holds the station, date, precipitation and temperature data) class and the station (which holds the station, station name, latitude, longitude and elevation data) class.

Once this is done, it is now possible to query the data using either SQL queries with engine.execute as shown here:

'''
engine.execute('SELECT date, tobs  FROM measurement WHERE date LIKE "%-xx-%"').fetchall()
'''

It's also possible to query the data using python as shown in the next example:

'''
session.query(Measurement.date, Measurement.tobs).filter(func.strftime("%m", Measurement.date) == 'xx').all()
'''

In both cases, xx refers to the month number. For this analysis, the information for June (06) and December (12) is queried.

By using pands, it's possible to transform the queried information into a DataFrame with the following segment of code:

'''
pd.DataFrame(mmmm_Temperatures, columns=['date','temperature'])
'''

Where mmmm refers to the month's name. 

## Results

The DataFrames were created using the code block quoted previously are summarized and are included below:

### June

![June_Summary](/Resources/June_Temperature_Summary.png)

### December
![December_Summary](/Resources/December_Temperature_Summary.png)

### Key Differences

* The first difference between both summarizations is the amount of data entries each had. Although December has 1 more day than June, it has less data entries (1700 for June vs 1517 for December)

* The minimum temperature that was registered from 2010 to 2017 shows the biggest difference between the two months. December, being part of the Winter months, has a minimum registered temperature of 56°F while June has a minimum temperature of 64°F, resulting in a maximum difference of 8°F. 

* The maximum temperature registered during both months is really close to each other, with June having a max heat of 85°F and December a max heat of 83°F

## Summary

This information shows that while there is a more noticeable difference on cold days during winter, there are also days which are almost as hot as June during winter. Moreover, the temperatures from the three quartiles is well within each other. Thus the icecream business would still be able to operate during winter season.

### Additional findings

![Temperature_Per_Station](/Resources/Temperatures_Per_Station.png)

This query extracts the maximum, minimum and average temperature record for all the registered data at each station through all their data entries from 2010 to 2017. To make it more readable, the station code is changed to its respective name.

This shows that the temperature readings through the different stations remain consistent, so going by the temperature, all locations remain viable.

![Precipitation_Per_Station](/Resources/Precipitation_Per_Station.png)

Unlike the temperature per station table, the maximum precipitation does show some deviation through the zones. The maximum registered precipitation is 11.53 at Kualoa Ranch Headquarters; however this location does not have the highest average; it belongs to Manoa Lyon Arbo. Thus it could be infered that Manoa Lyon Arbo has constant rain through its seasons while Kualoa Ranch can experience heavy rains occasionally. 

Inside the SurfsUp_Challenge.ipynb jupyter notebook are included the bar charts that plot all da data entries for each station as a visual comparison. Each station has its own max temperature and minimum temperature plot; these plots serve as a quick comparison about how the weather has changed through the years for each month at each station.