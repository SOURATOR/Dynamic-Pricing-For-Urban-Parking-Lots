# Dynamic-Pricing-For-Urban-Parking-Lots
## Overview
#### This project utilizes a simulated real time data stream to build an intelligent, data-driven pricing engine for 14 parking spaces. The goal is to dynamically adjust parking prices based on real-time utilization and demand conditions to facilitate revenue optimization. It implements two distinct pricing models using Pathway, a Python-native stream processing engine, and renders results using Bokeh and Panel dashboards. The data was sampled for 73 days at 18 time points per day with 30 minutes of time difference. 

#### The two pricing models used were:
### Baseline Linear Model: 
#### A simple model where the next price is a function of the previous price and current occupancy:

<p align="center">
<img src="/images/Baseline_Linear_Model_Formula.png"/>
</p>

#### This model utilizes two features: Capacity and Occupancy. The price increases linearly as the ratio between occupancy and capacity increases. 

### Demand Based Pricing Model: 
#### This model estimates demand for parking slots using the features: Occupancy, Queue length, Traffic level, Special day and Vehicle type. This is a more nuanced model as it incorporates several variables which influences demand. The demand estimation function used is as follows:

<p align="center">
<img src="/images/Demand_Estimaton_Formula.png"/>
</p>

#### The price is estimated as a function of the base price of $10 and the normalized demand estimated from the previous function. The demand estimate was normalized using sigmoid (logistic) function. The pricing formula is as follows:

<p align="center">
<img src="/images/Demand_Based_Pricing_Function.png"/>
</p>

## Tech Stack
#### Google Colab (Execution Environment)
#### Numpy (Numerical Computing)
#### Pathway (Stateful Stream Processing)
#### Bokeh + Panel (Interactive Dashboards)
#### Git (Version Control)
#### HTML (Image Rendering In GitHub)

## Project Architecture
### Baseline Linear Model
#### The csv file of parking slot data is loaded and replayed as a simulated data stream using Pathway after defining schema. Timestamps are created and parsed and the ratio of occupancy to capacity, known as utilization is calculated. The pricing model is implamanted as a recursive stateful function and a Python dictionary is used to maintain the internal state. The mean price for each day is calculated and 14 bokeh plots are used to visualize pricing plots in real time. The complete architecture diagram is as follows:
<p align="center">
<img src="/images/Baseline_Architecture.png" alt="Baseline_Architecture" width="200"/>
</p>

#### The bokeh plots reveals that some parking lots experience high price fluctuations due to high and volatile demand whereas price fluctuations is relatively smooth for other lots due to less volatility of demand. Example plots of four such parking lots are provided below.
<p align="center">
  <img src="/images/baseline_linear_BHMBCCMKT01.png" width="45%"/>
  <img src="/images/baseline_linear_Others-CCCPS105a.png" width="45%"/>
</p>
<p align="center">
  <img src="/images/baseline_linear_Others-CCCPS119a.png" width="45%"/>
  <img src="/images/baseline_linear_Others-CCCPST35a.png" width="45%"/>
</p>

#### Evidently the price fluctuation is smooth for Others-CCCPS119a and it is relatively high for Others-CCCPS135a. This might lead to the conclusion that demand is less volatile for Others-CCCPS119a and hence it is less sensitive to occupancy ratio. 

### Demand Based Pricing Model
#### The csv file of parking slot data is loaded and replayed as a simulated data stream using Pathway after defining schema. Timestamps are created and parsed and the ratio of occupancy to capacity, known as utilization is calculated. Categorical features such as traffic conditions and VehicleType are assigned relative weights and encoded. Parameter values are arbitrarily set and demand function is estimated. The raw demand function is normalized via sigmoid (logistic function) and price is estimated using the function of baseline price and demand. The price estimates are bounded at 0.5-2 times the baseline price to smooth fluctuations. 14 bokeh plots are used to visualize pricing plots in real time. The mean price is higher than the previous model since this model takes several determinants of demand into consideration. The complete architecture diagram is as follows:

<p align="center">
<img src="/images/Demand_Pricing_Architecture.png" alt="Demand_Pricing_Architecture" width="200"/>
</p>

#### The bokeh plots reveals that the minimum price level is above $17, hence overall price of the parking lots increase as more features are taken into consideration. Example plots of four such parking lots are provided below.
<p align="center">
  <img src="/images/demand_pricing_BHMBCCMKT01.png" width="45%"/>
  <img src="/images/demand_pricing_CCCPS105a.png" width="45%"/>
</p>
<p align="center">
  <img src="/images/demand_pricing_CCCPS119a.png" width="45%"/>
  <img src="/images/demand_pricing_CCCPS135a.png" width="45%"/>
</p>

#### Evidently the price fluctuation for the same four plots is much lower than the baseline linear model. This is not only due to reduction in noise but also the sigmoid normalization of the estimated demand function and the range capping of prices between 0.5-2 times baseline price. This pricing model is more efficient from a business perspective as the fluctuations in prices are smoother and it provides an overall idea about the relative demand for parking lots.

#### These two pricing models using real time data can help identify and understand which economic factors influence demand for parking slots in urban areas and dynamically set prices to ensure revenue optimization. 
