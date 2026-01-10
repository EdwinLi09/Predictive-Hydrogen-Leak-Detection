# Predictive Hydrogen Leak Detection and Localization (Machine Learning)

This repository contains work from a research project at NREL’s Energy Systems Integration Facility (ESIF) focused on **detecting and estimating the location of indoor hydrogen leaks** using sensor data and machine learning.

Hydrogen is hard to detect because it is colorless and odorless, and it can be dangerous in enclosed spaces. The goal of this project is to use readings from a sensor network to:
- detect a leak quickly,
- estimate where the leak started (leak “source” location),
- support better sensor placement and faster response in lab environments.

## What the project does
The models use time-series concentration readings from **16 fixed hydrogen sensors** to predict the leak location. The leak location is represented by **X and Z coordinates** (a 2D position on the lab floor plan).

Two modeling approaches are included:
1. **Artificial Neural Network (ANN)**  
   - Learns patterns in the sensor signals and predicts the leak location directly.
   - Trained and tested using two loss options:
     - standard mean squared error (MSE)
     - a “penalty-aware” loss that puts extra weight on larger location errors (helpful when mistakes are costly).

2. **K-Nearest Neighbors with Dynamic Time Warping (K-DTW)**  
   - Compares a new sensor signal to past signals and finds the most similar cases.
   - Dynamic Time Warping helps match signals even when they rise at different times (for example, when HVAC changes the timing).
   - The predicted leak location is the average location of the closest matches.

## Data summary (high level)
- Multiple leak scenarios from a mix of **experiments and simulations**
- Each scenario contains **2,000 seconds** of sensor readings
- Model training focuses on the **first 1,000 seconds**
- Some scenarios include **HVAC effects**, which can delay or shift sensor response

> Note: If the raw dataset is not included in this repo, you may need to add your own data files in the expected format (for example, CSV files with sensor channels over time and the leak coordinates as labels).

## Results (example comparison)
On sample tests used for evaluation, the ANN with the penalty-aware loss produced smaller location errors than the ANN without the penalty and the K-DTW setup. Results are reported as distance (meters) between the predicted leak point and the true leak point.

## Recommended repo layout
If you want a clean structure, here is a common layout:



