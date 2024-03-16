---
title: "Reproducible Research: Peer Assessment 1"
author: "Ivo Pinheiro"
date: "2024-03-16"
output: html_document
---

## Loading and preprocessing the data

- After downloading the file, I read the data in R using read.csv(). 
- I used str() and unique() on the 3 variables to get a sense of the data in terms of preprocessing at this stage. 


```r
library(tidyverse)
ActivityData <- read.csv("/Users/andreaaraujo/Downloads/Coursera_Project/activity.csv")
str(ActivityData)
```

```
## 'data.frame':	17568 obs. of  3 variables:
##  $ steps   : int  NA NA NA NA NA NA NA NA NA NA ...
##  $ date    : chr  "2012-10-01" "2012-10-01" "2012-10-01" "2012-10-01" ...
##  $ interval: int  0 5 10 15 20 25 30 35 40 45 ...
```

```r
unique(ActivityData$steps)
```

```
##   [1]  NA   0 117   9   4  36  25  90 411 413 415 519 529 613 562 612 534 323 600 533 251
##  [22]  56  32  80  10 145  46  44 126  42 138  53  22  57 161  19  15  16   8  51 516 245
##  [43]   7  72  73 116  97  69  99 100  33  88 154  20 198  61  75 193 298  21  26  39  52
##  [64]  41 159  34 128  47  18  40   1  17  49  86  29  59  30  31 113 181  87 507 522 510
##  [85] 508 423 499 259 453 229 144  82 180 160  79  66 127  28 496  78  77 354 310  37  92
## [106] 285 527 531 547 175 114  62  65 101  43  27 106 122  35   6  68  14  67 119  11  84
## [127]  50   2 171 400 451 371 470 473 512 449 530 509 252 541 555 345 485 515 168 349 341
## [148] 158 545 105 326 172 332 402  70  58  71  38 135 124 104 170 211 321 149  94 225 216
## [169] 199 187 173  95  64 221 439 440 394 443 500 465 351 511 506 486  12  24 140  48 115
## [190]  54  93  13 370 504 437 526 264 118 262  74 121  23 223 312 284 102 230 207 281 247
## [211] 235 334 389 414  83 146 422 523 165 142 107 190 290  45  63 257 748 743 727 393 667
## [232] 635 732 655 134 182 133 279 196 108 137  76   3 336 283  81 153 109  55  60 292 291
## [253] 317 129 103 125 176 340 271 272 308 111 139 260 364 219 174 205 152 112 619 446 424
## [274] 747 739 741 726 166 548 343 395 416  91 141 123 687 614 474 750 742 770 735 746 802
## [295] 280 328 156 339 150  96 267 365 432 275 433 463 248 542 265 497 476 479 491 488 498
## [316] 120 335 429 532 210 276 518 495 214  98 194 392 468 475 524 528 540 143 232 505 330
## [337] 250 302 520 535  85 157 224 786 315 781 757 686 592 203 581 406 178  89 758 721 697
## [358] 755 737 385 179 464 513 318 325 467 494 426   5 344 652 680 744 720 701 266 668 186
## [379] 241 163 408 297 483 319 759 618 608 568 571 355 286 362 167 303 428 236 258 311 282
## [400] 391 299 482 200 489 480 517 132 184 309 188 361 305 462 384 110 457 501 454 255 162
## [421] 729 783 756 715 713 136 403 263 375 472 487 396 189 192 376 209 346 237 304 201 261
## [442] 350 274 130 410 399 164 306 313 131 412 242 357 544 366 549 314 155 373 148 183 185
## [463] 208 380 204 289 401 397 591 477 213 425 436 594 749 717 751 714 301 584 358 206 492
## [484] 191 503 556 753 731 708 377 665 356 270 450 461 277 295 324 363 625 682 706 602 785
## [505] 754 638 606 404 630 372 195 238 294 387 197 243 643 573 690 745 698 766 466 147 322
## [526] 359 269 418 493 469 353 514 539 536 537 231 459 481 490 151 202 444 316 347 431 212
## [547] 471 427 639 597 368 733 405 681 634 725 177 333 718 738 789 559 546 327 693 679 736
## [568] 659 734 287 478 484 567 435 521 441 421 662 577 710 760 730 434 253 378 374 360 769
## [589] 768 765 752 293 551 331 320 244 388 458 456 256 709 611 637 442 794 777 767 806 417
## [610] 419 628 574 569 240 307 254 553 249
```

