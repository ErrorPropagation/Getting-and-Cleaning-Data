Course Project for Coursera Course: Getting and Cleaning Data Feb. 2015

Version Date		Why	
1.0	02.17.2015	first try

Additional documentation: README.md

A. Data Description 

The data sets to work with, consists of two groups (training and test data)
For every group there three files

For the training data
1. Filename X_train.txt: consists of measurements for different participants and different activities
2. Filename y_train.txt: consists of the employed activities for each participant
3. Filename subject_train.txt: consists of the ids of the participants

For the test data
1. Filename X_test.txt: consists of measurements for different participants and different activities
2. Filename y_test.txt: consists of the employed activities for each participant
3. Filename subject_test.txt: consists of the ids of the participants

In addition 
The file activity_labels.txt contains the labels of the activities.
The file features.txt contains the column names.

B: Requirements:

1. The activities and participant's id are not included in the training or test data and must be added.
2. Only columns witch indicate means or standard deviations are of interest. The resulting tidy data set should have column names.
3. training and test data are merged into one file
4. from the resulting file a new file has to be created. This file contains for every participant and every activity the column mean for every column.

C: Processing.

For the training data:

1. read the training data (X_train.txt)
2. read the subject id's from subject_train.txt 
3. read the activity id's from y_train.txt 
4. the test data are complemented with two columns to the left (subject and activity) from subject_train.txt and y_train.txt
5. the test data are complemented with column headers from features.txt. The first two columns are named "subjects" and "activities"
6. all columns which do not contain "mean" or "std" are removed
7. all activity id's are replaced by activity labels from activity_labels.txt

Likewise for test data:

1. read the test data (X_test.txt)
2. read the subject id's from subject_test.txt 
3. read the activity id's from y_test.txt 
4. the test data are complemented with two columns to the left (subject and activity) from subject_test.txt and y_test.txt
5. the test data are complemented with column headers from features.txt. The first two columns are named "subjects" and "activities"
6. all columns which do not contain "mean" or "std" are removed
7. all activity id's are replaced by activity labels from activity_labels.txt

The augmented test and training data are merged and sorted by subject id and activity labels
Form the resulting data columns means are computed for every subject and activity.

Finally the resulting data are stored in a text file named activityOut.txt. The output file 
