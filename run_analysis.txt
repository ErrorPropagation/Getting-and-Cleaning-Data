run_analysis <-function(){
# What's going on here?
#	
# Coursera Course: Getting and Cleaning Data by Jeff Leek, PhD, Roger D. Peng, PhD, Brian Caffo, PhD
# Course Project
#
# Version	Date		Why	
# 1.0		02.17.2015	first try
#
# Additional documentation: README.md
#							CodeBook.md
#
# Requirements: https://class.coursera.org/getdata-011/human_grading/view/courses/973498/assessments/3/submissions
#--------------------------------------------------------------------------------------------------------------------------	

res=require("dplyr")
	if(res==FALSE){stop("dplyr package required!")}
# filepath for column labels and activity labels
	filepathFeatures=".\\features.txt"
	filepathActivity=".\\activity_labels.txt"
# filepath for training data, activities and subjects
	filepathTrain=".\\X_train.txt"
	filepathTrainy=".\\y_train.txt"
	filepathTrainingSubjects=".\\subject_train.txt"
# filepath for test data, activities and subjects
	filepathTest=".\\X_test.txt"
	filepathTesty=".\\y_test.txt"
	filepathTestSubjects=".\\subject_test.txt"
# filepath for output
	filePathOut=".\\activityOut.txt"
# reads and returns columns labels
	readFeatureLabels <-function(filesPath){
		featureLabels=read.table(filesPath,header=FALSE)
		return(featureLabels$V2)
	}
# reads and returns activity labels
	readActivityLabels <-function(filePath){
		activityLabels=read.table(filePath,header=FALSE)
		return(activityLabels$V2)
	}
# reads and returns training data
	readTrainingData<-function(filePath){
		trainingData=read.table(filePath,header=FALSE)
		return(trainingData)
	}
# reads and returns training activities
	readTrainingActivities<-function(filePath){
		trainingActivities=read.table(filePath,header=FALSE)
		return(trainingActivities)
	}
# reads and returns training subjects
	readTrainingSubjects<-function(filePath){
		trainingSubjects=read.table(filePath,header=FALSE)
		return(trainingSubjects)
	}
# reads and returns test data
	readTestData<-function(filePath){
		testData=read.table(filePath,header=FALSE)
		return(testData)
	}
# reads and returns test activities
	readTestActivities<-function(filePath){
		testActivities=read.table(filePath,header=FALSE)
		return(testActivities)
	}
# reads and returns test subjects
	readTestSubjects<-function(filePath){
		testSubjects=read.table(filePath,header=FALSE)
		return(testSubjects)
	}
# selects columns including the literals "mean" and "std"
# adds subjects and activities
# adds column names
# returns data frame
	composeData<- function(subjects,activities,data){
		ind=grep("*.mean.*|.*std.*",featureLabels)
		collectedData<-data[,ind]
		collectedData=cbind(subjects,activities,collectedData)
		colnames(collectedData)<-c("subjects","activities",as.character(featureLabels[ind]))
		for(i in 1:6) {
			collectedData$activities<-
				replace(collectedData$activities,collectedData$activities==i,as.character(activityLabels[i]))
		}
		return(collectedData)
	}
# merges test and training data
	mergeData<-function(trainingData,testData){
		totalData=rbind(trainingData,testData)
		ind<-order(totalData$subjects,totalData$activities)
		totalData<-totalData[ind,]
		return(totalData)
	}
# computes column means grouped by subject and activity
# returns data.frame with column mean
	computeMeans<-function(totalData){
		totalData=as.tbl(totalData)
		by_subjects_and_activities<-group_by(totalData,subjects,activities)
		totalMeans<-by_subjects_and_activities%>%summarise_each(funs(mean))
		totalMeans=data.frame(totalMeans)
		return(totalMeans)
	}
#
#-here we go -------------------------------------------------------------------------	
# reading feature and activity labels
	featureLabels=readFeatureLabels(filepathFeatures)
	activityLabels=readActivityLabels(filepathActivity)

# reading training data, activities and subjects
	trainingRaw=readTrainingData(filepathTrain)
	trainingActivities=readTrainingActivities(filepathTrainy)
	trainingSubjects=readTrainingSubjects(filepathTrainingSubjects)

# reading test data, activities and subjects
	testRaw=readTestData(filepathTest)
	testActivities=readTestActivities(filepathTesty)
	testSubjects=readTestSubjects(filepathTestSubjects)

# compose training data
	trainingData=composeData(trainingSubjects,trainingActivities,trainingRaw)

# compose test data
	testData=composeData(testSubjects,testActivities,testRaw)

# merge training and test data
	totalData=mergeData(trainingData,testData)

# compute means
	totalMeans=computeMeans(totalData)
	
	write.table(totalMeans,filePathOut,row.names=FALSE)
}
