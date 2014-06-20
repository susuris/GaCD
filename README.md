## This repo contains course project for course 'Getting and cleaning data'.

* For description of the script's functionality and used data see file **'CodeBook.md'**.

* The following script is used for doing the course project and is saved in the file **'run_analysis.R'**:

```
library(plyr)
# Setting the directory where databaseis located
getwd()
setwd("C:/Users/Liga/Documents/Coursera/GaCD/UCI HAR Dataset")

# Getting test data sets
X_test<-read.table("test/X_test.txt")
Y_test<-read.table("test/Y_test.txt")
subject_test<-read.table("test/subject_test.txt")

# Getting train data set
X_train<-read.table("train/X_train.txt")
Y_train<-read.table("train/Y_train.txt")
subject_train<-read.table("train/subject_train.txt")

# Merging data together
testData<-cbind(subject_test,Y_test,X_test)
trainData<-cbind(subject_train, Y_train, X_train)
completeData<-rbind(data1,data2)

# getting and setting column names
Features<-read.table("features.txt")
dataNames<-as.vector(Features[['V2']])
dataNames<-c("Subject","Activity",dataNames)
names(completeData)<-dataNames

# extract only the measurements on the mean
# and standard deviation for each measurement.
modifiedData<-data[,grepl("mean()", names(data))|
                       grepl("std()", names(data))|
                    grepl("Subject", names(data))|
                    grepl("Activity", names(data))]

# get and add activily labels
activityLabels <- read.table("activity_labels.txt")
names(activityLabels)<- c("Activity","Activity_Name")

from <- as.vector(activityLabels[['Activity']])
to <- as.vector(activityLabels[['Activity_Name']])

gsub2 <- function(pattern, replacement, x, ...){
  for (i in 1:length(pattern))
    x<-gsub(pattern[i],replacement[i],x,...)
  x
}

modifiedData$Activity<-gsub2(from,to,modifiedData$Activity)

# Creates a second, independent tidy data set with the average of each
# variable for each activity and each subject.
meanValues<-ddply(ModifiedData1,.(Activity,Subject),colwise(mean))

# Resulting table is saved
write.table(meanValues,file = "C:/Users/Liga/GaCD/MeanValues.txt")
```