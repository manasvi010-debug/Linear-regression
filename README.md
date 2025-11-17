# Linear-regression
# Create final comprehensive analysis report
analysis_report = """
================================================================================
LINEAR REGRESSION ANALYSIS - HOUSING PRICE PREDICTION
================================================================================

DATASET OVERVIEW
--------------------------------------------------------------------------------
• Total samples: 545 houses
• Features: 13 independent variables
• Target variable: House price (in Indian Rupees)
• Missing values: None (clean dataset)

PREPROCESSING STEPS PERFORMED
--------------------------------------------------------------------------------
1. Categorical Encoding:
   - Binary variables (yes/no) mapped to 1/0:
     * mainroad, guestroom, basement, hotwaterheating, airconditioning, prefarea
   
2. One-Hot Encoding:
   - furnishingstatus (3 categories) converted using dummy variables
   - Drop first category to avoid multicollinearity
   
3. Feature Scaling:
   - StandardScaler applied to all features
   - Mean = 0, Standard Deviation = 1
   - Ensures all features contribute equally to the model

4. Train-Test Split:
   - Training set: 436 samples (80%)
   - Testing set: 109 samples (20%)
   - Random state: 42 (for reproducibility)

MODEL SPECIFICATIONS
--------------------------------------------------------------------------------
Algorithm: Linear Regression (Ordinary Least Squares)
Parameters:
  • fit_intercept = True
  • n_jobs = -1 (uses all CPU cores)

Assumptions:
  1. Linearity: Linear relationship between features and target
  2. Independence: Observations are independent
  3. Homoscedasticity: Constant variance of residuals
  4. Normality: Residuals follow normal distribution
  5. No multicollinearity: Features not highly correlated

MODEL PERFORMANCE METRICS
--------------------------------------------------------------------------------

TRAINING SET PERFORMANCE:
  • MAE:  ₹719,242.89
  • MSE:  968,358,188,440.72
  • RMSE: ₹984,051.92
  • R²:   0.6859 (68.59%)

TESTING SET PERFORMANCE:
  • MAE:  ₹970,043.40
  • MSE:  1,754,318,687,330.67
  • RMSE: ₹1,324,506.96
  • R²:   0.6529 (65.29%)

METRIC INTERPRETATIONS
--------------------------------------------------------------------------------

1. Mean Absolute Error (MAE): ₹970,043.40
   → The model's predictions are off by approximately ₹970,000 on average
   → This represents 19.37% of the average house price
   → MAE is less sensitive to outliers than MSE

2. Mean Squared Error (MSE): 1,754,318,687,330.67
   → Penalizes larger errors more heavily
   → Useful for comparing models but difficult to interpret directly
   → Square root gives us RMSE for better interpretation

3. Root Mean Squared Error (RMSE): ₹1,324,506.96
   → Standard deviation of prediction errors
   → In the same units as target (rupees)
   → Indicates typical magnitude of prediction error

4. R-Squared (R²): 0.6529 (65.29%)
   → Model explains 65.29% of variance in house prices
   → Indicates moderate predictive power
   → Remaining 34.71% due to unmeasured factors or model limitations

MODEL GENERALIZATION ASSESSMENT
--------------------------------------------------------------------------------
✓ Train-Test R² Difference: 0.033 (3.3%)
  → Minimal overfitting; model generalizes well
  → Similar performance on training and test data

✓ Performance Category: MODERATE TO GOOD
  → R² > 0.6 indicates acceptable predictive capability
  → Suitable for general price estimation
  → May benefit from additional features or non-linear methods

COEFFICIENT ANALYSIS - TOP 5 MOST INFLUENTIAL FEATURES
--------------------------------------------------------------------------------

1. BATHROOMS: ₹521,879.03
   • Strongest positive predictor
   • 1 additional bathroom (1 std dev) → ₹521,879 price increase
   • Impact: 11.09% of average price
   • Interpretation: Bathrooms are highly valued by buyers

2. AREA: ₹519,552.42
   • Second strongest predictor
   • Larger area directly translates to higher value
   • 1 std dev increase (~2,170 sq ft) → ₹519,552 increase
   • Impact: 11.04% of average price

3. AIR CONDITIONING: ₹365,157.39
   • Presence of AC adds significant value
   • Binary feature: has AC vs. no AC
   • Impact: 7.76% of average price
   • Reflects importance of comfort amenities

4. STORIES: ₹349,251.44
   • Multi-story houses command premium prices
   • Each additional story (1 std dev) → ₹349,251 increase
   • Impact: 7.42% of average price
   • May correlate with house size/prestige

5. PREFERRED AREA: ₹266,656.35
   • Location in preferred area adds value
   • Binary feature showing neighborhood desirability
   • Impact: 5.67% of average price
   • Location remains key real estate factor

NEGATIVE COEFFICIENTS
--------------------------------------------------------------------------------

• FURNISHINGSTATUS_UNFURNISHED: -₹192,015.92
  → Unfurnished houses valued lower than furnished
  → Buyers prefer move-in ready properties
  → Impact: -4.08% of average price

• FURNISHINGSTATUS_SEMI-FURNISHED: -₹62,837.32
  → Semi-furnished also reduces value vs. fully furnished
  → Smaller negative impact than unfurnished
  → Impact: -1.34% of average price

FEATURE IMPORTANCE RANKING (by absolute coefficient magnitude)
--------------------------------------------------------------------------------
1. bathrooms:          ₹521,879.03  (+)
2. area:               ₹519,552.42  (+)
3. airconditioning:    ₹365,157.39  (+)
4. stories:            ₹349,251.44  (+)
5. prefarea:           ₹266,656.35  (+)
6. parking:            ₹192,005.95  (+)
7. basement:           ₹187,067.80  (+)
8. unfurnished:       -₹192,015.92  (-)
9. hotwaterheating:    ₹149,862.70  (+)
10. mainroad:          ₹128,498.63  (+)
11. guestroom:         ₹88,768.67   (+)
12. semi-furnished:   -₹62,837.32   (-)
13. bedrooms:          ₹57,349.56   (+)

KEY INSIGHTS AND BUSINESS IMPLICATIONS
--------------------------------------------------------------------------------

✓ PRICING STRATEGY:
  • Bathrooms and area are top value drivers
  • Consider renovations adding bathrooms for maximum ROI
  • Area expansion provides similar value increase

✓ AMENITIES MATTER:
  • Air conditioning adds ₹365,157 to perceived value
  • Basement and parking also significant positive factors
  • Modern amenities justify premium pricing

✓ FURNISHING DECISIONS:
  • Fully furnished commands highest prices
  • Unfurnished properties face 4% price penalty
  • Consider furnishing as investment for better sale price

✓ LOCATION VALUE:
  • Preferred area location adds ₹266,656
  • Mainroad access contributes ₹128,499
  • Location factors remain critical

RESIDUAL ANALYSIS
--------------------------------------------------------------------------------
The residual plot shows:
  • Random scatter around zero indicates good model fit
  • No clear patterns suggest assumptions are reasonably met
  • Some heteroscedasticity may be present at higher price ranges
  • A few outliers exist but don't dominate the pattern

MODEL LIMITATIONS
--------------------------------------------------------------------------------
1. Linear assumption may not capture all non-linear relationships
2. 34.71% of variance remains unexplained
3. May not perform well on houses outside training data range
4. Some features may have interaction effects not captured
5. Location granularity limited to binary "preferred area"

RECOMMENDATIONS FOR IMPROVEMENT
--------------------------------------------------------------------------------
1. Feature Engineering:
   • Create interaction terms (e.g., area × bathrooms)
   • Add polynomial features for non-linear relationships
   • Include neighborhood-level statistics

2. Alternative Models:
   • Ridge/Lasso regression for feature selection
   • Decision trees for non-linear patterns
   • Ensemble methods (Random Forest, Gradient Boosting)

3. Data Enhancement:
   • Collect more location-specific features
   • Include property age and condition
   • Add market timing variables

4. Model Validation:
   • Cross-validation for robust performance estimation
   • Analysis of prediction errors by price segment
   • Feature correlation analysis to detect multicollinearity

CONCLUSION
--------------------------------------------------------------------------------
The linear regression model demonstrates MODERATE TO GOOD performance with an R²
of 0.6529 on the test set. The model successfully identifies key price drivers,
with bathrooms and area emerging as the strongest predictors. With MAE of
₹970,043 (19.4% of average price), the model provides reasonable price estimates
suitable for preliminary valuation and market analysis.

The model generalizes well (minimal overfitting) and reveals interpretable
relationships between housing features and prices. While there is room for
improvement through advanced techniques, this baseline linear model offers
valuable insights for real estate pricing decisions.

================================================================================
END OF REPORT
================================================================================
"""

with open('linear_regression_analysis_report.txt', 'w') as f:
    f.write(analysis_report)

print(analysis_report)
print("\nFull analysis report saved to 'linear_regression_analysis_report.txt'")
