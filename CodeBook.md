Activity Tidy data cookbook
===========================

This document provides the definition of the activity data summaraised
at the Subject and Activity level.Each row represent measurement for
each combination of subject and actvity level.

The Actvity Description
-----------------------

    ##   Code           Activity
    ## 1    1            WALKING
    ## 2    2   WALKING_UPSTAIRS
    ## 3    3 WALKING_DOWNSTAIRS
    ## 4    4            SITTING
    ## 5    5           STANDING
    ## 6    6             LAYING

The Measurement Features (mean and standard deviation)
------------------------------------------------------

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
