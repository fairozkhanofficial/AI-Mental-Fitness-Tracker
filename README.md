# Mental Fitness Tracker

A regression project that predicts the mental fitness level of a country from the
prevalence of mental and substance use disorders.

## Dataset

Two csv files from Our World in Data (IHME, Global Burden of Disease study),
covering around 200 countries and regions from 1990 to 2017:

- `data/mental-disease.csv` - share of DALYs (disability adjusted life years)
  caused by mental disorders. This is the target, treated as a "mental fitness"
  score for a country in a given year.
- `data/prevalence-by-mental-and-substance-use-disorder.csv` - prevalence rates
  of schizophrenia, bipolar disorder, eating disorders, anxiety, drug use,
  depression and alcohol use.

After merging on country and year the working dataset has 6750 rows.

## What the notebook does

1. Loads and merges the two datasets, drops the country code column and shortens
   the long column names
2. EDA - correlation heatmap, depression vs fitness score regression plot, global
   trend over the years, highest and lowest scoring countries
3. Label encodes the country column and does an 80/20 train test split
4. Trains and compares four regression models

## Results

| Model             | Test R2 | Test RMSE |
|-------------------|---------|-----------|
| Random Forest     | 0.993   | 0.197     |
| Decision Tree     | 0.982   | 0.313     |
| Linear Regression | 0.670   | 1.350     |
| SVR               | -0.006  | 2.358     |

Random forest wins clearly. The relationship between disorder prevalence and the
DALY share is non linear with strong country level patterns, which tree based
models pick up directly. Linear regression can only get part of the way, and SVR
fails completely without feature scaling.

Key EDA finding: depression and anxiety have the strongest positive correlation
with the DALY share, which makes sense since they are the most common disorders.

## Tools

Python, pandas, scikit-learn, matplotlib, seaborn, Jupyter

## Running it

```
pip install pandas scikit-learn matplotlib seaborn jupyter
jupyter notebook Mental_fitness_tracker.ipynb
```
