---
title: "codebook.md"
author: "David E. Kaufman"
date: "Friday, March 20, 2015"
output: html_document
---

This repo is to analyze data collected by test subjects wearing the Samsung Galaxy S smartphone, specifically the accelerometers therein.  Detail on the data collection, as taken from the features_info.txt in the data package available from the original source:

> The features selected for this database come from the accelerometer and gyroscope 3-axial raw signals tAcc-XYZ and tGyro-XYZ. These time domain signals (prefix 't' to denote time) were captured at a constant rate of 50 Hz. Then they were filtered using a median filter and a 3rd order low pass Butterworth filter with a corner frequency of 20 Hz to remove noise. Similarly, the acceleration signal was then separated into body and gravity acceleration signals (tBodyAcc-XYZ and tGravityAcc-XYZ) using another low pass Butterworth filter with a corner frequency of 0.3 Hz.   
>
>
> Subsequently, the body linear acceleration and angular velocity were derived in time to obtain Jerk signals (tBodyAccJerk-XYZ and tBodyGyroJerk-XYZ). Also the magnitude of these three-dimensional signals were calculated using the Euclidean norm (tBodyAccMag, tGravityAccMag, tBodyAccJerkMag, tBodyGyroMag, tBodyGyroJerkMag).   
>
>
> Finally a Fast Fourier Transform (FFT) was applied to some of these signals producing fBodyAcc-XYZ, fBodyAccJerk-XYZ, fBodyGyro-XYZ, fBodyAccJerkMag, fBodyGyroMag, fBodyGyroJerkMag. (Note the 'f' to indicate frequency domain signals).   
> 
>
> These signals were used to estimate variables of the feature vector for each pattern:  
> '-XYZ' is used to denote 3-axial signals in the X, Y and Z directions.  
>
>
> A large number of derived values comprise the dataset, involving functions such as mean, standard deviation, max, min, and so on, in separate columns for each dimension (x,y,z).  Additional variables were estimated as averages over time windows.  
> 
> 
> See the description files in http://archive.ics.uci.edu/ml/datasets/Human+Activity+Recognition+Using+Smartphones for complete explanation.

To process the data, the script run_analysis.R proceeds as follows:
* Load the dplyr package
* Read the first set of observations of the variables.
* Read the column of numbers indicating which test subject provided each observation.
* Read the table mapping the specific activity code (1-6) to its translation (WALKING, STANDING,etc.)
* Merge the preceding tables to a main data frame holding all the observations and their variables for test subject ID and activity name
* Take a breath
* Repeat the preceding reads and merges for the second set of observations
* Put the two data frames (first set and second set) into a single frame (by rbind())
* Locate the column indices of all variables whose names involve mean or std (standard deviation)
* Select only those columns into a new data frame, but also including the test subject ID, activity code, and activity name
* Use aggregate() to compute means of each variable within groups defined by distinct combinations of test subject ID and activity name
* Write the final resulting table to a final output file AvgByActivityandSubject.txt

This is an R Markdown document. Markdown is a simple formatting syntax for authoring HTML, PDF, and MS Word documents. For more details on using R Markdown see <http://rmarkdown.rstudio.com>.

When you click the **Knit** button a document will be generated that includes both content as well as the output of any embedded R code chunks within the document. You can embed an R code chunk like this:

```{r}
summary(cars)
```

You can also embed plots, for example:

```{r, echo=FALSE}
plot(cars)
```

Note that the `echo = FALSE` parameter was added to the code chunk to prevent printing of the R code that generated the plot.