```r
unique(ActivityData$interval)
```

```
##   [1]    0    5   10   15   20   25   30   35   40   45   50   55  100  105  110  115  120
##  [18]  125  130  135  140  145  150  155  200  205  210  215  220  225  230  235  240  245
##  [35]  250  255  300  305  310  315  320  325  330  335  340  345  350  355  400  405  410
##  [52]  415  420  425  430  435  440  445  450  455  500  505  510  515  520  525  530  535
##  [69]  540  545  550  555  600  605  610  615  620  625  630  635  640  645  650  655  700
##  [86]  705  710  715  720  725  730  735  740  745  750  755  800  805  810  815  820  825
## [103]  830  835  840  845  850  855  900  905  910  915  920  925  930  935  940  945  950
## [120]  955 1000 1005 1010 1015 1020 1025 1030 1035 1040 1045 1050 1055 1100 1105 1110 1115
## [137] 1120 1125 1130 1135 1140 1145 1150 1155 1200 1205 1210 1215 1220 1225 1230 1235 1240
## [154] 1245 1250 1255 1300 1305 1310 1315 1320 1325 1330 1335 1340 1345 1350 1355 1400 1405
## [171] 1410 1415 1420 1425 1430 1435 1440 1445 1450 1455 1500 1505 1510 1515 1520 1525 1530
## [188] 1535 1540 1545 1550 1555 1600 1605 1610 1615 1620 1625 1630 1635 1640 1645 1650 1655
## [205] 1700 1705 1710 1715 1720 1725 1730 1735 1740 1745 1750 1755 1800 1805 1810 1815 1820
## [222] 1825 1830 1835 1840 1845 1850 1855 1900 1905 1910 1915 1920 1925 1930 1935 1940 1945
## [239] 1950 1955 2000 2005 2010 2015 2020 2025 2030 2035 2040 2045 2050 2055 2100 2105 2110
## [256] 2115 2120 2125 2130 2135 2140 2145 2150 2155 2200 2205 2210 2215 2220 2225 2230 2235
## [273] 2240 2245 2250 2255 2300 2305 2310 2315 2320 2325 2330 2335 2340 2345 2350 2355
```

```r
unique(ActivityData$date)
```

```
##  [1] "2012-10-01" "2012-10-02" "2012-10-03" "2012-10-04" "2012-10-05" "2012-10-06"
##  [7] "2012-10-07" "2012-10-08" "2012-10-09" "2012-10-10" "2012-10-11" "2012-10-12"
## [13] "2012-10-13" "2012-10-14" "2012-10-15" "2012-10-16" "2012-10-17" "2012-10-18"
## [19] "2012-10-19" "2012-10-20" "2012-10-21" "2012-10-22" "2012-10-23" "2012-10-24"
## [25] "2012-10-25" "2012-10-26" "2012-10-27" "2012-10-28" "2012-10-29" "2012-10-30"
## [31] "2012-10-31" "2012-11-01" "2012-11-02" "2012-11-03" "2012-11-04" "2012-11-05"
## [37] "2012-11-06" "2012-11-07" "2012-11-08" "2012-11-09" "2012-11-10" "2012-11-11"
## [43] "2012-11-12" "2012-11-13" "2012-11-14" "2012-11-15" "2012-11-16" "2012-11-17"
## [49] "2012-11-18" "2012-11-19" "2012-11-20" "2012-11-21" "2012-11-22" "2012-11-23"
## [55] "2012-11-24" "2012-11-25" "2012-11-26" "2012-11-27" "2012-11-28" "2012-11-29"
## [61] "2012-11-30"
```


