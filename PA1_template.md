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

```r
stepsInterval <- aggregate(data$steps, 
                           by = list(interval = data$interval), 
                           FUN = mean, 
                           na.rm = TRUE)

colnames(stepsInterval) <- c("interval", "steps")
ggplot(stepsInterval, 
       aes(x= interval, y = steps)) +   
    geom_line(size = 1, color="gray") +   
    labs(x = "Interval", 
         y = "Steps", 
         title = "Average Daily Activity Pattern")
```

![](PA1_template_files/figure-html/unnamed-chunk-5-1.png)


```r
maxInterval <- stepsInterval[which.max(stepsInterval$steps),]
paste("The interval having the most steps is interval ",
      maxInterval[1],
      sep="")
```

```
## [1] "The interval having the most steps is interval 835"
```
## Imputing missing values



## Are there differences in activity patterns between weekdays and weekends?
