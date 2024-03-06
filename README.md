# Hotel-Reservations

## Business Problem & Understanding
**Stakeholders:** CEO of Hotel

The online Hotel reservations have dramatically changed booking possibilities and customer's behaviours. Most of the time hotel booking
cancellations can be hurtful to business owners, although it is often made easier at a low cost and beneficial to hotel guests. Last minute 
cancellations can result in lost revenue unless some measures are undertaken to mitigate the loss.

Goal: The purpose of this project is to analyze Hotel Bookings data and investigate cancellations. We are predicting the likelihood
of cancellations when booking reservation is made, we are tring to find the best Machine Learning model to answer this.

### Dataset and Data Exploration:

For analysis, we are using Hotel Reservation Dataset from Kaggle:

- <a href = "https://www.kaggle.com/datasets/ahsan81/hotel-reservations-classification-dataset/data"> 

This dataset is used in Portugal in the years 2017 & 2018, and each record shows booking and arrival info for each customer, This dataset has no missing values, contains 36K rows and 19 columns.

Numeric Columns    : no_of_adults, no_of_children, no_of_weekend_nights, no_of_week_nights, lead_time, no_of_previous_cancellations, 
                     no_of_previous_bookings_not_canceled, avg_price_per_room.

Categorical Columns: type_of_meal_plan, required_car_parking_space, room_type_reserved, arrival_year, arrival_month, arrival_date,
                     market_segment_type, repeated_guest, booking_status.

### Data Cleaning Before Preprocessing:

After exploring our Dataset, We added some new columns, replaced some categorcial columns to groups before preprocessing to reduce overfitting, following below was completed as the part of the process.

 - Columns with month date and year was concatenated to find `arrival_date`, which was used to find `booking_date`.
 - Categorical columns such as `type_of_meal_plan`, `room_type_reserved`, `market_segment_type` and `booking_status` was replaced with numbers
   before preprocessing.
 - Dropped columns `Booking_ID`, `arrival_day`, `booking_date` which may not be used later.

### Preprocessing:

Train_Test_Split was used to split our Train samples and Test samples before preprocessing to avoid Data Leakage. We applied Standard Scaler to
scale the numeric columns, and One Hot Encoder for categorical columns.

**Target y**:`booking_status` was chosen as our Target variable.
**X**       : Remaining columns except `booking_status`.

While checking the correlation factor with the function corr(), we came to know features `lead_time`, `no_of_special_requests`, `avg_price_per_room`, `length_of_stay`, `total_guests`, `market_segment_type`, `repeated_guest`, `booking_month` are highly
correlated with out Target variable `booking_status`.




