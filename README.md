# hotel-demand-forecasting project

## Overview

In this project, I built a forecasting pipeline to predict daily hotel demand across multiple properties. The goal was to compare different types of models and see which ones perform best on real-world time series data.

I tested a range of approaches—from simple baseline models to more advanced machine learning and neural network models—and evaluated them using a consistent cross-validation setup.

---

## Dataset

The dataset contains daily demand data for multiple hotels:

- `unique_id`: hotel identifier  
- `ds`: date  
- `y`: normalized demand (between 0 and 1)  

From exploring the data, a few patterns stood out:
- demand tends to follow a weekly cycle  
- hotels behave very differently from each other  
- some series are stable, while others are volatile or have sharp changes  

---

## Forecasting Approach

All models were evaluated using time-series cross-validation.

- Forecast horizon: 28 days (4 weeks)  
- Number of windows: 5 (for most models)

For each window:
1. Train on past data  
2. Predict the next 28 days  
3. Compare predictions to what actually happened  

This setup lets us simulate how the model would perform in real forecasting scenarios.

---

## Models Used

### Baseline Models
- Naive  
- Seasonal Naive  

### Statistical Models
- AutoETS  
- AutoARIMA  

### Machine Learning
- LightGBM (using lag features like 1, 7, 14, 28 days)
- Included day-of-week and month features

### Neural Models
- AutoNBEATS  
- AutoNHITS  

Because neural models take much longer to run, I used fewer cross-validation windows for them to keep the project practical.

---

## Evaluation Metrics

I compared models using:

- Bias (ME) → whether the model over/under predicts  
- MAE → average error  
- RMSE → penalizes large mistakes more  
- MAPE → error in percentage terms  

Lower values mean better performance.

---

## Results

### Statistical Models
- AutoARIMA performed best overall  
- AutoETS was consistently solid  
- Seasonal Naive didn’t perform well, even though weekly patterns exist  

---

### Machine Learning vs Statistical Models
- LightGBM improved accuracy, especially for MAE and MAPE  
- AutoARIMA still did well for RMSE  
- ML models handled more complex patterns better  

---

### Final Comparison (Including Neural Models)
- AutoNBEATS performed best overall (MAE, MAPE)  
- AutoNHITS performed best for RMSE  
- Neural models clearly outperformed the others  

This suggests that hotel demand has more complex behavior that simpler models struggle to capture.

---

## Forecast Plots

Forecast plots for every hotel are included in the `/plots` folder.

Each plot shows:
- recent actual demand  
- the 28-day forecast from the final model  

---

## Outputs

All outputs are included in the repository:

### `/outputs`
- cross-validation results  
- model comparison tables  
- model win counts  
- final forecasts  

### `/plots`
- forecast vs actual plots for each hotel  

---

## Key Takeaways

- Weekly patterns exist, but they’re not enough on their own  
- Machine learning improves performance by using lag relationships  
- Neural models perform best overall  
- There’s a tradeoff between accuracy and runtime  

---

## Final Thoughts

This project shows why it’s important to compare multiple approaches when working with time series data. Simpler models give a solid baseline, but more advanced models—especially neural networks—can capture more complex patterns and improve accuracy.


