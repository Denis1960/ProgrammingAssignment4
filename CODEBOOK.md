### Introduction

This codebook provides detailed information regarding run_analysis.R, not already included in the README.md file.
Please consult the README.md file for the objectives of the assignment and the programming steps taken to meet
the requirements of the assignment.

### Input Data Set

The input data set records experiments that have been carried out with a group of 30 volunteers within an age bracket of 19-48 years. Each person performed six activities (WALKING, WALKING_UPSTAIRS, WALKING_DOWNSTAIRS, SITTING, STANDING, LAYING) wearing a smartphone (Samsung Galaxy S II) on the waist. Using its embedded accelerometer and gyroscope, we captured 3-axial linear acceleration and 3-axial angular velocity at a constant rate of 50Hz. The experiments have been video-recorded to label the data manually. The obtained dataset has been randomly partitioned into two sets, where 70% of the volunteers was selected for generating the training data and 30% the test data. 

The sensor signals (accelerometer and gyroscope) were pre-processed by applying noise filters and then sampled in fixed-width sliding windows of 2.56 sec and 50% overlap (128 readings/window). The sensor acceleration signal, which has gravitational and body motion components, was separated using a Butterworth low-pass filter into body acceleration and gravity. The gravitational force is assumed to have only low frequency components, therefore a filter with 0.3 Hz cutoff frequency was used. From each window, a vector of features was obtained by calculating variables from the time and frequency domain. See 'features_info.txt' for more details. 

For each record the following information is provided:
======================================

- Triaxial acceleration from the accelerometer (total acceleration) and the estimated body acceleration.
- Triaxial Angular velocity from the gyroscope. 
- A 561-feature vector with time and frequency domain variables. 
- Its activity label. 
- An identifier of the subject who carried out the experiment.

## The dataset includes the following files:
## =============================================================================================================================================

## File Name           Description								Program Variable	R Class		Comments

- 'features_info.txt': Shows information about the variables used on the feature vector		None

- 'features.txt': List of all features.								featureNames		Data Frame

- 'activity_labels.txt': Links the class labels with their activity name.			activityLabels		Data Frame	

- 'train/X_train.txt': Training set.								xTrain			Data Frame	WALKING, WALKING_UPSTAIRS, WALKING_DOWNSTAIRS, SITTING, STANDING, LAYING

- 'train/y_train.txt': Training labels.								yTrain			Data Frame

- 'test/X_test.txt': Test set.									xTest			Data Frame

- 'test/y_test.txt': Test labels.								yTest			Data Frame


