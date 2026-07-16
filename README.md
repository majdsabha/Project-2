# Adult Income Classification Project

## Project Overview

This project uses the Adult Income dataset to build a binary classification model that predicts whether a person earns `>50K` or `<=50K`.

The goal of this project is to explore and clean the dataset, build a machine learning classification model, evaluate its performance, and identify the most important features related to higher income.

---

## Dataset

The selected dataset is the **Adult Income Dataset**.

Each row represents one person and includes demographic and work-related information such as:

- Age
- Workclass
- Education
- Marital status
- Occupation
- Relationship
- Race
- Gender
- Capital gain
- Capital loss
- Hours worked per week
- Native country
- Income

The target variable is:

- `income`

The target has two classes:

- `<=50K`
- `>50K`

This is a binary classification problem.

---

## Dataset Selection

### What is the target?

The target is `income`. It is a binary classification target with two classes: `<=50K` and `>50K`. The goal is to predict whether a person's income is greater than 50K or not.

### What does one row represent?

Each row represents one person, including demographic and work-related information such as age, workclass, education, occupation, hours worked per week, and income category.

### How many features does the data have?

The dataset originally has 15 columns. Since `income` is the target, the model uses 14 columns as features.

### How many rows are in the dataset?

The dataset originally had 48,842 rows. After removing 52 duplicate rows, the cleaned dataset has 48,790 rows.

### What opportunities exist for dimensionality reduction or feature selection with this dataset?

This dataset contains several categorical features, such as workclass, education, marital-status, occupation, relationship, race, gender, and native-country. After one-hot encoding, these features create many new columns. Therefore, feature selection can help identify the most important predictors. Dimensionality reduction may also be useful if the encoded dataset becomes very large.

### What challenges do you foresee in cleaning, exploring, or modeling this dataset?

Some values were written as `?`, which had to be treated as missing values. The dataset also contains both numerical and categorical features, so preprocessing requires scaling numerical features and encoding categorical features. Another challenge is class imbalance because about 76% of people earn `<=50K`, while only about 24% earn `>50K`.

---

## Data Cleaning

During data cleaning:

- Duplicate rows were removed.
- Values written as `?` were treated as missing values.
- Missing values in categorical columns were filled with `Unknown`.

The columns that contained missing or unknown values were:

- `workclass`
- `occupation`
- `native-country`

After cleaning, the dataset contained 48,790 rows and 15 columns.

---

## Exploratory Data Analysis

Exploratory visualizations were created to understand the relationship between the features and the target variable.

The analysis showed that:

- Most people in the dataset earn `<=50K`.
- People earning `>50K` tend to be older on average.
- People earning `>50K` tend to work more hours per week on average.
- Higher education levels are associated with a higher proportion of people earning `>50K`.
- Occupation also shows a clear relationship with income.

These findings suggest that age, education, occupation, and working hours may be useful predictors of income.

---

## Modeling

A default **Random Forest Classifier** was used for this classification task.

Before modeling, the data was preprocessed using a pipeline:

- Numerical features were scaled.
- Categorical features were one-hot encoded.
- The data was split into training and testing sets using stratification.

The model was evaluated using a classification report and a confusion matrix.

---

## Model Evaluation

The default Random Forest model achieved good overall accuracy on the test data. However, because the goal is to identify people who earn `>50K`, recall for the `>50K` class was especially important.

The model performed better on the `<=50K` class than on the `>50K` class. This is likely related to class imbalance, since the `<=50K` class is much larger.

For the `>50K` class, recall showed that the model identified many higher-income individuals, but it also missed some of them. This means future model tuning should focus on improving recall for the `>50K` class.

---

## Feature Importance

Permutation importance was used to identify the most important features based on recall for the `>50K` class.

Recall was used instead of accuracy because the dataset is imbalanced, and the main business goal is to correctly identify people who actually earn more than 50K.

The top features included:

- Marital status
- Relationship
- Age
- Occupation
- Educational number
- Capital gain
- Hours per week
- Gender
- Education
- Capital loss

These features make sense because income is often related to household structure, career stage, education level, occupation, work hours, and financial activity.

---

## Explanatory Visualizations

I selected `marital-status` and `relationship` because they were the top two features from the permutation importance results using recall as the scoring metric.

These visualizations show the relationship between each selected feature and the target variable `income`.

---

### Income by Marital Status

<img width="846" height="656" alt="marital status" src="https://github.com/user-attachments/assets/0c299bd0-862d-45ad-81d3-d328df114d94" />


This visualization shows the proportion of people earning `>50K` for each marital status category. The highest proportion is for `Married-civ-spouse`, where about 44.6% of people earn more than 50K. `Married-AF-spouse` also has a relatively high proportion.

On the other hand, categories such as `Never-married`, `Separated`, and `Widowed` have much lower proportions of people earning more than 50K.

This suggests that marital status is strongly related to income. This may be because marital status can reflect life stage, age, household structure, and financial stability.

---

### Income by Relationship

<img width="846" height="611" alt="relationship" src="https://github.com/user-attachments/assets/9b8c85d1-943d-4742-8e09-9f7412c6e2aa" />


This visualization shows the proportion of people earning `>50K` for each relationship category. The highest proportions are for `Wife` and `Husband`, where about 46.9% and 44.9% of people earn more than 50K.

Other categories, such as `Not-in-family`, `Unmarried`, `Other-relative`, and `Own-child`, have much lower proportions of people earning more than 50K.

This suggests that relationship status is strongly related to income. It may reflect household role, age, career stage, and financial responsibility.

---

## Final Conclusion

In this project, I used the Adult Income dataset to predict whether a person earns more than 50K. After cleaning the data, exploring trends, preprocessing features, and training a Random Forest model, I found that the model performed well overall but had room for improvement in identifying the `>50K` class.

Using permutation importance with recall, the most important features were related to marital status, relationship, age, occupation, and education. The final explanatory visualizations showed that marital and relationship status have a clear connection with income level.

Future improvements could include model tuning, trying other classification models, handling class imbalance, and comparing recall-focused models.
