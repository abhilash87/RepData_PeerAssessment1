---
title: "Assignment1"
author: "Abhilash Menon"
date: "Friday, January 16, 2015"
output: html_document
---

Assignment 1
**Loading and preprocessing the data**

Show any code that is needed to

Load the data (i.e. read.csv())

Process/transform the data (if necessary) into a format suitable for your analysis


```r
setwd("C:/Users/abhilash.s.menon/Downloads/Data Scientist/Codes/repdata-data-activity")
activity<-read.csv("activity.csv")
activity$date1<-as.POSIXct(activity$date,format = "%Y-%m-%d")
```

**What is mean total number of steps taken per day?**

For this part of the assignment, you can ignore the missing values in the dataset.

Make a histogram of the total number of steps taken each day

Calculate and report the mean and median total number of steps taken per day


```r
total_step<-tapply(activity$steps,activity$date1,sum,na.rm=TRUE)
hist(total_step)
```

![plot of chunk unnamed-chunk-2](figure/unnamed-chunk-2-1.png) 

```r
mean(total_step)
```

```
## [1] 9354.23
```

```r
median(total_step)
```

```
## [1] 10395
```

**What is the average daily activity pattern?**

Make a time series plot (i.e. type = "l") of the 5-minute interval (x-axis) and the average number of steps taken, averaged across all days (y-axis)

Which 5-minute interval, on average across all the days in the dataset, contains the maximum number of steps?


```r
day_time<-activity$interval
day_time<-day_time[1:288]
average_step_per_period<-tapply(activity$steps,activity$interval,mean,na.rm=TRUE)
plot(average_step_per_period,type="l")
```

![plot of chunk unnamed-chunk-3](figure/unnamed-chunk-3-1.png) 

```r
max_time<-which.max(average_step_per_period)
max_time2<-activity$interval[max_time]
activity$interval[max_time2]
```

```
## [1] 2130
```
**Imputing missing values**

Note that there are a number of days/intervals where there are missing values (coded as NA). The presence of missing days may introduce bias into some calculations or summaries of the data.

Calculate and report the total number of missing values in the dataset (i.e. the total number of rows with NAs)

Devise a strategy for filling in all of the missing values in the dataset. The strategy does not need to be sophisticated. For example, you could use the mean/median for that day, or the mean for that 5-minute interval, etc.

Create a new dataset that is equal to the original dataset but with the missing data filled in.

Make a histogram of the total number of steps taken each day and Calculate and report the mean and median total number of steps taken per day. Do these values differ from the estimates from the first part of the assignment? What is the impact of imputing missing data on the estimates of the total daily number of steps?