- 'train/subject_train.txt': Identifies the subject who performed the activity.		 	SubTest			Data Frame	Contains values 1-30
												SubTrain		Data Frame`	Contains values 1-30
  
The files listed below are not referenced in run_analysis.R

- 'train/Inertial Signals/total_acc_x_train.txt': The acceleration signal from the smartphone accelerometer X axis in standard gravity units 'g'. Every row shows a 128 element vector. The same description applies for the 'total_acc_x_train.txt' and 'total_acc_z_train.txt' files for the Y and Z axis. 

- 'train/Inertial Signals/body_acc_x_train.txt': The body acceleration signal obtained by subtracting the gravity from the total acceleration. 

- 'train/Inertial Signals/body_gyro_x_train.txt': The angular velocity vector measured by the gyroscope for each window sample. The units are radians/second. 


### Information regarding the features captured for each observation

## 1. 	Feature Selection 
## ==========================

The features selected for this database come from the accelerometer and gyroscope 3-axial raw signals tAcc-XYZ and tGyro-XYZ. These time domain signals (prefix 't' to denote time) were captured at a constant rate of 50 Hz. Then they were filtered using a median filter and a 3rd order low pass Butterworth filter with a corner frequency of 20 Hz to remove noise. Similarly, the acceleration signal was then separated into body and gravity acceleration signals (tBodyAcc-XYZ and tGravityAcc-XYZ) using another low pass Butterworth filter with a corner frequency of 0.3 Hz. 

Subsequently, the body linear acceleration and angular velocity were derived in time to obtain Jerk signals (tBodyAccJerk-XYZ and tBodyGyroJerk-XYZ). Also the magnitude of these three-dimensional signals were calculated using the Euclidean norm (tBodyAccMag, tGravityAccMag, tBodyAccJerkMag, tBodyGyroMag, tBodyGyroJerkMag). 

Finally a Fast Fourier Transform (FFT) was applied to some of these signals producing fBodyAcc-XYZ, fBodyAccJerk-XYZ, fBodyGyro-XYZ, fBodyAccJerkMag, fBodyGyroMag, fBodyGyroJerkMag. (Note the 'f' to indicate frequency domain signals). 

These signals were used to estimate variables of the feature vector for each pattern:  
'-XYZ' is used to denote 3-axial signals in the X, Y and Z directions.

tBodyAcc-XYZ
tGravityAcc-XYZ
tBodyAccJerk-XYZ
tBodyGyro-XYZ
tBodyGyroJerk-XYZ
tBodyAccMag
tGravityAccMag
tBodyAccJerkMag
tBodyGyroMag
tBodyGyroJerkMag
fBodyAcc-XYZ
fBodyAccJerk-XYZ
fBodyGyro-XYZ
fBodyAccMag
fBodyAccJerkMag
fBodyGyroMag
fBodyGyroJerkMag

The set of variables that were estimated from these signals are: 

mean(): Mean value
std(): Standard deviation
mad(): Median absolute deviation 
max(): Largest value in array
min(): Smallest value in array
sma(): Signal magnitude area
energy(): Energy measure. Sum of the squares divided by the number of values. 
iqr(): Interquartile range 
entropy(): Signal entropy
arCoeff(): Autorregresion coefficients with Burg order equal to 4
correlation(): correlation coefficient between two signals
maxInds(): index of the frequency component with largest magnitude
meanFreq(): Weighted average of the frequency components to obtain a mean frequency
skewness(): skewness of the frequency domain signal 
kurtosis(): kurtosis of the frequency domain signal 
bandsEnergy(): Energy of a frequency interval within the 64 bins of the FFT of each window.
angle(): Angle between to vectors.

Additional vectors obtained by averaging the signals in a signal window sample. These are used on the angle() variable:

gravityMean
tBodyAccMean
tBodyAccJerkMean
tBodyGyroMean
tBodyGyroJerkMean

## 2.	Features used in run_analysis.R
## ======================================

For this program a total of 65 observations is used. The 65 observations are derived by selecting only those features that include std() or mean() as part
of their calculation as follows:

	xTest <- select(xTest,contains('std()'),contains('mean()'))
  	xTrain <- select(xTrain,contains('std()'),contains('mean()'))

The resulting set of features is as follows:

tBodyAcc-std()-X"            "tBodyAcc-std()-Y"            "tBodyAcc-std()-Z"            "tGravityAcc-std()-X"         "tGravityAcc-std()-Y"         "tGravityAcc-std()-Z"         "tBodyAccJerk-std()-X"       
tBodyAccJerk-std()-Y"        "tBodyAccJerk-std()-Z"        "tBodyGyro-std()-X"           "tBodyGyro-std()-Y"           "tBodyGyro-std()-Z"           "tBodyGyroJerk-std()-X"       "tBodyGyroJerk-std()-Y"       "tBodyGyroJerk-std()-Z"       "tBodyAccMag-std()"           "tGravityAccMag-std()"       
tBodyAccJerkMag-std()"       "tBodyGyroMag-std()"          "tBodyGyroJerkMag-std()"      "fBodyAcc-std()-X"            "fBodyAcc-std()-Y"            "fBodyAcc-std()-Z"            "fBodyAccJerk-std()-X"        "fBodyAccJerk-std()-Y"        "fBodyAccJerk-std()-Z"        "fBodyGyro-std()-X"          
BodyGyro-std()-Y"           "fBodyGyro-std()-Z"           "fBodyAccMag-std()"           "fBodyBodyAccJerkMag-std()"   "fBodyBodyGyroMag-std()"      "fBodyBodyGyroJerkMag-std()"  "tBodyAcc-mean()-Y"           "tBodyAcc-mean()-Z"           "tGravityAcc-mean()-X"        "tGravityAcc-mean()-Y"       
tGravityAcc-mean()-Z"        "tBodyAccJerk-mean()-X"       "tBodyAccJerk-mean()-Y"       "tBodyAccJerk-mean()-Z"       "tBodyGyro-mean()-X"          "tBodyGyro-mean()-Y"          "tBodyGyro-mean()-Z"          "tBodyGyroJerk-mean()-X"      "tBodyGyroJerk-mean()-Y"      "tBodyGyroJerk-mean()-Z"     
tBodyAccMag-mean()"          "tGravityAccMag-mean()"       "tBodyAccJerkMag-mean()"      "tBodyGyroMag-mean()"         "tBodyGyroJerkMag-mean()"     "fBodyAcc-mean()-X"           "fBodyAcc-mean()-Y"           "fBodyAcc-mean()-Z"           "fBodyAccJerk-mean()-X"       "fBodyAccJerk-mean()-Y"      
fBodyAccJerk-mean()-Z"       "fBodyGyro-mean()-X"          "fBodyGyro-mean()-Y"          "fBodyGyro-mean()-Z"    


### Data Tables used in run_analysis.R

testDT - the set of combined test files (subTest, xTest, yTest) created using cbind()
trainDT- the set of combined train files (subTrain, xTrain, yTrain) created using cbind()
allDataDT - the comnbination of testDT and trainDT created using rbind()
mDataDT - a melted version of allDataDT created using melt(). Output as mdata.txt representing a long file version of all observations for all subjects and activities
tDataDT - the information in mDataDT presented in wide format and grouped by Subject and Activity. The mean for each of the features referenced above is included. Written as tData.txt.
meltDataDT - the tDataDT file melted to provide a long file version of the information in TDataDT. Creates on observation for row for each group created in tDataDT. Written as tidy_data.txt
