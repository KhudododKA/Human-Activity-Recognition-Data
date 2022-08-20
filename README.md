# Human-Activity-Recognition-Data

The project will clean the data from Human Activity Recognition data collected using smartphone dataset.

## Read the data
### train data first
df_train_sub<-read.table("UCI HAR Dataset/train/subject_train.txt")
df_train_x<-read.table("UCI HAR Dataset/train/X_train.txt")
df_train_y<-read.table("UCI HAR Dataset/train/y_train.txt")

## test data
df_test_sub<-read.table("UCI HAR Dataset/test/subject_test.txt")
df_test_x<-read.table("UCI HAR Dataset/test/X_test.txt")
df_test_y<-read.table("UCI HAR Dataset/test/y_test.txt")
df_features<-read.table("UCI HAR Dataset/features.txt")
## Data cleaning
# combine/merge the train and test data
df_merged_x<-rbind(df_train_x,df_test_x)
df_merged_y<-rbind(df_train_y,df_test_y)
df_merged_sub<-rbind(df_train_sub,df_test_sub)

## rename features adn merge
names(df_merged_x)<-df_features$V2
df_merged_sub<-df_merged_sub%>%rename(.,subject_id=V1)

# merge

df_total<-cbind(df_merged_sub,df_merged_x)
df_total<-cbind(df_merged_y,df_total)

## select and summarise

## select only the mean and standard deviation of each features
df_total<-df_total%>%select(V1,subject_id,contains(c("mean","std")))

## change the activity variable value to descriptive labels
df_total$V1<-factor(df_total$V1,levels = c(1,2,3,4,5,6),
                    labels = c("WALKING","WALKING_UPSTAIRS","WALKING_DOWNSTAIRS","SITTING","STANDING","LAYING"))
# Rename the variable as activity
df_total<-df_total%>%rename(.,Activity=V1)

## summarise across to get the average for each subject and activity
df_total1<-df_total%>%
  group_by(subject_id,Activity)%>%
  summarise(across(c(1:86),mean,na.rm=TRUE))

