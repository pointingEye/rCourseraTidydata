run_analysis <- function(){

#1. Merge the training and the test sets to create one data set.

# set working directory! (to adapt to your computer's path structure) one level beneath the folder "UCI HAR Dataset"

# Loading test data in one dataset
subject_test <- read.table("UCI HAR Dataset/test/subject_test.txt", quote="\"")
X_test <- read.table("UCI HAR Dataset/test/X_test.txt", quote="\"")
y_test <- read.table("UCI HAR Dataset/test/y_test.txt", quote="\"")
test <- data.frame(NULL)
test <- cbind(subject_test,y_test,X_test)

# Loading train data in one dataset + rbind test and train together
subject_train <- read.table("UCI HAR Dataset/train/subject_train.txt", quote="\"")
X_train <- read.table("UCI HAR Dataset/train/X_train.txt", quote="\"")
y_train <- read.table("UCI HAR Dataset/train/y_train.txt", quote="\"")
train <- data.frame(NULL)
train <- cbind(subject_train,y_train,X_train)

#binding the two datasets together under the name "tt"
tt <- rbind(test,train)

#read and add column names
#This is a task that comes later (4.) but I find it convenient to do it now already
features <- read.table("UCI HAR Dataset/features.txt", quote="\"")
colnames(tt) <- c("subject","activity",as.character(features[,2]))


#2. Extract only the measurements on the mean and standard deviation for each measurement. 

#find column names with 'mean' or 'std'
colsMean <- grep('mean', colnames(tt))
colsStd  <- grep('std', colnames(tt))
colsMeanStd <- unique(c(colsMean,colsStd))
colsMeanStd <- sort(colsMeanStd)
ttExtract <- tt[,c(1,2,colsMeanStd)]

#I also order the dataset for a better overview (1.prio subject, 2.prio activity) already now
ttOrd <- ttExtract[order(ttExtract[,1], ttExtract[,2]),]
rownames(ttOrd) <- NULL


#3. Uses descriptive activity names to name the activities in the data set

# I use the activity_labels to axchange the numbered activities by the actual labels
activities      <- read.table("UCI HAR Dataset/activity_labels.txt", quote="\"")
activity_labels <- activities[,2]
for (i in 1:6) ttOrd[ttOrd[,2]==i,2] <- as.character(activity_labels[i])

                        
#4. Appropriately labelling the data set with descriptive variable names. 

# see last step of 1.!


# 5. From the data set in step 4, creates a second, independent tidy data set with the average of each
# variable for each activity and each subject.

#I again use the reference to the mean and std columns to create a vector of all variable names
namesColsMeanStd <- colnames(tt[,colsMeanStd])

# I now melt the dataset by identifying the id variables subject and activity and use all relevant variable names
ttMelt <- melt(ttOrd, id=c("subject", "activity"), measure.vars=c(namesColsMeanStd))

# from the result, dataframes giving mean and std of subject and activity are created and then bound together
ttCastS <- dcast(ttMelt, subject  ~ variable, mean)
ttCastA <- dcast(ttMelt, activity ~ variable, mean)
# In ordder to bind the two section of the tidy_data, the firstcolumns are renamed to the same string "SubjectOrActivity"
ttCastS[,1] <- as.character(ttCastS[,1] )
colnames(ttCastA)[1]<- "SubjectOrActivity"
colnames(ttCastS)[1]<- "SubjectOrActivity"

# Generate subject labels: "subject 1", subject 2" etc.
subjectLabels <- NULL
for (i in 1:max(ttOrd[,1])) {
    x <- paste("subject",as.character(i))
    subjectLabels <- c(subjectLabels,x)
}
ttCastS[,1] <- subjectLabels

# Finally, the tidy data is bound
tidy_data <<- rbind(ttCastS, ttCastA)

}
