# PRODIGY_DS_02
Perform data cleaning and exploratory data analysis (EDA) on a dataset of your choice, such as the Titanic dataset from Kaggle. Explore the relationships between variables and identify patterns and trends in the data.

import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns
train_df = pd.read_csv(r'C:/Users/Praful J/Desktop/Prodigy/Task 2/train.csv')
test_df = pd.read_csv(r'C:\Users\Praful J\Desktop\Prodigy\Task 2\test.csv')
gender_submission = pd.read_csv(r'C:\Users\Praful J\Desktop\Prodigy\Task 2\gender_submission.csv')
# Combine the training and test datasets for analysis
full_df = pd.concat([train_df, gender_submission], sort=False)
print("Total number of passengers:", len(full_df))
print("Total number of survivors:", len(full_df[full_df["Survived"] == 1]))
print("Total number of deaths:", len(full_df[full_df["Survived"] == 0]))
Total number of passengers: 1422
Total number of survivors: 494
Total number of deaths: 815
# Plot the distribution of survivors and deaths
survivors = len(full_df[full_df["Survived"] == 1])
deaths = len(full_df[full_df["Survived"] == 0])
plt.pie([survivors, deaths], labels=["Survived", "Deaths"], autopct='%1.1f%%')
plt.title("Survivors and Deaths")
plt.show()

# Analyze passenger class distribution
sns.countplot(x='Pclass', data=full_df)
plt.title("Passenger Class Distribution")
plt.show()

# Calculate the average age of passengers
average_age = round(full_df["Age"].mean(), 2)
print("Average passenger age:", average_age)
Average passenger age: 29.88
# Calculate survival rate based on gender
survival_by_gender = full_df.groupby("Sex")["Survived"].mean() * 100
plt.pie(survival_by_gender, labels=["female", "male"], autopct='%1.1f%%')
plt.title("Survival Rate Based on Gender")
plt.show()

# Calculate survival rate based on passenger class and gender
sns.barplot(x="Pclass", y="Survived", hue="Sex", data=full_df)
plt.title("Survival Rate Based on Class and Gender")
plt.show()

# Calculate average fare paid by passengers in each class
average_fare_by_class = full_df.groupby("Pclass")["Fare"].mean()
print("Average fare paid by passengers from each class:")
print(average_fare_by_class)
Average fare paid by passengers from each class:
Pclass
1.0    87.508992
2.0    21.179196
3.0    13.302889
Name: Fare, dtype: float64
# Calculate survival rate based on age and sex
age_bins = [0, 18, 30, 50, 80]
age_labels = ["0-18", "18-30", "30-50", "50-80"]
full_df["AgeGroup"] = pd.cut(full_df["Age"], bins=age_bins, labels=age_labels)
survival_by_age_sex = full_df.groupby(["Sex", "AgeGroup"])["Survived"].mean()
print("Survival rate based on age and sex distribution:")
print(survival_by_age_sex)
sns.barplot(x="AgeGroup", y="Survived", hue="Sex", data=full_df)
plt.title("Survival Rate by Sex and Age")
plt.show()
Survival rate based on age and sex distribution:
Sex     AgeGroup
female  0-18        0.760870
        18-30       0.846154
        30-50       0.842975
        50-80       0.968750
male    0-18        0.237624
        18-30       0.102564
        30-50       0.158371
        50-80       0.095238
Name: Survived, dtype: float64

# Plot the survival rates by deck as a bar chart
sns.barplot(x='Deck', y='Survived', data=full_df, ci=None)
plt.title("Survival Rate by Deck")
plt.show()
C:\Users\Praful J\AppData\Local\Temp\ipykernel_7596\1606323110.py:2: FutureWarning: 

The `ci` parameter is deprecated. Use `errorbar=None` for the same effect.

  sns.barplot(x='Deck', y='Survived', data=full_df, ci=None)
