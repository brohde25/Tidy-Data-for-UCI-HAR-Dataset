# Tidy-Data-for-UCI-HAR-Dataset
Getting and Cleaning Coursera Data Project
Course Project demonstrating tidying data for Coursera “Getting and Cleaning Data”

This repo contains the R scripts to be used to analyze the UCI HAR dataset (Human Activity Recognition Using Smartphones Data Set)located at http://archive.ics.uci.edu/ml/datasets/Human+Activity+Recognition+Using+Smartphones#
and convert it into a tidy data set.

Project Requirements
You should create one R script called run_analysis.R that does the following. 
	1.	Merges the training and the test sets to create one data set.
	2.	Extracts only the measurements on the mean and standard deviation for each measurement. 
	3.	Uses descriptive activity names to name the activities in the data set
	4.	Appropriately labels the data set with descriptive variable names. 
	5.	From the data set in step 4, creates a second, independent tidy data set with the average of each variable for each 		activity and each subject.
	Code Book for Tidy UCI HAR Dataset describes the specific details of variables, values, and units in the tidy dataset.

The tidy_dataset.txt file in this directory is a tidy subset of the data provided in the Human Activity Recognition Using Smartphones Data Set. 

Description of run_analysis.R
	run_analysis.R script takes source data from the unzipped file of the UCI HAR Dataset directory, imports it into R, and 		transforms it into a tidy data subset. 

	The script performs the following operations to import, clean, and transform the data set. These steps are also indicated 	in comments throughout the .R file.
	1.	Read and merge the training and test data into one data set. 
		i.	Combine the values from the subject_test and subject_train files to create a single TestSubject column that 				identifies the study participant.
		ii.	Combine the values from the Y_test and Y_train data to create a single Activity column that indicates that 					activity class (for instance, walking or sitting).
		iii.	Combine the values from the X_test and X_train files to create additional variable columns, one column for 				each measurement and calculation included in the data set (561 variable columns total, in the initial combined 				data set; 563 columns including the TestSubject and Activity columns).
		iv.	Clean up the column names to remove hyphens and parentheses and replace them with periods.
	2.	Extract only the measurements on the mean and standard deviation for each measurement. 
		i.	The dplyr select function is used to create a subset of the data consisting of columns that have ".mean." and "				.std." in their column names.
		ii.	The script converts the test subject and activity columns to factors, to facilitate correct calculations later.
	3.	Use descriptive activity names to name the activities in the data set. 
		i.	Use the mapvalues function to map the numeric activity values to descriptive names like "Walking" and "Standing."
	4.	Appropriately label the data set with descriptive variable names. 
		i.	Use the stringr_replace_all function from the stringr library to do find and replace operations on the column 				names. The details of the resulting descriptive names are included in Code Book for Tidy UCI HAR Dataset
	5.	From the data set in step 4, create a second, independent tidy data set with the average of each variable for each 				activity and subject. 
		i.	Use split/apply/combine logic. First, split the data by subject and activity factors using  split method.
		ii.	Next, use lapply to iterate over each item in the created list, and use apply to apply the mean function to 				calculate the average of each column. 
		iii.	The output of lapply is a list, so combine it back to a data frame.
		iv.	Use strsplit to break the subject and activity factors back into separate sets, and use cbind to bind them as the 		first columns in the resulting data set. 
	6.	The tidy data set can be loaded back into R using the following command
		i.	read.table("tidy_dataset.txt", header = TRUE, colClasses=c('factor','factor', rep('numeric',66)))
		
Special instructions for running run_analysis.R
		•	The script assumes that the untouched data source files from UCI HAR Dataset are unzipped in the current 				  		working director. 
		•	The references to file locations in run_analysis.R are written to work with the Windows operating system.  
		