## What is mean total number of steps taken per day?

- Here I used dplyr's group_by() and summarise() to calculate the total number of steps per day.
- I also used dplyr to calculate the mean and median (but I sense something went wrong with the median perhaps?)
- There's a histogram showing the total number of steps, and then for the mean and median calculations it's a tibble. 


```r
ForHistogram <- ActivityData %>% group_by(date) %>% summarise(TotalSteps = sum(steps))

ggplot(ForHistogram, aes(x = date, y = TotalSteps)) +
        geom_bar(stat = "identity") +
        labs(title = "Total Steps Taken Each Day", x = "Date", y = "Total Steps") +
        theme(axis.text.x = element_text(angle = 45, hjust = 1))
```

```
## Warning: Removed 8 rows containing missing values (`position_stack()`).
```

![plot of chunk Second](figure/Second-1.png)

```r
mean(ForHistogram$TotalSteps, na.rm = TRUE)
```

```
## [1] 10766.19
```

```r
mean(ForHistogram$TotalSteps)
```

```
## [1] NA
```

```r
ActivityData %>% group_by(date) %>% summarise(MeanSteps = mean(steps, na.rm = TRUE), 
                                              MedianSteps = median(steps, na.rm = TRUE))
```

```
## # A tibble: 61 × 3
##    date       MeanSteps MedianSteps
##    <chr>          <dbl>       <dbl>
##  1 2012-10-01   NaN              NA
##  2 2012-10-02     0.438           0
##  3 2012-10-03    39.4             0
##  4 2012-10-04    42.1             0
##  5 2012-10-05    46.2             0
##  6 2012-10-06    53.5             0
##  7 2012-10-07    38.2             0
##  8 2012-10-08   NaN              NA
##  9 2012-10-09    44.5             0
## 10 2012-10-10    34.4             0
## # ℹ 51 more rows
```


## What is the average daily activity pattern?

- Here I used dplyr again to first group by date and then get a mean of steps. I also had to use as.Date() to transform a variable into the right data type. Only then was I able to construct the plot.


```r
AverageSteps <- ActivityData %>% group_by(date) %>% summarise(MeanSteps = mean(steps, na.rm = TRUE))

typeof(AverageSteps$date)
```

```
## [1] "character"
```

```r
AverageSteps$date <- as.Date(AverageSteps$date)

typeof(AverageSteps$date)
```

```
## [1] "double"
```

```r
ggplot(AverageSteps, aes(x = date, y = MeanSteps)) +
        geom_line() +
        labs(x = "Date", y = "Steps", title = "Time series plot of the average number of steps taken")
```

```
## Warning: Removed 2 rows containing missing values (`geom_line()`).
```

![plot of chunk Third](figure/Third-1.png)

- To find out the interval with the maximum number of steps I used which.max() after grouping by interval. 


```r
IntervalMax <- ActivityData %>% group_by(interval) %>% summarise(AvgSteps = mean(steps, na.rm = TRUE))

IntervalMax[which.max(IntervalMax$AvgSteps), ]
```

```
## # A tibble: 1 × 2
##   interval AvgSteps
##      <int>    <dbl>
## 1      835     206.
```



## Imputing missing values

- First I calculated just how many missing values were present in the data. 


```r
sum(!is.na(ActivityData$steps))
```

```
## [1] 15264
```

```r
sum(is.na(ActivityData$steps))   
```

```
## [1] 2304
```

```r
sum(is.na(ActivityData$date))
```

```
## [1] 0
```

```r
sum(is.na(ActivityData$interval))
```

```
## [1] 0
```

```r
sum(is.na(ActivityData))/NROW(ActivityData)*100
```

```
## [1] 13.11475
```

- I decided to assign to every NA the value of the overall mean, as my strategy for imputing missing values.


```r
MyNAData <- ActivityData[is.na(ActivityData$steps), ]
unique(MyNAData$date)
```

