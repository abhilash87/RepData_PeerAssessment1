---
title: "PA1_template.Rmd"
author: "Abhilash Menon"
date: "Sunday, September 14, 2014"
output: html_document
---

This is an R Markdown document. Markdown is a simple formatting syntax for authoring HTML, PDF, and MS Word documents. For more details on using R Markdown see <http://rmarkdown.rstudio.com>.

This assignment is to be done in several parts. First step is loading and preprocessing the data.

```r
activity<-read.csv("activity.csv")
activity<-activity[complete.cases(activity),]  #remove NA values
```

The next part of the code is aimed at drawing a histogram of the total number of steps taken each day. Also it gives mean and median total number of steps taken per day


```r
activity_aggr<-aggregate(activity$steps,list(date=activity$date),sum)
summary(activity_aggr)
```

```
##          date          x        
##  2012-10-02: 1   Min.   :   41  
##  2012-10-03: 1   1st Qu.: 8841  
##  2012-10-04: 1   Median :10765  
##  2012-10-05: 1   Mean   :10766  
##  2012-10-06: 1   3rd Qu.:13294  
##  2012-10-07: 1   Max.   :21194  
##  (Other)   :47
```

```r
hist(activity_aggr$x,col="grey")
```

![plot of chunk unnamed-chunk-2](figure/unnamed-chunk-2.png) 

```r
mean(activity_aggr$x)
```

```
## [1] 10766
```

```r
median(activity_aggr$x)
```

```
## [1] 10765
```

This part of the code gives an idea of the average daily activity pattern of the data and the interval for which daily average is maximum


```r
library(ggplot2)
activity_avg<-aggregate(activity$steps,list(interval=activity$interval),mean)
ggplot(data=activity_avg,aes(interval,x))+geom_line()
```

![plot of chunk unnamed-chunk-3](figure/unnamed-chunk-3.png) 

```r
activity_avg[max(activity_avg$x),]
```

```
##     interval    x
## 206     1705 56.3
```
Number of rows with NA values

```r
activity<-read.csv("activity.csv")
nrow(activity[is.na(activity$steps),])
```

```
## [1] 2304
```
