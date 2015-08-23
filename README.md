#####------------------------SCRIPTS - COURSE PROJECT - GETTING AND CLEANING DATA---------

####     Download file at :
####     https://d396qusza40orc.cloudfront.net/getdata%2Fprojectfiles%2FUCI%20HAR%20Dataset.zip 

####     Description of data available at:
         http://archive.ics.uci.edu/ml/datasets/Human+Activity+Recognition+Using+Smartphones

 
####     Download and unzip data file (used method described in StackOverflow.
####     All the unzipped data files were copied into the following working     
####     directory using  WINDOWS Copy and Paste functions:
####         C:/Users/Owner/Documents/KRISHNAN/TRAINING/HOPKINsDataScienceSpecialization/GettingAndCleaningData/PROJECT

 
        fileurl <- "http://d396qusza40orc.cloudfront.net/getdata%2Fprojectfiles%2FUCI%20HAR%20Dataset.zip" 
        download.file(fileurl, dest="dataset.zip", mode="w") 
        unzip("dataset.zip", exdir = "./data", unzip = "internal")
   
        
####     Date and time file downloaded - "Fri Aug 21 12:17:53 2015"

         date()

####--------------------------------------------------------------------------------
####     READ TRAINING SET FILES INTO R DATA FRAMES, CHECK FOR NA-NULL VALUES,
####        AND PREPARE PER TIDY DATA CRITERIA FOR MERGING AND ANALYSIS
####--------------------------------------------------------------------------------

###    Xtrain file includes the collected data for training set subjects and activities

       conXtrain <- file("X_train.txt", open = "")
       open(conXtrain)
       isOpen(conXtrain)
       Xtrain <- read.table(conXtrain, sep = "")
       dim(Xtrain)   #  Xtrain has 7352 rows, 561 columns
       sum(is.na(Xtrain))     ##     Number of NA values in Xtrain =  0
       sum(is.null(Xtrain))     ##     Number of NULL values in Xtrain =  0


###    Ytrain file indetifies activities for each record in Xtest file

       conYtrain <- file("Y_train.txt", open = "")
       open(conYtrain)
       isOpen(conYtrain)
       Ytrain <- read.table(conYtrain, sep = "")
       dim(Ytrain)       ##  Ytrain has 7352 rows and 1 column
       sum(is.na(Ytrain))     ##     Number of NA values in Ytrain =  0
       sum(is.null(Ytrain))     ##     Number of NULL values in Ytrain =  0

##     Following statements replace numeric values in Ytrain with corresponding
         activity name
       
       Ytrain$V1 <- gsub("1", "Walking", Ytrain$V1)
       Ytrain$V1 <- gsub("2", "WalkingUpstairs",Ytrain$V1)
       Ytrain$V1 <- gsub("3", "WalkingDownstairs",Ytrain$V1)
       Ytrain$V1 <- gsub("4", "Sitting",Ytrain$V1)
       Ytrain$V1 <- gsub("5", "Standing",Ytrain$V1)
       Ytrain$V1 <- gsub("6", "Laying",Ytrain$V1)


###    Subject_Train file identifies subject for each record in Xtest

       conSubject_Train <- file("subject_train.txt", open = "")
       open(conSubject_Train)
       isOpen(conSubject_Train)
       Subject_Train <- read.table(conSubject_Train, sep = "")
       dim(Subject_Train)           ##  Subject_Train has 7352 rows and 1 column
       sum(is.na(Subject_Train))     ##     Number of NA values in Subject_Train =  0
       sum(is.null(Subject_Train))     ##     Number of NULL values in Subject_Train =  0

##     Following statement pastes the text "SubjectNo. ahead of the numerical code 
         representing the subject number in Subject_Test

        Subject_Train$V1 <- paste0("SubjectNo ", Subject_Train$V1)


###     Column Bind first Subject_Train and then Ytrain to Xtrain

         XtrainA <-  cbind(Subject_Train, Xtrain)
         XtrainB <-  cbind(Ytrain, XtrainA)
         dim(XtrainB)  ##  XtrainB has 7352 rows and 563 columns
         sum(is.na(XtrainB))    ##  Number of NA values in XtrainB = 0
         sum(is.null(XtrainB))    ##  Number of NULL values in XtrainB = 0


###--------------------------------------------------------------------------------
###     READ TESTING SET FILES INTO R DATA FRAMES, CHECK FOR NA-NULL VALUES,
###        AND PREPARE PER TIDY DATA CRITERIA FOR MERGING AND ANALYSIS
###--------------------------------------------------------------------------------

###    Xtest file includes the collected data for test set subjects and activities
       conXtest <- file("X_test.txt", open = "")
       open(conXtest)
       isOpen(conXtest)
       Xtest <- read.table(conXtest, sep = "")
       dim(Xtest)   #  Xtest has 2947 rows, 561 columns
       sum(is.na(Xtest))     ##     Number of NA values in Xtest =  0
       sum(is.null(Xtest))     ##     Number of NULL values in Xtest =  0


###    Ytest file indetifies activities for each record in Xtest file

       conYtest <- file("Y_test.txt", open = "")
       open(conYtest)
       isOpen(conYtest)
       Ytest <- read.table(conYtest, sep = " ")
       dim(Ytest)       ##  Ytest has 2947 rows and 1 column
       sum(is.na(Ytest))     ##     Number of NA values in Ytest =  0
       sum(is.null(Ytest))     ##     Number of NULL values in Ytest =  0

##     Following statements replace numeric values in Ytest with corresponding
         activity name
       
       Ytest$V1 <- gsub("1", "Walking", Ytest$V1)
       Ytest$V1 <- gsub("2", "WalkingUpstairs",Ytest$V1)
       Ytest$V1 <- gsub("3", "WalkingDownstairs",Ytest$V1)
       Ytest$V1 <- gsub("4", "Sitting",Ytest$V1)
       Ytest$V1 <- gsub("5", "Standing",Ytest$V1)
       Ytest$V1 <- gsub("6", "Laying",Ytest$V1)


