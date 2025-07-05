# Dynamic-Pricing-For-Urban-Parking-Lots
## Overview
#### Urban parking spaces are a limited and highly demanded resource. Prices that remain static throughout the day can lead to inefficiencies — either overcrowding or underutilization. To improve utilization, dynamic pricing based on demand, competition, and real-time conditions is crucial. This project utilizes a simulated real time data stream to build an intelligent, data-driven pricing engine for 14 parking spaces. This project implements two dynamic pricing models for 14 urban parking slots over a span of 73 days. The data was sampled at 18 time points per day with 30 minutes of time difference (from 8:00 AM to 4:30 PM the same day). 

#### The two pricing models used were:
### Baseline Linear Model: 
#### A simple model where the next price is a function of the previous price and current occupancy:
![Baseline Linear Model](Baseline_Linear_Model_Formula.png)
#### This model utilizes two features: Capacity and Occupancy. The price increases linearly as the ratio between occupancy and capacity increases. 

### Demand Based Pricing Model: 
#### This model estimates demand for parking slots using the features: Occupancy, Queue length, Traffic level, Special day and Vehicle type. This is a more nuanced model as it incorporates several variables which influences demand. The demand estimation function used is as follows:
![Demand Estimation Formula](Demand_Estimaton_Formula.png)
#### The price is estimated as a function of the base price of $10 and the normalized demand estimated from the previous function. The demand estimate was normalized using sigmoid (logistic) function. The pricing formula is as follows:
![Demand_Based_Pricing_Function](Demand_Based_Pricing_Function.png)

#### These two pricing models using real time data can help understand how several economic factors influence demand for parking slots in urban areas. 