```
## [1] "2012-10-01" "2012-10-08" "2012-11-01" "2012-11-04" "2012-11-09" "2012-11-10"
## [7] "2012-11-14" "2012-11-30"
```

```r
OverallMean <- mean(ActivityData$steps, na.rm = TRUE)

ActivityData2 <- ActivityData  
ActivityData2$steps[is.na(ActivityData2$steps)] <- OverallMean

ForHistogram2 <- ActivityData2 %>% group_by(date) %>% summarise(SumSteps = sum(steps))

ggplot(ForHistogram2, aes(x = date, y = SumSteps)) +
        geom_bar(stat = "identity") +
        labs(title = "Total Steps Taken Each Day w/ Imputed Values", x = "Date", y = "Total Steps") +
        theme(axis.text.x = element_text(angle = 45, hjust = 1))
```

![plot of chunk Fourth.2](figure/Fourth.2-1.png)

## Are there differences in activity patterns between weekdays and weekends?

- I used the lubridate package to answer this question and the patchwork package to build a panel with the two plots. 


```r
library(lubridate)
library(patchwork)

ActivityData$date <- ymd(ActivityData$date)

ActivityData$WhichDays <- ifelse(weekdays(ActivityData$date) %in% c("Saturday", "Sunday"), "Weekend", "Weekday")

WeekendData <- subset(ActivityData, WhichDays == "Weekend")
WeekdayData <- subset(ActivityData, WhichDays == "Weekday")

head(WeekdayData)
```

```
##   steps       date interval WhichDays
## 1    NA 2012-10-01        0   Weekday
## 2    NA 2012-10-01        5   Weekday
## 3    NA 2012-10-01       10   Weekday
## 4    NA 2012-10-01       15   Weekday
## 5    NA 2012-10-01       20   Weekday
## 6    NA 2012-10-01       25   Weekday
```

```r
head(WeekendData)
```

```
##      steps       date interval WhichDays
## 1441     0 2012-10-06        0   Weekend
## 1442     0 2012-10-06        5   Weekend
## 1443     0 2012-10-06       10   Weekend
## 1444     0 2012-10-06       15   Weekend
## 1445     0 2012-10-06       20   Weekend
## 1446     0 2012-10-06       25   Weekend
```

```r
WeekdayData$interval <- factor(WeekdayData$interval)
WeekendData$interval <- factor(WeekendData$interval)


WeekDayForPlot <- WeekdayData %>% group_by(interval) %>% summarise(MeanSteps = mean(steps, na.rm = TRUE))
WeekendsForPlot <- WeekendData %>% group_by(interval) %>% summarise(MeanSteps = mean(steps, na.rm = TRUE))

Plot1 <- ggplot(WeekDayForPlot, aes(x = interval, y = MeanSteps, group = "interval")) +
        geom_line() + 
        labs(x = NULL, y = "Steps", 
             title = "Average number of steps per 5-minute interval during the week...") +
        scale_x_discrete(breaks = seq(0, 2355, by = 200))

Plot2 <- ggplot(WeekendsForPlot, aes(x = interval, y = MeanSteps, group = "interval")) +
        geom_line() +
        labs(x = "5-minute intervals", y = "Steps", 
             title = "... and during weekends") +
        scale_x_discrete(breaks = seq(0, 2355, by = 200))

PanelPlot <- Plot1 + Plot2 + plot_layout(ncol = 1)
print(PanelPlot)
```

![plot of chunk Fifth](figure/Fifth-1.png)

## In conclusion

- The mean total of steps per day is 10766.19.
- The 5-minute interval with the maximum number of steps is 835.
- Some differences between weekdays and weekends are, for example, an earlier slope increase during the week at the 600 interval against around 800 in the weekend. Also, the weekend data has more activity between the 1200-1400 intervals compared the the weekend. Although the weekend has two small peaks after the 2200 interval and the weekday has none, the highest peak seems to happen during the week round the 800 interval at +200 on average. 

