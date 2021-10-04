# NYC-Green-Taxi
Let's first load the data and look at the shape of the dataframe
```
df1.shape
```
(1224158, 18)

Let's get a peek into the data:
Field Name Description

- VendorID: A code indicating the LPEP provider that provided the record.

         1= Creative Mobile Technologies, LLC; 
         2= VeriFone Inc.
- lpep_pickup_datetime: The date and time when the meter was engaged.

- lpep_dropoff_datetime The date and time when the meter was disengaged.

- Passenger_count: The number of passengers in the vehicle.

             This is a driver-entered value.
- Trip_distance: The elapsed trip distance in miles reported by the taximeter.

- PULocationID: TLC Taxi Zone in which the taximeter was engaged

- DOLocationID: TLC Taxi Zone in which the taximeter was disengaged

- RateCodeID: The final rate code in effect at the end of the trip.

         1= Standard rate
         2=JFK
         3=Newark
         4=Nassau or Westchester
         5=Negotiated fare
         6=Group ride
- Store_and_fwd_flag: This flag indicates whether the trip record was held in vehicle memory before sending to the vendor, aka “store and forward,” because the
  vehicle did not have a connection to the server.

         Y= store and forward trip
         N= not a store and forward trip
- Payment_type A numeric code signifying how the passenger paid for the trip.

        1= Credit card
        2= Cash
        3= No charge
        4= Dispute
        5= Unknown
        6= Voided trip
- Fare_amount: The time-and-distance fare calculated by the meter.

- Extra: Miscellaneous extras and surcharges. Currently, this only includes

            the $0.50 and $1 rush hour and overnight charges.
- MTA_tax: $0.50 MTA tax that is automatically triggered based on the metered rate in use.

- Improvement_surcharge: $0.30 improvement surcharge assessed on hailed trips at the flag drop. The improvement surcharge began being levied in 2015.

- Tip_amount Tip amount – This field is automatically populated for credit card tips. Cash tips are not included.

- Tolls_amount: Total amount of all tolls paid in trip.

- Total_amount: The total amount charged to passengers. Does not include cash tips.

- Trip_type: A code indicating whether the trip was a street-hail or a dispatch that is automatically assigned based on the metered rate in use but can be altered by the driver.

        1= Street-hail
        2= Dispatch

## **Characterize the data and comment about its quality**
- ehail_fee has 99% Nan values.
- There are invalid/negative observations in variables- fare_amount, extra, mta_tax, tip_amount, improvement_surcharge and total_amount.
- There are 13958 rows out of 1224158 which has 0 trip distance.
- There were 166 trips with passenger count as 0. 

**Data Cleaning**
- droped ehail_fee- all transactions are NaNs
- Remove negative observations in variables- fare_amount, extra, mta_tax, tip_amount, improvement_surcharge, total_amount.
- Removed observations with 0 trip distance values. 
- Removed observations with passenger count as 0
- Removed outlier values in trip distance as seen from the box plot which are 3 standard deviations away from mean
- converted the pickup time and drop off time into datetime

## **Explore and visualize the data e.g. a histogram of trip distance**
**histogram of trip distance**
- plotted the histogram with 50 bins
- Outliers have been removed before plotting.
- Outliers are defined as any point located further than 3 standard deviations from the mean

![](histogram%20of%20trip%20distance%20without%20outliers.png)

Findings from the above histogram
- The trip distance is skewed to the right that means the mean is greater than the median.
- That means most of the data is on the left side of the histogram.
- This tells us most of the trips are short distance trips between 0-3 miles of distance.

## **Find interesting trip statistics grouped by hour**
**Feature Engineering**
- Added pickupday, pickupday_no, pickup_hour into dataframe.
- these features are extracted from lpep_pickup_datetime and lpep_dropoff_datetime
- added time of day feature- morning, afternoon, evening, late night
- added is_weekday- 1 for weekday and 0 for weekend.


From the above graph we can see that no of trips are

- maximum around 7 p.m. which could be because people usually go home from work at that hour and
minimum at 5 a.m when everyone sleeps :)

![](https://github.com/drsanchikagupta/NYC-Green-Taxi/blob/main/Graph%20plotting%20pickup%20hour%20against%20no%20of%20trips.png)
![](https://github.com/drsanchikagupta/NYC-Green-Taxi/blob/main/Graph_plotting_pickup_hour_against_trip_distance.png)

The above graph plots trip distance against pickup hour and from the graph we can see:

- The trip distance is maximum around 5 a.m. that maybe because of the long distance travel early morning rides. People who live far from there office have to start early to reach work.
- The trip distance is minimum around 6 p.m- 7 p.m.

