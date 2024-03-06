# Hotel-Reservations

## Business Problem & Understanding
**Stakeholders:** CEO of Hotel

The online Hotel reservations have dramatically changed booking possibilities and customer's behaviours. Most of the time hotel booking
cancellations can be hurtful to business owners, although it is often made easier at a low cost and beneficial to hotel guests. Last minute 
cancellations can result in loss of revenue unless some measures are undertaken to mitigate the loss.

Goal: The purpose of this project is to analyze Hotel Bookings data and investigate cancellations. We are predicting the likelihood
of cancellations when booking reservation is made, our goal is to find the best Machine Learning model.

### Dataset and Data Exploration:

For analysis, we are using a Hotel Reservation Dataset from Kaggle:

<a href = "https://www.kaggle.com/datasets/ahsan81/hotel-reservations-classification-dataset/data"> 

The Hotel-reservation Dataset 2017-2018 taken from Portugal, and each record shows booking and arrival info for each customer, This dataset has no missing values, contains 36K rows and 19 columns.

Numeric Columns    : no_of_adults, no_of_children, no_of_weekend_nights, no_of_week_nights, lead_time, no_of_previous_cancellations, 
                     no_of_previous_bookings_not_canceled, avg_price_per_room.

Categorical Columns: type_of_meal_plan, required_car_parking_space, room_type_reserved, arrival_year, arrival_month, arrival_date,
                     market_segment_type, repeated_guest, booking_status.

### Data Cleaning Before Preprocessing:

After exploring our Dataset, We added some new columns, replaced some categorcial columns to groups before preprocessing to reduce overfitting, 
following below was completed as the part of the process.

 - Columns with month date and year was concatenated to find `arrival_date`, which was used to find `booking_date`.
 - Categorical columns such as `type_of_meal_plan`, `room_type_reserved`, `market_segment_type` and `booking_status` was replaced with numbers
   before preprocessing.
 - Dropped columns `Booking_ID`, `arrival_day`, `booking_date` which may not be used later.

### Preprocessing:

Train_Test_Split was used to split our Train samples and Test samples before preprocessing to avoid Data Leakage. We applied Standard Scaler to
scale the numeric columns, and One Hot Encoder for categorical columns.

**Target y**:`booking_status` was chosen as our Target variable.

**X**       : Remaining columns except `booking_status`.

While checking the correlation factor with the function corr(), we came to know features `lead_time`, `no_of_special_requests`, `avg_price_per_room`, `length_of_stay`, `total_guests`, `market_segment_type`, `repeated_guest`, `booking_month` are highly correlated with out Target `booking_status`.

<p align="center">
    <img src = "https://" width = "  " height="  ">
</p>

### Models Used:

1. **Baseline Model Logistic Regression**:
   Using `booking_status` as y variable, remaining columns as X, and with following parameters: fit_intercept = False, max_iter = 1000,    C = 1e5, solver = 'liblinear', random_state=100. We got **AUC score 0.87** as results.

2. **Logistic Regression with High Correlated Features**:
   Using `booking_status` as y varaiable, and high correlated features as X, and with same parameters as baseline model: fit_intercept = False,     max_iter = 1000, C = 1e5, solver = 'liblinear', random_state=100. We got **AUC score 0.85** as results.

<p align="center">
    <img src = "https://" width = "  " height="  ">
</p>

3. **Decision Tree**:
   By Hyperparameter tuning to find best parameters, we found Max Tree depth 8, Min Sample splits 0.01, Min Sample Leafs 0.01 & Max Feature 12
   for Decision Tree. Building Tree model with following parameters, we got **AUC score 0.78** which was far away from our Baseline Model.

5. **Oversampling Technique, Logistic Regression**:
   Target variable has slightly imbalanced classes, Class 0 as 67% and Class 1 as 33%. We want to check if Oversampling technique will
   leads us to best model, we still got **AUC score as 0.85** .

6.  **Random Forest Classifier Baseline**:
    Using `booking_status` as y variable, remaining columns as X, and with parameters:n_estimators=100, criterion = 'entropy', random_state=100.
    We got the best **AUC score 0.93**, but was seeing our Test results are bad when Train results are doing good.

7. **Random Forest Classifier with High Correlated Features**:
    Using `booking_status` as y variable, high correlated features as X, and with parameters:n_estimators=100, criterion = 'entropy',                random_state=100. We were getting the best **AUC score 0.92**, but again seeing our Test results are bad when Train results are
    doing good.

8. **Random Forest Classifier, Optimal Hyperparameter**:
   Random Tree Classifier was improving our results, but model was overfitting with Baseline and High correlated feature models. Finally,
   we want to check tuning hyperparameter and found parameters:Max Tree depth 13, Min Sample splits 0.01, Min Sample Leafs 0.01,
   Max Feature 19 and applying n_estimators = 100. We got better **AUC score 0.88** and better train and test scores.

<p align="center">
    <img src = "https://" width = "  " height="  ">
</p>

   **Conclusion:**
   
   Above graph shows high AUC for Basemodel RandomForestClassifier, but model with Optimized Hyperparameters has best train and test metrics        compared to baseline and high correlated feature model. Both baseline and High correlated feature model shows best Train metrics and bad 
   test metrics, which is clear sign of overfitting. Final model chosen was Random Forest Classifier with Optimal Hyperparameter, which has         better AUC score and better train and test metric scores. 

   
    

