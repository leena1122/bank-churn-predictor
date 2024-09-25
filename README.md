# bank-churn-predictor
Churn Sight

Predicting whether credit card customers will churn

Description

Data Source and Overview

This project focuses on predicting customer churn from a bank’s credit card service based on many customer attributes, such that the bank can take action to prevent further customer churn in the future. For context, “churn” in this specific scenario is the proportion of customers who stop utilizing the bank’s services, and is used interchangeably with “attrition rate” in this report. Our specific dataset used for this project, Credit Card Customers, is a public dataset from Kaggle with such information. Hoping to make a real-world impact, the motivation behind our project is to target an issue that all successful businesses have to consider: customer retention. This dataset serves our purpose because it provides an “Attrition Flag” column, which creates a marker for all attrited customers from which we can calculate churn. By utilizing the other columns, including customer age, gender, income category, and more, we analyzed correlations and built a model that very accurately predicts attrition. The raw dataset provided by Kaggle contains over 10,000 customer instances with 18 unique identifiers/columns. It’s relatively well organized and complete–has great usability. With minor calculations, we find that 16.07% of customers existing within this dataset have an “Attrited” flag. With these factors in mind, our team decided to use this dataset to create our machine-learning model, and hope to apply it to other businesses and datasets in the future.

Data Exploration

We start off by inspecting the dataset per usual using Pandas. We look at the columns and a couple of random samples in order to determine how the data is structured. We make sure to convert values to their respective Pandas equivalent (numbers to int, unknowns to NA, yes and no to True/False. After making sure it is well structured, we graph some distributions of the numeric variables to make sure the data doesn’t have any surprises. We also take some descriptive statistics to get an idea of who these customers are. Most importantly, we then take a lot of the distributions of these variables split by the variable we’re trying to predict: attrition. We look for any patterns in these variables. We surprisingly found a huge difference in some of these distributions depending on whether or not the customer churned. For example a 71 yearly transaction count for existing customers as opposed to 43 for attritied customers. We then take this analysis a bit further by visualizing the correlation between these variables and attrition. We found that the variables that were the most correlated with attrition were Contacts_Count_12_Mon, Total_Revolving_Balance, and Total_Transaction_Count. Not surprisingly, these were the variables that were the most important when training tree-based models.

Data Cleaning

For data cleaning, we first wanted to figure out how to handle the unknown values in the Education_Level, Marital_Status, and Income_Category columns. We compared the overall distribution of each column with the distribution of the unknown values within each label. We determined that for Education_Level and Marital_Status, the unknown values were random since the distributions were within 10% of each other. However, we determined that the values for Income_Category were not random since 95% of the unknown values were from female customers, but only 52% of data was female. Next, we converted the categorical data to numerical formats. To do this, we binarized the columns with only 2 labels and mapped ordinal categorical data to sequential numerical values. For Income_Category and Education_Level, we converted 'Unknown' to NaN and for Marital_Status, we applied One-Hot encoding since the data was nominal. To handle the unknowns, we dropped all the rows where Education_Level was NaN and where Marital_Status_Unknown was equal to 1. We then deleted the Marital_Status_Unknown column and used KNN to impute the NaN values for Income_Category.

Data Modeling

The first step of data modeling was to split the data into training and testing datasets. We then conducted feature selection, for which we used sklearn’s SelectKBest function using the chi-squared metric. Out of the existing 21 features, 15 were selected. We then identified some common classification models and key hyperparameters for each. Specifically, for RandomForest we varied max_depth and min_samples_split, for XGBoost we varied min_samples_split, and for KNN we varied k. After initializing each of these models, we conducted 5-fold cross validation on the training dataset for each of them. This training itself was split into two sections: firstly, training on the training dataset pre-feature selection, and then training again on the dataset post-feature selection. We then extracted the training and testing results of each model. In order to aid with interpretability, we also extracted feature importances from the top-performing RandomForest and XGBoost models.

Data Interpretation

Our analysis achieved around 96% accuracy in predicting customer churn using Gradient Boosting, and 95% with Random Forest. This high accuracy demonstrates the effectiveness of these models in identifying at-risk customers and determining the key factors that lead to churning. We found several key factors that influence churn. First a high revolving balance (the amount of money owed on a credit card) and a high credit utilization ratio (the percentage of credit used) were one of the main indicators of likelihood to churn. Additionally, less frequent transactions and fewer bank products used are other central signals of whether a customer will leave. This leads us to the understanding that customers likely to churn tend to have higher debt, more financial stress, and less overall engagement with the bank.

Data Action/Conclusion

The findings from our models provide actionable insights for addressing customer churn in the bank's credit card service. High revolving balances and credit utilization ratios are significant predictors of churn, indicating financial stress as a key factor. Other customers at high risk are those with fewer interactions or inactivity, suggesting the need for enhanced engagement strategies. Income category and credit limit, while not the top predictors, still play a role in retention. These factors suggest that in order to mitigate churn, the bank should implement targeted engagement programs, increase communication with less engaged customers, offer incentives for active usage, develop tailored financial products, and regularly monitor at-risk customers.

Authors

Sorted by last name:

Josefina Camacho

Kathy Cui

Arturo Fonseca

Leena Shafi

Shreya Sridhar

Rebecca Xu


Version History

0.1

  Initial Release
  
License

This project is licensed under the Northwestern University License!
