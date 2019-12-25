# How is crime influenced by the surroundings?

Contents

-Introduction/Business Problem  3  
--Problem   3   
--Target Audience        3  
-Data        3  
--Sources        3  
--Data Description        3  
--Linking data to problem        5  
-Methodology        5  
-Data Preparation &amp; Transformation        5  
-Methodology        5  
-Results        6  
-Result Discussion        6  
-Conclusion        6  
-Further next steps        6  



## Introduction/Business Problem

Crime is a problem in any city and being prepared and planning to avert them is the key to dealing with it. 
Crime occurs for various reasons and in various circumstances and could be localized based on the surroundings. It could be advantageous to understand the impact of the variables on the occurrence of crime to make it more decipherable in pattern and occurrence. 
Toronto, the capital of the province of Ontario, is the most populous Canadian city. and will be the focal for us in this exercise 

### Problem 
In this data analysis exercise , I am aiming to explore and identify quantitatively if there is a pattern to crime in terms of its surroundings i.e. what areas does  crime occur in , do the surrounding locations have an impact on the number and nature of the crime that happens in an area,  

### Target Audience

I am hoping that an analysis like this will help in planning for the police department - where and how should they organize themselves to better thwart crime

It will also help citizens plan their way around the city and be cautious by knowing that certain surroundings and locations are more likely targets for crime than others.

It might also help business who are willing to set shop pick areas to make it safe place to work for employees and for the business.

There might be some intuitions or hypothesis on areas and crime but a quantitative lens offers a more useful &amp; concrete way to evaluate those and will also help plan and act correctly.

## Data acquisition and cleaning

### Sources

Toronto city has taken steps in the last few years to democratize data and information and will be our source in this exercise.

The central data will be from the Toronto Police department on Major Crimes called the [MCI data](http://data.torontopolice.on.ca/datasets/mci-2014-to-2018)

Data on the location and other information about various venues in Toronto is from the Foursquare&#39;s explore API

### Data Description

Lets go through some key columns in MCI data.

The data has the nature of the crime in the MCI and Offence columns  

![alt text](https://github.com/nutan2357/ApDaScCaPr/blob/master/Img/data1.png)

It has latitude [column named Y] and longitude data [column named X] and the name of the neighbourhood  

![alt text](https://github.com/nutan2357/ApDaScCaPr/blob/master/Img/dat2.png)
 

It has occurrence date when the crime has occurred and reported date i.e. when the crime was reported. There are also a number of columns which break down the dates into days, years, months, weekdays etc.  

![alt text](https://github.com/nutan2357/ApDaScCaPr/blob/master/Img/dat3.png)   



![alt text](https://github.com/nutan2357/ApDaScCaPr/blob/master/Img/dat4.png)  

The Foursquare API is expected to give us venue details close to each crime geo coordinates

The details of how this data was extracted will be elaborated in the data preparation and transformation section of the report but he final data structure is as below  

![alt text](https://github.com/nutan2357/ApDaScCaPr/blob/master/Img/dat5.png)  


i.e. for each event id , where the crime occurred  

![alt text](https://github.com/nutan2357/ApDaScCaPr/blob/master/Img/dat6.png)  


The details of the venues which are within 300 m of the crime scene are listed along with Venue Name, Venue category and the location of the venue  

![alt text](https://github.com/nutan2357/ApDaScCaPr/blob/master/Img/dat7.png)  

### Linking data to problem

With the MCI and foursquare data we have

- Type of the Crime – [MCI] column in the data
- Details of the crime
  - When the crime occurred - [occurrencedate, &#39;occurrenceyear&#39;, &#39;occurrencemonth&#39;, &#39;occurrenceday&#39;, &#39;occurrencedayofyear&#39;, &#39;occurrencedayofweek&#39;, &#39;occurrencehour&#39;]
  - Where the crime occurred - [&#39;X&#39;, &#39;Y&#39;,&#39;Neighbourhood&#39;]
- Venues which are close to the location of crime scene
  - [&#39;Venue&#39;, &#39;Venue Latitude&#39;, &#39;Venue Longitude&#39;, &#39;Venue Category&#39;]
  -

This data now allows for understanding the relationship between the crime scene and the venues surrounding the crime scene and if a particular type of crime scene is related to the surrounding venues

## Methodology
### Data Preparation & Transformation 
The data from MCI is primarily from 2014-2018 . In this case we restricted our analysis to an years’ worth of data from 2016 also cut down on some of the columns. This gave a dataset of 32K rows and 19 columns to explore.  
Repeated columns like [lat, long] or unique ID columns [ucr_code,  ucr_ext, Division, hood-id, ObjectId ] are dropped off for the rest of the analysis   

![alt text](https://github.com/nutan2357/ApDaScCaPr/blob/master/Img/Method1.png)   

Each crime in the MCI data has an [event_unique_id] and each [event_unique_id] has geo coordinates in the form of [X, Y]  
These coordinates are used to query the foursquare API to get the details of the venues within a 300m radius of the crime scene   

Foursquare returns the results in the form of JSON . This JSON is then parsed to extract ['Venue', 'Venue Latitude', 'Venue Longitude', 'Venue Category'] details and these were then combined with the Crime scene event id [event_unique_id] and the coordinates of the crime scene [X, Y] to arrive the data set which contained all the venues within a 300 m radius of the crime scene

### Exploratory Data Analysis

The goal of EDA was to better understand the data and the patterns in the data which could help interpret the final modelling results better   

First the data was plotted to understand the distribution of the crimes across the city.   
Downtown Toronto has a larger share of crimes than other neighbourhoods as can be seen in the map below   

![alt text](https://github.com/nutan2357/ApDaScCaPr/blob/master/Img/eda1.png)  

The second highest number of crimes are in the north western part of the city   

Similar story comes from the neighbourhood list as well. Church-Yonge and Water front are communities in downtown Toronto and have the highest number of major crimes   
![alt text](https://github.com/nutan2357/ApDaScCaPr/blob/master/Img/eda2.png)  

A chart on the type of crime frequency indicates that Assault is a very prevalent crime and is almost 3X more frequent than the next frequent crime – Break and Enter.  
![alt text](https://github.com/nutan2357/ApDaScCaPr/blob/master/Img/eda3.png)   

Summer months , with the exception of October have a higher crime rate than the winter months  
![alt text](https://github.com/nutan2357/ApDaScCaPr/blob/master/Img/eda4.png)   

A pivot on the occurrence hour of crime by the type of crime , shows that   
-Assault is highest at midnight, but is also higher in the evenings & nights    
-Break & Enter has a different pattern, its relatively flat all through out the day but has a high during midnight(possibly as lesser number of people would be around )    
-Auto Theft, Robbery are more frequent during evenings and nights  
![alt text](https://github.com/nutan2357/ApDaScCaPr/blob/master/Img/eda5.png)    


To profile crimes better, they are compared against each other based on the occurrence day of the week.   
-Assault seems to occur equally frequently during any day , Weekends seem be relatively higher   
-Friday for Break and enter criminal and almost any day for an auto thief seem to be good days. Noticeably Break and enter seems the least frequent during Saturdays and Sundays . The auto theft graph is relatively flat all through the week  

![alt text](https://github.com/nutan2357/ApDaScCaPr/blob/master/Img/eda6.png)    


### Methodology

## Results

## Result Discussion

## Conclusion

### Further next steps