###    Subject_Test file identifies subject for each record in Xtest

       conSubject_Test <- file("subject_test.txt", open = "")
       open(conSubject_Test)
       isOpen(conSubject_Test)
       Subject_Test <- read.table(conSubject_Test, sep = "")
       dim(Subject_Test)           ##  Subject_Test has 2947 rows and 1 column
       sum(is.na(Subject_Test))     ##     Number of NA values in Subject_Test =  0
       sum(is.null(Subject_Test))     ##     Number of NULL values in Subject_Test =  0

##     Following statement pastes the text "SubjectNo. ahead of the numerical code 
         representing the subject number in Subject_Test

        Subject_Test$V1 <- paste0("SubjectNo ", Subject_Test$V1)


###     Column Bind first Subject_Test and then Ytest to Xtest

         XtestA <-  cbind(Subject_Test, Xtest)
         XtestB <-  cbind(Ytest, XtestA)
         dim(XtestB)  ##  XtestB has 2947 rows and 563 columns
         sum(is.na(XtestB))    ##  Number of NA values in XtestB = 0
         sum(is.null(XtestB))    ##  Number of NULL values in XtestB = 0



#### --------------------------------------------------------------------------------
####    ROW BIND TRAINING AND TESTING DATA SETS;  VALIDATE MERGE BY CHECKING
####      ROW AND COLUMN COUNTS AND NA-NULL VALUES.
####    ADD COLUMN NAMES.
####      
####----------------------------------------------------------------------------------

        MergedDataA <- rbind(XtrainB, XtestB)
        dim(MergedDataA)  ##  MergedDataA has 10299 rows (equals sum of 2947 rows
                          ##   from XtestB, and 7352 rows from XtrainB.
                          ##  MergedDataA has 563 columns, the same as XtestB and XtrainB

###-------------------------------------------------------------------------------------
###     READ Features.txt INTO DATA FRAME.  
###     VALIDATE DIMENSIONS AND ABSENCE OF NA-NULL VALUES
###     CLEAN TEXT FOR mean AND std for READABILITY,  ADD "Activity" and "Subject" 
###--------------------------------------------------------------------------------------

       conFeatures <- file("features.txt", open = "")
       open(conFeatures)
       isOpen(conFeatures)
       Features <- read.table(conFeatures, sep = "")
       dim(Features)           ##  Number of rows in Features = 561, columns = 2
                               ##  Variable names in Features$V2 
       sum(is.na(Features))    ##     Number of NA values in Features =  0
       sum(is.null(Features))     ##     Number of NULL values in Features =  0
       FeaturesV2 <-  Features$V2
       FeaturesV2 <- gsub("mean", "Mean", FeaturesV2)  ##  Replace "mean" with "Mean"
       FeaturesV2 <- gsub("std", "Std", FeaturesV2)    ## Replave "std" with "Std"
       FeaturesCH <-  c("Activity", "Subject", FeaturesV2)     

###---------------------------------------------------------------------------------
###    ADD FeaturesCH  AS COLUMN HEADINGS TO MergedDataA
###----------------------------------------------------------------------------------

       colnames(MergedDataA) <- FeaturesCH

###-----------------------------------------------------------------------------------
###    EXTRACT DATA ON "Mean" and "Std" ON ALL VARIABLES
###-----------------------------------------------------------------------------------

        MeanOfMeasurements <-  FeaturesCH[grep("-Mean", FeaturesCH)]
        length(MeanOfMeasurements)  ##  46 variables representing Mean of measurements
         
        StdOfMeasurements <-   FeaturesCH[grep("-Std", FeaturesCH)]
        length(StdOfMeasurements)  ##   33 variables representing Std of measurements

        VariablesToExtract <-  c(MeanOfMeasurements, StdOfMeasurements)
        length(VariablesToExtract)  ##  Set of 79 variables Mean and Std measurements

        ColumnsToExtract <- c("Activity", "Subject", VariablesToExtract)
        length(ColumnsToExtract)  ##  Set of 81 columns to be extracted


##------------------------------------------------------------------------------------
##      SUBSET MergedDataA BASED ON COLUMNS INCLUDED IN "VariablesToExtract"
##        Replace "Std" with "StandardDeviation" in Columns Names         
##-------------------------------------------------------------------------------------

               
         DataExtract <-  subset(MergedDataA[ , ColumnsToExtract])
         dim(DataExtract)  ##  10299 rows and 81 columns
         sum(is.na(DataExtract))  ##   0 
         sum(is.null(DataExtract))  ##   0

         ColumnNames <-  gsub("Std", "StandardDeviation",ColumnsToExtract)
         length(ColumnNames)   ##  81 names for columns

         colnames(DataExtract) <-  ColumnNames
         colnames(DataExtract)   ##  To verify addition of columnnnames

         write.table(DataExtract, file = "Step4DataExtract.txt", sep = " ", eol = "\n", 
           col.names = TRUE, row.names= FALSE)

         

####-----------------------------------------------------------------------------------
####  AVERAGE OF EACH VARIABLE FROM DataExtract FOR EACH ACTIVTY AND EACH SUBJECT
####     ALSO INCLUDED IS THE AVERAGE OF EACH VARIABLE FOR EACH ACTIVTY BY SUBJECT
####-----------------------------------------------------------------------------------
      install.packages("plyr")
      library(plyr)

      install.packages("dplyr")
      library(dplyr)


###   WAS UNABLE TO COMPLETE STEP 5 OF PROJECT BY THE DEADLINE


 
     