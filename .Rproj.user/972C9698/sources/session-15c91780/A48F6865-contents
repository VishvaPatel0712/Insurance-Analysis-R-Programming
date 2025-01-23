# Load the CSV data
df <- read.csv("C:/Users/USER/Downloads/insurance.csv")
View(df)
show(df)
summary(df)

# rows
row <- head(df)
print(row)

# column names 
col_name <- colnames(df)
print(col_name)

# data types
data_type <- sapply(df, class)
print(data_type)

# shape
shape <- dim(df)
print(shape)

# missing values
missing_value <- sum(is.na(df))
print(missing_value)

missing_row <- which(rowSums(is.na(df)) >0)
print(missing_row)

# mean (age, bmi, children, charges)
age_mean <- mean(df$age)
print(age_mean)
bmi_mean <- mean(df$bmi)
print(bmi_mean)
children_mean <- mean(df$children)
print(children_mean)
charges_mean <- mean(df$charges)
print(charges_mean)

# median (age, bmi, children, charges)
age_median <- median(df$age)
print(age_median)
bmi_median <- median(df$bmi)
print(bmi_median)
children_median <- median(df$children)
print(children_median)
charges_median <- median(df$charges)
print(charges_median)

# standard deviation (age, bmi, children, charges)
age_std <- sd(df$age)
print(age_std)
bmi_std <- sd(df$bmi)
print(bmi_std)
children_std <- sd(df$children)
print(children_std)
charge_std <- sd(df$charges)
print(charge_std)

# Data Types Conversion (children should be integer)
child_int <- as.integer(df$children)
print(child_int)

# Count the unique values in the sex, smoker, and region columns
sex_unique <- length(unique(df$sex))
print(sex_unique)
smoker_unique <- length(unique(df$smoker))
print(smoker_unique)
region_unique <- length(unique(df$region))
print(region_unique)

# histogram to show the age distribution
ggplot(df, aes(x=age, col="red")) + 
  geom_histogram(fill="blue", bins=20) +labs(title = "Age Distribution")

# average charges for each gender
avg_charge <- df %>% group_by(sex) %>% summarise(
  AvgCharge = mean(charges))
print(avg_charge)

# average charges for smokers vs. non-smokers
avg_charge <- df %>% group_by(smoker) %>% summarise(
  AvgCharge = mean(charges))
print(avg_charge)

# unique values in the region column.
region_unique <- unique(df$region)
print(region_unique)

# correlation matrix for numeric columns
num_col <- df %>% select("age", "bmi", "children", "charges")
# print(num_col)
corr_matrix <- cor(num_col)
print(corr_matrix)

# Visualize the correlation matrix with a heatmap
corr_matrix <- cor(num_col)
corrplot(corr_matrix, method = "pie", type="full")

# scatter plot to visualize the relationship between bmi and charges.
ggplot(df, aes(x=bmi, y=charges, color="green")) + 
  geom_point() + 
  labs(title = "Relationship between bmi and charges")

# box plot to visualize the distribution of charges for smokers & non-smokers.
ggplot(df, aes(x=smoker, y=charges, col="blue", fill=sex)) + geom_boxplot() +
  labs(title = "Distribution of charges for smoker")

# box plot of charges by region 
ggplot(df, aes(x=region, y=charges, fill=region)) +geom_boxplot() +
  labs(title = "charges by region")

# Group the data by region and smoker, calculating the mean charges for each group.
group_reg_sm <- df %>% group_by(region, smoker) %>% summarise(
  MeanCharge = mean(charges))
print(group_reg_sm)

# count of smokers and non-smokers by gender.
count_smoker <- table(df$sex, df$smoker)
print(count_smoker)

# histogram to show the distribution of BMI values.
ggplot(df, aes(x=bmi, col="red")) + geom_histogram(fill="blue") +
  labs(title = "Distribution of BMI values")

# one-hot encoding to categorical columns (sex, smoker, and region).
data <- df %>% select("sex", "smoker", "region")
encode <- one_hot(as.data.table(data))
print(encode)

# Normalize the age, bmi, and charges columns to a scale of 0-1.
normalize <- df %>% mutate(across
                           (c(age, bmi, charges), ~ (.-min(.)) / (max(.) - min(.))))
print(normalize)

# pairplot to visualize relationships between age, bmi, children, and charges.
pairs(df[, c("age", "bmi", "children", "charges")], col="purple")

# violin plot to visualize the distribution of charges across different regions, 
# separated by smoker status.
ggplot(df, aes(x=region, y=charges, fill=smoker)) + geom_violin() +
  labs(title = "Distribution of charges vs different regions")

# linear regression to predict charges based on age, bmi, children, and 
# smoker status.
linear_model <- lm(charges ~ age + bmi + children + smoker, 
                   data=df, family = "binomial")
print(linear_model)

summary(linear_model)

predict_probability <- predict(linear_model, newdata = df, type="response")
print(predict_probability)

new_data <- data.frame(age=32, bmi=24.5, children=2, smoker="yes")
predict_charges <- predict(linear_model, newdata = new_data)
print(predict_charges)

# RMSE (root mean squared error)
rmse <- sqrt(mean(residuals(linear_model)^2))
print(rmse)

# confidence intervals for the average charges in each region.
confidence_interval <- df %>% group_by(region) %>% summarise(
  Mean_Charges = mean(charges),
  Sd_charges = sd(charges),
  n = n(),
  lower_ci = Mean_Charges - qt(0.975, df=n-1)* Sd_charges/ sqrt(n),
  upper_ci = Mean_Charges + qt(0.975, df=n-1)* Sd_charges/ sqrt(n))
print(confidence_interval)    

# t-test to see if there is a significant difference in average charges 
# between smokers and non-smokers.
t_test <- t.test(charges ~ smoker, data=df)
print(t_test)

# plot age vs. charges with a regression line, colored by smoking status.
ggplot(df, aes(x=age, y=charges, col=smoker)) + geom_point()+
  geom_smooth() + labs(title = "age vs. charges")

# Detect and visualize outliers in the bmi column using box plots.
ggplot(df, aes(x=bmi, col=sex)) + geom_boxplot() + labs(title = "outliers in the bmi") 

# Group the data by sex and calculate the mean, median, and count for 
# charges and bmi.
a <- df %>% group_by(sex) %>% summarise(mean_charges = mean(charges),
                                        median_charges = median(charges),
                                        count_charges = n(),
                                        mean_bmi = mean(bmi),
                                        median_bmi = median(bmi), 
                                        count_bmi = n())
print(a)

# Identify the most important features that affect charges using a simple
# feature importance method, such as correlation ranking or using a 
# decision tree model.
tree_model <- rpart(charges ~ ., data=df)
var_imp <- varImp(tree_model)
print(var_imp)
plot(tree_model)

# bar plot to show average charges based on the number of children.
data <- df %>% group_by(children) %>% 
  summarise(MeanCharge = mean(charges, na.rm = TRUE))
print(data)
ggplot(data, aes(x=children, y=MeanCharge)) + 
  geom_bar(stat = "identity", position = "dodge") +
  labs(title = "average charges based on the number of children")
