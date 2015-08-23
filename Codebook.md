Getting And Cleaning Data Course Project

CODEBOOK

DATA PROCESSING STEPS   (ALL FUNCTIONS REFERENCES ARE TO R FUNCTIONS UNLESS OTHERWISE NOTED)

1.  The data files at the link: http://archive.ics.uci.edu/ml/datasets/Human+Activity+Recognition+Using+Smartphones , were downloaded using the download.file().

    A summary of the data set information (from the UCI.edu website)follows:  

        The experiments have been carried out with a group of 30 volunteers within an age bracket of 19-48 years.
        Each person performed six activities (WALKING, WALKING_UPSTAIRS, WALKING_DOWNSTAIRS, SITTING, STANDING, LAYING)
        wearing a smartphone (Samsung Galaxy S II) on the waist. Using its embedded accelerometer and gyroscope,
        3-axial linear acceleration and 3-axial angular velocity at a constant rate of 50Hz were captured.
        The experiments have been video-recorded to label the data manually. The obtained dataset has been randomly 
        partitioned into two sets, where 70% of the volunteers was selected for generating the training data and 30% the test data. 

        The sensor signals (accelerometer and gyroscope) were pre-processed by applying noise filters and then
        sampled in fixed-width sliding windows of 2.56 sec and 50% overlap (128 readings/window). The sensor acceleration signal, 
        which has gravitational and body motion components, was separated using a Butterworth low-pass filter into body acceleration 
        and gravity. The gravitational force is assumed to have only low frequency components, therefore a filter with 0.3 Hz cutoff 
        frequency was used. From each window, a vector of features was obtained by calculating variables from the time and frequency domain.
        
        Additional information on the data is provided in the README.txt file downloaded with the data from the UCI.edu website, and is not included here.

        
2.  The files were then unzipped using unzip().

        A summary of the information in the key files follows (Source:  README.txt file downloaded with the data)
        
        
            - 'README.txt'
            - 'features_info.txt': Shows information about the variables used on the feature vector.
            - 'features.txt': List of all features.
            - 'activity_labels.txt': Links the class labels with their activity name.
            - 'train/X_train.txt': Training set.
            - 'train/y_train.txt': Training labels.
            - 'test/X_test.txt': Test set.
            - 'test/y_test.txt': Test labels.

            The following files were downloaded for train and test data. Their descriptions are equivalent.
            - 'train/subject_train.txt': Each row identifies the subject who performed the activity for each window sample. Its range is from 1 to 30. 
            - 'train/Inertial Signals/total_acc_x_train.txt': The acceleration signal from the smartphone accelerometer X axis in standard gravity units 'g'.
               Every row shows a 128 elementsame description applies for the 'total_acc_x_train.txt' and 'total_acc_z_train.txt' files for the Y and Z axis. 
            - 'train/Inertial Signals/body_acc_x_train.txt': The body acceleration signal obtained by subtracting the gravity from the total acceleration. 
            - 'train/Inertial Signals/body_gyro_x_train.txt': The angular velocity vector measured by the gyroscope for each window sample. The units are radians/second. 

                    Notes: 
                    ======
                    - Features are normalized and bounded within [-1,1].
                    - Each feature vector is a row on the text file.

                    For more information about this dataset contact: activityrecognition@smartlab.ws

                    License:
                    ========
                    Use of this dataset in publications must be acknowledged by referencing the following publication [1] 

                    [1] Davide Anguita, Alessandro Ghio, Luca Oneto, Xavier Parra and Jorge L. Reyes-Ortiz. Human Activity Recognition 
                    on Smartphones using a Multiclass Hardware-Friendly Support Vector Machine. International Workshop of Ambient Assisted Living (IWAAL 2012).
                    Vitoria-Gasteiz, Spain. Dec 2012

                    This dataset is distributed AS-IS and no responsibility implied or explicit can be addressed to the authors or their institutions for its 
                    use or misuse. Any commercial use is prohibited.

                    Jorge L. Reyes-Ortiz, Alessandro Ghio, Luca Oneto, Davide Anguita. November 2012.
        
        
3.  The unzipped files in various sub-directories were then copy-pasted to my working directory for R.
4.  The downloaded and unzipped files were then read into R data frames using read.table()
5.  The data in each data frame was checked to confirm the following:
     -  Number of rows and columns 
     -  No NA or NULL data within the data frame that needed to be cleaned
6.  The Subject_Train and Subject_Test data frames which identify  Subject (from 1:30) for each record in Xtrain and Ytrain respectively, were column binded  to Xtrain and Xtest respectively, after appending the characters "Subject No." to the numerical codes for the subjects.      
7.  The Ytrain and Ytest data frames which identify Activity (Codes for Walking, WalkingUpstairs, WalkingDownstairs,Sitting, Standing, Laying ) for each record  in Xtrain and Ytrain respectively, were column binded to the Step 6 data frames after converting the number codes from 1:6 to the corresponding activity.
8   Xtrain and Xtest were then row binded.  The number of rows in the merged data frame was confirmed equal to the sum of the rows in Xtrain and Xtest. 
9   The Features data frame identifies the column headings for Xtrain and Xtest .  The “Activity” and “Subject” headings were appended to the beginning of Features.  The modified Features, after nominal ediiting,  was added as Column Names to the merged data frame from Step 8.
10. A subset of the Step 9 data frame, with the Subject and Activity Columns, as well as all columns with “-Mean” and “-Std” was extracted.  This was to be used for the Step 5 analysis in the project.
11. Step 5 could  not be completed prior to the deadline.  The S.tep 4 data set has been submitted as evidence of the work completed
    
   
