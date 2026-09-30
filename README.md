# Python and Data Science Projects

A collection of my Python projects: two terminal games and four data science notebooks covering exploratory data analysis
and linear regression.

| Project | Folder | Topics |
|---|---|---|
| [Haberman breast cancer survival EDA](#haberman-breast-cancer-survival-eda) | [`EDA project`](EDA%20project/) | pandas, matplotlib, seaborn, exploratory data analysis |
| [Dice roller and Rock-Paper-Scissors](#dice-roller-and-rock-paper-scissors) | [`basic python project`](basic%20python%20project/) | Python basics, `random` module |
| [House price prediction](#house-price-prediction) | [`house price prediction`](house%20price%20prediction/) | multiple linear regression, statsmodels, scikit-learn, feature selection |
| [Salary prediction](#salary-prediction) | [`linear regression multivariate`](linear%20regression%20multivariate/) | linear regression with several variables, missing values |
| [Canada per capita income](#canada-per-capita-income) | [`linear regression univariate`](linear%20regression%20univariate/) | linear regression with one variable |

## Setup

The games only need Python 3. The notebooks need the libraries in `requirements.txt`.

```
python -m venv .venv
.venv\Scripts\python -m pip install -r requirements.txt
.venv\Scripts\python -m jupyter notebook
```

On macOS or Linux, use `python3` and `.venv/bin/python` instead. Each notebook reads its data file from its own folder,
so open the notebooks from Jupyter or VS Code as they are.

## Haberman breast cancer survival EDA

`EDA project/HabermanndatasetEDA.ipynb` explores Haberman's Survival dataset (`haberman.csv`): 306 patients who had
surgery for breast cancer, with their age, year of operation, number of positive axillary lymph nodes, and whether they
survived at least 5 years.

- Looks at the size of the data and how many patients are in each class
- Scatter plots and pair plots coloured by survival
- 1-D scatter plots, histograms, PDF and CDF curves, box plots and violin plots

**Findings:** 225 patients (73.5%) survived 5 years or longer and 81 (26.5%) did not. Patients who died within 5 years
had more positive lymph nodes (median 4, against 0 for survivors), while age and year of operation were similar in both groups.

## Dice roller and Rock-Paper-Scissors

Two terminal games in `basic python project/`, using only Python's standard library.

- **`Dice_Roll_Simulator.py`** rolls two six-sided dice and asks whether to roll again (`y` or `yes`).
- **`Rock_Paper_and_Scissors_Game.py`** asks for your name, then lets you play classic Rock-Paper-Scissors or
  Rock-Paper-Scissors-Lizard-Spock against the computer. Type a move, `help` for the rules, or `exit` to go back to the menu.

```
cd "basic python project"
python Dice_Roll_Simulator.py
python Rock_Paper_and_Scissors_Game.py
```

## House price prediction

`house price prediction/House_Price_Prediction.ipynb` is a capstone project from a data science course. It predicts house
prices (in Indian rupees) for 545 houses from their area, bedrooms, bathrooms, stories, parking, amenities (main road,
guest room, basement, hot water heating, air conditioning, preferred area) and furnishing status.

- Exploratory analysis with box plots and scatter plots
- Encodes the yes/no and furnishing columns as numbers
- Splits the data 67/33 into training and test sets
- Fits a multiple linear regression with statsmodels (OLS) and scikit-learn
- Tries correlation-based feature selection and recursive feature elimination (RFE)
- Checks the residuals

**Results:** R² of 0.687 on the training set and 0.658 on the test set (adjusted R² 0.675), with a test RMSE of about
1.21 million and MAE of about 0.90 million rupees. The biggest effects on price come from bathrooms, air conditioning,
hot water heating and being in a preferred area.

**Data:** the notebook loads the CSV from a course link that no longer works. The same data (545 rows, 13 columns) appears
to be Kaggle's "Housing Prices Dataset". To run the notebook, download that CSV into the folder and point the `read_csv`
line at it.

## Salary prediction

`linear regression multivariate/linear_regression_multivariate.ipynb` predicts a candidate's salary from years of
experience, a test score and an interview score, using `hiring.csv` (8 candidates).

- Fills the missing test score with the median and missing experience with 0
- Converts experience written as words ("five", "eleven") into numbers
- Fits a scikit-learn `LinearRegression` with the three features

**Result:** salary ≈ 17,737 + 2,813 × years of experience + 1,846 × test score + 2,205 × interview score.
It predicts $53,206 for 2 years of experience with scores of 9 and 6, and $92,002 for 12 years with scores of 10 and 10.
With only 8 rows, this shows how multiple regression works rather than giving a tested model.

## Canada per capita income

`linear regression univariate/linear_regression_univariate.ipynb` fits a straight line to Canada's per capita income from
1970 to 2016 (`canada_per_capita_income.csv`) and uses it to predict future income.

- Scatter plot of income against year
- Fits a scikit-learn `LinearRegression` with year as the only feature
- Checks the prediction by hand with y = m·x + b
- Saves the fitted income for every year to `prediction.csv` (`year.csv` and `income.csv` hold the two input columns)

**Result:** income rises by about US$828 per year, and the predicted per capita income for 2020 is US$41,289.

## Datasets

- **Haberman's Survival:** UCI Machine Learning Repository
- **Housing prices:** not included (see [House price prediction](#house-price-prediction))
- **`hiring.csv` and `canada_per_capita_income.csv`:** small practice datasets, included in their folders
