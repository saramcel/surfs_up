# Surf's Up

## Overview

We are hoping to open a new surf and ice cream shop on the beach in Oahu. First, our investor W. Avy is interested in a weather analysis to make sure that we are going to have enough demand (e.g. ensure that enough visitors will be on the island enjoying outdoor activities). 

### Purpose

The purpose of this weather analysis is to provide information to the investor W. Avy so that he can be confident that our surf supply and ice cream shop will have customers all year long. The temperature analysis from June and December will provide a good contrast for the kind of weather typical to Oahu. 

## Results
The following sections contain the June and December temperature summary statistics and three key differences between these two months. 

### June 

![June_Temperature_Stats](https://github.com/saramcel/surfs_up/blob/07bf5e2f45ba3dfdfbabeccdf9211f97eb247359/Resources/June_Temps_Stats.png)

### December

![December_Temperature_Stats](https://github.com/saramcel/surfs_up/blob/07bf5e2f45ba3dfdfbabeccdf9211f97eb247359/Resources/Dec_Temps_Stats.png)

* There are 183 (11%) fewer observations of December temperatures compared to June temperatures. Knowing this, we might view the December statistics as slightly less reliable than the June statistics. 
* Compared with June, December stats for mean temperature, maximum temperature, and each quartile are all 3-4 degrees less. This indicates that most of the time, the temperatures for each of these seasons is relatively similar. However, there is one exception: the minimum temperature.
* The minimum temperature for June 2010 to June 2017 is 64 degrees Fahrenheit. The minimum temperature for December 2010 to December 2016 is 56 degrees Fahrenheit. Although this is only an 8 degree difference, it indicates that it is possible for December to be noticeably cooler than June in Oahu. 

## Summary

The analysis showed promising results for the surf and ice cream shop. The temperature statistics from June and December did not show large differences, with December usually only about 3-4 degrees cooler than June. However, the minimum temperature is noticably cooler in December, so there might be a good reason to come up with a backup plan when the water is too cold to surf, and ice cream will be less popular. For example, we could also sell coffee and a small selection of sandwiches. 

### Additional Queries

* Query 1: The first suggested query is to plot all of the daily temperatures to examine whether there are trends due to climate change. 

```
# Suggestion 1: putting the temps in order and plotting trends
results3 = session.query(Measurement.date, func.avg(Measurement.tobs)).\
group_by(Measurement.date).order_by(Measurement.date).all()

df3 = pd.DataFrame(results3, columns=['date','tobs'])
# Sort the dataframe by date
df3.set_index(df3['date'], inplace=True)
df3 = df3.sort_index()
print(df3)

# Use Pandas Plotting with Matplotlib to plot the data
df3.plot(figsize=(50,20))
```

* Result of Query 1

![Query 1 Results](https://github.com/saramcel/surfs_up/blob/43d347243a44df37d81a20d6e0b4d88994baf8c3/Resources/Results_Query_1.png)

The dataframe shows that the data goes from 1-1-2010 to 8-23-2017. For that time period, the chart shows the average daily temperature observation. There is seasonal oscillation, but there is also a slight linear trend upward, towards hotter summers. The winter temperatures still reach the normal lows even in more recent observations.

* Query 2: The second suggested query is to plot the percipitation to see whether there are more extreme storms due to climate change. 

```
# Suggestion 2: Plotting precipitation trends
results4 = session.query(Measurement.date, func.max(Measurement.prcp)).\
group_by(Measurement.date).order_by(Measurement.date).all()


df4 = pd.DataFrame(results4, columns=['date','prcp'])
# Sort the dataframe by date
df4.set_index(df4['date'], inplace=True)
df4 = df4.sort_index()
print(df4)

# Use Pandas Plotting with Matplotlib to plot the data
df4.plot(figsize=(40,10))
```

* Result of Query 2

![Query 2 Results](https://github.com/saramcel/surfs_up/blob/43d347243a44df37d81a20d6e0b4d88994baf8c3/Resources/Results_Query_2.png)

This long chart has no apparent trends. Every few months there are some extreme precipitation events followed by a short period of dryness, but these extreme amounts of precipitation do not seem to be getting obviously worse or more frequent over time.
