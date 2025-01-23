library(dplyr)
library(ggplot2)
library(caret)

# load the csv dataframe
df <- read.csv("C:/Users/USER/Desktop/Heart.csv")
View(df)
show(df)
summary(df)

# rows
head(df, 5)

# columns
colnames(df)
names(df)

# datatypes
datatype <- sapply(df, class)
datatype

# shape
shape <- dim(df)
shape

# missing values
missing_value <- sum(is.na(df))
missing_value
missing_row_value <- which(rowSums(is.na(df)) > 0)
missing_row_value

# numerical col list
df_num_col <- df %>% select("Age", "Sex", "RestBP", "Chol", "Fbs", "RestECG",
                         "MaxHR", "ExAng", "Oldpeak", "Slope", "Ca")
df_num_col

# Mean (RestBP, MAxHR, Oldpeak, Chol)
restbp_Mean <- mean(df$RestBP)
restbp_Mean
maxHR_Mean <- mean(df$MaxHR)
maxHR_Mean
oldpeak_Mean <- mean(df$Oldpeak)
oldpeak_Mean
chol_Mean <- mean(df$Chol)
chol_Mean

# Median (RestBP, MAxHR, Oldpeak, Chol)
restBp_Median <- median(df$RestBP)
restBp_Median
maxHR_Median <- median(df$MaxHR)
maxHR_Median
oldpeak_Median <- median(df$Oldpeak)
oldpeak_Median
chol_Median <- median(df$Chol)
chol_Median

# standard deviation (RestBP, MAxHR, Oldpeak, Chol)
restbp_std <- sd(df$RestBP)
restbp_std
maxhr_std <- sd(df$MaxHR)
maxhr_std
oldpeak_std <- sd(df$Oldpeak)
oldpeak_std
chol_std <- sd(df$Chol)
chol_std

# Data Types Conversion(Sex should be categorical)
sex <- as.integer(df$Sex)
print(sex)

# unique values count (Sex, ChestPain, Thal, and AHD)
unique_sex <- length(unique(df$Sex))
print(unique_sex)
unique_cp <- length(unique(df$ChestPain))
print(unique_cp)
unique_thal <- length(unique(df$Thal))
print(unique_thal)
unique_ahd <- length(unique(df$AHD))
print(unique_ahd)

# histogram to show the age distribution
ggplot(data=df,aes(x=Age)) + 
  geom_histogram(fill="red", col="green", bins=20, binwidth = 2)

# average cholesterol level (Chol) for each sex
avg_chol_by_sex <- df %>% group_by(Sex)  %>% summarise
                  (avg_chol = mean(Chol))
print(avg_chol_by_sex)

# unique values in the Thal
unique_thal <- unique(df$Thal)
print(unique_thal)

# correlation matrix for numeric columns
corr_matrix <- cor(df_num_col)
print(corr_matrix)

# box plot of MaxHR by ChestPain type using seaborn
ggplot(df, aes(x=ChestPain, y=MaxHR))+geom_boxplot()

# Box Plot of Cholesterol by Sex
ggplot(data=df, aes(x=Sex, y=Chol)) + geom_boxplot() 

# scatter plot to visualize the relationship between Age and MaxHR
ggplot(data=df, aes(x=Age, y=MaxHR, col=Sex)) + geom_point()

# Group the data by ChestPain and AHD to calculate the mean Age and 
# Chol for each group
group_cp_ahd <- df %>% group_by(ChestPain, AHD) %>% summarise(
              meanAge = mean(Age))
print(group_cp_ahd)

group_cp_ahd <- df %>% group_by(ChestPain, AHD) %>% summarise(
              meanChol = mean(Chol))
print(group_cp_ahd)

# histogram to show the distribution of RestBP
ggplot(df, aes(x=RestBP, col="green")) + geom_histogram()

# violin plot to visualize the distribution of cholesterol across different AHD (heart disease) statuses
ggplot(df, aes(x=AHD, y=Chol, col="red")) + geom_violin()

