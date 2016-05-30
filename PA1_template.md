# Reproducible Research: Peer Assessment 1
Mac McEacharn  

## Loading and preprocessing the data


```r
library(ggplot2)
if (!file.exists("activity.csv") && file.exists("activity.zip")) {
    unzip("activity.zip", exdir = ".")
}
data <- na.omit(read.csv("activity.csv"))
data$date <- as.Date(data$date, format = "%Y-%m-%d")
```


## What is mean total number of steps taken per day?

```r
stepsDay <- tapply(data$steps, data$date, sum)

qplot(x=stepsDay,  
      binwidth = 1000,
      xlab = 'Total Steps per Day', 
      ylab = 'Frequency (binwith=1000)')
```

![](PA1_template_files/figure-html/unnamed-chunk-2-1.png)


```r
meanStepsDay <- mean(stepsDay,na.rm=TRUE)
paste("Mean Steps per Day=",meanStepsDay)
```

```
## [1] "Mean Steps per Day= 10766.1886792453"
```


```r
medianStepsDay <- median(stepsDay,na.rm = TRUE)
paste("Median Steps per Day=",medianStepsDay)
```

```
## [1] "Median Steps per Day= 10765"
```


## What is the average daily activity pattern?



## Imputing missing values



## Are there differences in activity patterns between weekdays and weekends?
