## Human-Activity-Recognition-Data

The project will read, clean, and prepare new analytic data from [Human Activity Recognition data](https://archive.ics.uci.edu/ml/datasets/Human+Activity+Recognition+Using+Smartphones)


### Read the data

A set of codes that will read the accompanying data for the train and test set. The train data files will be read first followed by the test data. Each train and test set will have three pairs of data files: 

- subject data
- X data
- Y data

The X data are the features and the Y data is the activity. In addition, the feature data file is independent of the train and test data that contains the names of the features. This file is a lookup for the feature names in the X data for the train and test set

### Data cleaning

The main aspect of the data cleaning will mostly include merging/combining the data files. Specifically, the the train and test data files will be merged for each of the 3 files mentioned above. That is, the subject data, X data, and Y data will be merged for the train and test set to make one merged file. After that the names in the feature column will be used for the column names in the merged data. Other columns will also be renamed such as V1 to subject_id.

The final step will include merging the subject file that contains subject id to the merged file

### select and summarise

Here we will do some data management to first select the mean and standard deviation columns only. Then we add the labels to the activity variable and rename it to activity. 

The final step is to summarise across the columns to create the average of each variable for each activity and each subject



