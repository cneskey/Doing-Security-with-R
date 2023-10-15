# Basic random forest classification model named classifier_RF visualized.
# 7 Partial Dependence Plots (PDPs), one for each of the categories of "Action" in the VERIS schema.
# Predictors:    malware, hacking, social, misuse, physical, error, environmental
# Predicted:     Time to Discovery (timeline.discovery.value)
# Refs:
# [1] http://veriscommunity.net/discovery.html#section-incident-timeline
# [2] https://stephenmilborrow.r-universe.dev/plotmo

library(readr)
library(tidyverse)
library(randomForest)
library(plotmo)
library(caTools)

# 1. Import the veris csv ----
vcdb <- read_csv("VCDB-master/data/csv/vcdb.csv/vcdb.csv")

# 2. Narrow to just `actions.*` and `timeline.discovery.value` ----
vcdb_ad <- select(vcdb,starts_with("action."))
vcdb_ad$"timeline.discovery.value" <- vcdb$"timeline.discovery.value"
vcdb_ad <- select(vcdb_ad,-ends_with(".notes"))
vcdb_ad <- select(vcdb_ad,-ends_with(".cve"))
vcdb_ad <- select(vcdb_ad,-contains("vector"))
vcdb_ad <- select(vcdb_ad,-contains("variety"))
vcdb_ad <- select(vcdb_ad,-contains("result"))
vcdb_ad <- select(vcdb_ad,-contains("action.social."))
vcdb_ad <- select(vcdb_ad,-contains("action.malware."))
vcdb_ad <- select(vcdb_ad,-contains("unknown"))

# 3. Trim "action." from the variable names. ----
names(vcdb_ad) <- sub("action.", "", names(vcdb_ad))

# 4. Drop rows w/o timeline values ----
vcdb_ad_remna <- filter(vcdb_ad, timeline.discovery.value != "N/A")

# 5. Change True and False to 1, 0 ----
vcdb_ad_remna_char <- vcdb_ad_remna*1

# 6. Classify the data with random forest ----
# Load data
data(vcdb_ad_remna_char)

# Check structure
str(vcdb_ad_remna_char)

# Split data into train and test sets
split <- sample.split(vcdb_ad_remna_char, SplitRatio = 0.7)
train <- subset(vcdb_ad_remna_char, split == "TRUE")
test <- subset(vcdb_ad_remna_char, split == "FALSE")

# Fit a Random Forest to the train dataset
classifier_RF = randomForest(x = train[-8],
                             y = train$timeline.discovery.value,
                             ntree = 10)

# Inspect Model ----
# Preview
classifier_RF

# Predict the Test set results
y_pred = predict(classifier_RF, newdata = test[-8])

# Plot a Confusion Matrix
confusion_mtx = table(test[, 8], y_pred)
confusion_mtx

# Plot the model
plot(classifier_RF)

# Plot Importance of model
importance(classifier_RF)

# Plot Variable Importance
varImpPlot(classifier_RF)

# Plot the residuals
plotres(classifier_RF)

# Plot model over the range of predictors
plotmo(classifier_RF,
       pmethod="partdep")
