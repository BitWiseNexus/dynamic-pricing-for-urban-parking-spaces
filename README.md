# 📑 Final Report: Dynamic Pricing for Urban Parking Spaces

---

## 📌 Introduction

Urban parking presents a significant logistical and economic challenge due to its limited availability and high demand variability. Traditional static pricing mechanisms often result in inefficiencies—either leading to underutilization of available parking or excessive congestion.

This project investigates and implements **dynamic pricing strategies** using real-time data to enhance efficiency and demand responsiveness. Two pricing models were developed and evaluated:

- **Model 1:** Linear Occupancy-Based Pricing (Baseline)
- **Model 2:** Multi-Factor Demand-Based Pricing

Both models are implemented using **NumPy** and **Pandas**, with parameter tuning via **grid search** to optimize pricing stability and responsiveness.

---

## 📌 Dataset Description

The dataset comprises detailed records from **14 urban parking locations** collected over a period of **73 days**, segmented into **18 half-hour intervals daily** (from 8:00 AM to 4:30 PM). The dataset includes the following features:

- Occupancy  
- Capacity  
- Queue Length  
- Traffic Conditions  
- Special Day Indicator (e.g., festivals, public holidays)  
- Vehicle Type  

This data enables temporal, spatial, and behavioral analysis of parking demand.

---

## 📌 Model 1: Baseline Linear Price Adjustment Model

### 📖 Pricing Function

A straightforward model that adjusts price in proportion to changes in occupancy:

NewPrice_t = PreviousPrice_t + α × (Occupancy_t - PrevOccupancy_t) / (Capacity - PrevOccupancy_t)

yaml
Copy
Edit

Where:
- **α (alpha)** controls the price sensitivity to occupancy change.

---

### 📌 Assumptions

- Price resets to a **base value of \$10** at the start of each day.  
- Pricing changes linearly with occupancy variation.  
- No additional factors are considered.  

---

### 📊 Optimization Strategy

A **grid search** over various alpha values was conducted to minimize the **mean of day-wise standard deviation in pricing**, promoting smoother daily price transitions.

---

## 📌 Model 2: Multi-Factor Demand-Based Pricing Model

### 📖 Demand and Pricing Function

This model introduces a more comprehensive demand function incorporating multiple influencing factors:

Demand = α × (Occupancy / Capacity) + β × QueueLength - γ × TrafficCondition + δ × IsSpecialDay + ε × VehicleTypeWeight

csharp
Copy
Edit

The price is then computed as:

NewPrice_t = BasePrice × (1 + λ × NormalizedDemand)

yaml
Copy
Edit

Where:
- **λ** is a demand scaling coefficient (set to 0.6).
- Prices are capped within the range **[0.5×, 2×]** of the base price.

---

### 📌 Assumptions

- Demand factors are linearly combined.  
- Demand is normalized daily to ensure consistency.  
- Prices are bounded to prevent volatility.  
- Traffic and vehicle type are encoded numerically:  

  - **Traffic Conditions:** {Low: 0.3, Medium: 0.6, High: 1.0}  
  - **Vehicle Types:** {Car: 1.0, Bike: 0.7, Truck: 1.3}  

---

### 📊 Optimization Strategy

A grid search was conducted over combinations of (α, β, γ, δ, ε) to minimize the **mean standard deviation of daily price changes**, ensuring stability without sacrificing demand responsiveness.

---

## 📊 Pricing Behavior Overview

The pricing dynamics follow intuitive patterns:

- **High Occupancy or Queue Length:** Indicates strong demand, resulting in price increases.  
- **High Traffic Congestion:** Reduces parking accessibility, decreasing demand and thus price.  
- **Special Days:** Tend to attract higher traffic, warranting price adjustments upward.  
- **Vehicle Type:** Adjusts demand weight based on expected space usage and vehicle impact.  

These effects are moderated by:
- **Daily normalization** of demand  
- **Pricing bounds**  
- **Smoothness-driven optimization**  

---

## 📌 Evaluation

In line with the project guidelines, no single quantitative metric was mandated. The models were evaluated based on:

- **Smoothness** of price transitions  
- **Responsiveness** to realistic changes in demand  
- **Interpretability** and clarity of pricing logic  

---

## 📌 Conclusion

- **Model 1** serves as a reliable baseline but lacks responsiveness to multifaceted demand signals.  
- **Model 2** demonstrates a more sophisticated and realistic pricing mechanism, adjusting to a broader set of contextual variables.  
- Optimization efforts ensure that pricing remains **stable, explainable, and adaptive** to real-time demand fluctuations.

---

## 📌 Future Directions

Potential avenues for enhancing this framework include:

- Incorporating **revenue or profit maximization** as an explicit objective  
- Imposing **responsiveness constraints** to avoid overly stable (and ineffective) pricing  
- Leveraging **machine learning models** or **non-linear regression** for dynamic parameter adaptation and learning-based decision-making  

---

## ✅ Deliverables

- ✅ A well-documented Google Colab notebook featuring all implementation code and **interactive Bokeh visualizations**  
- ✅ This comprehensive report detailing:

  - Model design and assumptions  
  - Demand and pricing logic  
  - Optimization techniques  
  - Behavioral insights and interpretation  
  - Evaluation rationale  

---