# Reproducible Research: Peer Assessment 1



## Loading and preprocessing the data


```r
unzip("activity.zip")
activity <- read.csv("activity.csv")
```

## What is mean total number of steps taken per day?

### Summarize by date

Group the data by date and compute the sum of steps taken per day. For this computation, NAs were removed . 
Column `interval` is not relevant for this summary, so we use the special `summarise_each_()` function to exclude it.


```r
library(dplyr)
groupByDay <- group_by(activity, date) 
stepsPerDay <- 
    summarise_each_(groupByDay, 
                    funs(sum(., na.rm = TRUE)), 
                    list(quote(-interval)))
```

### Histogram of steps per day


```r
library(ggplot2)
qplot(steps, data = stepsPerDay,
      main = "Histogram of steps per day",
      fill = I("wheat"),
      col = I("black"))
```

![](PA1_template_files/figure-html/histogramStepsPerDay-1.png) 

### Mean and median of steps per day


```r
meanStepsPerDay <- mean(stepsPerDay$steps)
medianStepsPerDay <- median(stepsPerDay$steps)
```

Of the total number of steps taken per day, the mean is 9354.2295082 and the median is 10395.

## What is the average daily activity pattern?



## Imputing missing values



## Are there differences in activity patterns between weekdays and weekends?
