# How is crime influenced by the surroundings?

Contents

-Introduction/Business Problem  3  
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

In this data analysis exercise , I am aiming to explore and identify quantitatively if there is a pattern to crime i.e. what areas does  crime occur in and do the surrounding locations have an impact on the number and nature of the crime that happens in an area.

Toronto, the capital of the province of Ontario, is the most populous Canadian city. and will be the focal for us in this exercise

### Target Audience

I am hoping that an analysis like this will help in planning for the police department - where and how should they organize themselves to better thwart crime

It will also help citizens plan their way around the city and be cautious by knowing that certain surroundings and locations are more likely targets for crime than others.

It might also help business who are willing to set shop pick areas to make it safe place to work for employees and for the business.

There might be some intuitions or hypothesis on areas and crime but a quantitative lens offers a more useful &amp; concrete way to evaluate those and will also help plan and act correctly.

## Data

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

### Data Preparation &amp; Transformation

### Exploratory Data Analysis

### Methodology

## Results

## Result Discussion

## Conclusion

### Further next steps
