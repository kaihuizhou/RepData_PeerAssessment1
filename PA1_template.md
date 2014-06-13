# Reproducible Research: Peer Assessment 1


## Loading and preprocessing the data

Show any code that is needed to

1. Load the data (i.e. read.csv())


```r
dat <- read.csv("activity.csv")
```


2. Process/transform the data (if necessary) into a format suitable for your analysis




## What is mean total number of steps taken per day?

For this part of the assignment, you can ignore the missing values in the dataset.

1. Make a histogram of the total number of steps taken each day


```r
steps_perday <- tapply(dat$steps, dat$date, sum, na.rm = TRUE)
hist(steps_perday, breaks = 20)
```

![plot of chunk unnamed-chunk-3](figure/unnamed-chunk-3.png) 


2. Calculate and report the mean and median total number of steps taken per day


```r
meansteps_perday = mean(steps_perday)
mediansteps_perday = median(steps_perday)
```


mean and median total number of steps taken per day are 9354.2295 and 10395

## What is the average daily activity pattern?

1. Make a time series plot (i.e. type = "l") of the 5-minute interval (x-axis) and the average number of steps taken, averaged across all days (y-axis)


```r
steps_perinterval <- tapply(dat$steps, dat$interval, mean, na.rm = TRUE)
intervals <- dimnames(steps_perinterval)[[1]]
plot(intervals, steps_perinterval)
```

![plot of chunk unnamed-chunk-5](figure/unnamed-chunk-5.png) 


2. Which 5-minute interval, on average across all the days in the dataset, contains the maximum number of steps?


```r
maxsteps_interval <- names(which(steps_perinterval == max(steps_perinterval)))
```


the 5-minute interval "835", contains the maximum number of steps

## Imputing missing values

Note that there are a number of days/intervals where there are missing values (coded as NA). The presence of missing days may introduce bias into some calculations or summaries of the data.

1. Calculate and report the total number of missing values in the dataset (i.e. the total number of rows with NAs)

2. Devise a strategy for filling in all of the missing values in the dataset. The strategy does not need to be sophisticated. For example, you could use the mean/median for that day, or the mean for that 5-minute interval, etc.

3. Create a new dataset that is equal to the original dataset but with the missing data filled in.

4. Make a histogram of the total number of steps taken each day and Calculate and report the mean and median total number of steps taken per day. Do these values differ from the estimates from the first part of the assignment? What is the impact of imputing missing data on the estimates of the total daily number of steps?

## Are there differences in activity patterns between weekdays and weekends?

For this part the weekdays() function may be of some help here. Use the dataset with the filled-in missing values for this part.

1. Create a new factor variable in the dataset with two levels - "weekday" and "weekend" indicating whether a given date is a weekday or weekend day.

2. Make a panel plot containing a time series plot (i.e. type = "l") of the 5-minute interval (x-axis) and the average number of steps taken, averaged across all weekday days or weekend days (y-axis).
