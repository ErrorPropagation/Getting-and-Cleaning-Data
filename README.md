# Getting-and-Cleaning-Data
Course Project for Coursera Course: Getting and Cleaning Data Feb. 2015

Version Date		Why	
1.0	02.17.2015	first try

Additional documentation: CodeBook.md

There is only one script to execute: run_analysis() ( file: run_analysis.R)

Assumptions: script and data are located in the working directory
Assertions: the package dplyr is loaded inside the script

The script performs several steps.

1. read file with column names from features.txt 
2. read file with activity labels from activity_labels.txt

For test data

3. read test data from X_test.txt
4. read test data activities from y_test.txt
5. read test data participants from subject_test.txt

likewise for training data

6. read training data from X_train.txt
7. read training data activities from y_train.txt
8. read training data participants from subject_train.txt

For test data

9. add two new columns to test data from subject_test.txt and y_test.txt
10. augment test data with column names from features.txt. The first two columns are added and named "subjects" and "activities"
11. from the resulting data frame select only columns which includes the pattern "mean" and "std" for standard deviation
12. the second column (activity) is coded with integers, starting with 1. The activity id's are replaced by activity lables from activity_labels.txt

Likewise for training data

13. add two new columns to training data from subject_train.txt and y_train.txt
14. augment training data with column names from features.txt. The first two columns are added and named "subjects" and "activities"
15. from the resulting data frame select only columns which includes the pattern "mean" and "std" for standard deviation
16. the second column (activity) is coded with integers, starting with 1. The activity id's are replaced by activity lables from activity_labels.txt

17. test and training data are merged and sorted by subject and activity label
18. for every subject and every activity column means are calculated
19. finally the resulting data are written to a file activityOut.txt in the working directory.
