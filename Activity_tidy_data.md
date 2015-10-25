Activity Tidy data cookbook
===========================

This document provides the definition of the activity data summaraised
at the Subject and Activity level. The data structure and definition are
explained at the end of processing.

Download Files
--------------

    # library(utils)
    # #Download File
    # setwd("C:/CourseraR/GettingandCleaning/Assigment1/code")
    # fileURL <- "https://d396qusza40orc.cloudfront.net/getdata%2Fprojectfiles%2FUCI%20HAR%20Dataset.zip"
    # download.file(fileURL, destfile = "../data/FUCR.zip")
    # unzip("../data/FUCR.zip", exdir = "../data")

Load Training Data
------------------

    #Load Training DataSets
    actv_lvls <- read.table(file = "../data/UCI HAR Dataset/activity_labels.txt")
    feat <- read.table(file = "../data/UCI HAR Dataset/features.txt")

    sub_trn <- read.table("../data/UCI HAR Dataset/train/subject_train.txt")
    X_trn <- read.table("../data/UCI HAR Dataset/train/X_train.txt")
    Y_trn <- read.table("../data/UCI HAR Dataset/train/y_train.txt")

    names(X_trn) <- feat$V2
    Y_trn$V1 <- factor(Y_trn$V1, labels = actv_lvls$V2)
    names(Y_trn) <- "Activity"
    sub_trn$V1 <- factor(sub_trn$V1)
    names(sub_trn) <- "Subject"

    all_trn <- cbind(sub_trn, Y_trn, X_trn)

Load Test Data
--------------

    #Load Test DataSets
    sub_test <- read.table("../data/UCI HAR Dataset/test/subject_test.txt")
    X_test <- read.table("../data/UCI HAR Dataset/test/X_test.txt")
    Y_test <- read.table("../data/UCI HAR Dataset/test/y_test.txt")

    names(X_test) <- feat$V2
    Y_test$V1 <- factor(Y_test$V1, labels = actv_lvls$V2)
    names(Y_test) <- "Activity"
    sub_test$V1 <- factor(sub_test$V1)
    names(sub_test) <- "Subject"
    all_test <- cbind(sub_test, Y_test, X_test)

Merge Training and Test data
----------------------------

    #Combine training and test data set
    all_data <- rbind(all_test, all_trn)

Subset for mean and standard deviation features
-----------------------------------------------

    #Identify subset of variables for mean and standard deviation
    feat_mn <- feat[grep("mean", feat$V2), 1 ]
    feat_std <- feat[grep("std", feat$V2), 1 ]
    feat_mn_std <- c(feat_mn, feat_std)
    all_data_mn_std <- all_data[,feat_mn_std]

Summarise by Subject and Activity
---------------------------------

    #Summarise data and create the tidy text file
    tidy_data <- aggregate(all_data_mn_std[-c(1:2)], 
                           by = list(all_data_mn_std$Subject, all_data_mn_std$Activity),
                           FUN = mean)
    names(tidy_data)[1] <- "Subject"
    names(tidy_data)[2] <- "Activity"

    write.table(tidy_data, file = "tidy_data.txt", row.name=FALSE )

The fine contains the features with the following labels -

    names(tidy_data)

    ##  [1] "Subject"                          "Activity"                        
    ##  [3] "tBodyAcc-mean()-X"                "tBodyAcc-correlation()-X,Z"      
    ##  [5] "tBodyAcc-correlation()-Y,Z"       "tGravityAcc-mean()-X"            
    ##  [7] "tGravityAcc-correlation()-X,Z"    "tGravityAcc-correlation()-Y,Z"   
    ##  [9] "tBodyAccJerk-mean()-X"            "tBodyAccJerk-correlation()-X,Z"  
    ## [11] "tBodyAccJerk-correlation()-Y,Z"   "tBodyGyro-mean()-X"              
    ## [13] "tBodyGyro-correlation()-X,Z"      "tBodyGyro-correlation()-Y,Z"     
    ## [15] "tBodyGyroJerk-mean()-X"           "tBodyGyroJerk-correlation()-X,Z" 
    ## [17] "tBodyAccMag-arCoeff()3"           "tGravityAccMag-arCoeff()3"       
    ## [19] "tBodyAccJerkMag-arCoeff()3"       "tBodyGyroMag-arCoeff()3"         
    ## [21] "tBodyGyroJerkMag-arCoeff()3"      "tBodyGyroJerkMag-arCoeff()4"     
    ## [23] "fBodyAcc-mean()-X"                "fBodyAcc-maxInds-Y"              
    ## [25] "fBodyAcc-maxInds-Z"               "fBodyAcc-meanFreq()-X"           
    ## [27] "fBodyAcc-bandsEnergy()-1,24"      "fBodyAcc-bandsEnergy()-25,48"    
    ## [29] "fBodyAccJerk-mean()-X"            "fBodyAccJerk-maxInds-Y"          
    ## [31] "fBodyAccJerk-maxInds-Z"           "fBodyAccJerk-meanFreq()-X"       
    ## [33] "fBodyAccJerk-bandsEnergy()-1,24"  "fBodyAccJerk-bandsEnergy()-25,48"
    ## [35] "fBodyGyro-mean()-X"               "fBodyGyro-maxInds-Y"             
    ## [37] "fBodyGyro-maxInds-Z"              "fBodyGyro-meanFreq()-X"          
    ## [39] "fBodyGyro-bandsEnergy()-1,24"     "fBodyAccMag-entropy()"           
    ## [41] "fBodyAccMag-skewness()"           "fBodyBodyAccJerkMag-entropy()"   
    ## [43] "fBodyBodyAccJerkMag-skewness()"   "fBodyBodyGyroMag-entropy()"      
    ## [45] "fBodyBodyGyroMag-skewness()"      "fBodyBodyGyroJerkMag-entropy()"  
    ## [47] "tBodyAcc-mean()-Y"                "tBodyAcc-mean()-Z"               
    ## [49] "tBodyAcc-std()-X"                 "tGravityAcc-mean()-Y"            
    ## [51] "tGravityAcc-mean()-Z"             "tGravityAcc-std()-X"             
    ## [53] "tBodyAccJerk-mean()-Y"            "tBodyAccJerk-mean()-Z"           
    ## [55] "tBodyAccJerk-std()-X"             "tBodyGyro-mean()-Y"              
    ## [57] "tBodyGyro-mean()-Z"               "tBodyGyro-std()-X"               
    ## [59] "tBodyGyroJerk-mean()-Y"           "tBodyGyroJerk-mean()-Z"          
    ## [61] "tBodyGyroJerk-std()-X"            "tBodyGyroJerk-correlation()-Y,Z" 
    ## [63] "tBodyAccMag-arCoeff()4"           "tGravityAccMag-arCoeff()4"       
    ## [65] "tBodyAccJerkMag-arCoeff()4"       "tBodyGyroMag-arCoeff()4"         
    ## [67] "fBodyAcc-mean()-Y"                "fBodyAcc-mean()-Z"               
    ## [69] "fBodyAcc-std()-X"                 "fBodyAccJerk-mean()-Y"           
    ## [71] "fBodyAccJerk-mean()-Z"            "fBodyAccJerk-std()-X"            
    ## [73] "fBodyGyro-mean()-Y"               "fBodyGyro-mean()-Z"              
    ## [75] "fBodyGyro-std()-X"                "fBodyGyro-bandsEnergy()-25,48"   
    ## [77] "fBodyAccMag-kurtosis()"           "fBodyBodyAccJerkMag-kurtosis()"  
    ## [79] "fBodyBodyGyroMag-kurtosis()"
