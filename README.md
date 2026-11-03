# King County House Sales: Price Analysis and Prediction

Exploratory data analysis and regression modelling to predict house sale prices in King County (Seattle area, USA), using Python, pandas and scikit-learn.

This project was completed as the final project of the **Data Analysis with Python** course (IBM, Coursera).

## Objective

Analyse which features of a house are most related to its sale price, and build regression models that predict that price from features such as square footage, number of bedrooms, grade and location.

## Dataset

- **Source:** [House Sales in King County, USA (Kaggle)](https://www.kaggle.com/harlfoxem/housesalesprediction), slightly modified for the course.
- **Size:** 21,613 house sales between May 2014 and May 2015, with 21 attributes (price, bedrooms, bathrooms, square footage, floors, waterfront, view, condition, grade, year built, location, etc.).
- The notebook loads the data directly from a URL provided by the course, so no local data file is needed.

## Workflow

1. **Data loading:** import the CSV and inspect data types and summary statistics.
2. **Data cleaning:** drop identifier columns and impute the missing values in `bedrooms` and `bathrooms` with the column mean.
3. **Exploratory analysis:** distribution of floors, price by waterfront view (boxplot), relationship between `sqft_above` and price (regplot) and correlation of all features with price.
4. **Modelling:** simple and multiple linear regression, and a pipeline with scaling, second-order polynomial features and linear regression.
5. **Model evaluation:** train/test split (85/15) and Ridge regression (α = 0.1), with and without polynomial features.

## Results

| Model | Features | Evaluated on | R² |
|---|---|---|---|
| Simple linear regression | `long` | Full dataset (in-sample) | 0.000 |
| Simple linear regression | `sqft_living` | Full dataset (in-sample) | 0.493 |
| Multiple linear regression | 11 features | Full dataset (in-sample) | 0.658 |
| Pipeline: scaling + polynomial (degree 2) + linear regression | 11 features | Full dataset (in-sample) | 0.751 |
| Ridge regression (α = 0.1) | 11 features | Test set (15%) | 0.648 |
| Ridge regression (α = 0.1) + polynomial (degree 2) | 11 features | Test set (15%) | **0.700** |

**Key findings**

- `sqft_living`, `grade` and `sqft_above` are the features most correlated with price.
- Adding more features and second-order polynomial terms clearly improves the fit.
- The best model on unseen data is the **second-order polynomial Ridge regression**, which explains about **70%** of the variation in price on the test set.
- The in-sample R² values are optimistic and are not directly comparable with the test-set R² values.

See the conclusions section of the notebook for the full discussion and possible improvements.

## Repository structure

```
├── house_sales_king_county.ipynb   # Analysis and models
├── requirements.txt                # Python dependencies
└── README.md
```

## How to run

1. Clone the repository:
   ```
   git clone https://github.com/JacoboDX/king-county-house-prices.git
   ```
2. Install the dependencies:
   ```
   pip install -r requirements.txt
   ```
3. Open `house_sales_king_county.ipynb` in VS Code (with the Jupyter extension) or in Jupyter Notebook, and run all cells. An internet connection is required to load the dataset.

## Tools

Python 3.13 · pandas · NumPy · Matplotlib · seaborn · scikit-learn · Jupyter

## Author

Jacobo Gutiérrez de Rubalcava · [GitHub](https://github.com/JacoboDX)