# Detect and visualize outliers in RestBP using box plots
ggplot(df, aes(x=RestBP, col="green")) + geom_boxplot()

# bar plot to show the count of each ChestPain type for people with and
# without heart disease
chestPain_Ahd <- df %>% group_by(ChestPain, AHD) %>% 
  summarise(Count = n())

ggplot(chestPain_Ahd, aes(x=ChestPain, y=Count, fill=AHD)) +
  geom_bar(stat = "identity", position = "dodge") +
  labs(title = "CP by AHD", x="Chest Pain Type", y="Count")

# scatter plot to visualize the relationship between Age and Chol, 
# with points colored by ChestPain type
ggplot(df,aes(x=Age, y=Chol, col=ChestPain)) + geom_point()

# pairplot to visualize relationships between Age, RestBP, MaxHR, and 
# Oldpeak
pairs(df[, c("Age", "RestBP", "MaxHR", "Oldpeak")], col="blue")

# one-hot encoding to categorical columns (ChestPain and Thal)
data <- df %>% select("ChestPain", "Thal")
print(data)
encoded_data <- one_hot(as.data.table(data))
print(encoded_data)

# Normalize the Age, RestBP, and Chol columns to a scale of 0-1
normalizeData <- df %>%
  mutate(across(c(Age, RestBP, Chol), ~ (.-min(.)) / (max(.) - min(.))))
print(normalizeData)

# plot Age vs. MaxHR with a regression line, colored by AHD status
ggplot(df, aes(x=Age, y=MaxHR, col=AHD)) +
  geom_point() +
  geom_smooth(method = "lm", se=FALSE)

# count of AHD (Heart Disease) status by sex
ahdBySex <- df %>%
  group_by(Sex, AHD) %>%
  summarise(Count=n())
print(ahdBySex)

# correlation matrix with a heatmap
corr_matrix <- cor(df_num_col)
corrplot(corr_matrix, method="square", type="upper", tl.col="black")

# Count of Chest Pain Types
chestPainCount <- table(df$ChestPain)
chestPainCount

# logistic regression model to predict AHD based on Age, RestBP, MaxHR,
# and Chol
df$AHD <- replace(df$AHD, df$AHD == "Yes", 1)
df$AHD <- replace(df$AHD, df$AHD == "No", 0)
df$AHD <- as.integer(df$AHD)

# model fitting
logisticModel <- glm(AHD ~ Age + RestBP + MaxHR + Chol, 
                     data = df, family = "binomial")
summary(logisticModel)

# prediction
predict_probability <- predict(logisticModel, newdata= df, 
                               type="response")
print(predict_probability)

# classification
predicted_classes <- ifelse(predict_probability > 0.5, 1, 0)
print(predicted_classes)

# Error metrics
confusion_matrix <- table(df$AHD, predicted_classes)
print(confusion_matrix)

# accuracy 
accuracy <- sum(diag(confusion_matrix)) / sum(confusion_matrix)
print(accuracy)

# confidence intervals for the average Age in each AHD group
confidence_interval <- df %>% group_by(AHD) %>% summarise(
  MeanAge = mean(Age), 
  sd_Age = sd(Age), 
  n = n(),
  lower_ci = MeanAge - qt(0.975, df=n-1)* sd_Age/ sqrt(n),
  upper_ci = MeanAge + qt(0.975, df=n-1)* sd_Age/ sqrt(n))

print(confidence_interval)

# t-test to determine if there is a significant difference in Chol levels 
# between individuals with and without heart disease
t_test <- t.test(Chol ~ AHD, data=df)
print(t_test)

# simple feature selection method (like correlation ranking or a 
# decision tree model) to identify the most important features for 
# predicting AHD.
tree_model <- rpart(AHD ~ ., data=df)
var_imp <- varImp(tree_model)
print(var_imp)
plot(var_imp)