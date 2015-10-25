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
    feat_mn_std <- c(1,2,(feat_mn+2), (feat_std+2))
    all_data_mn_std <- all_data[,feat_mn_std]

Summarise by Subject and Activity
---------------------------------

    #Summarise data and create the tidy text file
    tidy_data <- aggregate(all_data_mn_std[-c(1:2)], 
                           by = list(all_data_mn_std$Subject, all_data_mn_std$Activity),
                           FUN = mean)
    names(tidy_data)[1] <- "Subject"
    names(tidy_data)[2] <- "Activity"
    names(tidy_data) <- gsub("-","",names(tidy_data))
    names(tidy_data) <- gsub("\\(\\)","",names(tidy_data))
    names(tidy_data) <- gsub(",","",names(tidy_data))

    write.table(tidy_data, file = "tidy_data.txt", row.name=FALSE )

The file contains the following features for mean and standard deviation
-

    names(tidy_data)

    ##  [1] "Subject"                      "Activity"                    
    ##  [3] "tBodyAccmeanX"                "tBodyAccmeanY"               
    ##  [5] "tBodyAccmeanZ"                "tGravityAccmeanX"            
    ##  [7] "tGravityAccmeanY"             "tGravityAccmeanZ"            
    ##  [9] "tBodyAccJerkmeanX"            "tBodyAccJerkmeanY"           
    ## [11] "tBodyAccJerkmeanZ"            "tBodyGyromeanX"              
    ## [13] "tBodyGyromeanY"               "tBodyGyromeanZ"              
    ## [15] "tBodyGyroJerkmeanX"           "tBodyGyroJerkmeanY"          
    ## [17] "tBodyGyroJerkmeanZ"           "tBodyAccMagmean"             
    ## [19] "tGravityAccMagmean"           "tBodyAccJerkMagmean"         
    ## [21] "tBodyGyroMagmean"             "tBodyGyroJerkMagmean"        
    ## [23] "fBodyAccmeanX"                "fBodyAccmeanY"               
    ## [25] "fBodyAccmeanZ"                "fBodyAccmeanFreqX"           
    ## [27] "fBodyAccmeanFreqY"            "fBodyAccmeanFreqZ"           
    ## [29] "fBodyAccJerkmeanX"            "fBodyAccJerkmeanY"           
    ## [31] "fBodyAccJerkmeanZ"            "fBodyAccJerkmeanFreqX"       
    ## [33] "fBodyAccJerkmeanFreqY"        "fBodyAccJerkmeanFreqZ"       
    ## [35] "fBodyGyromeanX"               "fBodyGyromeanY"              
    ## [37] "fBodyGyromeanZ"               "fBodyGyromeanFreqX"          
    ## [39] "fBodyGyromeanFreqY"           "fBodyGyromeanFreqZ"          
    ## [41] "fBodyAccMagmean"              "fBodyAccMagmeanFreq"         
    ## [43] "fBodyBodyAccJerkMagmean"      "fBodyBodyAccJerkMagmeanFreq" 
    ## [45] "fBodyBodyGyroMagmean"         "fBodyBodyGyroMagmeanFreq"    
    ## [47] "fBodyBodyGyroJerkMagmean"     "fBodyBodyGyroJerkMagmeanFreq"
    ## [49] "tBodyAccstdX"                 "tBodyAccstdY"                
    ## [51] "tBodyAccstdZ"                 "tGravityAccstdX"             
    ## [53] "tGravityAccstdY"              "tGravityAccstdZ"             
    ## [55] "tBodyAccJerkstdX"             "tBodyAccJerkstdY"            
    ## [57] "tBodyAccJerkstdZ"             "tBodyGyrostdX"               
    ## [59] "tBodyGyrostdY"                "tBodyGyrostdZ"               
    ## [61] "tBodyGyroJerkstdX"            "tBodyGyroJerkstdY"           
    ## [63] "tBodyGyroJerkstdZ"            "tBodyAccMagstd"              
    ## [65] "tGravityAccMagstd"            "tBodyAccJerkMagstd"          
    ## [67] "tBodyGyroMagstd"              "tBodyGyroJerkMagstd"         
    ## [69] "fBodyAccstdX"                 "fBodyAccstdY"                
    ## [71] "fBodyAccstdZ"                 "fBodyAccJerkstdX"            
    ## [73] "fBodyAccJerkstdY"             "fBodyAccJerkstdZ"            
    ## [75] "fBodyGyrostdX"                "fBodyGyrostdY"               
    ## [77] "fBodyGyrostdZ"                "fBodyAccMagstd"              
    ## [79] "fBodyBodyAccJerkMagstd"       "fBodyBodyGyroMagstd"         
    ## [81] "fBodyBodyGyroJerkMagstd"
