# Prophet-forecasting-system
---
title: "MTH6139 Time Series"
subtitle: "Coursework 1"
author:
- name: Renjia Shi
date: "March 17th 2024"
output:
  html_document:
    toc: true
    toc_float: true
---


Meta’s Prophet forecasting system.

at first we load the prophet library to get the co2 data frame


```{r eval=FALSE, include=TRUE}
#download the data
install.packages("remotes")
remotes::install_github('facebook/prophet@*release', subdir='R')
library(prophet)
#define the datafrome
co2.df = data.frame(ds=zoo::as.yearmon(time(co2)),y=co2)
#define the model
model = prophet(df = co2.df, weekly = TRUE, daily = TRUE)
#define the future value
future.df = make_future_dataframe(model, periods=8, freq="quarter")
#predict the future value
pred.df = predict(model, future.df)
#plot the graph
plot(model,pred.df)
```



after all of this process we can get a co2 concentration graph
we can see this is a clear rising trend.



```{r, echo=FALSE}
htmltools::img(src = knitr::image_uri("QMlogo.png"), 
               alt = 'logo', 
               style = 'position:absolute; top:0; right:0; padding:10px; width:30%;')

co2.df = data.frame(
  ds=zoo::as.yearmon(time(co2)), 
  y=co2)
m = prophet::prophet(co2.df)
f = prophet::make_future_dataframe(m, periods=8, freq="quarter")
p = predict(m, f)
plot(m,p)

```



1.What is CO2 mean?

  The co2 dataset refers to a time series data set that records the atmospheric concentrations of carbon dioxide (CO2) over time.
  By running "?co2" we can get a help of "Mauna Loa Atmospheric CO2 Concentration"
Description
  Atmospheric concentrations of CO2 are expressed in parts per million (ppm) and reported in the    preliminary 1997 SIO manometric mole fraction scale.


Usage
  co2
  
Format
  A time series of 468 observations; monthly from 1959 to 1997.

Details
  The values for February, March and April of 1964 were missing and have been obtained by interpolating linearly between the values for January and May of 1964.

Source
  Keeling, C. D. and Whorf, T. P., Scripps Institution of Oceanography (SIO), University of California, La Jolla, California USA 92093-0220.
https://scrippsco2.ucsd.edu/data/atmospheric_co2/.

References
  Cleveland, W. S. (1993) Visualizing Data. New Jersey: Summit Press.

2.Explain the purpose of the project

  The purpose of the project is to find how the co2 concentration change by the time. Also to find the trend and the seasonality of this regression model.
  
3.Display some charts and explain what you see

From the plot we can see this is a positive rising trend.


```{r eval=FALSE, include=TRUE}
#we can summary the co2 plot
summary(co2.df)
```

```{r, echo=FALSE}
summary(co2.df)

```
From the summary we can see that in this datas, the largest data is in 1998 366.8, the mean of the data is 337.1 then the smallest measurement in the 468 datas is 313.2.
The median time point is 1978, meaning that half the data comes before this year and half comes after
These statistics suggest a data set with a steady progression over time and an increasing trend in the 'y' variable. The summary implies growth in the 'y' variable from at least 313.2 to 366.8 over the 40-year period.


```{r eval=FALSE, include=TRUE}
#we can randomly pick a specific number
specific_value <- co2.df[24, 2]
```

```{r, echo=FALSE}
specific_value <- co2.df[24, 2]

```



Meanwile we can analyze local data.


```{r eval=FALSE, include=TRUE}
#By running the fowwing code we can get the first ten data in co2.df
head(co2.df, 10)
```




          ds      y
1   Jan 1959   315.42

2   Feb 1959   316.31

3   Mar 1959   316.50

4   Apr 1959   317.56

5   May 1959   318.13

6   Jun 1959   318.00

7   Jul 1959   316.39

8   Aug 1959   314.65

9   Sep 1959   313.68

10  Otc 1959   313.18



```{r, echo=FALSE}
plot(head(co2.df, 10),type='o',xlab="year",ylab="co2 concentration")


```


In this 10 data we can see in 1959 the co2 concentration didn't change too much. We have the highest data in May. And the lowest data in October.

Then by running 'max_y <- with(co2.df, max(y))'
we can get through all of the 468 datas, the largest data is 366.84.






```{r eval=FALSE, include=TRUE}
#By running this code we can get the last ten data in co2.df
tail(co2.df, 10)
```



           ds      y
           
459  Mar 1997  364.61

460  Apr 1997  366.40

461  May 1997  366.84

462  Jun 1997  365.68

463  Jul 1997  364.52

464  Aug 1997  362.57

465  Sep 1997  360.24

466  Oct 1997  360.83

467  Nov 1997  362.49

468  Dec 1997  364.34



```{r, echo=FALSE}
plot(tail(co2.df, 10),type='o',xlab="year",ylab="co2 concentration")


```


 
From the data we can see the largest data in here is 366.84. The smallest data is 360.24.
This is not a clear rising or droing trend.
we can conclude all of the plot, that as the time go, the concentration of co2 is keep rising, the air is more dirty.




```{r setup, include=FALSE}

knitr::opts_chunk$set(echo = TRUE)


```

