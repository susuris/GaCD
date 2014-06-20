## Course 'Getting and Cleaning data'
## Course project code book

### Data

Initial data was acquired on [data download](https://d396qusza40orc.cloudfront.net/getdata%2Fprojectfiles%2FUCI%20HAR%20Dataset.zip) and [data description](http://archive.ics.uci.edu/ml/datasets/Human+Activity+Recognition+Using+Smartphones).
This data contains Human Activity Recognition database built from the recordings of 30 subjects
performing activities of daily living while carrying a waistmoounted smartphone with embedded inertial sensors.

The data was gathered on 30 subjects and it contains measurements over 561 features and 6 activities 
(both described in files features.txt and activity_labels.txt). Also initial data was split into 2 sets - training set 
(7352 rows) and testing set (2947 rows).

### Data processing

Following processing was done with the provided database:
* training and testing sets were merged together;
* measuremenets were merged with corresponding subject and activity information;
* Only measurements of the mean and standard deviation for each measurement were extracted;
* Dataset with the averages of each variable for each activity and each subject was created and stored.

### Code description

The code 'run_analysis.R' does following steps of data processing:
1. Gets both test data sets and train data sets (measurements, subject and activity information) from the working directory;
2. Merges together both sets and their corresponding subject and activity information, resulting data set is labeled 'completeData';
3. Column names are acquired from text file 'features.txt'. This file was located in database. The column names of data frame 'completeData' are labeled according to these names.
4. Following data is extracted from 'completeDate' and saved as 'modifiedData':
	* first column containing subject information;
	* second column containing activity information;
	* all columns with 'mean()' in their name;
	* all columns with 'std()' in their name.
5. Activity information in data frame 'modifiedData' was changed from numerical ID to appropriate description from the file 'activity_labels.txt';
6. Information from 'modifiedData' is used to create data frame 'meanValues' that contains averages of each variable for each activity and each subject;
7. The data frame 'meanValues' is saved.