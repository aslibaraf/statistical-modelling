Backorder Prediction Statistical Modeling - Himalay Parmar
================
Subject : Statistical Modeling 

| **Primary skills** | **Primary Programs** |
|--------------------|----------------------|
| Statistical Modeling           | Python               |

Background and Objective
========================

Material backorder is a common SUPPLY CHAIN PROBLEM, impacting an inventory system service level and effectiveness. Identifying parts with the highest chances of shortage prior its occurrence can present a high opportunity to improve an overall company’s performance..

Investigated in order to propose a predictive model for this imbalanced class problem, where the relative frequency of items that go on backorder is rare when compared to items that do not. 

Specific metrics such as area under the Receiver Operator Characteristic and precision-recall curves, sampling techniques and ensemble learning are employed in this particular task. Results are presented and future scope is discussed.

Data
====

I used [data](https://www.kaggle.com/tiredgeek/predict-bo-trial) from Kaggle, which had 1.9 million observations of parts in an 8 week period. The source of the data is unreferenced.

-   **Outcome**: whether the part went on backorder : Binary classification  Prob
-   **Predictors**: Current inventory, sales history, forecasted sales, recommended stocking amount, part risk flags etc. (22 predictors in total)

Modeling
========

### Key considerations of the data:

-   **Imbalanced outcome**: Only 0.7% of parts actually go on backorder.
-   **Outliers and skewed predictors**: Part quantities (stock, sales etc.) can be on very different scales.
-   **Missing data**: A few variables have data that are missing (not at random).
-   **n&gt;&gt;p**: There are many observations (1.9 million) relative to the number of predictors (22).

### Implemented Models

We made several modeling decisions to address these issues:

-   **Random forest** estimators are used
    -   **Perform well with imbalanced data typically**
    -   **Robust to outliers and the skewed predictors**: Because they are using tree partitioning algorithms and not producing coefficient estimates, outliers and skewness are not as much of a concern as for other predictive models.
-   **Down sampling**: to account for the imbalanced outcome, we try down sampling the data of parts that didn't go on backorder.
    -   We choose down sampling over other similar methods that resample the minority group (e.g. up sampling or SMOTE) as these are more computationally burdensome with a large sample size.



-   **Dealing with missing data**: The few variables with missing data had medians imputed, and a binary variable was created to indicate whether the observation had missing data, in hopes to account for the missing data not being random.

### Validation

-   We use **10-fold cross-validation** in order to tune model parameters (maximum number of variables to try and minimum leaf size), as well as compare model performance.

-   The **ROC Area Under the Curve (AUC)** was used as a validation metric because the outcome is so imbalanced. By looking at ROC curves, we may determine a cutoff threshold for classification after fitting the models, rather than naively assuming a threshold of 0.5.

### Choosing a classification threshold

We can choose a threshold that finds a balance of **precision** and **recall** appropriate for our problem. For example, we may be more concerned with the consequences of failure to predict a product going on backorder (e.g. canceled orders, customer loss) than the consequences of backorder false alarms (e.g. unnecessary overstocking, higher inventory costs).


<br> <br> <br> <br> <br>

