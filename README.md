                                     Pittsburgh bike share Demand Prediction




Introduction:

Bike sharing systems have been increasing in demand over the past two decades as a result of rapid advancements in technology. Healthy Ride is a public bicycle sharing system that serves parts of Pittsburgh to fulfill the growing need for changes in mobility pattern. Healthy Ride is operated by Pittsburgh Bike Share and has plans for expansion to reach new neighborhoods by adding more stations, including several electric bikes to help riders navigate Pittsburgh’s hilly geography, located throughout the city. 
In this project, we determine the results of machine learning models such as decision tree, Lasso, Ridge Regression, Random forests, Support-Vector, XG Boosting, Gradient Boosting and Linear Regression. The effect of factors such as weather, geographic location, time of day, day of week. Bike score, Walk-score, distance between stations etc. on the number of bikes at bike-share station are investigated.

Problem:

Bike-sharing systems are used world-wide. Given that the system tends to be unbalanced, there are challenging analytical issues such as accurately predicting the demand. This project explores on predicting the total number of bikes rented from individual stations on any given day.

Clients:

Bike sharing operators can use this model to proactively shape the mobility market by forecasting demand prediction and to meet customer expectations.

Link to the final project:

https://github.com/aspiringdatascientist/Capstone-1-Bike-Share-Project/blob/master/Capstone%201%20project%20%20-%20Pittsburgh%20Bike%20share%20demand%20prediction%20(2).ipynb

Data Collection:

Healthy Ride operated by Pittsburgh Bike Share data: 

https://data.wprdc.org/dataset/healthyride-trip-data

This dataset includes bike number, membership type, trip start and end timestamp, and origin and
destination information as features. A trip is defined as any valid rental one minute or longer that 
begins and ends at a Healthy Ride station. The combined dataset has roughly about 285455 rows of 
data. 

Bike Station data:

https://healthyridepgh.com/data/

This dataset includes StationNum , StationName,  RackQnty, Latitude, Longitude as columns.

Weather data: and Storm data:

NOAA makes available their daily weather station data (I used station ID FIPS:42003) to extract the data.
Bike score, Transit Score, Walk score Data:

https://www.walkscore.com

Bike Score service measures whether a location is good for biking on a scale from 0 - 100 based on four equally weighted components: -Bike lanes, Hills, Destinations and road connectivity. Transit Score is a patented measure of how well a location is served by public transit on a scale from 0 to 100. Walk Score measures the walkability of any address.

Data Cleaning and Data Wrangling:

Step 1:

The csv files downloaded as Zip files from  Healthy Ride operated by Pittsburgh Bike Share data shows trips taken using the Healthy Ride system by quarter. I have selected csv files from 2015, Quarter 2 to 2018, Quarter 4. The consolidated csv files were loaded as pandas dataframe and saved as “Rentals” dataframe did not include Latitude and longitudes as features.I extracted unique matching longitude and Latitude columns based on station id and merged the coordinates with "Rentals" dataset.
dataset, I extracted unique matching longitude and Latitude columns as follows:

https://github.com/aspiringdatascientist/Bike-Share-Project/blob/master/longitudes%20and%20latitudes.ipynb

I merged  the coordinates with "Rentals" dataframe as below:

https://github.com/aspiringdatascientist/Bike-Share-Project/blob/master/pittsburgh_dataset_lat_lon.ipynb


Step 2:

 To fetch  the  scores such as Bike Score, Transit score, and Walk score information  from this website  for specific bike stations, the python code had to perform multiple  HTTP requests from a single query. The latitudes and longitudes extracted from “Healthy Ride Bike Stations” dataset as explained in Step 1 were first saved as a text file. The responses from API were extracted by looping through every single line in the text file containing matching latitudes and longitudes. The link below provides the details:
 
 https://github.com/aspiringdatascientist/Bike-Share-Project/blob/master/Pittsb_dataframe.ipynb

https://github.com/aspiringdatascientist/Bike-Share-Project/blob/master/bikescore_transitscore_walkscore.ipynb


Step3:

The Transit score and bike score column had irrelevant data and only the numeric score was retained. “Rentals” data frame was joined with “Transit score” data based on the common station ids. I extracted these station ids by merging “Station’s” dataset with “Transit Score” dataset using common latitudes & longitudes (rounding it off to 4 digits after the decimal point) in both datasets.
https://github.com/aspiringdatascientist/Bike-Share-Project/blob/master/data_cleaning1.ipynb


Step 4:

Seasons (fall, summer, winter, spring) were segregated based on the fixed dates of the solstices and equinoxes as below:

https://github.com/aspiringdatascientist/Bike-Share-Project/blob/master/Pittsburgh%20seasons.ipynb

Step 5:

Federal holidays (1" if it is a holiday or "0") were mapped to the main data frame. This was done by creating an instance of class custom business day and using this as frequency to extract federal holidays as explained in the link below:

https://github.com/aspiringdatascientist/Bike-Share-Project/blob/master/Pi_seasons_holidays_rentals.ipynb


Step 6:

Distances between stations are not included in Healthy Ride Bike share's data. To find distances based on Latitude and Longitudes, I used the  Haversine’s  formula . Later, the trips with ‘0’ distance were dropped since the start station id and the end station id were same and only the person who rented the bike knows about the distance covered and the duration of the trip taken per rental.
https://github.com/aspiringdatascientist/Capstone-1-Bike-Share-Project/blob/master/haversine's-Copy1.ipynb

Step 7:

A separate “weather” column was added to the main data frame after scoring, based on windspeed, rain, fog, lightening, temperature, and also event types such as tornados, hurricanes as below:
          0 = Worst weather including all the event types listed in the Storm dataset 
         1 = Moderate weather including
         2 = Good weather not listed in either 1 or 2 
         
         
Github link:

https://github.com/aspiringdatascientist/Bike-Share-Project/blob/master/weather%20final%20.ipynb
         
I formatted the “Storm” dataset downloaded from NOAA website  as below:

https://github.com/aspiringdatascientist/Bike-Share-Project/blob/master/stormalleghany2.ipynb

         
         

Step 8:

What is the number of bike rentals per day? This would be our target variable. To do this, a pandas group-by function was performed for counting the number of trips per day. 

https://github.com/aspiringdatascientist/Bike-Share-Project/blob/master/number%20of%20bike%20rentals.ipynb



